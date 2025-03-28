# ⚡ **Event Handling (Learning Unit 4 – Section 2)**

**Event handling** in Android refers to how your app responds to user actions like clicks, touches, typing, or swiping. 

These interactions trigger **events**, and you write code to **handle** what happens when those events occur.

---

## 🧩 **1. Common Events**

| Event Type | Triggered When... |
|------------|-------------------|
| `onClick`  | A button is clicked/tapped |
| `onTouch`  | The user touches the screen |
| `onTextChanged` | Text input changes |
| `onCheckedChanged` | A CheckBox or RadioButton is selected or deselected |
| `onSeekBarChange` | A SeekBar is moved |

---

## 🖱 **2. Handling a Button Click**

Two main ways:

### Option A: **Using XML**

```xml
<Button
    android:id="@+id/btnClick"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:onClick="handleButtonClick"
    android:text="Click Me" />
```

```kotlin
fun handleButtonClick(view: View) {
    Toast.makeText(this, "Button clicked!", Toast.LENGTH_SHORT).show()
}
```

### Option B: **In Kotlin Code**

More flexible, especially when attaching multiple listeners.

```kotlin
val btnClick = findViewById<Button>(R.id.btnClick)
btnClick.setOnClickListener {
    Toast.makeText(this, "Button clicked!", Toast.LENGTH_SHORT).show()
}
```

---

### **3. Example: SeekBar Event**

```kotlin
val seekBar = findViewById<SeekBar>(R.id.seekBar)
seekBar.setOnSeekBarChangeListener(object : SeekBar.OnSeekBarChangeListener {
    override fun onProgressChanged(seekBar: SeekBar?, progress: Int, fromUser: Boolean) {
        // Update a TextView or perform an action
    }

    override fun onStartTrackingTouch(seekBar: SeekBar?) {
        // Optional: Respond when the user starts touching
    }

    override fun onStopTrackingTouch(seekBar: SeekBar?) {
        // Optional: Respond when the user stops touching
    }
})
```

---

## 🎯 Why It Matters:
Event handling connects your app’s **UI** to the **logic**. Without it, your app wouldn’t respond to user input.
