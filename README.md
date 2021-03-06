# object-fit-polyfill
A polyfill for browsers that don't support the `object-fit` CSS property. Unsure of what the `object-fit` does? Essentially `object-fit` is to `<img>` tags what `background-size` is to `background-image`. You can check out the [MDN page](https://developer.mozilla.org/en-US/docs/Web/CSS/object-fit) for more details.

## Features

- Lightweight - 2.6KB (1.8KB with the basic version)
- Vanilla Javascript - works with or without jQuery
- Supports IE 9+, iOS 7-, and Android 4.4-
- Supports `object-position`
- Works with `image`, `video`, `srcset`, and `picture`
- Plug and play - just include the .js file and set data attributes on your elements.
- Please note: This plugin makes the assumption that the parent container is acting as a picture frame, and already has a height & width set.

## Demo

You can check out the [bare-bones demo here](http://constancecchen.github.io/object-fit-polyfill). Note that the plugin simply won't do anything if you're on a browser that already supports object-fit, so you'll want to test it on IE or older iOS/Android browsers.

## How does it work?

Unlike [object-fit-images](https://github.com/bfred-it/object-fit-images) or [Primož Cigler's method](https://medium.com/@primozcigler/neat-trick-for-css-object-fit-fallback-on-edge-and-other-browsers-afbc53bbb2c3#.17fpxgk0w) (both excellent alternatives if you'd rather not use this one), this polyfill does not set a background image on the parent container, but instead resizes and repositions the image (using inline CSS for height, width, absolute positioning, and negative margins).

The polyfilled item will get the class `object-fit-polyfill` if styling-issues are occuring.

If you're wondering: why bother using `<img>` tags versus `background-image`? Here's a couple reasons:

1. `<img>` tags have better SEO/crawling visibility.
2. In cases where images are dynamically returned and can't simply be added to your stylesheets (e.g., CMS's), you're forced to inline your background-image. This solves that somewhat-ugly-looking inline CSS.
3. `background-image` doesn't work with `video` or `picture` elements.

Of course, there's still plenty of cases where using a background image makes more sense than a regular image.

## Usage

Initialization:

```html
<!-- Minimum CSS -->
<style>
.container {
  width: 25em; /* Or whatever you want it to be */
  height: 25em; /* Or whatever you want it to be */
}
.media {
  width: 100%;
  height: 100%;
  object-fit: cover; /* Or whatever object-fit you want */
}
</style>

<!-- Minimum HTML -->
<div class="container">
  <img class="media" data-object-fit="cover" src="https://unsplash.it/800/600/" alt="">
</div>

<script src="dist/objectFitPolyfill.min.js"></script>
```

Customized object-fit/object-position:

```html
<div class="container">
  <img class="media" data-object-fit="contain" data-object-position="top left" src="https://unsplash.it/800/600/" alt="">
</div>

<div class="container">
  <img class="media" data-object-fit="none" data-object-position="25% 75%" src="https://unsplash.it/800/600/" alt="">
</div>

<div class="container">
  <img class="media" data-object-fit="scale-down" data-object-position="3em -1em" src="https://unsplash.it/800/600/" alt="">
</div>
```

If you're only interested in using the basic polyfill (which assumes `object-fit: cover` and `object-position: 50% 50%`), you can save yourself some bytes by using:

```html
<div class="container">
	<img class="media" data-object-fit src="https://unsplash.it/800/600/" alt="">
</div>

<script src="dist/objectFitPolyfill.basic.min.js"></script>
```

## Installation via package managers

Alternatively, if you prefer not to manually add Javascript files to your sites, you can use bower and npm like so:

```
bower install objectFitPolyfill
```

```
npm install objectFitPolyfill
```

## Requests?

If you'd like to make feature requests such as IE 8- or adding object-position support for Safari, feel free to open an issue or pull request! It's doable and on my radar, but I probably won't get to it without some prodding.
