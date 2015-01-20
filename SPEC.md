# Goals

## Components

React can be too verbose and clunky, which causes a lot of dependence on the documentation to figure out the correct method names. A more intuitive API should be exposed to make development feel more natural and eliminate this constraint.

```js
var Photo = fission.component({
  // prop validation will resemble mongoose schemas
  props: {
    username: String,
    height: Number,
    width: Number
  },
  
  // init = getInitialState
  init: function(){},

  // defaults = getDefaultProps
  // can also just be an object
  defaults: function(){},

  // mounting = componentWillMount
  mounting: function(){},

  // mounted = componentDidMount
  mounted: function(){},
  
  // unmounting = componentWillUnmount
  unmounting: function(){},

  // unmounted = componentDidUnmount
  unmounted: function(){},

  render: function() {}
});
```

## Models and Collections

Ampersand models and collections under the hood, with some nice stuff on top.

### Models

```js
// prop validation will resemble mongoose schemas
// event hook functions should have same naming as component
```

### Collections

```js
// prop validation will resemble mongoose schemas
// event hook functions should have same naming as component
```

## Data Binding (AKA Model and Collection Views)

TODO

## Routing

TODO (react-router?)

## Responsive

Responsive design is no longer a "nice to have" when building a web application. As such, tools that help make responsive interfaces easier should be included by default. See [react-responsive](https://github.com/wearefractal/react-responsive) for the low level implementation. An additional layer with sane defaults (retina/mobile/tablet/desktop) should be added on top of react-responsive to make things easier.

### New State

Responsive media becomes a first class state object on components. When responsive state changes, components will be re-rendered accordingly.

```js
var photo = fission.component({
  // tells fission to include this.media information and re-render on change
  responsive: true,
  props: {
    username: String,
    height: Number,
    width: Number
  },

  render: function() {
    var h = this.props.height * this.media.resolution;
    var w = this.props.width * this.media.resolution;
    var url = 'http://graph.facebook.com/'+this.props.username+'/picture?height='+h+'&width='+w;
    var image = DOM.img({
      src: url,
      height: this.props.height,
      width: this.props.width
    });
    return image;
  }
});
```

## Internationalization and Localization

TODO (L20n.js?)

## Accessiblity

TODO:

[https://github.com/rackt/react-a11y](https://github.com/rackt/react-a11y)

## DOM Sugar

###  null props inference

Having to specify `DOM.h3(null, 'Text here')` is annoying. If the first argument is a renderable then props should be inferred as null. This allows for `DOM.h3('Text here')` or `DOM.div(DOM.h3('Text here'), DOM.h3('Text here'))`

### classNames = classSet wrapper

The react classSet addon is powerful, but not included by default which makes it clunky to use.

```js
DOM.div({
  classNames: {
    active: this.state.active,
    bold: true,
    italic: false
  }
}, 'Test');
```

should be the equivalent of

```js
var cx = require('react/addons').addons.classSet;
DOM.div({
  className: cx({
    active: this.state.active,
    bold: true,
    italic: false
  })
}, 'Test');
```

## Animation

TODO

[react-tween-state](https://github.com/chenglou/react-tween-state) sugar. [react-state-stream](https://github.com/chenglou/react-state-stream) sugar

## State Batching

Fission will only diff/render state changes once per animation frame. This will lead to a smoother user experience and conserve CPU cycles. See [this repo](https://github.com/petehunt/react-raf-batching) for an example implementation.

## Application

TODO, central config location and place to set up data stores

## Testing

TODO
