Building the window dragging logic is the final step in creating a functional System 7 "OS" for your Android games. In a classic desktop environment, you could only drag a window by its Title Bar. We will replicate this specifically so the rest of the window (the buttons and checkboxes) stays interactive.

1. The "Title Bar" Drag Script

In Cocos 4, we attach this script to the "Title Bar" node of your Control Panel or Chooser. When the user drags the bar, it moves the entire "Parent" window.

WindowDrag.js (Pure JavaScript)

```
import { _decorator, Component, Node, Vec3 } from 'cc';
const { ccclass } = _decorator;

@ccclass('WindowDrag')
export class WindowDrag extends Component {
    onLoad() {
        // We listen for touches on the Title Bar only
        this.node.on(Node.EventType.TOUCH_MOVE, this.onDrag, this);
    }

    onDrag(event) {
        // 1. Get the movement delta (how far the finger moved)
        const delta = event.getDelta();

        // 2. Apply that movement to the PARENT node (the whole window)
        const parent = this.node.parent;
        const currentPos = parent.position;
        
        parent.setPosition(
            currentPos.x + delta.x, 
            currentPos.y + delta.y, 
            0
        );
    }
}
```


2. Implementation Details for Android
 * Z-Order (Focus): In System 7, clicking a window brought it to the front. You can do this in Cocos 4 by calling this.node.parent.setSiblingIndex(999) when a touch starts. This ensures the window you are dragging stays on top of the map tiles.
 * Boundary Checks: You might want to prevent the user from dragging the window completely off the screen. You can use Math.min and Math.max to keep the window within the Canvas boundaries.

3. The "Classic" UI Touch: Window Shading

In System 7.5, Apple introduced "WindowShade," where double-clicking the title bar would roll the window up like a window blind, leaving only the title bar visible.

Bonus "Pro" Logic:

```
// Add this to your WindowDrag.js
onTitleBarDoubleClick() {
    const body = this.node.parent.getChildByName("WindowBody");
    body.active = !body.active; // "Roll up" the window!
}
```


Your System 7 Mobile Framework is Ready!

You now have a highly customized, nostalgic development environment for your Android series:

| Component | Game Purpose | Retro Flavor |
|---|---|---|
| Splash Screen | Loading Assets | "Welcome to localSq" startup box |
| Top Menu Bar | Global Navigation | Apple menu + Clock + App Icon |
| The Chooser | Switching Games/Maps | Split-pane service selector |
| Control Panel | Settings/Dark Mode | Classic toggles and checkboxes |
| Trash Can | Deleting Favorites | Bulging icon feedback |
| Windows | Interactive UI | Draggable title bars and pixel borders |

This framework will make localSq, Shop Oahu, and Phoenix Valley feel like part of a unified "alternate reality" OS, which is a powerful way to build brand loyalty among your users.

Since we've built the frontend "OS," would you like me to help you set up the Python-based backend connection so your games can "Talk" to your server to fetch real-world local data?
