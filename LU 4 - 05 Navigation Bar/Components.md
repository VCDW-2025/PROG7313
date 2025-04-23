
| Layer | File / Class | Why it matters | Typical contents |
|-------|--------------|----------------|------------------|
| **1. Navigation graph** | `res/navigation/nav_graph.xml` (`<navigation>` root) | Declares every destination (fragment, dialog, activity) and the routes between them. At compile time it becomes a generated class (`NavDirections`) that gives you type-safe navigation. | `<fragment>` nodes, `<action>` links, global actions, arguments, deep-link specs. |
| **2. Fragment destinations** | `HomeFragment.kt`, `ProfileFragment.kt`, … | Each screen the user can land on. With Navigation Component you seldom move between activities; you swap fragments inside a single host. | UI code, ViewModel hookup, lifecycle observers. |
| **3. NavHostFragment container** | Placed in your main Activity’s layout (`activity_main.xml`) | A dummy “window” that Navigation Component controls. It swaps in the fragment that matches the current destination. | ```xml <androidx.fragment.app.FragmentContainerView android:id="@+id/nav_host" app:navGraph="@navigation/nav_graph" app:defaultNavHost="true" … />``` |
| **4. Menu resource for the bar** | `res/menu/bottom_nav_menu.xml` | Holds one `<item>` per tab. The `android:id` **must match** the destination IDs in the nav graph so that `setupWithNavController()` can map taps to navigation actions. | `android:icon`, `android:title`, optional `app:showAsAction` flags. |
| **5. BottomNavigationView widget** | Usually in the same layout as the NavHostFragment | Renders the bar itself. It inflates the menu above and provides ripple, badge, elevation, etc. | ```xml <com.google.android.material.bottomnavigation.BottomNavigationView android:id="@+id/bottom_nav" app:menu="@menu/bottom_nav_menu" … />``` |
| **6. NavController** | Obtained in your Activity (or fragment) at runtime | The central dispatcher that knows the current destination and back-stack. You pass it to helper methods so UI widgets stay in sync with navigation. | ```val navController = findNavController(R.id.nav_host)``` |
| **7. UI → NavController handshake** | `NavigationUI.setupWithNavController(bottomNav, navController)` | Binds the BottomNavigationView to the NavController so taps trigger `navigate()` calls and the correct tab stays highlighted when you navigate programmatically. | One-line call in `onCreate()`. |
| **8. Optional styling assets** | `drawable` selectors, `color` state lists, themes | Control icon tint, text colour in selected/unselected states, bar background, elevation shadows, etc. | `@color/bottom_nav_item_color`, `shape` drawable for rounded corners. |
| **9. Gradle dependencies** | `implementation "androidx.navigation:navigation-fragment-ktx:2.7.7"` and `"androidx.navigation:navigation-ui-ktx:2.7.7"` plus Material library | Provide Navigation run-time and Kotlin extensions; Material gives you BottomNavigationView. | Added in `app/build.gradle`. |
| **10. (Optional) AppBarConfiguration** | In Activity when you also have an `ActionBar` or `Toolbar` | Tells Navigation which destinations are “top-level” so back button behaviour and hamburger/arrow icons are set automatically. | ```val config = AppBarConfiguration(setOf(R.id.homeFragment, R.id.profileFragment))``` |

---

## Different Implementation:

Clean “parts list” for a **navigation bar that you build yourself with `RecyclerView` + `ViewHolder`** instead of the out-of-the-box `BottomNavigationView` / `NavigationView`.  

---

### 1. Data model - `NavItem`
* **What** – a Kotlin data class that represents one slot in the bar.  
* **Why** – `RecyclerView` needs a list of objects to bind; the model keeps the adapter logic type-safe.
  
```kotlin
data class NavItem(
    val destinationId: Int,      // matches an ID in your nav_graph
    val title: String,
    @DrawableRes val iconRes: Int
)
```

---

### 2. Row layout - `res/layout/item_nav.xml`
* **What** – a tiny layout file for one item in the bar.  
* **Why** – inflating this once per row is cheaper than building views in code.  
```xml
<LinearLayout …>
    <ImageView
        android:id="@+id/ivIcon" …/>
    <TextView
        android:id="@+id/tvLabel" …/>
</LinearLayout>
```

---

### 3. ViewHolder - `NavItemViewHolder`
* **What** – a small class that *caches* the views from the row layout.  
* **Why** – avoids repeated `findViewById` calls during fast scroll / re-bind cycles.  
```kotlin
class NavItemViewHolder(
    val binding: ItemNavBinding        // ViewBinding for `item_nav.xml`
) : RecyclerView.ViewHolder(binding.root)
```

---

### 4. Adapter - `NavBarAdapter`
* **What** – `RecyclerView.Adapter<NavItemViewHolder>` that glues the model list to the rows.  
* **Why** – handles inflation, binding, click events, and “selected” styling in one place.
  
```kotlin
class NavBarAdapter(
    private val items: List<NavItem>,
    private val onClick: (NavItem) -> Unit
) : RecyclerView.Adapter<NavItemViewHolder>() {

    private var selectedPos = 0

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int) =
        NavItemViewHolder(ItemNavBinding.inflate(
            LayoutInflater.from(parent.context), parent, false))

    override fun onBindViewHolder(holder: NavItemViewHolder, pos: Int) =
        with(holder) {
            val item = items[pos]
            binding.ivIcon.setImageResource(item.iconRes)
            binding.tvLabel.text = item.title
            binding.root.isSelected = pos == selectedPos      // highlight current
            binding.root.setOnClickListener {
                if (selectedPos != pos) {
                    notifyItemChanged(selectedPos)
                    selectedPos = pos
                    notifyItemChanged(selectedPos)
                    onClick(item)                             // bubble up event
                }
            }
        }

    override fun getItemCount() = items.size
}
```

---

### 5. RecyclerView container
* **What** – the view that draws the bar itself (horizontal orientation for bottom bar, vertical for a drawer).  
* **Why** – `RecyclerView` supplies view recycling, item animations, and optional scrolling for free.  
```xml
<androidx.recyclerview.widget.RecyclerView
    android:id="@+id/navBar"
    android:layout_width="match_parent"
    android:layout_height="56dp"
    android:orientation="horizontal"
    app:layoutManager="androidx.recyclerview.widget.LinearLayoutManager"
    app:orientation="horizontal" />
```

---

### 6. NavController hookup
* **What** – the `NavController` from Jetpack Navigation that actually performs screen changes.  
* **Why** – keeps your custom bar in sync with the fragment back-stack.  
```kotlin
class MainActivity : AppCompatActivity() {
    private val navController by lazy { findNavController(R.id.nav_host) }

    override fun onCreate(savedInstanceState: Bundle?) {
        …
        val items = listOf(
            NavItem(R.id.homeFragment,    "Home",    R.drawable.ic_home),
            NavItem(R.id.ordersFragment,  "Orders",  R.drawable.ic_orders),
            NavItem(R.id.profileFragment, "Profile", R.drawable.ic_profile)
        )

        binding.navBar.apply {
            adapter = NavBarAdapter(items) { navItem ->
                navController.navigate(navItem.destinationId)
            }
            setHasFixedSize(true)
        }
    }
}
```

---

### 7. Selection state & styling
* **What** – selector drawable, color state list, or DataBinding logic that shows which tab is active.  
* **Why** – the user needs visual feedback; the adapter updates `selectedPos` on click and `isSelected` in `onBindViewHolder`.  
* **How** – supply `item_nav.xml` with `android:foreground="?attr/selectableItemBackground"` and override `state_selected` tint in a color state list.

