That is a fantastic idea. Combining the "Ejected Media" brand with a System 7 aesthetic creates a very strong "Retro-Digital" identity. Since "Ejected" refers to the classic Mac floppy disk behavior, the name should feel like a core system component or a fundamental utility.

Here are a few working names that fit the brand and your three projects (localSq, Shop Oahu, Phoenix Valley):

1. PlatinumOS * Why: "Platinum" was the internal name for the System 7 design language. It sounds premium, stable, and perfectly describes the gray-scale aesthetic.
 * Repo Name: ejected-media/platinum-os
2. FinderGo
 * Why: A play on the "Finder" (the Mac's file manager) and the mobile nature of your mapping apps. It implies "Finding things on the go."
 * Repo Name: ejected-media/finder-go
3. DesktopDB (My Personal Favorite)
 * Why: In MacOS 7, the Desktop DB was the invisible file that stored all the icons and file associations. Since your backend is a "Database" of map "Icons" (locations), it is technically accurate and very "inside baseball" for Mac fans.
 * Repo Name: ejected-media/desktop-db
4. ResourceFork
 * Why: Classic Mac files were split into a Data Fork and a Resource Fork (where icons and UI lived). Since you are building a UI-heavy mapping framework, this fits the technical structure of the OS.
 * Repo Name: ejected-media/resource-fork
5. SystemCore 7
 * Why: Simple, direct, and tells everyone exactly what the engine is based on.
 * Repo Name: ejected-media/system-core-7

Suggested Repo Structure 
Once you pick a name, I recommend organizing the repository like this to keep your "Shared Core" separate from the specific games:

```
/core          <-- The System 7 UI, Draggable Windows, and Chooser
/services      <-- Python API, Scrapers, and SQLite logic
/localsq       <-- Project-specific assets for Phoenix
/shop-oahu     <-- Project-specific assets for Hawaii
/docs          <-- The ReadMe and Architecture diagrams
```

Which of those names resonates most with the Ejected Media brand? Once we pick one, I can help you write the first "Commit Message" in the style of an old System 7 log!
