In Cocos 4, while the engine is designed to be "TypeScript-first," you can still use pure JavaScript files. However, the way you use them depends on whether you want them to be part of your main game logic or treated as external libraries.

1. Can I write pure .js files?

Yes, but with caveats.
 * Mixed Mode: You can have a project with both .ts and .js files. Cocos will compile them together.
 * The "Plugin" Script Method: For vanilla JS files (like a custom mapping library or an old game logic script), you can import them into the project and mark them as "Import as Plugin" in the editor. This tells the engine not to modify the code and to make it available globally in the browser or native environment.

2. Why TypeScript is the "Default"
Cocos 4 uses TypeScript for its user-level APIs because it provides IntelliSense (autocomplete) and Type Safety. Since you are building a series of games, TypeScript is actually a massive advantage for your "Shared Core":
 * Refactoring: If you change a variable name in your shared mapping library, TypeScript will highlight every error in all five of your game projects instantly. In pure JS, you would have to find those bugs at runtime.
 * Documentation: Your shared code becomes self-documenting. A teammate (or "future you") will know exactly what parameters a function needs without digging through the source code.

3. Recommendation: The "Bridge" Strategy
Since you mentioned your mapping knowledge is in Python, and you likely have existing JS logic, here is the most efficient workflow for your Android series:

| Content Type | Recommended Format | Why? |
|---|---|---|
| High-level Game Logic | TypeScript | Best for UI, event handling, and Android bridge calls. |
| Existing JS Libraries | JavaScript (.js) | Import as "Plugin" to save time porting code. |
| Python Mapping Logic | Transpiled or API-based | Use a tool like Transcrypt to turn Python into JS, or run the Python on a small local server (for dev) and communicate via fetch. |

Summary for your Projects:
For localSq and Shop Oahu, I recommend keeping your Project Structure in TypeScript but importing your specific Mapping or Shop algorithms as .js files. This gives you the robust organization of a modern engine while letting you use the "pure" code you're already comfortable with.

Would you like to see how to set up a "Global Variable" in a pure JS file so that your TypeScript game code can talk to it easily?
