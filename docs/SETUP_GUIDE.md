# Complete Roblox Hunter Leveling System - Setup Guide

## 🎮 What You're Building
A simple Hunter leveling game with:
- Player leveling system
- Experience points (XP)
- Level display UI
- Settings menu
- Data persistence

---

## 📁 STEP 1: Roblox Studio Folder Structure

Open **Roblox Studio** and create this exact folder structure in **Explorer Panel** (left side):

```
StarterPlayer
├── StarterCharacterScripts
├── StarterPlayerScripts
└── StarterGui
    ├── MainMenu (ScreenGui)
    │   ├── LevelDisplay (TextLabel)
    │   ├── XPBar (Frame with ImageLabel)
    │   ├── HuntButton (TextButton)
    │   ├── SettingsButton (TextButton)
    │   └── SettingsPanel (Frame - hidden by default)
    │       ├── CloseButton (TextButton)
    │       └── SettingsList (ScrollingFrame)

ServerScriptService
├── PlayerManager (Script)
├── LevelingSystem (Script)
└── DataStore (Script)
```

**How to create folders in Roblox Studio:**
1. Right-click on **StarterGui** → Insert Object → ScreenGui (name it "MainMenu")
2. Right-click on **MainMenu** → Insert Object → TextLabel (for each UI element)
3. Right-click on **ServerScriptService** → Insert Object → Script (for server scripts)

---

## 🔧 STEP 2: Create Constants File

**Location:** ServerScriptService → New ModuleScript called "Constants"

**Purpose:** Store all game settings in one place

**Code to add:** (See PROMPTS.md for Claude prompt)

---

## 📝 STEP 3: Create DataStore Script

**Location:** ServerScriptService → New Script called "DataStore"

**Purpose:** Save and load player data (level, XP, etc.)

**Code to add:** (See PROMPTS.md for Claude prompt)

---

## ⚙️ STEP 4: Create Player Manager

**Location:** ServerScriptService → New Script called "PlayerManager"

**Purpose:** Manage player data when they join/leave

**Code to add:** (See PROMPTS.md for Claude prompt)

---

## 💪 STEP 5: Create Leveling System

**Location:** ServerScriptService → New Script called "LevelingSystem"

**Purpose:** Handle XP gains, level ups, calculations

**Code to add:** (See PROMPTS.md for Claude prompt)

---

## 🎨 STEP 6: Create Main Menu UI (Client)

**Location:** StarterGui → MainMenu → New LocalScript called "MainMenuScript"

**Purpose:** Handle UI buttons and display

**Code to add:** (See PROMPTS.md for Claude prompt)

---

## 🎯 STEP 7: Create UI Controller

**Location:** StarterGui → MainMenu → New LocalScript called "UIController"

**Purpose:** Update UI with player data in real-time

**Code to add:** (See PROMPTS.md for Claude prompt)

---

## ⚡ STEP 8: Create Settings UI

**Location:** StarterGui → MainMenu → SettingsPanel → New LocalScript called "SettingsUI"

**Purpose:** Handle settings menu interactions

**Code to add:** (See PROMPTS.md for Claude prompt)

---

## 🧪 Testing Your Game

1. **Play the game** (click Play in Roblox Studio)
2. **Check console** (View → Output for errors)
3. **Test buttons** (Hunt button should add XP)
4. **Test UI** (Level and XP should display)

---

## 📊 Expected Flow

```
Player Joins
    ↓
PlayerManager loads data from DataStore
    ↓
UIController displays player level/XP
    ↓
Player clicks "Hunt" button
    ↓
LevelingSystem adds XP
    ↓
UIController updates display
    ↓
If XP >= max, level up!
    ↓
DataStore saves new data
```

---

## ✅ Checklist

- [ ] Folder structure created in Roblox Studio
- [ ] All scripts created in correct locations
- [ ] Code added to each script
- [ ] Game tested and running
- [ ] Player data saving and loading
- [ ] Buttons working and responding
- [ ] UI updating correctly

---

## 🆘 Troubleshooting

**Problem:** Scripts not running
- **Solution:** Check Output (View → Output) for red errors

**Problem:** Buttons not working
- **Solution:** Make sure LocalScripts are in StarterGui, not ServerScriptService

**Problem:** Data not saving
- **Solution:** Check DataStore script is in ServerScriptService

**Problem:** UI not showing
- **Solution:** Make sure ScreenGui is enabled (check properties panel)

---

## 📚 Next Steps

After this works:
1. Add more hunter abilities
2. Add different enemy types
3. Create progression tiers
4. Add trading system
5. Add leaderboards

