# 🪻 **Layouts and Controls**

This section teaches how to structure your Android app’s UI using **layouts** and add interactive **controls** that users can interact with.

---

## 🧩 **1. Layouts**

**Layouts** define how UI elements (widgets) are arranged on the screen. They act as containers for views like buttons, text fields, and images.

#### Common Types:
- **LinearLayout**: Arranges elements **vertically** or **horizontally**.
- **RelativeLayout**: Positions elements **relative to each other** or the parent.
- **ConstraintLayout**: A flexible layout that lets you **position elements with constraints** (used in most modern Android apps).
- **FrameLayout**: Useful for **stacking** views.

You define layouts in XML files like activity_main.xml.  

#### Example (LinearLayout):

```xml
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    
    <TextView
        android:text="Hello, User!"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>
</LinearLayout>
```

---

## 🎮 **2. Controls/Widgets**

Controls are the building blocks that allow user interaction. Examples include:

| Control     | Description |
|-------------|-------------|
| **EditText** | Text input field for users (e.g., entering a name). |
| **Button**   | Performs an action when clicked. |
| **TextView** | Displays text. |
| **SeekBar**  | Slider control for selecting a value (e.g., volume). |
| **CheckBox** / **RadioButton** | For selecting options. |

#### Example of EditText:

```xml
<EditText
    android:id="@+id/editTextName"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:hint="Enter your name" />
```

#### SeekBar Example (in XML):

```xml
<SeekBar
    android:id="@+id/seekBar"
    android:layout_width="match_parent"
    android:layout_height="wrap_content" />
```

---

### 🎯 **Putting It Together**
You combine **layouts** and **controls** in XML to define your UI, then use Kotlin/Java code to handle user interactions.
