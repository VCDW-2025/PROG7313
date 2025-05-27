# 🧠 What Is a Bitmap?

A **Bitmap** is a **2D array of pixels** that represents an image. Each pixel has data about its color and (optionally) transparency.

In Android, bitmaps are handled by the `android.graphics.Bitmap` class.

---

### 🔄 How Bitmaps Work in Android

#### 1. **Loading a Bitmap**

To load a bitmap (like a PNG or JPG) from resources:

```kotlin
val bitmap = BitmapFactory.decodeResource(resources, R.drawable.my_image)
```

This converts the image in `res/drawable` into a `Bitmap` object in memory.

#### 2. **Drawing a Bitmap**

To draw it on the screen (e.g., in a game), use `Canvas.drawBitmap()`:

```kotlin
override fun onDraw(canvas: Canvas) {
    canvas.drawBitmap(bitmap, xPosition, yPosition, null)
}
```

This renders the bitmap at the specified `x` and `y` position.

#### 3. **Scaling / Resizing a Bitmap**

You can create a smaller/larger version of the bitmap:

```kotlin
val resized = Bitmap.createScaledBitmap(bitmap, width, height, true)
```

#### 4. 🧪**Creating a Blank Bitmap**

You can create an empty canvas to draw on (like a whiteboard):

```kotlin
val blankBitmap = Bitmap.createBitmap(300, 300, Bitmap.Config.ARGB_8888)
val canvas = Canvas(blankBitmap)
canvas.drawColor(Color.WHITE)
```

---

### 🔧 Common Bitmap Use Cases

| Use Case                  | Example                                         |
| ------------------------- | ----------------------------------------------- |
| Show image in `ImageView` | `imageView.setImageBitmap(bitmap)`              |
| Draw game objects         | Used in `Canvas`-based game loops               |
| Apply effects             | Manually change pixels for filters or grayscale |
| Save view as image        | Draw a view to bitmap to save as a screenshot   |

---
