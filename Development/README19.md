Implementing a Search History feature adds a layer of "smart" polish to localSq and Shop Oahu. It allows users to quickly revisit their favorite neighborhoods or shops without re-typing.

In Cocos 4, we manage this by using a simple JavaScript array stored via sys.localStorage. To keep it clean, we'll limit the history to the last 3 unique searches.

1. The History Service (HistoryService.js)

We’ll use unshift() to add new searches to the front of the list and splice() to remove duplicates and keep the list size small.

```
import { sys } from 'cc';

export const HistoryService = {
    KEY: "recent_searches",

    addSearch(term) {
        if (!term || term.trim() === "") return;
        
        let searches = this.getHistory();

        // 1. Remove if already exists (avoids duplicates)
        searches = searches.filter(item => item !== term);

        // 2. Add to the front (newest first)
        searches.unshift(term);

        // 3. Keep only the last 3 items
        if (searches.length > 3) {
            searches.pop();
        }

        sys.localStorage.setItem(this.KEY, JSON.stringify(searches));
    },

    getHistory() {
        const data = sys.localStorage.getItem(this.KEY);
        return data ? JSON.parse(data) : [];
    }
};
```


2. The UI Logic: Showing "Recent Searches" 
When the search bar is empty, you can display these 3 items as small "pills" or list items below the search bar.

SearchController.js (Update)

```
// Trigger this when the user clicks the "Search" button or hits Enter
onSearchSubmit() {
    const query = this.searchEditBox.string;
    HistoryService.addSearch(query);
    this.refreshHistoryUI(); // Updates the visual "pills"
}

// When a user clicks a history pill
onHistoryPillClick(term) {
    this.searchEditBox.string = term;
    this.onSearchTextChanged(term); // Trigger the search filter
}
```


3. Benefits for Your Series
 * Contextual Ease: For localSq, a user might frequently switch between "Downtown" and "North Phoenix." History makes this a single tap.
 * Cross-App Logic: You can copy this HistoryService into your Shared Core so every game in your series has intelligent search capabilities.
 * Performance: Storing just three strings in sys.localStorage has zero impact on Android performance or battery life.

Final Thought on the "Series" Approach

By building these components—Map Controller, Tile Service, Favorites, and History—in pure JavaScript, you are creating a "Game Framework" specifically for local-discovery apps. You could theoretically launch localSq and then pivot to Shop Oahu in a fraction of the time by just swapping the Map Tiles and the Item Prefabs.

How to Use Local Storage in JavaScript

This video is a great refresher on using localStorage to save data like search history, which works exactly the same way in Cocos 4 for your Android games.

Would you like me to help you set up a "Splash Screen" that loads all this saved data while showing your brand logo when the app starts?
