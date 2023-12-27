---
title: "Metadata Propagation"
linkTitle: "Metadata Propagation"
weight: 4
description: >

---

## Preface

Based on TTHeader, we provide the capability to transmit certain metadata in the protocol header.

Despite its convenience, we do not recommend using this capability extensively for transmitting large amounts of information or as a general parameter-passing method, for the following reasons:

1. It doesn't align with API specifications; it's purely an implementation-specific behavior.
2. This approach nullifies the purpose of defining and constraining RPC APIs using Thrift / Protobuf IDL.
3. TTHeader has limitations on the total header size (64K). Slightly exceeding this limit could result in transmission failures. If extensively used for transmission, it will eventually reach the limit, causing all RPC requests to fail.
4. This method has poor performance, both in terms of implementation and the additional resources consumed at each hop during transmission.
5. Imagine if all businesses transmit fields through this method; the future maintainability would be almost zero, and it would be impossible to converge.

## Solution Overview

For forward propagation (from upstream to downstream), we offer two methods:

1. Persistent: These metadata types will continuously propagate down the invocation chain until actively removed by some node (not recommended for extensive use).
2. Transient: These metadata types propagate only for one hop, i.e., to the immediate downstream service (preferred method).

For backward propagation (from downstream to upstream), we provide only one method: Transient (which returns only one hop). We do not consider it a reasonable requirement or scenario to return a certain metadata from the lowest-level service all the way up to the top-level service. If such a need arises, please explicitly define the relevant fields in the IDL and return them.

## Usage

To use this feature with Volo-Thrift, TTHeader protocol is required; Volo-gRPC doesn't have any additional requirements.

If your scenario involves scaffolding code generated by Volo-Thrift server as the entry point, you can directly import the corresponding trait and perform retrieval or setting:


```rust
use metainfo::{Backward, Forward};

pub struct S;

#[volo::async_trait]
impl volo_gen::volo::example::ItemService for S {
    async fn get_item(
        &self,
        req: volo_gen::volo::example::GetItemRequest,
    ) -> Result<volo_gen::volo::example::GetItemResponse, pilota::AnyhowError>
    {
        metainfo::METAINFO.with(|mi| {
            let mut mi = mi.borrow_mut();
            println!(
                "{:?}, {:?}",
                mi.get_all_persistents(),
                mi.get_all_upstreams()
            );
            mi.set_backward_transient("test_backward", "test_backward_value");
        });
        Ok(Default::default())
    }
}
```

If you're writing your own `main` function and using the client for invocation, you'll first need to insert `MetaInfo` into the task local context:

```rust
use lazy_static::lazy_static;
use metainfo::{Backward, Forward, MetaInfo, METAINFO};
use std::{cell::RefCell, net::SocketAddr};

use volo_example::LogLayer;

lazy_static! {
    static ref CLIENT: volo_gen::volo::example::ItemServiceClient = {
        let addr: SocketAddr = "127.0.0.1:8080".parse().unwrap();
        volo_gen::volo::example::ItemServiceClientBuilder::new("volo-example-item")
            .layer_outer(LogLayer)
            .address(addr)
            .build()
    };
}

#[volo::main]
async fn main() {
    let mut mi = MetaInfo::new();
    mi.set_persistent("test_persistent_key", "test_persistent");
    mi.set_transient("test_transient_key", "test_transient");

    METAINFO
        .scope(RefCell::new(mi), async move {
            let req = volo_gen::volo::example::GetItemRequest { id: 1024 };
            let resp = CLIENT.get_item(req).await;
            match resp {
                Ok(info) => tracing::info!("{:?}", info),
                Err(e) => tracing::error!("{:?}", e),
            }

            METAINFO.with(|mi| {
                println!("{:?}", mi.borrow().get_all_backward_downstreams());
            })
        })
        .await;
}
```

Of course, if your client invocation occurs after receiving a request from the server, you don't need to manually set up the metainfo task local. Volo-Thrift framework will automatically manage these values for you.

## Summary

In essence, the steps can be broken down as follows:

1. Ensure that you currently have the METAINFO in the task local (typically available by default in server methods without the need for manual creation).
2. Import the traits from the metainfo.
3. Call the corresponding methods to set or retrieve values.

## Integration with Third-Party Frameworks

To integrate the metadata propagation functionality with other frameworks (such as HTTP frameworks), simply adhere to the header constant strings defined in the metainfo package.

Kitex and Hertz frameworks inherently support and comply with the metadata propagation specifications.