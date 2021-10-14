---
title: "Node Dependencies"
date: 2021-10-14T10:37:27+02:00
draft: false
---
# Node.js dependencies
There are several dependencies that Node.js relies on to work the way it does.
To get more information on Node.js dependencies, you can take a look [here](https://nodejs.org/en/docs/meta/topics/dependencies).

## Find library dependencies used by installed Nodejs
One way to check those dependencies is to issue this command:
```bash
node -e "console.log(process.versions)"
```
\
Example output for node v12.18.4:
```json
{
  node: '12.18.4',
  v8: '7.8.279.23-node.39',
  uv: '1.38.0',
  zlib: '1.2.11',
  brotli: '1.0.7',
  ares: '1.16.0',
  modules: '72',
  nghttp2: '1.41.0',
  napi: '6',
  llhttp: '2.1.2',
  http_parser: '2.9.3',
  openssl: '1.1.1g',
  cldr: '37.0',
  icu: '67.1',
  tz: '2019c',
  unicode: '13.0'
}
```

## Find dependencies by looking at the source code
You can get the openssl version used by a specific version of Node.js:
```bash
NODE_VERSION="6.9.2"
curl -q "https://raw.githubusercontent.com/nodejs/node/v${NODE_VERSION}/deps/openssl/openssl/README" | head
```
