# clv WebRTC SIP JavaScript library

![npm (scoped)](https://img.shields.io/npm/v/clv-sipjs)

The clv SIP-based WebRTC JS library powers up your web application with the ability to make and receive phone calls directly in the browser.

Check out the library in action in [this web dialer demo](https://webrtc.clv.com/).

_Looking for more WebRTC features, JSON-RPC support or need to quickly get spun up with a React app? clv also has a robust [WebRTC SDK](https://github.com/team-clv/webrtc) available as a separate npm module._

## Installation

Install this package with [npm](https://www.npmjs.com/):

```shell
$ npm install --save clv-sipjs
```

or using [yarn](https://yarnpkg.com/lang/en/):

```shell
$ yarn add clv-sipjs
```

## Usage

Import [clvDevice](https://github.com/team-clv/clv-sipjs/docs/clvDevice.md) in the module where you need it.

```javascript
import { clvDevice } from "clv-sipjs";
```

```javascript
<audio id="clv-sipjs-remote-audio"></audio>
```

### Example config and initiation

```javascript
let config = {
  host: "sip.clv.com",
  wsServers: "wss://sip.clv.com:7443",
  displayName: "Phone User",
  username: "testuser",
  password: "testuserPassword",
};

let device = new clvDevice(config);

device.on("connecting", () => {
  console.log("connecting!");
});
device.on("accepted", () => {
  console.log("We're on a phone call!");
});
device.on("invite", (data) => {
  console.log("Incoming", data);
});
device.on("accept", (accept) => {
  console.log("accept", accept);
});
device.on("cancel", (cancel) => {
  console.log("cancel", cancel);
});
device.on("rejected", (rejected) => {
  console.log("rejected", rejected);
});
device.on("failed", (failed) => {
  console.log("failed", failed);
});
device.on("bye", (bye) => {
  console.log("bye", bye);
});
device.on("replaced", (replaced) => {
  console.log("replaced", replaced);
});
device.on("rejected", (rejected) => {
  console.log("rejected", rejected);
});
device.on("trackAdded", (trackAdded) => {
  console.log("trackAdded", trackAdded);
});
```

### Example phone call

```javascript
let activeCall = device.initiateCall("1235556789");

activeCall.on("connecting", () => {
  console.log("it's connecting!");
});
activeCall.on("accepted", () => {
  console.log("We're on a phone call!");
});
```

### Example answer

```javascript
device.on("invite", (data) => {
  console.log("Incoming", data);
});
device.accept();
```

### Example hangup

```javascript
device.reject();
```

See the [clvDevice](https://github.com/team-clv/clv-sipjs/docs/clvDevice.md) and [clvCall](https://github.com/team-clv/clv-sipjs/docs/clvCall.md) for more details.

## Development

### Building the package

When working on the package directly, please use [yarn](https://github.com/yarnpkg/yarn) instead of npm.

```shell
$ yarn build
# Or to watch for changes to files:
$ yarn start
```

### Running tests

```shell
$ yarn test
```

### Generating Docs

We use [jsdoc-to-markdown](https://github.com/jsdoc2md/jsdoc-to-markdown) to generate GitHub friendly docs.

```shell
$ yarn docs
```
