## 📊 **SkillMaster Tracker – Visualise Your Learning Progress**


Create a Kotlin-based Android app that helps students **visually track their time spent learning different tech skills** using a **bar chart**.

This app will use the MPAndroidChart library to display hours spent on learning topics such as Kotlin, Firebase, SQL, and more.

---

## 🔧 Instructions

---

### 🧱 **Part A – Project Setup**

#### Step 1: Create a New Project

### 📦 **Part B – Add MPAndroidChart Dependency**

#### Step 1: Add MPAndroidChart to `build.gradle.kts`

#### Step 2: Add JitPack to your repositories (if needed)

### 🧩 **Part C – Design the Layout**

#### Step 1: Edit `activity_main.xml`

Add: 

* A `BarChart` view to display the data.
* The layout should be clear, with proper padding and spacing.

---

### 📊 **Part D – Prepare the Data in Kotlin**

#### Step 1: Open `MainActivity.kt`

* Use `ViewBinding` to access your chart.

#### Step 2: Define Mock Data

Create a `Map` of skills and hours:

```kotlin
val learningData = mapOf(
    "Kotlin" to 40f,
    "Firebase" to 20f,
    "SQL" to 25f,
    "UI Design" to 15f,
    "Git" to 30f
)
```
OR let the user enter details.
---

### 📈 **Part E – Set Up the Bar Chart**

#### Step 1: Convert to BarEntries

* Loop through the `learningData` map.
* Create `BarEntry` objects where:

  * X = index (e.g., 0f, 1f…)
  * Y = hours (e.g., 40f, 30f…)

#### Step 2: Add Labels

* Store the skill names in a list so they can be shown on the X-axis.

#### Step 3: Populate the Chart

* Create a `BarDataSet` and set its color.
* Use `BarData` to link the data set.
* Assign the data to your `BarChart` and call `invalidate()` to render it.

---

### 🎨 **Part F – Customise the Chart Appearance**

* Set chart description to blank.
* Enable animation (`animateY()`).
* Show values above bars (`setDrawValues(true)`).
* Use `XAxis` to show the skill names instead of numbers.
* Use colors to distinguish each bar.

---

### ✨ You Could Add:

1. **Clickable Bars**: Show a toast message when a bar is tapped (e.g., “Keep going with SQL!”).
2. **Progress Goal Line**:

   * Add a **LimitLine** at 50 hours to represent a mastery goal.
3. **Pie Chart View**:

   * Add a second screen with a pie chart showing each skill’s share of total hours.

---

Resources:

- How to use MPAndroidChart in Android Studio!, Medium. https://medium.com/@SeanAT19/how-to-use-mpandroidchart-in-android-studio-c01a8150720f
- Android – Create BarChart with Kotlin, Geeksforgeeks. https://www.geeksforgeeks.org/android-create-barchart-with-kotlin/
- Official Documentation: github.com/PhilJay/MPAndroidChart


