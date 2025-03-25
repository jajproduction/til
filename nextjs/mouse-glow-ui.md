# Mouse Glow UI

I usually put this on the components folder and use them for styling.

```tsx
"use client";

import { useEffect, useState } from "react";

interface Position {
  x: number;
  y: number;
}

export default function MouseGlow() {
  const [position, setPosition] = useState<Position>({ x: 0, y: 0 });
  const [isMouseMoving, setIsMouseMoving] = useState<boolean>(false);

  useEffect(() => {
    const handleMouseMove = (e: MouseEvent) => {
      setPosition({ x: e.clientX, y: e.clientY });
      setIsMouseMoving(true);
    };

    const handleMouseStop = () => {
      setIsMouseMoving(false);
    };

    window.addEventListener("mousemove", handleMouseMove);
    window.addEventListener("mouseover", handleMouseMove);
    window.addEventListener("mouseout", handleMouseStop);

    return () => {
      window.removeEventListener("mousemove", handleMouseMove);
      window.removeEventListener("mouseover", handleMouseMove);
      window.removeEventListener("mouseout", handleMouseStop);
    };
  }, []);

  return (
    <div className="fixed top-0 left-0 w-full h-full pointer-events-none z-50">
      {isMouseMoving && (
        <div
          className="absolute w-[700px] h-[700px] rounded-full bg-blue-700/10 mix-blend-overlay blur-3xl"
          style={{
            left: position.x,
            top: position.y,
            transform: "translate(-50%, -50%)",
          }}
        ></div>
      )}
    </div>
  );
}
```
