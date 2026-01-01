In Cocos 4, the most approachable way to save "Favorites" on Android is using the sys.localStorage API.

If you are coming from web development, this will feel exactly like using window.localStorage. On Android, Cocos automatically maps this to an SQLite database under the hood, ensuring your data is saved permanently even if the user closes the app or restarts their phone.

1. The "Favorites" Data Structure

Since you want to save multiple shops (for Shop Oahu) or locations (for localSq), the best practice is to store an Array of Objects and use JSON.stringify to turn it into a string that the storage can handle.

```
// Example structure
let favorites = [
    { id: "shop_001", name: "Waikiki Surf", lat: 21.27, lon: -157.82 },
    { id: "shop_042", name: "Phoenix Coffee", lat: 33.44, lon: -112.07 }
];
```


2. Implementation: The Storage Script

You can create a small utility script in pure JavaScript to handle the "Saving" and "Loading" logic for your entire series.
StorageService.js


```
import { sys } from 'cc';

export const StorageService = {
    KEY_FAVORITES: "user_favorites_list",

    // Save a new favorite
    saveFavorite(shopData) {
        // 1. Get existing list from storage
        let list = this.getFavorites();
        
        // 2. Add the new shop if it's not already there
        if (!list.find(s => s.id === shopData.id)) {
            list.push(shopData);
            
            // 3. Convert to String and Save
            const dataString = JSON.stringify(list);
            sys.localStorage.setItem(this.KEY_FAVORITES, dataString);
            console.log("Saved to Android storage!");
        }
    },

    // Retrieve all favorites
    getFavorites() {
        const data = sys.localStorage.getItem(this.KEY_FAVORITES);
        return data ? JSON.parse(data) : [];
    }
};
```

3. Connecting to your Pop-up UI 
In the Pop-up UI we discussed earlier, you just need to call this service when the user clicks the "Favorite" (heart) button.

```
// Inside your Pop-up Button click handler
onFavoriteClick() {
    // 'this.currentShopData' comes from when the popup was opened
    StorageService.saveFavorite(this.currentShopData);
    
    // Visual feedback (change button color, etc.)
    this.favoriteButton.color = cc.Color.RED;
}
```


Why this works for your Android Series:
 * Permanent Storage: On Android, these files are stored in the app's private data folder (/data/data/your.package.name/). They won't be deleted unless the user uninstalls the app.
 * No Server Needed: This allows your games to have a "Save" feature that works completely offline—ideal for travelers using Shop Oahu.
 * Cross-Game Potential: If you use the same KEY_FAVORITES string across different games in your series, they can technically "share" data if you configure the Android shared user ID (though usually, they stay separate for safety).

Pro-Tip for Android 16 (2026)

With modern Android versions focusing on "Scoped Storage," sys.localStorage is the safest bet because it doesn't require any special permissions. It’s "private" to your app, so you don't need to ask the user for permission to save their own favorite shops.

Would you like me to show you how to build a "Favorites List" screen that displays all these saved shops in a scrollable list?
