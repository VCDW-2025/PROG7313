## 📅 **24 March – 25 March**  
### 🔧 **Integrating Firebase Authentication in an Android App**

---

### 📖 **Scenario**  
You’re developing a simple **Authentication App** for a **local book club**. Members should be able to **sign up** and **log in** using their **email and password**.

---

### 🎯 **Objectives**
- Integrate **Firebase Authentication** into an Android project.
- Implement **email/password login and registration** functionality.
- Use **ViewBinding** for efficient UI handling.

---

### 🔗 **Firebase Setup**

1. **Go to**:  
   [https://firebase.google.com/docs/android/setup](https://firebase.google.com/docs/android/setup)  
   Follow the official guide to connect your project to Firebase.

2. **Firebase Console**:
   - Open your project in the [Firebase Console](https://console.firebase.google.com)
   - Go to **Authentication > Sign-in method**
   - Enable **Email/Password**

---

### ⚙️ **Dependencies**

#### 🔸 If using **manual (direct)** dependencies:
Ensure you're using **Kotlin version 2.1.0**  
```kotlin
implementation("com.google.firebase:firebase-auth")
```

---

#### 🔹 If using the **Version Catalog (recommended)**

In `build.gradle.kts` (Module: app):

```kotlin
implementation(platform(libs.firebase.bom))
implementation(libs.firebase.analytics)
implementation(libs.firebase.auth)
```

✅ **Benefits of Version Catalog**:
- Easy to maintain
- Automatically resolves compatibility
- Centralized versioning

---

### 🛠️ **Development Steps**

#### 1. **Create Two Activities**
- `MainActivity.kt` → **Login screen**
- `RegisterActivity.kt` → **Registration screen**

---

#### 2. **Enable ViewBinding**
- Activate ViewBinding in `build.gradle.kts`
- Set up ViewBinding in both activities for efficient UI access

---

#### 3. **Initialize FirebaseAuth**
In both `MainActivity` and `RegisterActivity`:
```kotlin
val auth = FirebaseAuth.getInstance()
```

---

### 📝 **Implement Registration Logic**  
In `RegisterActivity.kt`:
- When the **register button** is clicked:
  - Get the email and password from input fields
  - Check that both fields are not empty
  - Use `createUserWithEmailAndPassword(email, password)`
  - If successful:  
    → Show a Toast  
    → Redirect to login screen
  - If failed:  
    → Show a Toast with the error message

---

### 📝 **Implement Login Logic**  
In `MainActivity.kt`:
- When the **login button** is clicked:
  - Get the email and password from input fields
  - Validate inputs
  - Use `signInWithEmailAndPassword(email, password)`
  - Show success/failure using Toast messages

---

### 🔁 **Link Login and Register Screens**
- In both activities, allow navigation between them using `Intent` when the **TextView link** is clicked (e.g., “Don’t have an account? Register here.”)

---

### 🔐 **Handle “Forgot Password” Button**
- Implement the **Reset Password** functionality:
  - Use `sendPasswordResetEmail(email)`
  - Show confirmation or error in a Toast

---

