# 🐾 ** `PetAdoptionActivity`**

### 🐶 **Scenario:**

You’re building a **Pet Adoption app** for a local animal shelter. The goal is to help staff manage information about adoptable pets and update the status of each pet (e.g., adopted or available). Data is stored in **Firebase Firestore**.

---

### 📲 **UI Elements:**

* Button: “Upload Sample Pets”
* Button: “Show Available Pets”
* Button: “Mark ‘Buddy’ as Adopted”
* Button: “Remove Breed Info from ‘Mittens’”

---

### 🎯 **Features:**

#### ✅ **1. Upload Sample Pets**

Stores sample pet entries into the `adoptable_pets` Firestore collection, such as:

```json
{
  "name": "Buddy",
  "type": "Dog",
  "age": 3,
  "breed": "Golden Retriever",
  "status": "Available"
}
```

#### ✅ **2. Show Available Pets**

Fetches and displays all pets where the `status` is `"Available"`. Could be shown in Logcat or as a simple list.

#### ✅ **3. Mark ‘Buddy’ as Adopted**

Updates the `status` field of the document with ID `"Buddy"` to `"Adopted"`.

#### ✅ **4. Remove Breed Info**

Deletes only the `"breed"` field from `"Mittens"`’s document (maybe breed is unknown or no longer needed).

---


