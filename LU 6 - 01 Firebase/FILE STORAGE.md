### 📅 **7 April - 10 April**

# **Activity: Integrating Firebase Firestore**

You're extending the **Book Club App** to allow members to upload and view book-related images using Firestore to store the image URLs, rather than Firebase Storage for the images themselves.

---

### 🧩 Objectives:

- Use **Firebase Firestore** to store metadata about the book images (not the images themselves).
- Store **image URLs** in Firestore rather than uploading the actual image files to Firebase Storage.
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

5. Set up your Firestore security rules like this for testing (remember to change these before going to production):

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

When a user logs in, they should be directed to the **UploadActivity Screen**.

1. **Design the UI**  
   Create a new screen (`UploadActivity`) to handle image URL uploads and display:
   - **Select a book cover** (button to select)
   - **Upload a book cover** (button to upload)
   - **View the uploaded image** (ImageView to display image)
   - **Add an book name**
   - **Add an author name**

2. **Add Permissions**  
   - In your `AndroidManifest.xml`, request permission to read external storage (if targeting SDK < 33).
   - If targeting Android 13 and above, use `READ_MEDIA_IMAGES`.

3. **Select an Image**  
   - Use an `Intent.ACTION_PICK` to allow users to choose a photo from their gallery.

4. **Store Details in Firestore**  
   After the user selects the image and enters the book details, instead of uploading the image to Firebase Storage, you’ll upload the book information to the Firestore Database.
   Use cloud storage to store the image and hardcode the url into the android project.

   Here’s an example of storing the data in Firestore:

   ```json
   {
     "bookTitle": "Book Name",
     "author": "Author Name",
     "imageUrl": "Https:..."
   }
   ```
**Opional** Store the image in local storage.(RoomDB)

5. **Retrieve and Display the Image**  
   - Use **Firestore queries** to retrieve the image URL and other details like the book title.
   - Use **Glide** (or similar libraries) to load the image from the Firestore URL into an `ImageView`.

   Example code to retrieve the image and display it using Glide:
   ```kotlin
   FirebaseFirestore.getInstance().collection("books")
       .get()
       .addOnSuccessListener { result ->
           for (document in result) {
               val imageUrl = document.getString("imageUrl")
               Glide.with(this).load(imageUrl).into(imageViewBookCover)
           }
       }
       .addOnFailureListener { exception ->
           Log.w(TAG, "Error getting documents: ", exception)
       }
   ```

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
