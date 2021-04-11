# videojs-contextmenu-pt

A cross-device context menu UI for video.js players. Forked from `videojs-contextmenu-ui` to add support for features needed in PeerTube's development, hence the suffix.

Features added:
- support for content as a function, allowing dynamic menus evaluated on `oncontextmenu` event

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Installation](#installation)
- [Usage](#usage)
- [Options](#options)
  - [`content`](#content)
  - [`keepInside`](#keepinside)
  - [`excludeElements`](#excludeelements)
- [Inclusion](#inclusion)
  - [`<script>` Tag](#script-tag)
  - [CommonJS/Browserify](#commonjsbrowserify)
  - [RequireJS/AMD](#requirejsamd)
- [License](#license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


## Installation

```sh
npm install --save videojs-contextmenu-pt
```

## Usage

The plugin is invoked as a method of a video.js `Player` object:

```js
player.contextmenuUI();
```

Once the plugin is invoked, a modal will appear with a list of links when the `contextmenu` event is triggered on the `Player` object.

## Options

Options may be passed to the plugin in a plain object:

```js
player.contextmenuUI({
  content: [{

    // A plain old link.
    href: 'https://www.brightcove.com/',
    label: 'Brightcove'
  }, {

    // A link with a listener. Its `href` will automatically be `#`.
    label: 'Example Link',
    listener: function() {
      alert('you clicked the example link!');
    }
  }]
});
```

### `content`

**Required**
**Type**: Array

The plugin requires that `content` be passed as an array. If it is not, an error will be thrown. The array should contain any number of objects which define a series of links that appear in the modal. These objects support the following properties:

- `href`: Defines the value of the `href` attribute of the generated link.
- `listener`: A function which will be bound to the `click` event of the generated link.
- `label`: Text for the link.

### `keepInside`

**Type**: Boolean

If `true` (default), the context menu will be kept within the bounds of the player. If `false`, it may extend outside. When set to `false`, the menu would still stay within the player if the menu would otherwise extend outside the document body, including fullscreen players and players in an iframe.

### `excludeElements`

**Type**: Function
**Parameters**: The DOM element that is being targeted
**Returns**: Boolean | Returns `true` if the targeted element should be excluded from displaying context menu

Defines which elements should be excluded from displaying the context menu. `input` and `textarea` elements are excluded by the default function.

```js
player.contextmenuUI({
  ...
  excludeElements: (targetEl) => {
    const tagName = targetEl.tagName.toLowerCase();

    return tagName === 'input';
  }
});
```

## Inclusion

To include videojs-contextmenu-pt on your website or web application, use any of the following methods.

### `<script>` Tag

This is the simplest case. Get the script in whatever way you prefer and include the plugin _after_ you include [video.js][videojs], so that the `videojs` global is available.

```html
<script src="//path/to/video.min.js"></script>
<script src="//path/to/videojs-contextmenu-pt.min.js"></script>
<script>
  var player = videojs('my-video');

  player.contextmenuUI();
</script>
```

### CommonJS/Browserify

When using with Browserify, install videojs-contextmenu-pt via npm and `require` the plugin as you would any other module.

```js
var videojs = require('video.js');

// The actual plugin function is exported by this module, but it is also
// attached to the `Player.prototype`; so, there is no need to assign it
// to a variable.
require('videojs-contextmenu-pt');

var player = videojs('my-video');

player.contextmenuUI();
```

### RequireJS/AMD

When using with RequireJS (or another AMD library), get the script in whatever way you prefer and `require` the plugin as you normally would:

```js
require(['video.js', 'videojs-contextmenu-pt'], function(videojs) {
  var player = videojs('my-video');

  player.contextmenuUI();
});
```

## License

Apache-2.0. Copyright (c) Brightcove, Inc.

[contextmenu]: https://github.com/brightcove/videojs-contextmenu
[videojs]: http://videojs.com/
