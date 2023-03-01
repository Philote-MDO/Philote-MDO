# Supported Languages

## Direct Support

As Philote uses gRPC and protocol buffers to define a data and communications
standard for MDO applications, individual disciplines may be interface using any
language with gRPC bindings. The official list of supported languages is
(according to the [gRPC website](https://grpc.io/docs/languages/)):

- [C#/.NET](https://grpc.io/docs/languages/csharp/)
- [C++](https://grpc.io/docs/languages/cpp/)
- [Dart](https://grpc.io/docs/languages/dart/)
- [Go](https://grpc.io/docs/languages/go/)
- [Java](https://grpc.io/docs/languages/java/)
- [Kotlin](https://grpc.io/docs/languages/kotlin/)
- [Node](https://grpc.io/docs/languages/node/)
- [Objective-C](https://grpc.io/docs/languages/objective-c/)
- [PHP](https://grpc.io/docs/languages/php/)
- [Python](https://grpc.io/docs/languages/python/)
- [Ruby](https://grpc.io/docs/languages/ruby/)

Additionally, unofficial third-party bindings exist for a variety of languages
such as [Rust](https://docs.rs/grpc/latest/grpc/).


## Fortran

Noticeably absent, yet an important language in scientific computing, is
Fortran. There appear to be no gRPC binding, certainly no mature ones, available
for Fortran. However, due to the widespread use of Fortran in high-performance
scientific analyses (particularly legacy codes), ignoring it in an MDO setting
is impractical.

Despite the absence of native bindings, however, Fortran codes can still be
connected to Philote generated components. To do this, Philote must be used in
another language (such as C/C++ or Rust) and the Fortran code must then be
called via a foreign function interface.