# Img-previewer Js

Lightweight and powerful `javascript` image preview plug-in, silky animation allows you to elegantly preview the images in your website. Out of the box, you don't need extra configuration (by default) or change the page `html` code structure, you can easily enable the plugin in any type of website and upgrade your user experience

These functions are provided:

1. Silky, interruptible transition animation
2. Use mouse wheel to zoom picture
3. Icon drag picture
4. Previous & Next
5. Shortcut key support
6. Support for mobile gestures (zoom in with two fingers)
7. Multi-language internationalization support
8. Picture loading monitor

**tips: For performance reasons, the mobile terminal does not do swiper**

# Example

[Preview](https://www.ltp110.tk/img-previewer/)

# How to use

```html
<link rel="stylesheet" href="./img-previewer.css">
<script src="./img-previewer.js"></script>
<script>
  const imgPreviewer = new ImgPreviewer('#app', {
    scrollbar: true
  });
</script>
```

# Property list

|               | Type   | Description                                                                         | Default Value                                   |
| ------------- | ------ | ----------------------------------------------------------------------------------- | ----------------------------------------------- |
| fillRatio     | number | The proportion of the image that fills the preview area                             | 0.9(90%)                                        |
| dataUrlKey    | string | The key of the image address value                                                  | src                                             |
| triggerEvent  | string | trigger event                                                                       | click                                           |
| imageZoom     | object | Zoom image configuration                                                            | {min: 0.1,max: 5,step: 0.1}                     |
| style         | object | Style configuration                                                                 | {modalOpacity: 0.6,headerOpacity: 0,zIndex: 99} |
| i18n          | object | tooltips International configuration                                                | null                                            |
| bubblingLevel | number | Bubble to detect whether the parent element of the image is hidden by the css style | 0                                               |

> Optional values for triggerEvent are: click and dblclick
## bubblingLevel Description
You should try to use this property when you notice an abnormal image hide animation. Because when the image or the parent element of the image is hidden by some CSS styles, it cannot be detected through the js api, so you need to pass in the correct upward lookup level according to the actual situation to help the plug-in complete the correct hiding animation. As shown below, the correct bubblingLevel is at least 3

**for performance considerations, it is not recommended to fill in this attribute value at will**

```html
<div style="opacity:0"> <!-- 3 -->
	<div> <!-- 2 -->
		<img src="" alt="" /> <!-- 1 -->
	</div>
</div>
```

**Notice:**
Currently detecting that an element or parent element is hidden by a css style only supports the following styles:

- opacity: 0;
- height: 0;
- width: 0;
- visibility: hidden;

## options.imageZoom

|      | Description                                    | Default value |
| ---- | ---------------------------------------------- | ------------- |
| min  | Minimum zoom ratio                             | 0.1(10%)      |
| max  | Maximum zoom ratio                             | 5(500%)       |
| step | The change ratio of the scroll wheel each time | 0.1           |

## options.style

|               | Description                    | Default value |
| ------------- | ------------------------------ | ------------- |
| modalOpacity  | Preview area mask transparency | 0.6           |
| headerOpacity | Toolbar transparency           | 0             |
| zIndex        | Level of plug-in rendering     | 99            |

## options.i18n

Simplified Chinese and English are supported by default, others need to be configured by themselves

|              | Description   |
| ------------ | ------------- |
| RESET        | Reset         |
| ROTATE_LEFT  | Rotate Left   |
| ROTATE_RIGHT | Rotate right  |
| CLOSE        | Close preview |
| NEXT         | Next          |
| PREV         | Previous      |

## api methods

|       Method name             | Description                |
| ------------------ | -------------------------- |
| update()           | update image els           |
| getTotalIndex()    | get total image el numbers |
| show(index:number) | show index image           |
| next()             | goto next                  |
| prev()             | goto prev                  |

### hot key

| Button | Description   |
| ------ | ------------- |
| Esc    | Close preview |
| <=     | Previous      |
| =>     | Next          |

# Update picture

Some dynamically updated picture lists use

```js
const imgPreviewer = new ImgPreviewer('body')
// Called after the image is rendered on the page
imgPreviewer.update()
```

# play slideshow

```js
let timer = null
function play() {
	timer && clearInterval(timer)
	let index = 0
	a.show(index)
	timer = setInterval(() => {
		if (index < a.getTotalIndex()) {
			index++
		} else {
			index = 0
		}
		a.show(index)
	}, 2000)
}
play()
``` 
