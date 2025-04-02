# Radial Gradient Background

You can use this for your landing page, but be aware to configure this in your project.

```tsx
<div className="relative w-full overflow-hidden pt-12">
  <div className="mx-auto mb-24 max-w-3xl text-center text-7xl font-semibold text-white">
    <h1>{"Let's Craft Beautiful & Functional Web Experience"}</h1>
  </div>
  <div className="relative mx-auto w-full pt-[20%]">
    <div className="absolute top-0 -left-[15%] z-90 w-[130%] overflow-hidden rounded-[100%] border-2 border-zinc-300/60 bg-zinc-950/50 pt-[100%] shadow-[50px_60px_300px_10px_rgba(161,161,170,0.7),_0px_0px_64px_rgba(39,39,42,0.3),0px_0px_2px_rgba(107,114,128,0.7)_inset]">
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
      <div className="absolute left-1/2 h-[256px] w-[60%] -translate-x-1/2 -translate-y-1/2 scale-[2.5] rounded-[50%] bg-radial from-zinc-600/50 from-10% to-zinc-600/0 to-60% opacity-20 opacity-100 sm:h-[512px]"></div>
      <div className="absolute left-1/2 h-[128px] w-[40%] -translate-x-1/2 -translate-y-1/2 scale-200 rounded-[50%] bg-radial from-zinc-500/30 from-10% to-zinc-600/0 to-60% opacity-20 opacity-100 sm:h-[256px]"></div>
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
