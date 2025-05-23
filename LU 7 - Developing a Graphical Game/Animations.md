# ✅ 2. Apply Animations to Controls in an App

Animations enhance interactivity and improve user engagement in mobile apps, especially in games.

**Types of Animations:**

* **Property Animation**
  Uses classes like `ObjectAnimator` and `AnimatorSet` to animate properties such as:

  * `alpha` (fade in/out)
  * `translationX`, `translationY` (movement)
  * `scaleX`, `scaleY` (resizing)
  * `rotation` (spinning)

* **Tween Animation**
  Predefined transformations including:

  * **Scale** – resize a view
  * **Rotate** – spin a view
  * **Translate** – move a view from one point to another
  * **Alpha** – change opacity (fade effects)

* **Frame Animation**
  Shows a sequence of images (like a cartoon flipbook). Defined in XML using `<animation-list>` and used for character or sprite animations.

**Usage in Apps:**

* Adds dynamic behavior to UI elements (e.g., buttons, game objects).
* Makes the interface feel more responsive and alive.
* Enhances visual feedback (e.g., button pulse when tapped).

**How to Apply Animations:**

* Use XML files in the `animator/` or `anim/` directory (for reusable animations).
* Or apply animations programmatically in Kotlin using Android’s animation libraries.
