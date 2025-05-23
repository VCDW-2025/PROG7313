# ✅ 1. Explain the Purpose of Defining XML Resource Files

XML resource files in Android development are used to define elements of the app's user interface and design in a structured, reusable way.

**Key Purposes:**

* **Separation of Concerns**:
  Keeps UI design (XML) separate from app logic (Kotlin/Java), making development cleaner and easier to manage.

* **Maintainability**:
  Allows developers to change the UI without modifying the underlying code. For example, changing a button’s text doesn’t require code changes.

* **Reusability**:
  Styles, strings, colors, and layouts can be defined once and reused throughout the app to ensure consistency and reduce duplication.

**Types of XML Files:**

* `layout/` – Defines the UI structure of activities and fragments (e.g., `activity_game.xml`).
* `drawable/` – Used for defining shapes, gradients, and image resources.
* `values/` – Holds constant values:

  * `strings.xml` – for text resources.
  * `colors.xml` – for color definitions.
  * `styles.xml` – for themes and text styles.
