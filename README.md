# React event listener

> A React component for binding events on the global scope.

[![npm version](https://img.shields.io/npm/v/react-event-listener.svg?style=flat-square)](https://www.npmjs.com/package/react-event-listener)
[![npm downloads](https://img.shields.io/npm/dm/react-event-listener.svg?style=flat-square)](https://www.npmjs.com/package/react-event-listener)
[![Build Status](https://travis-ci.org/oliviertassinari/react-event-listener.svg?branch=master)](https://travis-ci.org/oliviertassinari/react-event-listener)

[![Dependencies](https://img.shields.io/david/oliviertassinari/react-event-listener.svg?style=flat-square)](https://david-dm.org/oliviertassinari/react-event-listener)
[![DevDependencies](https://img.shields.io/david/dev/oliviertassinari/react-event-listener.svg?style=flat-square)](https://david-dm.org/oliviertassinari/react-event-listener#info=devDependencies&view=list)

## Getting Started

```sh
npm install react-event-listener
```

## Usage

```js
import React, {Component} from 'react';
import EventListener from 'react-event-listener';

class MyComponent extends Component {
  handleResize = () => {
    console.log('resize');
  };

  handleMouseMove = () => {
    console.log('mousemove');
  };

  render() {
    return (
      <div>
        <EventListener target="window" onResize={this.handleResize} />
        <EventListener target={document} onMouseMove={this.handleMouseMove} capture={true} />
      </div>
    );
  }
}
```

### Note on Server Side rendering

When doing server side rendering, the `document` and the `window are not be available.
For those circonstances, you can use a string as a `target` or check that they exist
before rendering the component.


### Note on Performance

You should avoid passing inline functions for listeners, because this creates a new `Function` instance on every
render, defeating `EventListener`'s `shouldComponentUpdate`, and triggering an update cycle where it removes its old
listeners and adds its new listeners (so that it can stay up-to-date with the props you passed in).


### Note on Testing

In [this](https://github.com/facebook/react/issues/5043) issue from React, `TestUtils.Simulate.` methods won't bubble up to `window` or `document`. As a result, you must use [`document.dispatchEvent`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/dispatchEvent) or simulate event using [native DOM api](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/click).

See our [test cases](https://github.com/oliviertassinari/react-event-listener/blob/master/src/index.spec.js) for more information.


## Contributing

Note: you need to have Flow 0.23.0 or greater to be installed.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request


## Collaborators

 - Andy Edwards ([jedwards1211](https://github.com/jedwards1211))


## License

MIT
