<p align="center">
  <img alt="OS.js Logo" src="https://raw.githubusercontent.com/os-js/gfx/master/logo-big.png" />
</p>

[OS.js](https://www.os-js.org/) is an [open-source](https://raw.githubusercontent.com/os-js/OS.js/master/LICENSE) web desktop platform with a window manager, application APIs, GUI toolkit, filesystem abstractions and much more.

[![Support](https://img.shields.io/badge/patreon-support-orange.svg)](https://www.patreon.com/user?u=2978551&ty=h&u=2978551)
[![Support](https://img.shields.io/badge/opencollective-donate-red.svg)](https://opencollective.com/osjs)
[![Donate](https://img.shields.io/badge/liberapay-donate-yellowgreen.svg)](https://liberapay.com/os-js/)
[![Donate](https://img.shields.io/badge/paypal-donate-yellow.svg)](https://paypal.me/andersevenrud)
[![Community](https://img.shields.io/badge/join-community-green.svg)](https://community.os-js.org/)

# OS.js wireless-tools Service Provider

This provider simply binds https://github.com/bakerface/wireless-tools to the internal API.

## Installation

```bash
npm install @osjs/wireless-tools-provider
```

In your initialization scripts:

```javascript
// Client index.js file
import {WirelessToolsServiceProvider} from '@osjs/wireless-tools-provider';
osjs.register(WirelessToolsServiceProvider);

// Server index.js file
const {WirelessToolsServiceProvider} = require('@osjs/wireless-tools-provider/src/server.js');
osjs.register(WirelessToolsServiceProvider);
```

## Configuration

By default the server provider is set up to only allow users with the `admin` group to access this feature.

You can change this by adding options:

```javascript
const {WirelessToolsServiceProvider} = require('@osjs/wireless-tools-provider/src/server.js');
osjs.register(WirelessToolsServiceProvider, {
  args: {
    groups: ['other-group']
  }
});
```

## API

Simply use `core.make('osjs/wireless-tools').call('namespace', 'method', ...args)` and you will get a `Promise<any, Error>`.

You can also add subscriptions for these calls over websockets so that you get data on a regular interval:

```javascript
// Subscribe
core.make('osjs/wireless-tools')
  .subscribe('ifconfig', 'status')
  .then(subscription => {
    // Attach a callback to get data when server pushes it out
    subscription.bind(data => {
      console.log(data)
    });

    // Unsubscribe when you're done
    subscription.unsubscribe();
  });
```

You can see namespaces, method names and the return data in the wireless-tools documentation.

## Features

- Uses 1:1 function signatures (except promise instead of callback)
- Support for subscriptions over websocket
- Wifi connection settings via tray icon

## TODO

- [ ] Finish wifi tray icon
- [ ] Add support for custom intervals on subscriptions
- [ ] Add support for subscription emit only when data has changed

## Contribution

* **Sponsor on [Github](https://github.com/sponsors/andersevenrud)**
* **Become a [Patreon](https://www.patreon.com/user?u=2978551&ty=h&u=2978551)**
* **Support on [Open Collective](https://opencollective.com/osjs)**
* [Contribution Guide](https://github.com/os-js/OS.js/blob/master/CONTRIBUTING.md)

## Documentation

See the [Official Manuals](https://manual.os-js.org/) for articles, tutorials and guides.

## Links

* [Official Chat](https://gitter.im/os-js/OS.js)
* [Community Forums and Announcements](https://community.os-js.org/)
* [Homepage](https://os-js.org/)
* [Twitter](https://twitter.com/osjsorg) ([author](https://twitter.com/andersevenrud))
* [Google+](https://plus.google.com/b/113399210633478618934/113399210633478618934)
* [Facebook](https://www.facebook.com/os.js.org)
* [Docker Hub](https://hub.docker.com/u/osjs/)
