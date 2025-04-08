## ✅ **Overview**
You’ll be doing two things:
1. **Set up local tests** 
2. **Create a GitHub Actions workflow** that:
   - Runs these tests on every push or pull request.
   - Builds your app to check for errors.

---

## ✅ **PART 1: Write a Simple Test (optional but I recommend it)**

Add a basic test if you don't already have one.

### 🔹 In Android Studio:
1. Right-click the `java` folder of your app module.
2. Go to:  
   **New → Java/Kotlin Class → JUnit Test**
3. Example (in `app/src/test/java/...`):

```kotlin
import org.junit.Test
import org.junit.Assert.*

class OrderTest {
    @Test
    fun testOrderCreation() {
        val order = Order(1, "Test", "Latte")
        assertEquals("Latte", order.item)
    }
}
```

This test checks that an `Order` object is created correctly.

---

## ✅ **PART 2: Create GitHub Actions Workflow**

### 🔹 Step 1: Push Your Code to GitHub
Make sure your Android project is in a GitHub repository.

---

### 🔹 Step 2: Add a GitHub Actions Workflow

In your repo, go to:
```
.github/workflows/
```

Create a file named:
```
android.yml
```

Paste this standard Android CI configuration:

```yaml
name: Android CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Set up JDK 11
      uses: actions/setup-java@v3
      with:
        distribution: 'temurin'
        java-version: 11

    - name: Setup Android SDK
      uses: android-actions/setup-android@v2

    - name: Build project
      run: ./gradlew build

    - name: Run unit tests
      run: ./gradlew test
```

---

## ✅ **What This Workflow Does**
- **Triggers** every time you push to `main` or open a pull request.
- **Checks out your code**
- **Sets up Java and Android SDK** on a GitHub-hosted machine.
- **Builds your app** to catch compile errors.
- **Runs your tests** to catch logic issues.

---

## ✅ View Results on GitHub

Once you push:
1. Go to your GitHub repo.
2. Click the **"Actions" tab**.
3. You’ll see a workflow run triggered.
4. You can expand the steps to view logs, errors, or test results.

---

## 🧠 Why This Matters
- Confirms your code works on other machines, not just yours (like your marker's).
- Catches errors early when collaborating.
- Encourages test-driven development.
- Impresses industry professionals — many expect CI/CD workflows like this.

---
