## 24 March - 27 March

Activity: Integrating Firebase Authentication in an Android App

You're developing a simple Authentication App for a local book club. Members should be able to sign up and log in using their email and password. 

Objectives:

### Integrating Firebase Authentication into an Android project. Use this website as a guide:

https://firebase.google.com/docs/android/setup

- Make sure you're using Kotlin version 2.1.0
- In this site you manually specify versions for each library. This is the  “old” or direct dependency way to add dependencies:

**implementation("com.google.firebase:firebase-auth")**

**Catalog version:**

gradle - module: app:

**implementation(platform(libs.firebase.bom))**

**implementation(libs.firebase.analytics)**

**implementation(libs.firebase.auth)**

Easy to update and maintain.

Less chance of version conflicts.

### Connect firebase to your project

Go to the Firebase Console > Authentication > Sign-in method and enable Email/Password.

### Implement email and password authentication.

**Eoor Tips:**

**Make sure internet permissions for you project is enabled in your android manifest file**

**Make sure your emulator is connected to the wifi**

**Make sure your API key in your json file matches you API key in your Firebase project**

https://cloud.google.com/apis - This is where you will find your APIs for firebase projects

**Instructions:**

Create Two Kotlin Classes:

MainActivity.kt for the login screen

RegisterActivity.kt for the registration screen

Make sure both extend AppCompatActivity.

- Set Up ViewBinding in Each Activity

- Initialise FirebaseAuth in both activites

Create a FirebaseAuth instance using:
FirebaseAuth.getInstance().

- Implement Register Logic
  
In RegisterActivity:

When the register button is clicked:

Collect the email and password from input fields.

Check that neither is empty.

Use FirebaseAuth’s createUserWithEmailAndPassword() method.

If successful: show a toast and navigate to the login screen.

If it fails: show a toast with the error message.

- Implement Login Logic
  
In MainActivity:

When the login button is clicked:

Collect email and password.

Validate inputs.

Use signInWithEmailAndPassword().

Show a success or failure toast based on the result.

- Link Login and Register Screens
  
In both activities:

Use an Intent to navigate between screens when the TextView link is clicked.

- Handle “Forgot Password” Button

Implement the Reset logic.
