# Cards For Pricing

A good example I created for pricing this is useful for your Saas.

```tsx
<div>
  <h3 className="text-zinc-200 font-medium">Simple Pricing. No Suprises.</h3>
  <p className="mt-1 text-zinc-400">
    Our plans are designed to fit businesses of all sizes—pay only for what you
    need, with the flexibility to grow.
  </p>
  <div className="mt-8 flex-col items-center md:flex md:justify-center">
    <div className="flex-col-reverse space-y-8 md:flex-row md:space-y-0 md:flex md:items-center md:gap-4">
      <div>
        <div className="relative w-full h-[420px] rounded-lg z-[1111] overflow-hidden flex flex-col justify-center shadow-lg shadow-[#36506c]/80 outline-2 outline-zinc-600 md:w-80 ">
          <div className="absolute w-full h-full z-[2] bg-zinc-900/50 backdrop-blur-4xl rounded-lg overflow-hidden"></div>
          <div className="absolute z-[1] top-1/2 left-1/2 w-80 h-[420px] rounded-full bg-[#36506c] opacity-100 blur-2xl"></div>
          <div className="absolute z-[1] top-1/2 right-1/2 w-80 h-[420px] rounded-full bg-zinc-900 opacity-100 blur-2xl"></div>
          <div className="absolute z-[1] bottom-1/2 right-1/2 w-80 h-[420px] rounded-full bg-zinc-900 opacity-100 blur-2xl"></div>
          <div className="z-[3] p-4 pt-0">
            <span>Starter</span>
            <p className="text-zinc-500">For small businesses starting out</p>
            <div className="mt-6">
              <span className="text-lg">
                ₱<span className="ml-1 text-4xl font-bold">2,999</span>
                <span className="text-xs">/month</span>
              </span>
            </div>
            <button className="mt-6 text-center bg-zinc-50 text-zinc-900 text-sm w-full p-2 rounded-lg cursor-pointer hover:bg-zinc-200">
              Get Started
            </button>
            <div className="mt-4">
              <p className="text-zinc-500 text-sm">Up to 5 users only.</p>
              <p className="text-zinc-500 text-sm">Extra user ₱200/month.</p>
            </div>
            <hr className="mt-4 border-zinc-600" />
            <div className="mt-4 space-y-2">
              <div className="flex items-center space-x-2">
                <CircleCheckBig className="w-4 h-4 text-zinc-400" />
                <span className="text-sm">POS (point-of-sale)</span>
              </div>
              <div className="flex items-center space-x-2">
                <CircleCheckBig className="w-4 h-4 text-zinc-400" />
                <span className="text-sm">Inventory Management</span>
              </div>
              <div className="flex items-center space-x-2">
                <CircleCheckBig className="w-4 h-4 text-zinc-400" />
                <span className="text-sm">CRM</span>
              </div>
              <div className="flex items-center space-x-2">
                <CircleCheckBig className="w-4 h-4 text-zinc-400" />
                <span className="text-sm">Basic Analytics</span>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div>
        <div className="relative w-full h-[450px] rounded-lg z-[1111] overflow-hidden flex flex-col justify-center shadow-lg shadow-[#36506c]/80 outline-2 outline-zinc-600 md:w-80">
          <div className="absolute w-full h-full z-[2] bg-[#36506c]/60 backdrop-blur-4xl rounded-lg overflow-hidden"></div>
          <div className="absolute z-[1] top-1/2 left-1/2 w-80 h-[450px] rounded-full bg-[#36506c] opacity-100 blur-2xl blob"></div>
          <div className="z-[3] p-4 pt-0">
            <span>Growth</span>
            <p className="text-zinc-500">For growing teams with more needs</p>
            <div className="mt-6">
              <span className="text-lg">
                ₱<span className="ml-1 text-4xl font-bold">5,999</span>
                <span className="text-xs">/month</span>
              </span>
            </div>
            <button className="mt-6 text-center bg-zinc-50 text-zinc-900 text-sm w-full p-2 rounded-lg cursor-pointer hover:bg-zinc-200">
              Get Started
            </button>
            <div className="mt-4">
              <p className="text-zinc-500 text-sm">Up to 10 users only.</p>
              <p className="text-zinc-500 text-sm">Extra user ₱250/month.</p>
            </div>
            <hr className="mt-4 border-zinc-600" />
            <div className="mt-4 space-y-2">
              <div className="flex items-center space-x-2">
                <CircleCheckBig className="w-4 h-4 text-zinc-400" />
                <span className="text-sm">Multi-Branch Support</span>
              </div>
              <div className="flex items-center space-x-2">
                <CircleCheckBig className="w-4 h-4 text-zinc-400" />
                <span className="text-sm">Advanced Reports</span>
              </div>
              <div className="flex items-center space-x-2">
                <CircleCheckBig className="w-4 h-4 text-zinc-400" />
                <span className="text-sm">Integrations</span>
              </div>
              <div className="flex items-center space-x-2">
                <CircleCheckBig className="w-4 h-4 text-zinc-400" />
                <span className="text-sm">Tasks Management</span>
              </div>
              <div className="flex items-center space-x-2">
                <CircleCheckBig className="w-4 h-4 text-zinc-400" />
                <span className="text-sm">POS</span>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div>
        <div className="relative w-full h-[420px] rounded-lg z-[1111] overflow-hidden flex flex-col justify-center shadow-lg shadow-[#36506c]/80 outline-2 outline-zinc-600 md:w-80">
          <div className="absolute w-full h-full z-[2] bg-zinc-900/50 backdrop-blur-4xl rounded-lg overflow-hidden"></div>
          <div className="absolute z-[1] top-1/2 right-1/2 w-80 h-[420px] rounded-full bg-[#36506c] opacity-100 blur-2xl"></div>
          <div className="absolute z-[1] top-1/2 left-1/2 w-80 h-[420px] rounded-full bg-zinc-900 opacity-100 blur-2xl"></div>
          <div className="absolute z-[1] bottom-1/2 left-1/2 w-80 h-[420px] rounded-full bg-zinc-900 opacity-100 blur-2xl"></div>
          <div className="z-[3] p-4 pt-0">
            <span>Custom</span>
            <p className="text-zinc-500">
              For businesses needing tailored solutions{" "}
            </p>
            <div className="mt-6">
              <p>Starts at</p>
              <span className="text-lg">
                ₱<span className="ml-1 text-4xl font-bold">40,000</span>
                <span className="text-xs">/month</span>
              </span>
            </div>
            <button className="mt-6 text-center bg-zinc-50 text-zinc-900 text-sm w-full p-2 rounded-lg cursor-pointer hover:bg-zinc-200">
              Get Started
            </button>
            <hr className="mt-4 border-zinc-600" />
            <div className="mt-4 space-y-2">
              <div className="flex items-center space-x-2">
                <CircleCheckBig className="w-4 h-4 text-zinc-400" />
                <span className="text-sm">Fully Tailored Development</span>
              </div>
              <div className="flex items-center space-x-2">
                <CircleCheckBig className="w-4 h-4 text-zinc-400" />
                <span className="text-sm">Advanced Features</span>
              </div>
              <div className="flex items-center space-x-2">
                <CircleCheckBig className="w-4 h-4 text-zinc-400" />
                <span className="text-sm">Special Integrations</span>
              </div>
              <div className="flex items-center space-x-2">
                <CircleCheckBig className="w-4 h-4 text-zinc-400" />
                <span className="text-sm">POS</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
```

Don't forget to add this to your `global.css` file.

```css
@keyframes blob-bounce {
  0% {
    transform: translate(-100%, -100%) translate3d(0, 0, 0);
  }
  25% {
    transform: translate(-100%, -100%) translate3d(100%, 0, 0);
  }
  50% {
    transform: translate(-100%, -100%) translate3d(100%, 100%, 0);
  }
  75% {
    transform: translate(-100%, -100%) translate3d(0, 100%, 0);
  }
  100% {
    transform: translate(-100%, -100%) translate3d(0, 0, 0);
  }
}

.blob {
  animation: blob-bounce 24s infinite ease-in-out;
}
```
