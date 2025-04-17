### 🍩 Practical Activity – “Galactic Donut Shop” (Navigation‑First)

Build a small Android app with **two distinct screens**:

1. **Add Donut** – users enter a donut name, description and pick an image.  
2. **Donut List** – users see all saved donuts in a scrolling list.

The two screens are connected with a **bottom navigation bar**. You **must implement the nav bar first** before designing either screen.

---

#### Phase‑by‑Phase Instructions

**1. Project Skeleton**  
- Create a new Android Studio project (Empty Activity, Kotlin).  
- Choose a minimum SDK that supports the libraries you intend to use and briefly note why you picked it.

**2. Build the Bottom Navigation Bar (start here!)**  
- Add a bottom navigation view to your main layout.  
- Create two menu items: “Add Donut” and “Donut List,” each with an intuitive icon and label.  
- Set up a Navigation Component graph that swaps fragments when the user selects an item.  
- Test navigation right away; both items can display placeholder text for now.

**3. Screen A – Add Donut**  
- Design a simple form containing:  
  • Name field (single‑line)  
  • Description field (multi‑line)  
  • Button or image placeholder to pick a gallery photo  
  • Save button (disabled until all fields are valid)  
- Plan image selection with the modern Activity Result API and decide how you will store the returned URI.  
- Draft validation rules (no empty fields, optional image placeholder if none chosen).  
- Decide what feedback the user receives on successful save or validation failure.

**4. Screen B – Donut List**  
- Sketch a RecyclerView layout where each list item shows the donut’s image, name and a short description.  
- Determine a strategy for refreshing the list automatically whenever new donuts are added (think LiveData or Flow observed in a ViewModel).  
- Provide a pleasant empty‑state message when the list is empty.

**5. Local Persistence with Room**  
- Outline an Entity that stores an auto‑generated id, name, description and image URI string.  
- List the DAO actions you need (insert donut, get all donuts).  
- Explain where you will create the database instance and how fragments will obtain a reference (e.g., via a Repository and shared ViewModel).  
- Mention thread safety: inserts should occur on a background dispatcher.

**6. Data Flow**  
- Describe how pressing **Save** on the Add Donut screen writes to Room, then how the Donut List screen observes changes and updates instantly.  
- Note what should happen when users navigate away and return, or when they rotate the device.

**7. UX Polish & Error Handling**  
- Save button remains disabled until inputs are valid.  
- Show concise toasts or snackbars for successes and errors.  
- Provide a default placeholder image if the user cancels image selection.  
- Think about state restoration after process death (e.g., use ViewModel to store temporary input).


Have fun exploring the galaxy of donuts 🚀
