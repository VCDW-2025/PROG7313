## **Learning Unit 7: Developing a Graphical Game**

### **Learning Objectives & Notes**

---

### ✅ **1. Explain the purpose of defining XML resource files**

* **Separation of concerns**: XML files allow you to separate UI design from app logic.
* **Maintainability**: UI changes don’t require altering Kotlin/Java code.
* **Reusability**: Define styles, strings, colors, and layouts once and reuse them.
* **Types of XML files**:

  * `layout` (e.g., `activity_game.xml`) – defines screen structure.
  * `drawable` – shapes, gradients, and images.
  * `values` – for storing constants (`strings.xml`, `colors.xml`, `styles.xml`).

---

### ✅ **2. Apply animations to controls in an app**

* **Types of animations**:

  * **Property Animation** (`ObjectAnimator`, `AnimatorSet`) – animates view properties like `alpha`, `translationX`.
  * **Tween Animation** – scale, rotate, move, or fade a view.
  * **Frame Animation** – display a series of images (like a flipbook).
* **Usage**: Improves user experience, adds fun to game UI.
* **Tools**: Use `animator/` XML directory or animate programmatically.

---

### ✅ **3. Explain the use of touch events**

* **Touch events** detect interaction with the screen.
* **Handled using**: `onTouchEvent(MotionEvent event)` or `setOnTouchListener`.
* **Common touch event actions**:

  * `ACTION_DOWN` – user touches screen.
  * `ACTION_MOVE` – user drags finger.
  * `ACTION_UP` – user lifts finger.
* **Game use**: Detect taps, swipes, or dragging objects.

---

### ✅ **4. Explain how to draw on a canvas**

* **Canvas**: A surface where you draw 2D graphics (lines, shapes, text, images).
* **Used inside a `View` subclass**:

  * Override `onDraw(Canvas canvas)` to customize drawing.
  * Use `Paint` objects to style (color, stroke, text size).
* **Example**: Drawing game characters, scores, or custom backgrounds.

---

### ✅ **5. Use a Timer object in Android**

* **Purpose**: Create timed events, e.g., game loops, countdowns.
* **Options**:

  * `Handler.postDelayed()` – run code after delay.
  * `CountDownTimer` – for countdown logic.
  * `Timer` and `TimerTask` – schedule repeated actions.
* **Example**: Move an object every 100ms to simulate motion.

---

### **Material Used**

* **GitHub repository**: `LearningUnit6`
  ➤ Ensure you've cloned or downloaded the repository from GitHub.

---

### **Preparation Checklist**

* ✅ Android Studio is updated.
* ✅ You can open and run the `LearningUnit6` project.
* ✅ You are familiar with locating and editing XML files.
* ✅ You know where to insert animation or timer logic in the codebase.

