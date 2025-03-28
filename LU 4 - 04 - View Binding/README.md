# 🧷 **ViewBinding**

**ViewBinding** is a modern and safer way to access views in your Android app. 

It eliminates the need for `findViewById()` and prevents null pointer exceptions and type mismatches.

---

## 🧩 **What is ViewBinding?**

ViewBinding creates a binding class for each XML layout file. 

That binding class holds references to all the views with an `id` in that layout, making it easy to interact with them in Kotlin or Java.

---

## ✅ **Benefits of ViewBinding**

- **Type-safe**: No casting needed.
- **Null-safe**: Catches errors at compile time.
- **Cleaner code**: Less boilerplate compared to `findViewById()`.
- Works well with **fragments**, **activities**, and **recyclers**.

---

## 🔧 **How to Enable ViewBinding**

In your `build.gradle (Module: app)` file:

```gradle

android {
    ...
    viewBinding {
        enabled = true
    }
}
```

Sync your project after adding it.

---

### 📄 **Example XML Layout**

`activity_main.xml`
```xml
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello ViewBinding!" />

    <Button
        android:id="@+id/buttonClick"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Click Me" />
</LinearLayout>
```

---

### 📄 **Using ViewBinding in Activity**

```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        binding.buttonClick.setOnClickListener {
            binding.textView.text = "Button was clicked!"
        }
    }
}
```

> `ActivityMainBinding` is auto-generated from `activity_main.xml`.

---

## 🧩 **ViewBinding vs findViewById**

| Feature              | ViewBinding        | findViewById        |
|----------------------|--------------------|----------------------|
| Type safety          | ✅ Yes             | ❌ No                |
| Null safety          | ✅ Yes             | ❌ No                |
| Required boilerplate | ❌ Minimal         | ✅ More              |
| Build-time checking  | ✅ Yes             | ❌ No                |

