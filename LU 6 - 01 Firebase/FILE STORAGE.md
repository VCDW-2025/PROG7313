### 📅 **8 April**  

# **Activity: Integrating Firebase Firestore**

You're extending the Book Club App to allow members to upload and view book-related images using Firestore, rather than Firebase Storage.

---

### 🧩 Objectives:

- Use Firebase Firestore to upload and retrieve data (not files).
- Use Firestore to store image URLs rather than image files.
- Secure access to Firestore via rules.
- Display images based on data stored in Firestore.

---

### 🔧 Dependencies to Add

You’ll continue using the **Firebase BoM** (Bill of Materials) approach for version consistency:

```kotlin
implementation(platform(libs.firebase.bom))
implementation("com.google.firebase:firebase-firestore:24.3.0")
//Catalog Ver:
implementation(libs.firebase.firestore)
```

This will ensure version consistency with other Firebase services already added.

---

### 🔌 Connect Firebase Firestore

1. **Open Firebase Console**  
   Go to [https://console.firebase.google.com](https://console.firebase.google.com).

2. **Select your Firebase project** (Book Club App).

3. In the **Build** section of the sidebar, select **Firestore Database**.

4. Click **Create Database** and choose **Start in test mode** while developing (make sure to change these rules before going to production).

5. Set up your security rules like this for testing:
   ```json
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /{document=**} {
         allow read, write: if true;
       }
     }
   }
   ```

---

### 🧠 Implementation Steps:

1. **Design the UI**
   - Create a New Screen (UploadActivity) to handle image uploads and display:
     - **Select a book cover** (button to select)
     - **Upload a book cover** (button to upload)
     - **View the uploaded image** (ImageView to display image)
   
2. **Add Permissions**  
   - In your `AndroidManifest.xml`, request permission to read external storage (if targeting SDK < 33).
   - If targeting Android 13 and above, use `READ_MEDIA_IMAGES`.

3. **Select an Image**  
   - Use an `Intent.ACTION_PICK` to let users choose a photo from their gallery.

4. **Upload Image to Firestore**
   - Convert the selected image URI to a `StorageReference`.
   - **Upload image to Firebase Storage** (this can still be done via Firebase Storage).
   - After uploading, get the **download URL** of the image and store it in Firestore with relevant metadata (e.g., book name, author).

   Example of Firestore data:
   ```json
   {
     "bookTitle": "Book Name",
     "author": "Author Name",
     "imageUrl": "https://path/to/your/image.jpg"
   }
   ```

   You would store this in a Firestore collection, say `books`.

5. **Retrieve and Display the Image**
   - Use Firestore queries to retrieve the image URL and other details like book title.
   - Use **Glide** (or similar libraries) to load the image from the Firestore URL into an `ImageView`.

---

### 🔐 Firestore Rules & Security

Consider:
- **Public vs private access**: Set read and write rules based on user authentication.
- **Using Firebase Authentication** to secure uploads/downloads by users:
   ```json
   allow read, write: if request.auth != null;
   ```

---

### 🧪 Challenge Tasks

- Allow users to delete or update their uploaded images by interacting with Firestore (deleting/updating documents).

---
