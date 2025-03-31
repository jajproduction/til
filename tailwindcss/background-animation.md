# Background Animation

This could be a perfect example for background animation using tailwindcss, put this in your `global.css` file:

```css
.bg-custom-gradient {
  background:
    radial-gradient(at 19% 86%, #000000 0px, transparent 50%),
    radial-gradient(at 17% 57%, #36506c 0px, transparent 50%),
    radial-gradient(at 57% 54%, #36506c 0px, transparent 50%),
    radial-gradient(at 24% 21%, #000000 0px, transparent 50%), #000000;

  background-size: 200% 200%;
  animation: pulse-bg 20s infinite ease-in-out;
}

@keyframes pulse-bg {
  0% {
    background-position: 0% 0%;
  }
  50% {
    background-position: 50% 50%;
  }
  100% {
    background-position: 0% 0%;
  }
}
```

```html
<div className="bg-custom-gradient">
  <!-- contents -->
</div>
```
