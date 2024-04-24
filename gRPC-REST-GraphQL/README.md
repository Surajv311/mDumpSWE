
# gRPC_REST_GraphQL

gRPC (Remote Procedure Call) uses Protobufs to encode and send data (.proto file) (It can use other formats like JSON as well). In an RPC, a client causes a procedure to execute on a different address space, usually a remote server. The procedure is coded as if it were a local procedure call, abstracting away the details of how to communicate with the server from the client program. Remote calls are usually slower and less reliable than local calls so it is helpful to distinguish RPC calls from local calls. Popular RPC frameworks include Protobuf, Thrift, and Avro.
- Protocol buffers are Google's language-agnostic, platform-neutral, extensible mechanism for serializing structured data. gRPC uses HTTP2. 
- Also, in other words, **LPC (Local Procedure Call)** vs **RPC (Remote Procedure Call)**: 
  - Host machine invokes a function call in itself, executes & gets the output - LPC
  - Host machine invokes a function call on another machine, executes & gets the output - RPC
- In RPC, there can be issues like: RPC is slower than LPC since it uses the network to invoke the method. Failures can happen, etc. 

REST is an architectural style enforcing a client/server model where the client acts on a set of resources managed by the server. The server provides a representation of resources and actions that can either manipulate or get a new representation of resources. All communication must be stateless and cacheable.

GraphQL is an open source query language that describes how a client should request information through an API.

[gRPC vs REST vs. GraphQL _al](https://www.linkedin.com/pulse/rest-graphql-grpc-comparing-contrasting-modern-api-design-walpita/),
[gRPC over REST _al](https://medium.com/@sankar.p/how-grpc-convinced-me-to-chose-it-over-rest-30408bf42794),
[RPC vs REST _al](https://github.com/donnemartin/system-design-primer?tab=readme-ov-file#rpc-and-rest-calls-comparison),
[Graphql _al](https://www.youtube.com/watch?v=yWzKJPw_VzM),
[gRPC _vl](https://www.youtube.com/watch?v=gnchfOojMk4)

----------------------------------------------------------------------





















