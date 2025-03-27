# **What is ViewBinding?**

ViewBinding is a feature provided by Android Studio that generates a binding class for each XML layout file. This binding class contains direct references to all views with an ID, so you don’t have to call findViewById manually. 
This results in safer, cleaner, and more maintainable code.

## **Benefits of Using ViewBinding:**
- Each view reference is generated using the correct type.
- Reduces the risk of null pointer exceptions since the binding class only includes views present in the layout.
- Eliminates the boilerplate code of finding views by ID.

### **How to implement View Binding:**

1. **Enable ViewBinding in the App level gradle file**

    buildFeatures {
        
        viewBinding = true
   
    }
   
   This enables ViewBinding for your project.

   Layouts will be automatically generated with a name similar to: ActivityMainBinding.

2. **Use View Binding in Your Activity**

Import the generated binding class at the top of the .kt activity file

eg:

import com.talia.meetmewheregroup2.databinding.ActivityMainBinding

3. **Use Kotlin’s lateinit to declare the binding variable.**

eg:

private lateinit var binding: ActivityMainBinding

4. **Inflate the layout and set the content view and set the activity's content view to the root of the binding.**

eg:

binding = ActivityMainBinding.inflate(layoutInflater)

  setContentView(binding.root)
    
   
"ActivityMainBinding.inflate(layoutInflater)" creates an instance of the binding class, which holds references to every view in your layout.

"setContentView(binding.root)" sets the root view as the content view of the activity.

### **Good Luck!**

