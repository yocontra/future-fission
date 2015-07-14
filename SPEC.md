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
  // can also just be an object
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

## Data

Using Relay (or Turbine for interim) to gather data via graphql

## Routing

A declarative layer on top of react-router should be used.

```js
var appRouter = Router({
  // Route = /
  splash: {
    path: '/',
    view: SomeReactComponent
  },
  // Route = /login
  login: {
    path: 'login',
    view: SomeReactComponent
  },
  // Route = /home
  home: {
    path: 'home',
    view: SomeReactComponent,
    children: {
      // Route = /home, this is a default subview of home with no path specified
      dashboard: {
        default: true,
        view: SomeReactComponent
      },
      // Route = /home/statistics, this is a subview of home
      stats: {
        path: 'statistics',
        view: SomeReactComponent
      },
      // Route = /home/job/123, this is a subview of home
      job: {
        path: 'job/:jobId',
        view: SomeReactComponent
      }
    }
  }
});

appRouter.start(document.body);
```

[fission-router](https://github.com/fissionjs/fission-router) for initial implementation.

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

## Animation

[react-motion](https://github.com/chenglou/react-motion)

## State Batching

Fission will only diff/render state changes once per animation frame. This will lead to a smoother user experience and conserve CPU cycles. See [this repo](https://github.com/petehunt/react-raf-batching) for an example implementation.

## Testing

TODO
