Imagine you’re creating an Android app called “**Galactic Donut Shop**.” In this fun, space-themed app, users can explore different types of interstellar donuts and then customise how many donuts they want to buy (with a sleek slider/SeekBar). The app will automatically calculate the total cost using NumberFormat, ensuring everything looks neat and readable—just like a professional receipt. Navigation between different parts of the app (like the donut menu, checkout, and fun facts about space) is handled with a modern Navigation Drawer.

---

## Description of the App

1. **Splash Screen**  
   - When the user opens the app, a splash screen briefly shows the “Galactic Donut Shop” logo and a spaceship background.

2. **Main Activity with Navigation Drawer**  
   - The main screen contains a **Navigation Drawer** on the left side. This lets users move between:
     - **Donut Menu**: A list of all the cosmic donuts available (e.g., “Martian Matcha,” “Saturn Sprinkle,” “Black Hole Chocolate”).
     - **Customize/Calculator**: The screen where the user picks how many donuts they want.
     - **Fun Facts**: Fun, random facts about donuts in space!
     - **Checkout**: A summary of the user’s order.

3. **Using a SeekBar for Donut Quantity**  
   - On the “Customize/Calculator” screen, there is a **SeekBar** that allows the user to select how many donuts they want to purchase, ranging from 1 donut up to, say, 50 donuts.
   - As the user slides the SeekBar, the quantity displays in real-time on the screen (like “You’ve selected 25 donuts!”).

4. **NumberFormat for Prices**  
   - The price of each donut is, for example, **2.99** (in some Earth currency or maybe Martian credits—get creative).
   - When the user moves the SeekBar, the app multiplies the donut price by the number of donuts selected.
   - **NumberFormat** is used to convert the resulting price into a **currency format** (e.g., `$29.90` or `USD 29.90`). This ensures it always looks professional (two decimals, currency symbol, etc.).

5. **Checkout Screen**  
   - Shows a neat receipt:
     - Donut type(s) selected
     - Quantity
     - Formatted total cost (using NumberFormat)
   - The user can then confirm the purchase or go back to tweak their order.

---

## Assignment Prompt for Students

1. **Outline the App Flow**  
   - Describe the overall flow of the “Galactic Donut Shop” app: from the splash screen through the main screen and navigation drawer items.

2. **Detail the Navigation Drawer Integration**  
   - Explain how you added the navigation drawer.
   - What are the **menu items**, and how do you handle item selection?

3. **Implementing the SeekBar**  
   - Show how you manage the SeekBar in code:
     - Where do you initialize it?
     - How do you set a **maximum** value?
     - How do you **listen** for changes so the app updates the displayed quantity live?

4. **Formatting the Price**  
   - Discuss how you import and use **NumberFormat** (e.g., `NumberFormat.getCurrencyInstance()`).
   - Show how the chosen locale or currency symbol is displayed.

5. **In-Depth Program Flow**  
   - Step-by-step, what happens when the user slides the SeekBar to select 25 donuts?
   - How does the app calculate total cost and format it with NumberFormat?
   - How is this displayed to the user?
   - How does the user navigate back to the donut menu if they want a different flavor?

6. **Class & Activity Structures**  
   - Provide an overview of how you organized your app’s classes/activities/fragments.
   - For example:
     - **MainActivity** (contains the Navigation Drawer)
     - **CalculatorFragment** or **Activity** (contains the SeekBar logic and NumberFormat code)
     - **FunFactsFragment** (displays the donut facts)
     - **CheckoutFragment** (final order summary)
   - Explain how data (like donut price, quantity, total) is passed around.

7. **User Experience**  
   - How does the user know the cost? (Always keep it updated in real-time on the screen.)
   - How do they confirm/cancel an order?

8. **Potential Edge Cases**  
   - What happens if the user tries to buy zero donuts or goes beyond your maximum limit?
   - How do you handle any errors or unusual user interactions?

---

### **Your Task**  
Pretend you’re explaining your “Galactic Donut Shop” app to someone who wants to read your entire blueprint. **Walk through** the code sections, **show** how each feature is implemented, and **justify** why you used these components (Navigation Drawer, SeekBar, NumberFormat). Make your explanation **detailed**, so others can see exactly how it all works, from launching the app to final checkout. 

