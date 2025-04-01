## 📅 **1 April**  

# **Activity: Integrating Firebase Cloud Storage**

You're extending the Book Club App to allow members to upload images.

---

### 🧩 Objectives:

- Use Firebase Storage to upload and retrieve files.
- Apply image selection using an `Intent`.
- Secure access to storage via rules.
- Display uploaded content in the app.

---

### 🔧 Dependencies to Add

You’ll continue using the **Firebase BoM** (Bill of Materials) approach:

```kotlin
implementation(platform(libs.firebase.bom))
implementation("com.google.firebase:firebase-storage:20.3.0")
//Catalog Ver:
implementation(libs.firebase.storage)
```

This will ensure version consistency with other Firebase services already added.

---

### 🔌 Connect Firebase Storage

1. **Open Firebase Console**  
   Go to [https://console.firebase.google.com](https://console.firebase.google.com).

2. **Select your Firebase project** (Book Club App).

3. In the **Build** section of the sidebar, select **Storage**.

4. Click **Get Started** and select a region (europe-west1 is a good default).

5. Set the security rules to **Test Mode** while developing:

   ```json
   rules_version = '2';
   service firebase.storage {
     match /b/{bucket}/o {
       match /{allPaths=**} {
         allow read, write: if true;
       }
     }
   }
   ```

   > ⚠️ *Important:* Tighten these rules before going to production.

---

### 🧠 Implementation Steps:

1. **Design the UI**
   - Create a New Screen

After a user logs in successfully, they get redirected to UploadActivity where they:

- Select a book cover (button to select)
- Upload a book cover (button to upload)
- View the uploaded image (imageView to display image)

The seperate screen keeps UI responsibilities clearer and avoids overloading one activity with too many features.

2. **Add Permissions**  
   - In your `AndroidManifest.xml`, request permission to read external storage (if targeting SDK < 33).
   - If targeting Android 13 and above, use `READ_MEDIA_IMAGES`.

3. **Select an Image**  
   - Use an `Intent.ACTION_PICK` to let users choose a photo from their gallery.

4. **Upload Image to Firebase Storage**  
   - Convert the selected image URI to a `StorageReference`.
   - Upload using `putFile()`.

5. **Retrieve and Display the Image**  
   - Once uploaded, retrieve the download URL.
   - Use Glide or another image-loading library to display the image from the URL.

---

### 🔐 Storage Rules & Security

Consider:

- Public vs private access.
- Using Firebase Authentication to secure uploads/downloads.
- Setting rules like:
  ```json
  allow read, write: if request.auth != null;
  ```

---

### 🧪 Challenge Tasks

- Allow users to delete or replace their uploaded images.

---

### 💬 Think about:

- Why Cloud Storage is preferred for large files like images?
- What are the limitations of using Realtime Database or Firestore for storing images?
- How would you secure uploads on a per-user basis?

---
