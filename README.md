<p align="center">
  <a href="https://www.npmjs.com/package/v-img-viewer"><img src="https://img.shields.io/npm/v/v-img.svg" alt="Version"></a>
  <a href="https://www.npmjs.com/package/v-img-viewer"><img src="https://img.shields.io/npm/dm/v-img.svg" alt="Downloads"></a>
  <a href="https://www.npmjs.com/package/v-img-viewer"><img src="https://img.shields.io/npm/l/v-img.svg" alt="License"></a>
</p>


<p align="center">
  <img src="https://media.giphy.com/media/xUA7b26WKJvTa04lby/giphy.gif" alt="Demonstration">
</p>

v-img is a plugin for [Vue.js](https://vuejs.org/) that allows you to show images in full-screen gallery by adding only one directive to the `<img>` tag.


## Installation

#### via npm
```
npm install v-img-viewer --save
```

In your script entry point:

```javascript
import Vue from 'vue';
import VueImg from 'v-img-viewer';

Vue.use(VueImg);
```

#### For Nuxt application:
1. create a new package `v-img.js`

```javascript

import Vue from 'vue';
import VueImg from 'v-img-viewer';

Vue.use(VueImg, {
  // configuration
});
```

2. Register the package in `nuxt.config.ts`

```javascript
plugins: [
  ...,
  '~/plugins/v-img.js'
]
```
3. and now you can use `v-img` directive everywhere.

#### via CDN
[![](https://data.jsdelivr.com/v1/package/npm/v-img-viewer/badge)](https://www.jsdelivr.com/package/npm/v-img-viewer)
* make sure to change `latest` to the number of latest version of the plugin to avoid compatibility problems.
```html
<!-- After vuejs -->
<script src="https://cdn.jsdelivr.net/npm/v-img@latest/dist/v-img-viewer.min.js"></script>
```

### Optional configurations
*in this snippet all settings has its default value. No need to specify them unless you want to change default behavior. Unfortunately if you used CDN way to include plugin you can't set up these options, but still can set them up inline.
```javascript
const vueImgConfig = {
  // Use `alt` attribute as gallery slide title
  altAsTitle: false,
  // Display 'download' button near 'close' that opens source image in new tab
  sourceButton: false,
  // Event listener to open gallery will be applied to <img> element
  openOn: 'click',
  // Show thumbnails for all groups with more than 1 image
  thumbnails: false,
}
Vue.use(VueImg, vueImgConfig);
```

## Usage

Add `v-img` directive to the image.
```vue
<img v-img class="v-img" src="...">
```

### Available options
Add similar directive arguments to place images to one gallery. (`:name` from the example below could be anything you want)
```vue
<img v-img:name class="v-img" src="...">
<img v-img:name class="v-img" src="...">
```

Options that could be specified in directive value

```vue
<img v-img="{ ... }" class="v-img" src="...">
```

| Option | Description | Default value | Data type |
| :----: | :---------: | :-----------: | :-------: |
| group  | The same as directive argument, but could be set dynamically | directive argument or undefined | string |
| src    | Image source that will be displayed in gallery | src attribute value from html tag | string |
| title  | Caption that will be displayed | empty string or value of the `alt` attribute, if `altAsTitle` is true | string |
| openOn | Event listener to open gallery will be applied to `<img>`. Available options are 'dblclick', 'mouseover' and all native JS events. | 'click' if another not stated when initializing plugin | string |
| sourceButton | Display 'download' button near 'close' that opens source image in new tab | `false` if `sourceButton` is not set to true when initializing plugin | boolean |
| thumbnails | When opening group by clicking (or other `openOn` event) on this image, thumbnails of images for this group will be visible | `false` if `thumbnails` is not set to true when initializing plugin | boolean |
| opened | Function that will be executed on gallery open | undefined | function |
| closed | Function that will be executed on gallery close | undefined | function |
| changed(imageIndex) | Function that will be executed when switching between images in gallery | undefined | function |
| cursor | Cursor when hovering original `<img>` | 'pointer' | string |

* Any of these options except `opened`, `closed`, `changed` functions and `openOn` property could be changed at runtime.
