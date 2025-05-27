### 🖼️ What Is `Canvas` in Android?

In Android, a **`Canvas`** is like a **blank sheet of paper** you can draw on. It’s a powerful class that allows you to render 2D graphics (like shapes, text, and images) directly on the screen using code — especially useful for games, custom views, and drawing apps.

---

### 🎯 Purpose of `Canvas`

* **Draw shapes**: lines, rectangles, circles
* **Draw text**: labels, scores, titles
* **Draw bitmaps**: images, characters, backgrounds
* **Animate custom graphics**: move objects across the screen

---

### 🔧 How Canvas Works (Basic Flow)

1. You create a **custom view class** by extending `View`.
2. Override the `onDraw(canvas: Canvas)` method.
3. Use the `canvas` object to draw whatever you need.

---

### 🛠️ Example

```kotlin
class MyDrawingView(context: Context) : View(context) {
    override fun onDraw(canvas: Canvas) {
        super.onDraw(canvas)
        
        val paint = Paint()
        paint.color = Color.RED
        paint.strokeWidth = 10f

        // Draw a red circle
        canvas.drawCircle(200f, 200f, 100f, paint)
    }
}
```

> This draws a red circle on the screen at (200, 200) with radius 100.

---

### ✏️ What You Can Draw with Canvas

| Method                               | Purpose              |
| ------------------------------------ | -------------------- |
| `drawLine(x1, y1, x2, y2)`           | Draw a straight line |
| `drawRect(left, top, right, bottom)` | Draw a rectangle     |
| `drawCircle(cx, cy, r)`              | Draw a circle        |
| `drawBitmap(bitmap, x, y, paint)`    | Draw an image        |
| `drawText("Hello", x, y, paint)`     | Draw text            |

You can control colors, fonts, line thickness, and styles using the `Paint` object.

---

### 🕹️ Canvas in Games (Like PROG7313)

In **Learning Unit 7**, games use `Canvas` to:

* Continuously **draw bitmaps** at updated positions
* Display scores, lives, and “Game Over” text
* Handle real-time visual updates by calling `invalidate()` (which triggers `onDraw()`)

---

### 🔄 Game Loop with Canvas

A timer or thread calls `invalidate()` repeatedly (e.g., every 30 ms):

```kotlin
postInvalidate() // or invalidate()
```

This re-triggers `onDraw()` → which redraws your scene (updated positions, animations, etc.)

---

### 💡 

`Canvas` is **low-level**, but extremely flexible. It’s perfect when:

* You want full control over your UI
* You’re building a **game**, **custom chart**, or **interactive drawing tool**

---

## 🔍 When *Canvas* Is Enough

Canvas is:

* Great for **simple 2D games**
* Good for **custom views** (drawing shapes, bitmaps, charts)
* Lightweight and native to Android

But it has **limitations**:

* Manual redrawing (no built-in animation engine)
* No hardware acceleration for advanced rendering
* Tedious for large games or complex UIs

---

## 🚀 Alternatives:

### 1. **Jetpack Compose**

> 🧠 **Modern UI toolkit for Android** (declarative and reactive)

✅ Better when:

* You’re building **modern UIs** with animations, state, and responsiveness
* You want less boilerplate and cleaner code
* You need built-in animations

🚫 Not for: low-level drawing (though Compose has `Canvas()` API too)

---

### 2. **SurfaceView / TextureView**

> 🛠️ Used for **high-performance real-time rendering**

✅ Better than Canvas when:

* You need **hardware acceleration**
* You’re rendering **fast-moving graphics or video**
* Ideal for **games and camera apps**

```kotlin
class GameSurfaceView(context: Context) : SurfaceView(context), Runnable { ... }
```

---

### 3. **OpenGL ES**

> 🎮 For **3D or GPU-accelerated 2D rendering**

✅ Use it when:

* You're building **high-performance games**
* You need **particle effects**, **shaders**, **3D graphics**

🚫 Steep learning curve. Often used with engines like Unity or LibGDX.

---

### 4. **Game Engines (LibGDX, Unity, Godot)**

> 🧩 Frameworks built on top of OpenGL or Vulkan

✅ Best for:

* Complex 2D/3D games
* Cross-platform development (iOS, Desktop, Web)
* Built-in physics, animation, asset management

---

### ✨ Summary

| Use Case                        | Recommended Option        |
| ------------------------------- | ------------------------- |
| Simple 2D drawings & games      | Canvas                    |
| Modern UI with animation        | Jetpack Compose           |
| Real-time, smooth graphics      | SurfaceView / TextureView |
| Full-featured game engine       | LibGDX / Unity / Godot    |
| Advanced graphics (3D, shaders) | OpenGL ES or Vulkan       |

---


