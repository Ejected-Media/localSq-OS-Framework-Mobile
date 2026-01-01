To truly nail the MacOS 7 aesthetic for your main app screen, we’ll build a "Desktop" style menu bar. In the classic System 7 days, the menu bar was a permanent, 20-pixel-high strip at the top of the screen that housed the Apple menu, File, Edit, and the legendary Application menu on the far right.

1. The Classic Menu Bar UI Setup

In the Cocos Editor, create a Sprite node at the very top of your Canvas.
 * Dimensions: Set the height to 40px (or 60px for modern high-DPI Android screens).
 * Color: Use the classic Platinum gray (#D8D8D8).
 * Border: Add a 1px solid black line only at the bottom of the bar to separate it from the map.
 * The Apple Menu: Place a small 1-bit style icon (the rainbow Apple or a simple custom logo) on the far left.

2. The "Pull-Down" Menu Logic 
Classic Mac menus didn't "hover"; they were clicked/touched to stay open. We can build this using a simple Toggle logic in JavaScript.

MenuBarController.js

```
import { _decorator, Component, Node, Label, Color, v3 } from 'cc';

export class MenuBarController extends Component {
    @property(Node)
    fileMenuDropdown = null; // The hidden list of options

    onLoad() {
        this.fileMenuDropdown.active = false;
        
        // Listen for the "Apple" or "File" click
        this.node.getChildByName("FileButton").on(Node.EventType.TOUCH_END, this.toggleMenu, this);
    }

    toggleMenu() {
        this.fileMenuDropdown.active = !this.fileMenuDropdown.active;
        
        // Highlight the menu title (Invert colors like classic MacOS)
        const titleLabel = this.node.getChildByName("FileButton").getComponent(Label);
        if (this.fileMenuDropdown.active) {
            titleLabel.color = Color.WHITE;
            this.node.getChildByName("FileButton").getComponent(Sprite).color = Color.BLACK;
        } else {
            titleLabel.color = Color.BLACK;
            this.node.getChildByName("FileButton").getComponent(Sprite).color = Color.TRANSPARENT;
        }
    }
}
```


3. Iconic Features for Your Series 
To make localSq or Shop Oahu feel like a genuine System 7 environment, add these "Widgets" to your bar:
 * The Clock: On the far right, add a simple Label that updates every minute.
 * The "Application" Icon: In System 7, the far right showed the icon of the app you were using. You could put the localSq or Shop Oahu logo here.
 * The "About" Box: Clicking the Apple menu should trigger a pop-up (using the "Welcome" box style from the splash screen) that says "About localSq" with the version number.

4. Retro Font Integration 
The "Chicago" font is the soul of MacOS 7. Since it's a bitmap font, it scales beautifully in Cocos 4 if you use it as a Label with "Sharp" sampling.
 * Tip: Look for "Chicago.ttf" or "Geneva.ttf" and drag it into your assets. Set your labels to use this font exclusively.

Why this is perfect for your Projects:
 * Series Branding: This top bar becomes your "Global Navigation." No matter which game the user is in, they always know where the "Home" and "Settings" buttons are—just like a Mac user in 1991.
 * Android Usability: This "Desktop" metaphor works surprisingly well on mobile because it keeps the center of the screen clear for your map tiles and shop markers.
 * Low Overhead: These are just simple Sprites and Labels. They won't slow down your Android performance.

Would you like me to show you how to add the "Trash Can" icon to the bottom right of the screen so users can "drag and drop" markers to delete them?
