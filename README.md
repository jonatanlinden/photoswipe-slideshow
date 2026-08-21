# PhotoSwipe Slideshow plugin

Slideshow plugin for [PhotoSwipe](https://photoswipe.com/) v5

**[> Plugin demo <](https://codepen.io/dpet23/pen/dywPbGy)**

## Initialization

The plugin has a single JS file that must be imported.

It can be initialized like this:

```html
<script type="module">
import PhotoSwipeLightbox from 'photoswipe/dist/photoswipe-lightbox.esm.min.js';
import PhotoSwipeSlideshow from 'photoswipe-slideshow/photoswipe-slideshow.esm.min.js';

const lightbox = new PhotoSwipeLightbox({
  gallerySelector: '#gallery',
  childSelector: '.pswp-gallery__item',
  pswpModule: () => import('photoswipe/dist/photoswipe.esm.js'),
});

const _slideshowPlugin = new PhotoSwipeSlideshow(lightbox, {
  // Plugin options, for example:
  defaultDelayMs: 4000, // 4 sec
});

lightbox.init();
</script>
```

### Plugin options

#### `defaultDelayMs: 4000`

Slideshow delay in milliseconds.

Must be a number between `1000` (1 second) and `2147483647` (approximately 24.85 days).

If using the [Video plugin](https://github.com/dimsemenov/photoswipe-video-plugin),
note that slides with playing video will use the video's remaining length as the slideshow delay.

#### `playPauseButtonOrder: 6`

Where to place the slideshow toggle button, relative to other toolbar items.

By default, it's placed next to the slide counter.
See [PhotoSwipe's API](https://photoswipe.com/adding-ui-elements/#uiregisterelement-api) for the order of the default elements.

#### `restartOnSlideChange: true`

Whether slide changes should restart the timer.

This is useful if manual slide changes are expected during a slideshow,
especially if mixing image and video content.

## Differences from upstream

This fork has no progress bar. Upstream registers a `.pswp__progress-bar` element
and injects a `<style>` block for it from the plugin constructor; both are removed
here, along with the `progressBarPosition`, `progressBarTransition` and
`autoHideProgressBar` options that only configured them.

Two reasons beyond taste: a countdown drawn over the image competes with the image
for attention, and because the injection was unguarded, an application that
constructs the plugin more than once per document — anything rebuilding its
lightbox after client-side navigation — accumulated one `<style>` element per
construction.

## Added HTML elements

The plugin adds elements with the following CSS attributes:

* `.pswp__button--playpause-button`: A button for starting or stopping the slideshow

## Keyboard bindings

* `Space`: Start or stop the slideshow

* `+`/`-` or the Up/Down arrow keys: Change the slideshow playback speed by 1 second
---

<a href="https://www.buymeacoffee.com/htmltiger"><img src="https://www.buymeacoffee.com/assets/img/custom_images/white_img.png" alt="Buy Me A Coffee"></a>
