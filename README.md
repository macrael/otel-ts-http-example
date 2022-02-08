# Overview

MacRae's Notes:

* I took this example and tried to transform it into something that would fit into our application bit by bit
* I enabled typescript, you can build and run this project (after `yarn install`) with `tsc && node ./build/server.js`
* I got stuck by trying to convert all the require()s into imports. I think related to (this issue)[https://github.com/open-telemetry/opentelemetry-js/issues/1946]
    * Basically, everything works if in server.ts you do `const tracer = require('./tracer').tracer` but not if you do `import { tracer } from './tracer'`
    * and by "everything works"I mean that the call to registerInstrumentations in tracer.ts seems to do something, you get a trace automatically created for all http calls.
* The "bad_tsconfig.json" file more closely mirrors our own and makes it impossible to make this work as far as I can tell

EOM

OpenTelemetry HTTP Instrumentation allows the user to automatically collect trace data and export them to the backend of choice (we can use Zipkin or Jaeger for this example), to give observability to distributed systems.

This is a simple example that demonstrates tracing HTTP request from client to server. The example
shows key aspects of tracing such as

- Root Span (on Client)
- Child Span (on Client)
- Child Span from a Remote Parent (on Server)
- SpanContext Propagation (from Client to Server)
- Span Events
- Span Attributes

## Installation

```sh
# from this directory
npm install
```

Setup [Zipkin Tracing](https://zipkin.io/pages/quickstart.html)
or
Setup [Jaeger Tracing](https://www.jaegertracing.io/docs/latest/getting-started/#all-in-one)

## Run the Application

### Zipkin

- Run the server

   ```sh
   # from this directory
   npm run zipkin:server
   ```

- Run the client

   ```sh
   # from this directory
   npm run zipkin:client
   ```

#### Zipkin UI

`zipkin:server` script should output the `traceid` in the terminal (e.g `traceid: 4815c3d576d930189725f1f1d1bdfcc6`).
Go to Zipkin with your browser <http://localhost:9411/zipkin/traces/(your-trace-id)> (e.g <http://localhost:9411/zipkin/traces/4815c3d576d930189725f1f1d1bdfcc6)>

<p align="center"><img src="./images/zipkin-ui.png?raw=true"/></p>

### Jaeger

- Run the server

   ```sh
   # from this directory
   npm run jaeger:server
   ```

- Run the client

   ```sh
   # from this directory
   npm run jaeger:client
   ```

#### Jaeger UI

`jaeger:server` script should output the `traceid` in the terminal (e.g `traceid: 4815c3d576d930189725f1f1d1bdfcc6`).
Go to Jaeger with your browser <http://localhost:16686/trace/(your-trace-id)> (e.g <http://localhost:16686/trace/4815c3d576d930189725f1f1d1bdfcc6)>

<p align="center"><img src="images/jaeger-ui.png?raw=true"/></p>

## Useful links

- For more information on OpenTelemetry, visit: <https://opentelemetry.io/>
- For more information on OpenTelemetry for Node.js, visit: <https://github.com/open-telemetry/opentelemetry-js/tree/main/packages/opentelemetry-sdk-trace-node>

## LICENSE

Apache License 2.0
