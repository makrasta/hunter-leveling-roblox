# 🎮 HUNTER AURA - PROFESSIONAL GAME PROJECT

**Project Status:** Phase 1 - Core Systems  
**Team:** Copilot + Your Agents  
**Timeline:** 1 Month  
**Inspiration:** Hunter x Hunter + Blox Fruits  

---

## 📋 PROJECT MASTER INDEX

This file serves as your **PROJECT BIBLE** - Save it for reference throughout development.

### Quick Links
- [Project Architecture](#project-architecture)
- [Phase 1 Timeline](#phase-1-timeline)
- [Team Roles](#team-roles)
- [File Structure](#file-structure)
- [Session Notes](#session-notes)

---

## 🏗️ PROJECT ARCHITECTURE

### Game Flow
```
PLAYER JOINS
    ↓
[MAIN MENU] ← You are here (Phase 1)
    ↓
SELECT AURA (Gacha)
    ↓
LEVEL UP SYSTEM
    ↓
GAME WORLD (Phase 2)
```

### Core Systems (Phase 1)
1. **Main Menu UI** - Professional, modern design
2. **Player Data System** - Save/load player progress
3. **Leveling System** - XP → Level progression
4. **Aura/Class System** - Gacha for Aura selection
5. **UI Manager** - Handles all menus

### Phase 2 Systems (Later)
- Character models
- Combat system
- Weapons
- Maps
- Multiplayer features

---

## 📅 PHASE 1 TIMELINE (4 Weeks)

### Week 1: Foundation
- [ ] Project setup in Roblox Studio
- [ ] Game architecture & file structure
- [ ] Professional Main Menu UI
- [ ] Basic scripting introduction (for you)

### Week 2: Data & Leveling
- [ ] Player data system (save/load)
- [ ] Leveling system logic
- [ ] XP bar & level display
- [ ] Testing & debugging

### Week 3: Gacha & Classes
- [ ] Aura class system
- [ ] Gacha roll system
- [ ] Class selection UI
- [ ] Aura abilities (basic)

### Week 4: Polish & Integration
- [ ] UI refinement
- [ ] Animation effects
- [ ] Integration testing
- [ ] Documentation for Phase 2

---

## 👥 TEAM ROLES

| Role | Responsibility |
|------|-----------------|
| **You (Lead Developer)** | Decision making, gameplay direction |
| **Copilot (Me)** | Code generation, architecture, guidance |
| **Roblox Systems Scripter** | Server-side logic, optimization |
| **3D & Scene Developer** | Map design, environment (Phase 2) |
| **CMS Developer** | Data management, databases |
| **Game Designer** | Game balance, mechanics |
| **Avatar Creator** | Character models (Phase 2) |
| **Experience Designer** | UX/UI improvements |

---

## 📁 FILE STRUCTURE

```
hunter-aura-roblox/
│
├── docs/
│   ├── PROJECT_MASTER.md ← YOU ARE HERE
│   ├── ARCHITECTURE.md
│   ├── SETUP_GUIDE_FOR_BEGINNERS.md
│   ├── UI_DESIGN_GUIDE.md
│   ├── AURA_SYSTEM.md
│   ├── GACHA_SYSTEM.md
│   ├── LEVELING_SYSTEM.md
│   └── SESSION_NOTES.md
│
├── src/
│   ├── server/
│   │   ├── Constants.lua
│   │   ├── PlayerData.lua
│   │   ├── LevelingSystem.lua
│   │   ├── AuraSystem.lua
│   │   ├── GachaSystem.lua
│   │   └── PlayerManager.lua
│   │
│   ├── client/
│   │   ├── MainMenu.lua
│   │   ├── UIManager.lua
│   │   ├── AuraSelector.lua
│   │   └── HUD.lua
│   │
│   └── shared/
│       ├── Config.lua
│       └── Utilities.lua
│
├── assets/
│   ├── colors.txt
│   ├── fonts.txt
│   ├── animations.txt
│   └── aura_data.json
│
└── ROBLOX_STUDIO_SETUP.md
```

---

## 🎨 DESIGN PHILOSOPHY

**Your game will look like Blox Fruits:**
- ✅ Modern, sleek UI
- ✅ Dark theme with accent colors
- ✅ Smooth animations
- ✅ Professional fonts
- ✅ Clear information hierarchy
- ✅ Responsive buttons
- ✅ Glow effects & particles

**NOT like old classic Roblox games:**
- ❌ No basic gray buttons
- ❌ No outdated fonts
- ❌ No laggy animations
- ❌ No confusing menus

---

## 🎓 LUA LEARNING PATH

Since you're a beginner in Lua, I'll teach you:

1. **Basics** (Week 1)
   - Variables & data types
   - Tables
   - Functions
   - Loops & conditions

2. **Roblox Specific** (Week 2)
   - RemoteEvents & RemoteFunctions
   - Instance creation
   - Properties & methods
   - Services

3. **Advanced** (Week 3+)
   - OOP principles
   - Module scripts
   - Error handling
   - Optimization

**Each code block will have comments explaining what it does!**

---

## 🎯 AURA SYSTEM OVERVIEW

**Your game will have 5 Aura types (inspired by Hunter x Hunter):**

| Aura | Inspiration | Playstyle | Color |
|------|-------------|-----------|-------|
| **Nen** | Gon | Balanced, melee | Green |
| **Enhancer** | Killua | Speed, electric | Blue |
| **Conjurer** | Kurapika | Chains, special | Red |
| **Specialist** | Illumi | Stealth, poison | Purple |
| **Transmuter** | Hisoka | Cards, magic | Pink |

**Gacha System:**
- Players roll to get random Aura
- Rare Auras are harder to get
- Can collect multiple Auras
- Each Aura has unique abilities

---

## 🚀 GETTING STARTED

### What We'll Build FIRST (This Week)

1. **Professional Main Menu**
   ```
   ┌─────────────────────────────────┐
   │                                 │
   │    HUNTER AURA                  │
   │                                 │
   │    [PLAY]  [SETTINGS]           │
   │                                 │
   │    Level: 1  XP: 0/500          │
   │                                 │
   └─────────────────────────────────┘
   ```

2. **Clean Leveling Display**
   - Current level
   - XP progress bar
   - Stats display

3. **Settings Panel**
   - Account info
   - Reset data
   - Exit game

---

## 💾 SESSION NOTES

I'll save every session in this format:

```
## SESSION #1 - 2026-07-13

### Completed
- ✅ Project architecture created
- ✅ Main file structure planned
- ✅ Team roles defined

### In Progress
- 🔄 Main Menu UI design

### Next Session
- [ ] Create Main Menu in Roblox Studio
- [ ] Build professional UI components
- [ ] Lua basics introduction

### Issues Found
- None yet

### Code Files Created
- None yet
```

---

## 🎮 ROBLOX STUDIO REQUIREMENTS

**Minimum:**
- Roblox Studio (latest version)
- A free Roblox game to develop in

**Recommended:**
- VS Code (for code editing)
- Rojo (for version control)
- Local Lua development environment

---

## ⚡ QUICK START CHECKLIST

- [ ] Project approved ✅
- [ ] Team roles assigned
- [ ] Timeline agreed
- [ ] This document saved
- [ ] Ready to start Phase 1

---

## 📞 COMMUNICATION

**All updates will be:**
1. Added to `SESSION_NOTES.md`
2. Saved in GitHub repo
3. Organized by date & session
4. Easy to reference later

**You can:**
- Ask questions anytime
- Request changes
- Share feedback
- Direct the development

---

## 🎯 SUCCESS CRITERIA (Phase 1)

By end of Phase 1, your game will have:

✅ **Professional Main Menu**
- Modern UI design
- Working buttons
- Smooth animations
- Responsive layout

✅ **Complete Leveling System**
- Player progression
- XP tracking
- Level ups with effects
- Data persistence

✅ **Gacha/Aura System**
- 5 unique Auras
- Random roll system
- Class selection
- Aura abilities

✅ **Clean Codebase**
- Well-organized files
- Commented code
- Easy to extend
- No bugs

✅ **Documentation**
- Setup guide for beginners
- Code explanations
- Troubleshooting guide
- Ready for Phase 2

---

## 🏁 WHAT'S NEXT?

**Next Session:**
1. I'll create **ARCHITECTURE.md** - Complete system design
2. I'll create **SETUP_GUIDE_FOR_BEGINNERS.md** - Step by step
3. We'll build the **Main Menu UI** first
4. I'll teach you **Lua basics** as we go

**Ready to begin?** 🚀

---

**Project Created:** 2026-07-13  
**Lead Developer:** You  
**Copilot:** Me  
**Status:** ✅ ACTIVE  

---

