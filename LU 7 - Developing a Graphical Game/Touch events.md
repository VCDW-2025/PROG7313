# ✅ 3. Explaination of the Use of Touch Events

**Touch events** allow an app to respond to user interactions with the screen — a crucial part of interactive and game-based apps.

---

### **Purpose:**

Detect and respond to user gestures such as taps, swipes, and drags.

---

### **How They Are Handled:**

* `onTouchEvent(MotionEvent event)` – Override this method in a `View` or `Activity` to respond to touch.
* `setOnTouchListener { v, event -> ... }` – Attach a listener to a specific view like an image or button.

---

### **Common Touch Event Actions:**

* **`ACTION_DOWN`** – User touches the screen (start of interaction).
* **`ACTION_MOVE`** – User moves finger on the screen (drag or swipe).
* **`ACTION_UP`** – User lifts finger off the screen (end of touch).

---

### **Use in Games:**

* Detect when and where a character or object is tapped.
* Move or drag game elements.
* Recognize swipe gestures for in-game controls (e.g., to jump, slide, or attack).

---

