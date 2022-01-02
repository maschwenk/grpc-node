[![Build Status](https://travis-ci.org/grpc/grpc-node.svg?branch=master)](https://travis-ci.org/grpc/grpc-node)
# gRPC on Node.js

## Implementations

For a comparison of the features available in these two libraries, see [this document](https://github.com/grpc/grpc-node/tree/master/PACKAGE-COMPARISON.md)

### C-based Client and Server

Directory: [`packages/grpc-native-core`](https://github.com/grpc/grpc-node/tree/grpc@1.24.x/packages/grpc-native-core) (lives in the `grpc@1.24.x` branch) (see here for installation information)

npm package: [grpc](https://www.npmjs.com/package/grpc).

This is the existing, feature-rich implementation of gRPC using a C++ addon. It works on all LTS versions of Node.js on most platforms that Node.js runs on.

### Pure JavaScript Client

Directory: [`packages/grpc-js`](https://github.com/grpc/grpc-node/tree/master/packages/grpc-js)

npm package: [@grpc/grpc-js](https://www.npmjs.com/package/@grpc/grpc-js)

This library implements the core functionality of gRPC purely in JavaScript, without a C++ addon. It works on the latest version of Node.js on all platforms that Node.js runs on.

## Other Packages

### gRPC Protobuf Loader

Directory: [`packages/proto-loader`](https://github.com/grpc/grpc-node/tree/master/packages/proto-loader)

npm package: [@grpc/proto-loader](https://www.npmjs.com/package/@grpc/proto-loader)

This library loads `.proto` files into objects that can be passed to the gRPC libraries.

### gRPC Tools

Directory: [`packages/grpc-tools`](https://github.com/grpc/grpc-node/tree/master/packages/grpc-tools)

npm package: [grpc-tools](https://www.npmjs.com/package/grpc-tools)

Distribution of protoc and the gRPC Node protoc plugin for ease of installation with npm.

### gRPC Health Check Service

Directory: [`packages/grpc-health-check`](https://github.com/grpc/grpc-node/tree/master/packages/grpc-health-check)

npm package: [grpc-health-check](https://www.npmjs.com/package/grpc-health-check)

Health check service for gRPC servers.

### Building gprc-tools

I needed to compile `gprc-tools` from source to be able to run it on Apple Silicon because builds are not provided.

My steps:

```sh
git clone git@github.com:grpc/grpc-node.git
cd grpc-node
brew install cmake # ./build_binaries.sh needs cmake. also tried xcode-select --install but it didn't seem to work
cd packages/grpc-tools && git submodule update --init --recursive && ./build_binaries.sh

# then to install in pnpm (does not support npm flag)
npm_config_grpc_tools_binary_host_mirror="https://github.com/maschwenk/grpc-node/raw/2dd28e1ab8211533007dd2df5ae632de60006983/artifacts/" pnpm install
# checkout https://github.com/mapbox/node-pre-gyp/blob/master/lib/util/versioning.js#L316
# seems passing as an ENV also works (so will probably work for PNPM and Yarn)
```
