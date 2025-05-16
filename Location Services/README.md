# 📍 **“WanderBuddy” – Your Personal Travel Tracker**

## 🎯 **App Concept:**

- Shows your current location on Google Maps.
- Lets you save favorite places by tapping on the map.
- Calculates and displays the distance between your current location and a selected place.
- Saves all your “visited places” with name, coordinates, and visit time in a RoomDB.

## 🗺️ **Phase 1: Project Setup & Permissions**

### ✅ Tasks:

1. Create a new Android project in Android Studio (Kotlin).
2. Set **minimum SDK to 21+**.
3. Add required **permissions** in `AndroidManifest.xml`.
4. Request **runtime permissions** in code using `ActivityCompat`.

---

## 📍 **Phase 2: Google Maps Setup**

### ✅ Tasks:

1. Add Google Maps dependency in `build.gradle`.
2. Get a **Google Maps API key** from the [Google Cloud Console](https://console.cloud.google.com/).
3. Add a `SupportMapFragment` to your layout.
4. Show the map with user’s location enabled.

---

## 🧭 **Phase 3: Location Updates**

### ✅ Tasks:

1. Use `FusedLocationProviderClient` to get current location.
2. Show a **moving location marker**.
3. Update every few seconds (or based on movement).

**Resource: Real-Time Location Tracking Made Easy with Fused Location Provider, Medium - https://medium.com/@myofficework000/real-time-location-tracking-made-easy-with-fused-location-provider-43de6437fbd3**
---

## ⭐ **Phase 4: Drop Pins & Save Places**

### ✅ Tasks:

1. On long-press of the map, drop a pin.
2. Show a dialog to **name the place**.
3. Save place details (name, lat, lng, timestamp) to **RoomDB**.

---

## 🧠 **Phase 5: Distance Calculation**

### ✅ Tasks:

1. Let the user tap a saved place from a list or map.
2. Get current location.
3. Display the distance in a `TextView`.

---

## 📊 **Phase 6: View Saved Places**

### ✅ Tasks:

1. Create a `RecyclerView` to list saved places.
2. Allow user to **tap to view on map** and **calculate distance**.
3. Store and retrieve from RoomDB using a DAO.


