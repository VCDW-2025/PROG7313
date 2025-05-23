# ✋ **Part 2: Add Touch-Based Interaction**

### **🎯 Objective:**

Bring your animated game button to life by adding interactive touch gestures. This will give your app game-like responsiveness and deepen your understanding of touch handling.

---

### **🧪 Instructions:**

#### 🔹 **A. Detect a Basic Touch**

> 🎯 Goal: Make your app respond to any tap on the screen.

1. Attach a touch listener to the root layout of your screen (e.g., `RelativeLayout`, `ConstraintLayout`, or similar).
2. Within your touch listener, check for the **initial touch action** (`ACTION_DOWN`).
3. When the screen is touched:

   * Display a short message on screen (use a `Toast`, `Snackbar`, or change text).
   * OR trigger a simple animation on the Play button (e.g., make it bounce or glow briefly).
4. Make sure the gesture only triggers once per tap (avoid repeated triggers on move or hold).

🧠 *Think about:* Why is it useful to filter touch actions by type (e.g., DOWN vs MOVE)? What might go wrong if you don’y?

---

#### 🔹 **B. Respond to Drag or Swipe**

> 🎯 Goal: Track finger movement and create a visual response.

1. Inside your touch listener, check for the `ACTION_MOVE` event.
2. As the user drags their finger across the screen:

   * Update the position of an object on screen (you can reuse your Play button or add a new shape/image).
   * You'll need to calculate new coordinates based on the finger’s position — think about using raw X/Y values.
3. Make sure the object smoothly follows the finger without snapping or jumping unexpectedly.

💡 *Challenge yourself to:* Handle screen boundaries so the object doesn’t go off-screen.

---

#### 🔹 **C. Optional Challenge (Bonus): Drag and Drop Interaction**

> 🎯 Goai: Make the Play button draggable and only move when actually touched.

1. Only allow dragging if the touch **starts on the Play button** (not anywhere on the screen).
2. Use a combination of `ACTION_DOWN`, `ACTION_MOVE`, and `ACTION_UP` to:

   * Begin dragging only when the button is touched.
   * Move it while the finger moves.
   * Stop moving when the finger lifts off.

✨ *Extra Features:*

* Snap the button to a fixed position when dropped.
* Add a sound or animation on successful drop.

---

### **Touch Actions You’ll Work With:**

* `ACTION_DOWN` – The initial touch (like mouse down).
* `ACTION_MOVE` – Dragging motion.
* `ACTION_UP` – Finger release (like mouse up).

---

