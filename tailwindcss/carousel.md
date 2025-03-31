# Carousel

Take note to adjust the `scrollCarousel` and the seconds inside `animate-scrollCarousel` to loop the images.

```tsx
import Image from "next/image";

const imgs = [
  "1.jpeg",
  "2.jpeg",
  "3.jpeg",
  "4.jpeg",
  "5.jpeg",
  "6.jpeg",
  "7.jpeg",
  "8.jpeg",
  "9.jpeg",
  "10.jpg",
  "11.jpg",
  "12.jpg",
];

export function Posts() {
  return (
    <div className="relative overflow-hidden w-full">
      <div className="flex whitespace-nowrap animate-scrollCarousel">
        {[...imgs, ...imgs]
          .slice()
          .reverse()
          .map((name, index) => (
            <div key={index} className="flex-none w-[300px] h-[200px] mx-2">
              <Image
                src={`/${name}`}
                alt="Photo"
                width={300}
                height={200}
                className="w-full h-full rounded-lg shadow-md object-cover"
              />
            </div>
          ))}
      </div>
    </div>
  );
}
```

Add this to your `global.css` file.

```css
@keyframes scrollCarousel {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(-900%);
  }
}

.animate-scrollCarousel {
  display: flex;
  animation: scrollCarousel 90s linear infinite;
}
```
