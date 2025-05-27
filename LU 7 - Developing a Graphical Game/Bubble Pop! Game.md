# 🎮 **Building a Bubble Pop Game in Android**

---

## 📋 **Objective:**

Create a simple tap-based reaction game where the player earns points by popping bubbles that float upwards on the screen. The aim is to test your understanding of **custom drawing using Canvas**, **user touch interaction**, **random positioning**, and **score tracking using SharedPreferences**.

---

## 🧩 **Learning Outcomes:**

By completing this activity, you will be able to:

* Use the `Canvas` and `Paint` classes to draw shapes dynamically
* Handle touch events and detect collisions using geometry
* Apply `Handler` or `postDelayed` for creating an animation loop
* Use `SharedPreferences` to store simple game data persistently

---

## 🛠️ **Breakdown:**

### 🔹 Part 1: Drawing the Game Elements

* Create a **custom View class**.
* Use the `onDraw()` method to draw multiple blue **circles (bubbles)** at random positions on the canvas.
* Continuously move bubbles **upwards** using a repeating update.

🎨 **Step 1: Create a Custom View Class**

🖼️ **Step 2: Override the `onDraw()` Method**

🌀 **Step 3: Make the Bubbles Move Upward**

---

### 🔹 Part 2: Handling User Interaction

Allow the player to tap on a bubble to “pop” it:

* Detect the location of the screen tap
* Check if a bubble was hit
* Remove that bubble
* Increase and track the score

**Step 1: Override the `onTouchEvent()` Method**

1. Inside your custom `View` class, override the `onTouchEvent()` method.

**Step 2: Loop Through All Bubbles to Check for a Hit**

Use the **distance formula**:

   * Distance = √((x2 - x1)² + (y2 - y1)²)
   * If this distance is **less than or equal to the bubble’s radius**, the tap hit that bubble.

**Step 3: Pop the Bubble and Update the Game State**

1. If a tap hit a bubble:

   * Remove the bubble from the list
   * Increase the player’s score by 1
    
2. You could show a toast, sound effect, or visual pop animation 

**Step 4: Redraw the View**

1. After modifying the bubble list or score reflect the updated bubble positions.

---

#### 🔹 Part 3: Tracking and Displaying Score

* Display the current score on the screen.
* Use `SharedPreferences` to save the last score and retrieve it when the app is reopened.

---

#### 🔹 Part 4: Finishing Touches (Optional)

* Add sound when a bubble is popped.
* Display “Game Over” if too many bubbles escape unpopped.
* Show a welcome screen that transitions into the game view.

---

### 💡 **Hints & Guidelines:**

* Use `Canvas.drawCircle()` to draw each bubble.
* Use `MotionEvent.ACTION_DOWN` to detect screen taps.
* Remember to call `invalidate()` to continuously redraw the canvas.
* Use `Random.nextInt()` to generate different starting positions for bubbles.

---


### 🧪 **Bonus Challenge:**

