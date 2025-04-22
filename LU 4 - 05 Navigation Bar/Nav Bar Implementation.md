# 🚀**Navigation Bar Implementation**
---

### 1  Set up the fragments

1. **Plan the screens**  
   * Sketch two rectangles on paper or in Figma and label them **Add Donut** and **Donut List**.  
   * Choose exact fragment class names now (e.g. `AddDonutFragment`, `DonutListFragment`). Keeping names consistent from the outset prevents XML/Gradle typos later.

2. **Generate the fragment classes and their layouts**  
   * In **Android Studio ▸ Project pane**: right‑click your code package → **New ▸ Fragment ▸ Fragment (Blank)**.  
   * Name the first one **AddDonutFragment**; repeat for **DonutListFragment**.  
   * Accept the check‑boxes to create a Kotlin/Java class, a layout file, and a factory method.  
   * In each auto‑generated layout, drop a temporary **TextView** so you can recognise the screen at runtime. (You will delete these soon.)

---

### 2  Prepare the Navigation Component
1. **Create a Navigation graph**  
   * Right‑click **res/navigation** → **New ▸ Navigation Resource File**. Call it `nav_graph`.  
   * The Navigation Editor opens automatically. Drag both fragments from the left panel onto the canvas.  
   * Click **DonutListFragment** once and, in the **Attributes** panel, tick **Start Destination** so the app launches into the list first.

2. **Declare both fragments as top‑level**  
   * Still in the editor, select one fragment at a time and locate the **Default Nav Options** section.  
   * For **Launch Single Top** set **true**.  
   * For **Pop Up To** leave blank (top‑level screens should not pop anything off the stack).  
   * These settings ensure pressing the system Back button exits the app from either tab instead of returning to previously selected tabs.

---

### 3  Embed the NavHost in your Activity
1. **Open `activity_main.xml`** (or whatever xml your lone Activity inflates).  
2. Remove any placeholder container (e.g. FrameLayout) originally auto‑generated.  
3. From the **Palette** ▸ **Layouts & Containers** section, drag **FragmentContainerView** onto the canvas.  
4. In the properties pane for that view:  
   * **Name**: `androidx.navigation.fragment.NavHostFragment`.  
   * **app:navGraph**: point to `@navigation/nav_graph`.  
   * **app:defaultNavHost**: set **true** so the NavHost intercepts system Back events.  
5. Constrain or size this container to fill all space *above* where the BottomNavigation bar will sit.

---

### 4  Create the BottomNavigation bar
1. **Add the view**  
   * Still inside `activity_main.xml`, drag **BottomNavigationView** from the **Material Components** group and anchor it to the bottom of the parent.  
   * Give it an ID (e.g. `bottomNav`).  
   * Ensure the FragmentContainerView’s bottom constraint is linked to the top of this view so the fragments occupy only the remaining space.

2. **Supply a menu resource for the bar**  
   * Right‑click **res/menu** → **New ▸ Menu Resource File** called `bottom_nav_menu`.  
   * Add two `<item>` elements:  
     * **ID** `nav_add_donut`, title “Add Donut”, icon “add” (Material).  
     * **ID** `nav_donut_list`, title “Donut List”, icon “list” (Material).  
   * Use **File ▸ New ▸ Vector Asset** to import “add” and “list” Material icons. Vector assets keep icons crisp on every DPI.  
   * In the BottomNavigationView’s XML attributes, set **app:menu** to `@menu/bottom_nav_menu`.

---

### 5  Wire bottom nav to Navigation Component
1. **Add the Navigation dependencies** *(Gradle, no code shown)*  
   * Navigation fragment‑ktx  
   * Navigation ui‑ktx  
   * Material Components (already present in most templates)  
   * Optional: the `androidx.navigation.safeargs` plugin for type‑safe navigation.

2. **Link at runtime**  
   * Inside **MainActivity ▸ onCreate**:  
     * Obtain the **NavController** from the FragmentContainerView (`findNavController(R.id.nav_host_fragment)`).  
     * Call the Navigation‑UI helper that ties your BottomNavigationView to that controller (`setupWithNavController`). This single call:  
       * Changes the selected icon automatically when a tab is pressed.  
       * Issues `navigate()` requests to swap fragments.  
       * Syncs the system Back button with the graph’s back‑stack.

---

Good luck guiding your users across the galaxy of screens—your navigation bar is now mission‑ready! 🚀


External Link: https://www.geeksforgeeks.org/bottom-navigation-bar-in-android/ only addkeep in studd for nav bar. not drawer
