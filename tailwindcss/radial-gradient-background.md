# Radial Gradient Background

You can use this for your landing page, but be aware to configure this in your project.

```tsx
<div className="relative w-full h-screen overflow-hidden pt-12">
  <div className="mx-auto mb-24 max-w-3xl text-center text-7xl font-semibold text-white">
    <h1>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</h1>
  </div>
  <div className="relative mx-auto w-full pt-[20%]">
    <div className="absolute top-0 -left-[15%] z-90 w-[130%] overflow-hidden rounded-[100%] border-2 border-zinc-50 bg-zinc-950 pt-[100%] shadow-[4px_60px_100px_4px_rgba(161,161,170,0.7),_0px_0px_64px_rgba(39,39,42,0.3),0px_0px_2px_rgba(107,114,128,0.7)_inset]"></div>
    <div className="absolute top-0 -left-[15%] z-90 w-[130%] overflow-hidden rounded-[100%] border-4 border-zinc-300/50 bg-zinc-950/50 pt-[100%] shadow-[50px_60px_300px_10px_rgba(161,161,170,0.7),_0px_0px_64px_rgba(39,39,42,0.3),0px_0px_2px_rgba(107,114,128,0.7)_inset]">
      <div
        className="absolute top-0 -left-[50%] h-[200%] w-[200%] rounded-[100%] bg-zinc-950/80"
        style={{
          maskImage:
            "radial-gradient(140% 100%, transparent 0%, transparent 15%, black 95%)",
        }}
      ></div>
      <div
        className="animate-pulse-hover absolute -top-[1%] -left-[50%] h-[200%] w-[200%] rounded-full bg-zinc-400/80"
        style={{
          maskImage:
            "radial-gradient(140% 120%, transparent 0%, transparent 38%, black 43%)",
        }}
      ></div>
    </div>
    <div data-slot="glow" className="absolute top-[50%] w-full">
      <div className="absolute left-1/2 h-[154px] w-[60%] -translate-x-1/2 -translate-y-1/2 scale-[1.5] rounded-[50%] bg-radial from-zinc-100/50 from-4% to-zinc-200/0 to-50% opacity-100 md:h-[554px]"></div>
      <div className="absolute left-1/2 h-[160px] w-[40%] -translate-x-1/2 -translate-y-1/2 scale-200 rounded-[50%] bg-radial from-zinc-200/20 from-8% to-zinc-300/0 to-60% opacity-100 md:h-[624px]"></div>
      <div className="absolute z-95 top-1/2 left-3/4 w-full h-[134px] translate-y-16 rounded-full bg-zinc-950 blur-xl"></div>
      <div className="absolute z-95 top-1/2 right-3/4 w-full h-[134px] translate-y-16 rounded-full bg-zinc-950 blur-xl"></div>
    </div>
  </div>
</div>
```

Then add this to your `global.css` file.

```css
@keyframes pulse-hover {
  0% {
    transform: translate(0, 0);
    opacity: 1;
  }
  25% {
    transform: translate(2px, -8px);
    opacity: 0.95;
  }
  50% {
    transform: translate(0px, -10px);
    opacity: 0.8;
  }
  75% {
    transform: translate(-2px, -8px);
    opacity: 0.95;
  }
  100% {
    transform: translate(0, 0);
    opacity: 1;
  }
}

.animate-pulse-hover {
  border-radius: 100%;
  filter: blur(10px);
  animation: pulse-hover 10s infinite;
}
```
