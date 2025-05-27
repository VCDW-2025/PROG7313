# 🎮 **Building a Bubble Pop Game in Android**

---

### 📋 **Objective:**

Create a simple tap-based reaction game where the player earns points by popping bubbles that float upwards on the screen. The aim is to test your understanding of **custom drawing using Canvas**, **user touch interaction**, **random positioning**, and **score tracking using SharedPreferences**.

---

### 🧩 **Learning Outcomes:**

By completing this activity, you will be able to:

* Use the `Canvas` and `Paint` classes to draw shapes dynamically
* Handle touch events and detect collisions using geometry
* Apply `Handler` or `postDelayed` for creating an animation loop
* Use `SharedPreferences` to store simple game data persistently

---

### 🛠️ **Breakdown:**

#### 🔹 Part 1: Drawing the Game Elements

* Create a **custom View class**.
* Use the `onDraw()` method to draw multiple blue **circles (bubbles)** at random positions on the canvas.
* Continuously move bubbles **upwards** using a repeating update.

#### 🔹 Part 2: Handling User Interaction

* Implement `onTouchEvent()` to detect taps.
* Determine if the user tapped within a bubble (use distance formula).
* Remove the tapped bubble and increase the player’s score.

#### 🔹 Part 3: Tracking and Displaying Score

* Display the current score on the screen.
* Use `SharedPreferences` to save the last score and retrieve it when the app is reopened.

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

