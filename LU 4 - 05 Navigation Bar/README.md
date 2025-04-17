Page 114 of 221  in your module manual

Navigation Bar
Screen Sketch & Naming

On paper or in a design tool, draw two clean rectangles labeled Add Donut and Donut List.

Decide on concise names for your fragments (e.g. AddDonutFragment, DonutListFragment) so everything stays consistent.

Generate Blank Fragments

In Android Studio’s Project pane, right‑click your package → New → Fragment → Fragment (Blank).

Name it exactly AddDonutFragment. Repeat for DonutListFragment.

In each fragment’s layout XML, drop in a simple TextView (“Add Donut Screen” / “Donut List Screen”) to verify you’ve got the right file.

Create the Navigation Graph

In res/navigation, create a new Navigation resource file (e.g. nav_graph.xml).

Open it in the Navigation Editor: drag both fragments onto the canvas.

In the properties panel, mark DonutListFragment as the Start Destination.

Host Your Fragments

Open activity_main.xml (or your single‑Activity layout).

Replace any placeholder container (FrameLayout) with a NavHostFragment from the palette.

In its attributes, set navGraph to your newly created nav_graph.xml.

Add the BottomNavigationView

Still in activity_main.xml, below (or alongside) the NavHostFragment, drag in a BottomNavigationView.

Give it an ID (e.g. bottomNav).

Ensure its layout constraints or parent layout allow it to sit at the bottom of the screen.

Build the Menu Resource

Under res/menu, create a new menu resource file (e.g. bottom_nav_menu.xml).

Define two <item> entries:

One with ID nav_add_donut, title “Add Donut” and a gallery or “+” icon.

One with ID nav_donut_list, title “Donut List” and a list or donut icon.

Use Android Studio’s built‑in Vector Asset tool to pick Material icons—this guarantees crisp, scalable graphics.

Link Menu to Your Nav View

In the BottomNavigationView’s XML attributes, point app:menu to your bottom_nav_menu.xml.

Now the bar will render both icons and labels—no further code needed to draw it.

Wire Navigation Logic

In your Activity’s initialization (onCreate), obtain the NavController tied to your NavHostFragment.

Use the Navigation‑Component helper to bind your BottomNavigationView to that NavController.

This single binding instructs the nav component to swap fragments when an item is tapped and to highlight the selected icon.

Top‑Level Destinations & Back‑Stack

In your Navigation Graph properties, ensure both “Add Donut” and “Donut List” are marked as top‑level.

This makes the system back button exit the app from either screen rather than popping intermediate fragments.

Confirm that no unintended back‑stack entries accumulate as you switch tabs.


Next Steps

With your nav bar solid, every fragment you now open will slot neatly into place.

Future work—Add Donut form logic, Room integration, RecyclerView—lives entirely inside those fragments, leaving your navigation layer untouched.

Good luck guiding your users across the galaxy of screens—your nav bar is now mission‑ready! 🚀
