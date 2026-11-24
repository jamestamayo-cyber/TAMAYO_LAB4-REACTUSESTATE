# DCIT26 - Laboratory Exercise 4: React useState and useEffect (Live Search and Filter)

Name: James Tamayo  
Course: DCIT26 - Application Development and Emerging Technologies  

## About This Project
For this lab, I updated our CvSU Mini Store product catalog in React by adding live search, category filtering, and price sorting. I used useState and useEffect so the search waits a bit before filtering, updates the browser tab title with the result count, and filters or sorts the items without messing up the original product list.

### What I Built
- SearchBar Component: Made a reusable search bar with a keyword text box, a category dropdown (All, Electronics, Books, School Supplies, Accessories), a price sort dropdown (Default, Price: Low to High, Price: High to Low), and a Clear Filters button.
- 300ms Debounced Search: Used useEffect with setTimeout and clearTimeout so the product list only updates after I stop typing for 300 milliseconds.
- Safe Filtering and Sorting: Filtered and sorted a copy of the products during render so the original products list stays unchanged.
- Dynamic Tab Title and Empty State: Made the browser tab title update whenever the result count changes, and added a message when no products match.

---

## Guide Questions

### 1. Why do we use two separate states, searchText and debouncedSearch, instead of only one?
I use searchText so the input box updates right away while I type and does not feel laggy. I use debouncedSearch so the actual filtering waits until I pause for 300ms, instead of running on every single letter I press.

### 2. What would happen if the debounce effect did not return a cleanup function?
Without clearTimeout, every keystroke would start its own 300ms timer that never gets canceled. Instead of filtering once after I stop typing, it would still fire delayed updates for every single letter I typed earlier.

### 3. What is the purpose of the dependency array? What happens if it is empty ([])? What happens if it is left out completely?
- Purpose: It tells React which values to watch so the effect only runs again when those values change.
- If it is empty ([]): The effect runs only once when the component first loads.
- If it is left out completely: The effect runs after every single render, which can slow down the app or cause infinite loops.

### 4. Why should we avoid sorting the original products array directly?
Because .sort() changes the original array in place. If I sort the original products array directly, I lose its starting order forever, so picking Default sort later would not bring back the original order.

### 5. Is the filtered product list better stored in its own state, or calculated from existing state during rendering? Explain your choice.
It is better to calculate it during rendering. If I saved the filtered list in its own state, I would need extra useEffect code just to keep it updated whenever the search, category, or sort changes, which makes the code more complicated and easier to break.
