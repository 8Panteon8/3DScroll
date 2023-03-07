# 3D Scroll

## Key points

- Main container styling

```css
.container {
  width: 100%;
  height: 100%;
  position: fixed;
  perspective: 1500px;
}
```

>Note that if you add a [`perspective`](https://developer.mozilla.org/en-US/docs/Web/CSS/perspective) css class, its children must have the [`transform-style: preserve-3d`](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-style)

- Setting scroll

```javascript
let zSpacing = -1000;
let lastPos = zSpacing / 5;
let $frames = document.getElementsByClassName("frame");
let frames = Array.from($frames);
let zVals = [];

window.onscroll = function () {
  let top = document.documentElement.scrollTop;
  let delta = lastPos - top;

  lastPos = top;

  frames.forEach(function (n, i) {
    zVals.push(i * zSpacing + zSpacing);
    zVals[i] += delta * -5.5;
    let frame = frames[i];
    let transform = `translateZ(${zVals[i]}px)`;
    let opacity = zVals[i] < Math.abs(zSpacing) / 1.8 ? 1 : 0;
    frame.setAttribute("style", `transform: ${transform}; opacity: ${opacity}`);
  });
};
```

>Add mini animation when opening the page

```javascript
window.scrollTo(0, 1);
```

---
- Adding audio

```javascript
let soundButton = document.querySelector(".soundbutton");
let audio = document.querySelector(".audio");

soundButton.addEventListener("click", (e) => {
  soundButton.classList.toggle("paused");
  audio.paused ? audio.play() : audio.pause();
});
```

- Setting playback triggers

```javascript
window.onfocus = function () {
  soundButton.classList.contains("paused") ? audio.pause() : audio.play();
};

window.onblur = function () {
  audio.pause();
};
```

## Screenshot

![ezgif com-video-to-gif-2](https://user-images.githubusercontent.com/113831614/223494675-24b825c3-832c-4a5d-aa52-4793e917b2bb.gif)





