In Cocos 4, the most efficient way to handle a pop-up system for your series of games is to use a Prefab-based Template.

Since you prefer the "Web Developer" approach, think of a Prefab as a reusable React or Vue component. You design the pop-up once in the editor (background, text, close button) and then "instantiate" it with JavaScript whenever a user clicks a map marker in localSq or an item in Shop Oahu.

1. The Interaction: Clicking a Marker

First, we need to make the markers we created in the previous step "clickable." In Cocos 4, we use the input.on or this.node.on method to listen for touch events on the marker's Node.

MarkerScript.js (Attached to each Marker)

```
import { _decorator, Component, Node, input, Input } from 'cc';

export class MarkerScript extends Component {
    onLoad() {
        // Listen for a touch end (click) on this specific marker
        this.node.on(Node.EventType.TOUCH_END, this.onMarkerClick, this);
    }

    onMarkerClick() {
        console.log("Marker clicked!");
        // Emit a global event that the UI layer can hear
        // This is a common "Web-style" pattern to decouple logic
        cc.game.emit('SHOW_SHOP_POPUP', {
            name: "Waikiki Surf Shop",
            description: "Best boards on the island.",
            id: "shop_001"
        });
    }
}
```


2. The Pop-up Manager: Instantiating the UI

You should have a central UI node in your scene (under the Canvas) that listens for these events and shows the pop-up.

PopupManager.js (Pure JavaScript)

```
import { _decorator, Component, instantiate, Prefab, Label, Node } from 'cc';
const { ccclass, property } = _decorator;

@ccclass('PopupManager')
export class PopupManager extends Component {
    @property(Prefab)
    detailsPopupPrefab = null; // Drag your UI Prefab here in the Editor

    onLoad() {
        // Listen for the global event from the markers
        cc.game.on('SHOW_SHOP_POPUP', this.openPopup, this);
    }

    openPopup(data) {
        // 1. Create a "Live" instance of the UI from the template
        const popupNode = instantiate(this.detailsPopupPrefab);
        
        // 2. Add it to the Canvas so it's visible
        this.node.addChild(popupNode);
        
        // 3. Update the text labels inside the popup
        const nameLabel = popupNode.getChildByName("Title").getComponent(Label);
        const descLabel = popupNode.getChildByName("Desc").getComponent(Label);
        
        nameLabel.string = data.name;
        descLabel.string = data.description;
    }
}
```

3. Closing the Pop-up

To keep your memory clean on Android, always ensure you destroy the pop-up node when the close button is clicked.

Inside your Pop-up UI Script:

```
onCloseClick() {
    // Standard JS way to remove an element
    this.node.destroy();
}
```

Why this is effective for your Series:
 * Shared UI Kit: You can put the detailsPopupPrefab in your "Shared Core" folder. localSq might use it to show park info, while Shop Oahu uses it for product details.
 * Decoupled Logic: The markers don't need to know how the pop-up works. They just say "I was clicked," and the PopupManager handles the rest.
 * Performance: By using instantiate, the engine only keeps the pop-up in memory when it's actually being used.

Build a Popup With JavaScript

This video is helpful because it explains the core logic of creating, showing, and closing modals using vanilla JavaScript, which maps directly to how you would structure your logic in the Cocos 4 engine.

Would you like me to show you how to connect this UI to a "Save to Favorites" feature that stores data locally on the Android device so users can bookmark shops in Shop Oahu?

YouTube video views will be stored in your YouTube History, and your data will be stored and used by YouTube according to its Terms of Service
