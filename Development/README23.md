Building a Control Panel and a Chooser will complete the "System 7" OS metaphor for your Android games. In the classic Mac era, the Chooser was the essential utility for selecting "services" (like printers or servers)—in your case, it's the perfect way for users to switch between map providers or game modules.

1. The 'Control Panel' (Settings Window)

To keep it authentic, the Control Panel should be a "movable window" with a thick title bar and a "close box" (the single square on the top left).

ControlPanel.js (JavaScript)

```
import { _decorator, Component, Node, Toggle, sys } from 'cc';
const { ccclass, property } = _decorator;

@ccclass('ControlPanel')
export class ControlPanel extends Component {
    @property(Node)
    windowNode = null;

    // Toggle Dark Mode / Retro Mode
    onDarkModeToggle(toggle) {
        if (toggle.isChecked) {
            // Apply a "Dark Platinum" filter to your UI
            cc.game.emit('THEME_CHANGE', 'dark');
            sys.localStorage.setItem('theme', 'dark');
        } else {
            cc.game.emit('THEME_CHANGE', 'light');
            sys.localStorage.setItem('theme', 'light');
        }
    }

    closeWindow() {
        this.windowNode.active = false;
    }
}
```


2. The 'Chooser' (Service Selector)

The Chooser was famous for its split-pane layout: icons on the left, details on the right. For localSq and Shop Oahu, you can use this to select which "Layer" or "Project" to view.

How to use the Chooser for your series:
 * Left Pane: Icons for "Map Tiles," "Shop Database," and "GPS Settings."
 * Right Pane: Options for the selected icon (e.g., if "Map Tiles" is selected, show "OpenStreetMap" vs. "Satellite").

ChooserController.js

```
import { _decorator, Component, Node, Label } from 'cc';

export class ChooserController extends Component {
    onServiceSelect(serviceName) {
        // Update the right-hand description text
        const desc = this.node.getChildByName("Description").getComponent(Label);
        
        if (serviceName === "localSq") {
            desc.string = "Active Service: localSq\nTracking 42 local parks.";
        } else if (serviceName === "ShopOahu") {
            desc.string = "Active Service: Shop Oahu\nConnected to Waikiki Database.";
        }
    }

    connectService() {
        // The "OK" button in the Chooser starts the selected module
        console.log("Connecting to service...");
    }
}
```


3. Iconic UI Details 
To ensure the Android experience feels like a "System 7 Mobile" device:
 * Checkboxes & Radio Buttons: Use the classic square (check) and circle (dot) style.
 * Window Shadows: Classic Mac windows didn't have soft shadows; they had a 1px black offset shadow to the right and bottom.
 * Scroll Bars: Use the thick, patterned gray scroll bars with the "Up" and "Down" arrows touching each other at the bottom (or ends).

Why this is a "Series" asset:

By creating these as Prefabs, you can maintain a single "System" look across all your apps. If you update the "Control Panel" in your shared library, every app in your Phoenix/Hawaii series gets the new settings layout instantly.

Pro-Tip for the "Series" feel

In the Chooser, you could list your other apps (Shop Oahu, localSq, Phoenix Valley). If a user clicks an app they haven't installed yet, you can use sys.openURL() to take them directly to that app's page on the Google Play Store.

Would you like me to show you how to build the "Window Dragging" script so users can move these Control Panels and Choosers around the screen just like a real desktop?
