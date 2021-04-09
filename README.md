protobuf-ts [![<timostamm>](https://circleci.com/gh/timostamm/protobuf-ts.svg?style=svg)](https://app.circleci.com/pipelines/github/timostamm/protobuf-ts) [![npm](https://img.shields.io/npm/v/@protobuf-ts/plugin)](https://www.npmjs.com/package/@protobuf-ts/plugin)
===========


Protocol buffers and RPC for Node.js and the Web Browser. Pure TypeScript.

For the following `.proto` file:
```proto
syntax = "proto3";

message Person {
    string name = 1;
    uint64 id = 2;
    int32 years = 3;
    optional bytes data = 5;
}
```

`protobuf-ts` generates code that can be used like this:

```typescript
let pete: Person = {
    name: "pete", 
    id: 123n, // it's a bigint
    years: 30
    // data: new Uint8Array([0xDE, 0xAD, 0xBE, 0xEF]);
};

let bytes = Person.toBinary(pete);
pete = Person.fromBinary(bytes);

pete = Person.fromJsonString('{"name":"pete", "id":"123", "years": 30}')
```


### Quickstart

- `npm install @protobuf-ts/plugin`
  > installs the plugin and the compiler "protoc"

- download the example file [msg-readme.proto](https://raw.githubusercontent.com/timostamm/protobuf-ts/master/packages/test-fixtures/msg-readme.proto) and place it into a `protos/` directory

- `npx protoc --ts_out . --proto_path protos protos/msg-readme.proto`
  > generates msg-readme.ts  
  > if your protoc version asks for it, add the flag "--experimental_allow_proto3_optional"


### Features

- [x] implements the [canonical proto3 JSON format](MANUAL.md#json-format)
- [x] implements the [binary format](MANUAL.md#binary-format) and respects [unknown fields](MANUAL.md#unknown-field-handling)
- [x] strictly [conforms to the protobuf spec](MANUAL.md#conformance)
- [x] generates clients that can be used with [gRPC web](MANUAL.md#grpc-web-transport), [Twirp](MANUAL.md#twirp-transport) or [gRPC](MANUAL.md#grpc-transport)
- [x] generates [gRPC servers](MANUAL.md#grpc-server)
- [x] supports [Angular](MANUAL.md#angular-support) dependency injection and pipes
- [x] automatically [installs protoc](./packages/protoc/README.md)
- [x] can optimize for [speed or code size](MANUAL.md#code-size-vs-speed)  
- [x] supports [proto3 optionals](MANUAL.md#proto3-optionals)
- [x] [supports bigint](MANUAL.md#bigint-support) for 64 bit integers
- [x] every [message type](MANUAL.md#imessagetype) has methods to compare, clone, merge and type guard messages
- [x] provides [reflection information](MANUAL.md#reflection), 
  including [custom options](MANUAL.md#custom-options)
- [x] supports all [well-known-types](MANUAL.md#well-known-types) with custom JSON representation and helper methods
- [x] uses standard [TypeScript enums](MANUAL.md#enum-representation)
- [x] runs [in the Web Browser](MANUAL.md#running-in-the-web-browser) and in [Node.js](MANUAL.md#running-in-nodejs)
- [x] uses an [algebraic data type for oneof](MANUAL.md#oneof-representation) groups


Read the [MANUAL](MANUAL.md) to learn more.




### Copyright

- The [algorithm to decode UTF8](./packages/runtime/src/protobufjs-utf8.ts) is Copyright 2016 by Daniel Wirtz, licensed under BSD-3-Clause.
- The [algorithm to encode and decode varint](./packages/runtime/src/goog-varint.ts) is Copyright 2008 Google Inc., licensed under BSD-3-Clause.
- The files [plugin.ts](./packages/plugin-framework/src/google/protobuf/compiler/plugin.ts) and [descriptor.ts](./packages/plugin-framework/src/google/protobuf/descriptor.ts) are Copyright 2008 Google Inc., licensed under BSD-3-Clause
- The [gRPC status codes](./packages/grpcweb-transport/src/goog-grpc-status-code.ts) are Copyright 2016 gRPC authors, licensed under Apache-2.0.
- The [Twirp error codes](./packages/twirp-transport/src/twitch-twirp-error-code.ts) are Copyright 2018 Twitch Interactive, Inc., licensed under Apache-2.0.
- The proto files in [test-fixtures/google](./packages/test-fixtures/google) and [test-fixtures/conformance](./packages/test-fixtures/conformance) are Copyright Google Inc. / Google LLC, licensed under Apache-2.0 / BSD-3-Clause.
- The proto files in [test-fixtures/validate](./packages/test-fixtures/validate) are Copyright 2019 Envoy Project Authors, licensed under Apache License 2.0.
- All other files are licensed under Apache-2.0, see [LICENSE](./LICENSE). 


