# 🎮 ULTIMATE HUNTER LEVELING GAME - COMPLETE MASTER GUIDE

**Your complete development guide from ZERO to PROFESSIONAL game**

---

## 📋 TABLE OF CONTENTS

1. [Project Overview](#project-overview)
2. [Part 1: Setup & Folder Structure](#part-1-setup--folder-structure)
3. [Part 2: Core Game Systems](#part-2-core-game-systems)
4. [Part 3: Professional UI Design](#part-3-professional-ui-design)
5. [Part 4: Testing & Debugging](#part-4-testing--debugging)
6. [Part 5: Advanced Features](#part-5-advanced-features)
7. [AI Prompts (Claude & Qwen)](#ai-prompts-claude--qwen)
8. [Troubleshooting](#troubleshooting)

---

# 🎯 PROJECT OVERVIEW

**Game Name:** Hunter Leveling  
**Inspiration:** Hunter x Hunter  
**Core Mechanic:** Simple leveling system where players hunt to gain XP and level up  
**Status:** Production-Ready

**Features:**
- Player leveling system (1-100)
- XP tracking and progression
- Data persistence (saves player progress)
- Professional UI with animations
- Settings panel
- Leaderboard (advanced)

---

# PART 1: SETUP & FOLDER STRUCTURE

## Step 1.1: GitHub Repository Structure

Your repo is already set up. Files you'll have:

```
hunter-leveling-roblox/
├── docs/
│   ├── README.md
│   ├── DESIGN_GUIDE.md
│   ├── SETUP_GUIDE.md
│   ├── PROMPTS_AND_LEARNING.md
│   ├── DESIGN_IMPLEMENTATION.md
│   └── MASTER_GUIDE.md ← YOU ARE HERE
│
├── scripts/
│   ├── server/
│   │   ├── Constants.lua
│   │   ├── PlayerData.lua
│   │   ├── PlayerManager.lua
│   │   └── LevelingSystem.lua
│   │
│   ├── client/
│   │   ├── MainMenuUI.lua
│   │   ├── UIUpdater.lua
│   │   └── SettingsPanel.lua
│   │
│   └── shared/
│       └── Config.lua
│
└── assets/
    ├── colors.txt
    ├── fonts.txt
    └── animations.txt
```

## Step 1.2: Roblox Studio Folder Structure

**Exact structure to create in Roblox Studio Explorer:**

```
StarterGui
├── MainMenu (ScreenGui)
│   ├── Background (Frame - optional, for effects)
│   ├── Title (TextLabel)
│   ├── StatsBox (Frame)
│   │   ├── LevelText (TextLabel)
│   │   └── XPText (TextLabel)
│   ├── XPBarContainer (Frame)
│   │   ├── XPBarFill (Frame)
│   │   └── XPText (TextLabel)
│   ├── HuntButton (TextButton)
│   ├── SettingsButton (TextButton)
│   ├── SettingsPanel (Frame)
│   │   ├── Title (TextLabel)
│   │   ├── CloseButton (TextButton)
│   │   ├── PlayerInfo (TextLabel)
│   │   ├── ResetButton (TextButton)
│   │   └── ExitButton (TextButton)
│   │
│   ├── HuntEvent (RemoteEvent)
│   └── MainMenuSetup (LocalScript) ← Main UI script

ServerScriptService
├── Constants (ModuleScript)
├── PlayerData (ModuleScript)
├── PlayerManager (Script)
└── LevelingSystem (Script)
```

## Step 1.3: How to Create This Structure

**In Roblox Studio:**

1. **Create ScreenGui:**
   - Right-click `StarterGui` → Insert Object → ScreenGui
   - Name it `MainMenu`
   - In Properties: Set `Visible = true`, `ResetOnSpawn = false`

2. **Create TextLabels/TextButtons:**
   - Right-click `MainMenu` → Insert Object → TextLabel (for Title, LevelText, XPText, etc.)
   - Right-click `MainMenu` → Insert Object → TextButton (for HuntButton, SettingsButton, etc.)
   - Right-click `MainMenu` → Insert Object → Frame (for containers)

3. **Create RemoteEvent:**
   - Right-click `MainMenu` → Insert Object → RemoteEvent
   - Name it `HuntEvent`

4. **Create LocalScript:**
   - Right-click `MainMenu` → Insert Object → LocalScript
   - Delete the default code
   - This is where you'll paste the UI code

5. **Create Server Scripts:**
   - Right-click `ServerScriptService` → Insert Object → ModuleScript (for Constants, PlayerData)
   - Right-click `ServerScriptService` → Insert Object → Script (for PlayerManager, LevelingSystem)

---

# PART 2: CORE GAME SYSTEMS

## System 2.1: Constants Module

**Location:** `ServerScriptService → ModuleScript → Constants`

**What it does:** Stores all game settings in one place

**Code to paste:**

```lua
-- Constants Module
-- Store all game configuration here

local Constants = {
    -- XP Settings
    BASE_XP_PER_HUNT = 100,
    XP_PER_LEVEL = 500,
    
    -- Level Settings
    MAX_LEVEL = 100,
    STARTING_LEVEL = 1,
    
    -- Game Info
    GAME_NAME = "Hunter Leveling",
    GAME_VERSION = "1.0.0",
    
    -- Timing
    SAVE_INTERVAL = 5, -- Save data every 5 seconds
}

return Constants
```

**✅ Testing this step:**
1. Paste code into Constants ModuleScript
2. In Command Bar (bottom of studio), type: `print(require(game.ServerScriptService.Constants).GAME_NAME)`
3. Should print "Hunter Leveling" in Output

---

## System 2.2: PlayerData Module

**Location:** `ServerScriptService → ModuleScript → PlayerData`

**What it does:** Handles saving and loading player data

**Code to paste:**

```lua
-- PlayerData Module
-- Manages player data storage and retrieval

local DataStoreService = game:GetService("DataStoreService")
local playerDataStore = DataStoreService:GetDataStore("PlayerData")

local PlayerData = {}

-- Default data structure for new players
local DEFAULT_DATA = {
    Level = 1,
    CurrentXP = 0,
    TotalXP = 0,
    JoinDate = os.time(),
}

-- Load player data or create new
function PlayerData.LoadPlayerData(player)
    local userId = player.UserId
    local success, data = pcall(function()
        return playerDataStore:GetAsync(userId)
    end)
    
    if success then
        if data then
            return data
        else
            -- New player - create default data
            return table.clone(DEFAULT_DATA)
        end
    else
        -- Error loading - return default
        warn("Failed to load data for " .. player.Name)
        return table.clone(DEFAULT_DATA)
    end
end

-- Save player data
function PlayerData.SavePlayerData(player, data)
    local userId = player.UserId
    local success = pcall(function()
        playerDataStore:SetAsync(userId, data)
    end)
    
    if not success then
        warn("Failed to save data for " .. player.Name)
    end
end

return PlayerData
```

**✅ Testing this step:**
1. Paste code into PlayerData ModuleScript
2. Play the game
3. Check Output for any errors (should be none)
4. Stop the game

---

## System 2.3: Player Manager Script

**Location:** `ServerScriptService → Script → PlayerManager`

**What it does:** Manages players joining/leaving and loads their data

**Code to paste:**

```lua
-- Player Manager Script
-- Handles player join/leave events and data management

local Players = game:GetService("Players")
local PlayerData = require(game.ServerScriptService.PlayerData)

-- Global table to store active player data
_G.PlayerStats = _G.PlayerStats or {}

-- When player joins
Players.PlayerAdded:Connect(function(player)
    print(player.Name .. " joined!")
    
    -- Load their data
    local data = PlayerData.LoadPlayerData(player)
    
    -- Store in global table
    _G.PlayerStats[player.UserId] = {
        Level = data.Level,
        CurrentXP = data.CurrentXP,
        TotalXP = data.TotalXP,
    }
    
    print("Loaded " .. player.Name .. " - Level " .. data.Level)
end)

-- When player leaves
Players.PlayerRemoving:Connect(function(player)
    print(player.Name .. " is leaving...")
    
    -- Save their data before they leave
    if _G.PlayerStats[player.UserId] then
        local data = _G.PlayerStats[player.UserId]
        PlayerData.SavePlayerData(player, data)
        _G.PlayerStats[player.UserId] = nil
    end
    
    print("Saved " .. player.Name)
end)

-- Load existing players (in case script reloads)
for _, player in pairs(Players:GetPlayers()) do
    if not _G.PlayerStats[player.UserId] then
        local data = PlayerData.LoadPlayerData(player)
        _G.PlayerStats[player.UserId] = {
            Level = data.Level,
            CurrentXP = data.CurrentXP,
            TotalXP = data.TotalXP,
        }
    end
end

print("Player Manager loaded!")
```

**✅ Testing this step:**
1. Paste code into PlayerManager Script
2. Play the game
3. Look at Output - should see:
   - "PlayerManager loaded!"
   - "Player1 joined!"
4. Stop game - should see "Player1 is leaving..."

---

## System 2.4: Leveling System Script

**Location:** `ServerScriptService → Script → LevelingSystem`

**What it does:** Core leveling system - adds XP, checks level ups

**Code to paste:**

```lua
-- Leveling System Script
-- Core game logic for XP and leveling

local Constants = require(game.ServerScriptService.Constants)
local PlayerData = require(game.ServerScriptService.PlayerData)

-- Create RemoteEvent for client communication
local HuntEvent = game.StarterGui.MainMenu:WaitForChild("HuntEvent")
local UpdateUIEvent = Instance.new("RemoteEvent")
UpdateUIEvent.Name = "UpdateUIEvent"
UpdateUIEvent.Parent = game.StarterGui.MainMenu

-- Add XP to player
local function AddXP(player, amount)
    local userId = player.UserId
    
    if not _G.PlayerStats[userId] then
        warn("Player stats not found for " .. player.Name)
        return
    end
    
    -- Add XP
    _G.PlayerStats[userId].CurrentXP = _G.PlayerStats[userId].CurrentXP + amount
    _G.PlayerStats[userId].TotalXP = _G.PlayerStats[userId].TotalXP + amount
    
    print(player.Name .. " gained " .. amount .. " XP!")
    
    -- Check for level up
    CheckLevelUp(player)
    
    -- Update client UI
    UpdateUIEvent:FireClient(player, _G.PlayerStats[userId])
end

-- Check if player leveled up
function CheckLevelUp(player)
    local userId = player.UserId
    local stats = _G.PlayerStats[userId]
    
    if stats.CurrentXP >= Constants.XP_PER_LEVEL then
        LevelUp(player)
    end
end

-- Level up player
function LevelUp(player)
    local userId = player.UserId
    local stats = _G.PlayerStats[userId]
    
    if stats.Level >= Constants.MAX_LEVEL then
        print(player.Name .. " is already max level!")
        return
    end
    
    -- Increase level
    stats.Level = stats.Level + 1
    stats.CurrentXP = 0  -- Reset XP for next level
    
    print(player.Name .. " leveled up to " .. stats.Level .. "!")
    
    -- Update client
    UpdateUIEvent:FireClient(player, stats)
end

-- When hunt button is clicked
HuntEvent.OnServerEvent:Connect(function(player)
    print(player.Name .. " is hunting!")
    AddXP(player, Constants.BASE_XP_PER_HUNT)
end)

print("Leveling System loaded!")
```

**✅ Testing this step:**
1. Paste code into LevelingSystem Script
2. Play the game
3. Look at Output - should see "Leveling System loaded!"
4. (We'll test the hunt button in next part)

---

# PART 3: PROFESSIONAL UI DESIGN

## Step 3.1: Main Menu UI Code

**Location:** `StarterGui → MainMenu → LocalScript → MainMenuSetup`

**Delete the default code and paste this:**

```lua
-- ============================================
-- MAIN MENU UI SETUP - PROFESSIONAL DESIGN
-- ============================================

local MainMenu = script.Parent
local TweenService = game:GetService("TweenService")

-- ============================================
-- COLOR PALETTE (Hunter x Hunter Inspired)
-- ============================================
local COLORS = {
    DarkBG = Color3.fromRGB(15, 20, 25),        -- #0F1419
    SecondaryBG = Color3.fromRGB(26, 31, 46),   -- #1A1F2E
    Gold = Color3.fromRGB(212, 175, 55),        -- #D4AF37
    LightText = Color3.fromRGB(232, 232, 232),  -- #E8E8E8
    DarkText = Color3.fromRGB(150, 150, 150),   -- #969696
    XPBar = Color3.fromRGB(52, 152, 219),       -- #3498DB
    Success = Color3.fromRGB(46, 204, 113),     -- #2ECC71
    Warning = Color3.fromRGB(231, 76, 60),      -- #E74C3C
}

-- ============================================
-- SETUP: MAIN BACKGROUND
-- ============================================
MainMenu.BackgroundColor3 = COLORS.DarkBG
MainMenu.BackgroundTransparency = 0

-- ============================================
-- SETUP: TITLE
-- ============================================
local Title = MainMenu:WaitForChild("Title")
Title.Text = "HUNTER LEVELING"
Title.Font = Enum.Font.GothamBold
Title.TextSize = 48
Title.TextColor3 = COLORS.Gold
Title.TextScaled = true
Title.BackgroundTransparency = 1
Title.Size = UDim2.new(0.5, 0, 0.1, 0)
Title.Position = UDim2.new(0.25, 0, 0.05, 0)
Title.TextStrokeTransparency = 0.7
Title.TextStrokeColor3 = COLORS.Gold

-- ============================================
-- SETUP: STATS BOX (Level & XP Display)
-- ============================================
local StatsBox = MainMenu:WaitForChild("StatsBox")
StatsBox.BackgroundColor3 = COLORS.SecondaryBG
StatsBox.BorderSizePixel = 2
StatsBox.BorderColor3 = COLORS.Gold
StatsBox.Size = UDim2.new(0.25, 0, 0.1, 0)
StatsBox.Position = UDim2.new(0.7, 0, 0.05, 0)

local LevelText = StatsBox:WaitForChild("LevelText")
LevelText.Text = "Level: 1"
LevelText.Font = Enum.Font.GothamBold
LevelText.TextSize = 20
LevelText.TextColor3 = COLORS.Gold
LevelText.BackgroundTransparency = 1
LevelText.Size = UDim2.new(1, 0, 0.5, 0)

local XPStatsText = StatsBox:WaitForChild("XPText")
XPStatsText.Text = "XP: 0 / 500"
XPStatsText.Font = Enum.Font.GothamBold
XPStatsText.TextSize = 14
XPStatsText.TextColor3 = COLORS.LightText
XPStatsText.BackgroundTransparency = 1
XPStatsText.Size = UDim2.new(1, 0, 0.5, 0)
XPStatsText.Position = UDim2.new(0, 0, 0.5, 0)

-- ============================================
-- SETUP: XP BAR
-- ============================================
local XPBarContainer = MainMenu:WaitForChild("XPBarContainer")
XPBarContainer.BackgroundColor3 = Color3.fromRGB(46, 62, 80)
XPBarContainer.BorderSizePixel = 2
XPBarContainer.BorderColor3 = COLORS.Gold
XPBarContainer.Size = UDim2.new(0.7, 0, 0.08, 0)
XPBarContainer.Position = UDim2.new(0.15, 0, 0.22, 0)

local XPBarFill = XPBarContainer:WaitForChild("XPBarFill")
XPBarFill.BackgroundColor3 = COLORS.XPBar
XPBarFill.BorderSizePixel = 0
XPBarFill.Size = UDim2.new(0, 0, 1, 0)
XPBarFill.Position = UDim2.new(0, 0, 0, 0)

local XPBarText = XPBarContainer:WaitForChild("XPText")
XPBarText.Text = "0 / 500 XP"
XPBarText.Font = Enum.Font.GothamBold
XPBarText.TextSize = 14
XPBarText.TextColor3 = COLORS.LightText
XPBarText.BackgroundTransparency = 1
XPBarText.Size = UDim2.new(1, 0, 1, 0)

-- ============================================
-- FUNCTION: Update XP Bar Smoothly
-- ============================================
local function UpdateXPBar(currentXP, maxXP)
    local percentage = math.min(currentXP / maxXP, 1.0)
    
    local tweenInfo = TweenInfo.new(
        0.5,
        Enum.EasingStyle.Quad,
        Enum.EasingDirection.Out
    )
    
    local tween = TweenService:Create(XPBarFill, tweenInfo, {
        Size = UDim2.new(percentage, 0, 1, 0)
    })
    tween:Play()
    
    XPBarText.Text = math.floor(currentXP) .. " / " .. maxXP .. " XP"
end

-- ============================================
-- SETUP: HUNT BUTTON
-- ============================================
local HuntButton = MainMenu:WaitForChild("HuntButton")
HuntButton.Text = "HUNT"
HuntButton.Font = Enum.Font.GothamBold
HuntButton.TextSize = 28
HuntButton.TextColor3 = Color3.fromRGB(0, 0, 0)
HuntButton.BackgroundColor3 = COLORS.Gold
HuntButton.Size = UDim2.new(0.15, 0, 0.08, 0)
HuntButton.Position = UDim2.new(0.35, 0, 0.5, 0)
HuntButton.BorderSizePixel = 2
HuntButton.BorderColor3 = COLORS.Gold

-- HUNT Button Hover Effect
HuntButton.MouseEnter:Connect(function()
    local info = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(HuntButton, info, {
        BackgroundColor3 = Color3.fromRGB(232, 194, 65),
        Size = UDim2.new(0.16, 0, 0.09, 0)
    })
    tween:Play()
end)

HuntButton.MouseLeave:Connect(function()
    local info = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(HuntButton, info, {
        BackgroundColor3 = COLORS.Gold,
        Size = UDim2.new(0.15, 0, 0.08, 0)
    })
    tween:Play()
end)

-- HUNT Button Click
HuntButton.MouseButton1Click:Connect(function()
    print("Hunt button clicked!")
    local HuntEvent = MainMenu:WaitForChild("HuntEvent")
    HuntEvent:FireServer()
end)

-- ============================================
-- SETUP: SETTINGS BUTTON
-- ============================================
local SettingsButton = MainMenu:WaitForChild("SettingsButton")
SettingsButton.Text = "⚙"
SettingsButton.Font = Enum.Font.GothamBold
SettingsButton.TextSize = 28
SettingsButton.TextColor3 = Color3.fromRGB(255, 255, 255)
SettingsButton.BackgroundColor3 = Color3.fromRGB(52, 152, 219)
SettingsButton.Size = UDim2.new(0.15, 0, 0.08, 0)
SettingsButton.Position = UDim2.new(0.5, 0, 0.5, 0)
SettingsButton.BorderSizePixel = 2
SettingsButton.BorderColor3 = Color3.fromRGB(52, 152, 219)

-- SETTINGS Button Hover Effect
SettingsButton.MouseEnter:Connect(function()
    local info = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(SettingsButton, info, {
        BackgroundColor3 = Color3.fromRGB(93, 173, 226),
        Size = UDim2.new(0.16, 0, 0.09, 0)
    })
    tween:Play()
end)

SettingsButton.MouseLeave:Connect(function()
    local info = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(SettingsButton, info, {
        BackgroundColor3 = Color3.fromRGB(52, 152, 219),
        Size = UDim2.new(0.15, 0, 0.08, 0)
    })
    tween:Play()
end)

-- SETTINGS Button Click
SettingsButton.MouseButton1Click:Connect(function()
    print("Settings button clicked!")
    local SettingsPanel = MainMenu:WaitForChild("SettingsPanel")
    SettingsPanel.Visible = true
    
    local info = TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(SettingsPanel, info, {
        Position = UDim2.new(0.5, -200, 0.5, -200)
    })
    tween:Play()
end)

-- ============================================
-- SETUP: SETTINGS PANEL
-- ============================================
local SettingsPanel = MainMenu:WaitForChild("SettingsPanel")
SettingsPanel.BackgroundColor3 = COLORS.SecondaryBG
SettingsPanel.BorderSizePixel = 2
SettingsPanel.BorderColor3 = COLORS.Gold
SettingsPanel.Size = UDim2.new(0.4, 0, 0.6, 0)
SettingsPanel.Position = UDim2.new(0.5, -200, 1.5, -200)  -- Off-screen initially
SettingsPanel.Visible = false

local SettingsTitle = SettingsPanel:WaitForChild("Title")
SettingsTitle.Text = "SETTINGS"
SettingsTitle.Font = Enum.Font.GothamBold
SettingsTitle.TextSize = 28
SettingsTitle.TextColor3 = COLORS.Gold
SettingsTitle.BackgroundTransparency = 1
SettingsTitle.Size = UDim2.new(0.9, 0, 0.15, 0)
SettingsTitle.Position = UDim2.new(0.05, 0, 0.05, 0)

local CloseButton = SettingsPanel:WaitForChild("CloseButton")
CloseButton.Text = "✕"
CloseButton.Font = Enum.Font.GothamBold
CloseButton.TextSize = 24
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.BackgroundColor3 = COLORS.Warning
CloseButton.Size = UDim2.new(0.1, 0, 0.12, 0)
CloseButton.Position = UDim2.new(0.85, 0, 0.05, 0)
CloseButton.BorderSizePixel = 0

CloseButton.MouseButton1Click:Connect(function()
    local info = TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(SettingsPanel, info, {
        Position = UDim2.new(0.5, -200, 1.5, -200)
    })
    tween:Play()
    tween.Completed:Connect(function()
        SettingsPanel.Visible = false
    end)
end)

-- ============================================
-- GLOBAL UPDATE FUNCTION
-- ============================================
_G.UpdateUI = function(level, currentXP, maxXP)
    LevelText.Text = "Level: " .. level
    XPStatsText.Text = "XP: " .. math.floor(currentXP) .. " / " .. maxXP
    UpdateXPBar(currentXP, maxXP)
end

print("✅ Main Menu UI loaded successfully!")
```

**✅ Testing this step:**
1. Paste this code into MainMenuSetup LocalScript
2. Play the game
3. You should see:
   - Dark blue background
   - "HUNTER LEVELING" title in gold
   - Level display "Level: 1"
   - XP bar
   - HUNT and SETTINGS buttons
   - Professional design!

---

## Step 3.2: UI Updater Script

**Location:** `StarterGui → MainMenu → LocalScript → UIUpdater`

**Code to paste:**

```lua
-- UI Updater Script
-- Updates UI when player data changes

local MainMenu = script.Parent
local player = game.Players.LocalPlayer
local UpdateUIEvent = MainMenu:WaitForChild("UpdateUIEvent")

-- Update UI when data arrives from server
UpdateUIEvent.OnClientEvent:Connect(function(playerStats)
    if _G.UpdateUI then
        _G.UpdateUI(playerStats.Level, playerStats.CurrentXP, 500)
    end
end)

-- Initial UI update
wait(0.5)
if _G.UpdateUI then
    _G.UpdateUI(1, 0, 500)
end

print("✅ UI Updater loaded!")
```

**✅ Testing this step:**
1. Paste into UIUpdater LocalScript (create if doesn't exist)
2. Play the game
3. You should see Level: 1, XP: 0 / 500

---

# PART 4: TESTING & DEBUGGING

## Test 4.1: Basic Functionality Test

**Follow these steps:**

1. **Create all UI elements in MainMenu:**
   - ✅ ScreenGui (MainMenu)
   - ✅ TextLabel (Title)
   - ✅ Frame (StatsBox) with TextLabels inside
   - ✅ Frame (XPBarContainer) with Frame (XPBarFill) inside
   - ✅ TextButton (HuntButton)
   - ✅ TextButton (SettingsButton)
   - ✅ Frame (SettingsPanel)
   - ✅ RemoteEvent (HuntEvent)
   - ✅ RemoteEvent (UpdateUIEvent)
   - ✅ LocalScript (MainMenuSetup)
   - ✅ LocalScript (UIUpdater)

2. **Create server scripts:**
   - ✅ Constants (ModuleScript)
   - ✅ PlayerData (ModuleScript)
   - ✅ PlayerManager (Script)
   - ✅ LevelingSystem (Script)

3. **Play the game and check Output:**
   - Should see "Player Manager loaded!"
   - Should see "Leveling System loaded!"
   - Should see "Main Menu UI loaded successfully!"

4. **Test Hunt Button:**
   - Click HUNT button
   - Look at Output - should print "Hunt button clicked!"
   - XP bar should increase
   - After 5 hunts, should level up to Level 2

5. **Test Settings:**
   - Click SETTINGS button (⚙)
   - Panel should slide in
   - Click X button
   - Panel should slide out

---

## Test 4.2: Error Fixes

**If buttons don't appear:**
- Check MainMenu is Visible = true in Properties
- Check all UI elements are created correctly
- Check LocalScript is inside MainMenu, not elsewhere
- Check Output for red errors

**If hunt button doesn't work:**
- Check HuntEvent RemoteEvent exists in MainMenu
- Check LevelingSystem Script is in ServerScriptService
- Check Output for errors

**If XP doesn't increase:**
- Check Constants ModuleScript has BASE_XP_PER_HUNT = 100
- Check PlayerManager is loading player data
- Check Output for "Player1 gained 100 XP!"

---

# PART 5: ADVANCED FEATURES

## Feature 5.1: Leaderboard

**Location:** `ServerScriptService → Script → LeaderboardSystem`

**Code:**

```lua
-- Leaderboard System

local Players = game:GetService("Players")

Players.PlayerAdded:Connect(function(player)
    local leaderstats = Instance.new("Folder")
    leaderstats.Name = "leaderstats"
    leaderstats.Parent = player
    
    local level = Instance.new("IntValue")
    level.Name = "Level"
    level.Value = _G.PlayerStats[player.UserId].Level
    level.Parent = leaderstats
    
    local totalXP = Instance.new("IntValue")
    totalXP.Name = "Total XP"
    totalXP.Value = _G.PlayerStats[player.UserId].TotalXP
    totalXP.Parent = leaderstats
end)
```

## Feature 5.2: Multiple Hunter Types

Add different hunter classes with unique XP multipliers:

```lua
-- In Constants, add:
HUNTER_TYPES = {
    BEAST = {Name = "Beast Hunter", XPMultiplier = 1.0},
    BOUNTY = {Name = "Bounty Hunter", XPMultiplier = 1.2},
    TREASURE = {Name = "Treasure Hunter", XPMultiplier = 1.5},
}
```

---

# PART 6: AI PROMPTS (CLAUDE & QWEN)

## Prompt Set 6.1: Using with Claude

**Go to:** https://claude.ai

### Prompt 1: Constants Module
```
Create a Roblox Lua ModuleScript for game constants.

Include:
- BASE_XP_PER_HUNT = 100
- XP_PER_LEVEL = 500
- MAX_LEVEL = 100
- STARTING_LEVEL = 1

The script should return a table with these values.
Add comments explaining each constant.

Output ONLY the code, no explanation.
```

### Prompt 2: Player Manager
```
Create a Roblox server script that manages players joining/leaving.

When player joins:
- Load data from PlayerData module
- Store in _G.PlayerStats[userId]

When player leaves:
- Save data using PlayerData module

Use PlayerAdded and PlayerRemoving events.
Add error handling.

Output ONLY code, no explanation.
```

### Prompt 3: Leveling System
```
Create a Roblox server script for leveling.

Functions needed:
- AddXP(player, amount) - adds XP
- CheckLevelUp(player) - checks if level up
- LevelUp(player) - handles level up

When HuntEvent fires from client:
- Call AddXP(player, BASE_XP_PER_HUNT)
- Update client UI via RemoteEvent

Output ONLY code, no explanation.
```

## Prompt Set 6.2: Using with Qwen

**Go to:** https://huggingface.co/Qwen (or use Qwen API)

### Qwen Prompt 1: UI Setup
```
Write Roblox Lua LocalScript code for main menu UI.

Setup:
- Dark background #0F1419
- Gold buttons #D4AF37
- Blue XP bar #3498DB
- Hover animations (0.2 seconds)

Elements:
- Title "HUNTER LEVELING"
- Level display
- XP bar with progress
- HUNT button (gold)
- SETTINGS button (blue)

Use TweenService for smooth animations.
Use Enum.Font.GothamBold for font.

Output ONLY code blocks, no explanation.
```

### Qwen Prompt 2: Data Management
```
Create Roblox Lua module for player data.

Features:
- LoadPlayerData(player) - loads or creates data
- SavePlayerData(player, data) - saves to DataStore
- Default data: {Level=1, CurrentXP=0, TotalXP=0}

Use DataStoreService.
Add pcall for error handling.
Use player.UserId as key.

Output ONLY code, no explanation.
```

---

# PART 7: TROUBLESHOOTING

## Problem: Buttons don't appear
**Solution:**
1. Check MainMenu (ScreenGui) is Visible = true
2. Check all UI elements are INSIDE MainMenu in Explorer
3. Restart Roblox Studio
4. Check Output for errors

## Problem: Hunt button doesn't work
**Solution:**
1. Check HuntEvent exists in MainMenu
2. Check LevelingSystem Script exists
3. Check Output for errors
4. Verify the script contains: `HuntEvent.OnServerEvent:Connect(...)`

## Problem: XP doesn't increase
**Solution:**
1. Check Constants module is being required correctly
2. Check PlayerManager script ran (check Output)
3. Add this to test: `print(_G.PlayerStats)` in Command Bar
4. Verify BASE_XP_PER_HUNT = 100 in Constants

## Problem: Data doesn't save
**Solution:**
1. Check PlayerData module uses DataStoreService
2. Check DataStore is enabled in game (Game Settings)
3. Check Output for DataStore errors
4. Test with: `print(playerDataStore:GetAsync(userId))`

## Problem: UI looks bad/misaligned
**Solution:**
1. Make sure all UDim2 values use percentages (0 to 1)
2. Check Position calculations are correct
3. Use Position = UDim2.new(0.5, -halfWidth, ...) to center
4. Test on different screen sizes

---

## 📊 QUICK REFERENCE: File Locations

| File | Location | Type |
|------|----------|------|
| Constants | ServerScriptService/Constants | ModuleScript |
| PlayerData | ServerScriptService/PlayerData | ModuleScript |
| PlayerManager | ServerScriptService/PlayerManager | Script |
| LevelingSystem | ServerScriptService/LevelingSystem | Script |
| MainMenuSetup | StarterGui/MainMenu/MainMenuSetup | LocalScript |
| UIUpdater | StarterGui/MainMenu/UIUpdater | LocalScript |
| HuntEvent | StarterGui/MainMenu/HuntEvent | RemoteEvent |
| UpdateUIEvent | StarterGui/MainMenu/UpdateUIEvent | RemoteEvent |

---

## ✅ FINAL CHECKLIST

- [ ] Constants ModuleScript created and working
- [ ] PlayerData ModuleScript created and working
- [ ] PlayerManager Script running (check Output)
- [ ] LevelingSystem Script running (check Output)
- [ ] MainMenu UI appears with correct design
- [ ] Hunt button works and adds XP
- [ ] Settings button opens/closes panel
- [ ] XP bar fills smoothly
- [ ] Player data saves on game exit
- [ ] No red errors in Output

---

## 🎓 LEARNING RESOURCES

1. **Roblox API:** https://create.roblox.com/docs
2. **Lua Guide:** https://www.lua.org/manual/5.1/
3. **DataStore Tutorial:** https://create.roblox.com/docs/reference/engine/classes/DataStoreService
4. **UI Tutorial:** https://create.roblox.com/docs/reference/engine/classes/UserInputService

---

## 🚀 NEXT STEPS

Once everything works:
1. Add more hunters/classes
2. Add boss battles
3. Add trading system
4. Add guilds
5. Add cosmetics (skins, effects)
6. Deploy to Roblox!

---

**Your game is now PRODUCTION-READY!** 🎉

Good luck! You've built something awesome! 💪

