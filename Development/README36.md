Here is the comprehensive .gitignore file. It is specifically tuned to keep your Cocos 4 project artifacts, Python virtual environments, and SQLite databases (which can get massive) out of your version history while keeping your code safe.

```
.gitignore for SystemCore-7
# --- Cocos Creator 4 ---
/frontend/library/
/frontend/local/
/frontend/temp/
/frontend/build/
/frontend/profiles/
/frontend/native/
/frontend/assets/resources/import/
*.meta

# --- Python & Backend ---
__pycache__/
*.py[cod]
*$py.class
/backend/venv/
/backend/env/
.env

# --- Database & Cache ---
# We ignore the live DB, but you can keep your 'seed_data.py' 
# to recreate it anywhere.
*.db
*.sqlite3
/backend/map_cache.db

# --- OS / IDE ---
.DS_Store
.vscode/
.idea/
Thumbs.db

# --- Docker ---
.dockerignore
```

🧠 Brand Name Brainstorming (Ejected Media)

Since we want to avoid collisions with existing "Platinum" or "SystemCore" projects, let's lean into terms that are deeply specific to 1991-era Apple but feel fresh as a modern framework name.

Category A: The "Desktop" Icons 
These names play on the physical metaphors of the classic Mac desktop.
 * StationeryOS: "Stationery Pads" were a System 7 feature that let you create template files. It’s perfect for a framework meant to be a template for multiple games.
 * AliasFramework: An "Alias" was System 7's version of a shortcut. It sounds techy and mysterious.
 * BalloonHelp: (Classic Mac’s tooltips). It sounds friendly and lightweight—great if the framework is easy to use.

Category B: The "Architecture" 
Names that sound like the underlying engine.
 * TrueType-7: System 7 was the first to include TrueType fonts. Since your UI is so typography-focused, this is a strong nod to the tech.
 * ResEdit-OS: Named after the legendary "Resource Editor" tool used to hack Mac apps. It implies a high level of customization.
 * MicroKernel-7 (MK7): Sounds like a heavy-duty system architecture, but the "7" anchors it to the aesthetic.

Category C: The "Ejected Media" Synergy

Names that bridge your brand and the OS.
 * Ejecta-7: Short, punchy, and unique. It sounds like a chemical or a high-speed engine.
 * FloppyFlow: A bit more playful, emphasizing the "Ejected" brand and the "Flow" of data in your map.
 * DiskCopy-7: A classic utility name. It implies that your framework is a perfect "copy" of the System 7 experience.
Category D: Abstract & Retro
 * BlueMeanies: The internal Apple codename for the System 7 group. Very "insider" and very cool for a GitHub repo name.
 * 7-Platinum-Core: Adding the numbers and descriptors together to create a unique string that won't be confused with other OS projects.

Which of these directions feels like it has the "right" energy for Ejected Media? Personally, StationeryOS or Ejecta-7 have a very modern-yet-retro "Indie Dev" ring to them.

Would you like me to see if any of these have particularly cool 1-bit style logo potential to go with the anime Vtube girl portrait we made?
