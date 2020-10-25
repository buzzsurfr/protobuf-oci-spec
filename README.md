# Protocol Buffers OCI Specification

## Abstract

Protocol Buffers (a.k.a., protobuf) are Google's language-neutral, platform-neutral, extensible mechanism for serializing structured data.

This README file is the start of a specification to store and transmit protocol buffers using the OCI specifications.

## Format

The protobuf OCI Spec consists of the `.proto` file, an optional layer for the [FileDescriptorSet](https://github.com/protocolbuffers/protobuf/blob/de5d1b98c27428450b9a38ab5c2de479f59025af/src/google/protobuf/descriptor.proto#L57) (a binary representation of the `.proto` file, typically stored with a `.bin` extension), and optional layers that contain the generated code for a supported programming language.

Each layer is associated with its own Media Type, which is stored in the OCI Descriptor for that layer:

| Media Type | Type | Description |
|------------|------|-------------|
| `application/vnd.protobuf.proto.v2` | Proto file (v2) | The protocol buffer represented in a `.proto` file. (Version 2) |
| `application/vnd.protobuf.proto.v3` | Proto file (v3) | The protocol buffer represented in a `.proto` file. (Version 3) |
| `application/vnd.protobuf.content.v1.bin` | binary data (byte array) | The compiled protocol buffer. |
| `application/vnd.protobuf.content.v1.bin+gzip` | binary data (gzipped) | The compressed compiled protocol buffer. |
| `application/vnd.protobuf.codegen.go.v1.tar+gzip` | Generated code for Go | The generated code from the protocol buffer used in Go programs. |

The `.proto` file should be curated using the Language Guide for that version of the protocol buffer.

* [Language Guide (proto2)](https://developers.google.com/protocol-buffers/docs/proto)
* [Language Guide (proto3)](https://developers.google.com/protocol-buffers/docs/proto3)

The binary data can be compiled using `protoc`. For example, to compile **helloworld.proto** to **helloworld.bin**, run

```
protoc -o helloworld.bin helloworld.proto
```
