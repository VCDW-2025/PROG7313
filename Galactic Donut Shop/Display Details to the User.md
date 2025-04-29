# **Donut Display**🍩📲

## 1. Add a RecyclerView to Your Fragment Layout  🎯

## 2. Create an Item Layout 📐

## 3. Build a Simple Adapter 🔧

### 3.1:

- Define an inner ViewHolder that finds the related ui components.

- Hold a List<Donut> and inflate the item layout in onCreateViewHolder.

- In onBindViewHolder, bind:

donutName.text = donut.name

donutDescription.text = donut.description

If donut.imageUri is non-null, parse it to a Uri and call imageView.setImageURI(uri), otherwise set a placeholder.

- getItemCount() returns the list size.

## 4. Wire It Up in DisplayDonutsFragment 🔗

- Find the RecyclerView by ID.

- Set its layout manager

- Launch a coroutine on Dispatchers.IO to fetch your list

- If the list is empty, show a “No donuts yet” message

