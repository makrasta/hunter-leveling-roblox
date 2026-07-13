# Claude Prompts for Code Generation + Lua Learning Guide

## 📚 Lua Basics for Beginners

Before you start, here are key Lua concepts you'll need to understand:

### 1. **Variables** (Store data)
```lua
local myVariable = 10          -- A number
local myString = "Hello"       -- Text
local myBoolean = true         -- true or false
local myTable = {1, 2, 3}      -- List of values
```

**Key:** Always use `local` to avoid global pollution!

### 2. **Tables** (Collections)
```lua
local player = {
    level = 45,
    xp = 250,
    name = "Hunter"
}

print(player.level)  -- Output: 45
player.level = 50    -- Change value
```

### 3. **Functions** (Reusable code)
```lua
local function AddXP(amount)
    print("Added " .. amount .. " XP")
end

AddXP(100)  -- Calls the function
```

### 4. **Loops** (Repeat code)
```lua
-- For loop
for i = 1, 5 do
    print(i)  -- Prints 1, 2, 3, 4, 5
end

-- While loop
local count = 0
while count < 5 do
    print(count)
    count = count + 1
end
```

### 5. **If Statements** (Conditions)
```lua
local level = 45

if level >= 50 then
    print("You're high level!")
elseif level >= 30 then
    print("You're mid level")
else
    print("You're low level")
end
```

### 6. **Strings** (Text manipulation)
```lua
local name = "Hunter"
local level = 45

-- Concatenation (joining)
local message = name .. " is level " .. level
print(message)  -- Output: Hunter is level 45

-- String formatting
local formatted = string.format("Level: %d", 45)
```

---

## 🎯 Claude Prompt System

**How to use:**
1. Copy the entire prompt below
2. Go to [Claude.ai](https://claude.ai)
3. Paste it in the chat
4. Claude will generate the code
5. Copy the code from Claude
6. Paste into your Roblox script (at the location specified)

---

## 📝 PROMPT 1: Constants Module (Learning Guide Included)

**Location in Roblox:** `ServerScriptService → ModuleScript called "Constants"`

**What this does:** Stores all game settings in ONE place so you can easily change them later.

**Copy and paste this into Claude:**

```
You are helping me create a Roblox Lua module for game constants/settings.

Requirements:
1. Create a ModuleScript that returns a table
2. Include these constants:
   - BASE_XP_PER_HUNT = 100 (XP you get per hunt)
   - XP_PER_LEVEL = 500 (XP needed to level up)
   - MAX_LEVEL = 100 (highest level)
   - STARTING_LEVEL = 1 (level new players start at)
   - GAME_NAME = "Hunter Leveling"

3. Structure should be:
   local Constants = {
       BASE_XP_PER_HUNT = 100,
       -- ... more constants
   }
   return Constants

4. Add comments explaining each constant

Output ONLY the Lua code, no explanation.
Format: Plain code block with ```lua and ```
```

**After Claude generates it:**

1. Copy the code
2. In Roblox Studio, right-click `ServerScriptService`
3. Click `Insert Object` → `ModuleScript`
4. Name it "Constants"
5. Delete the default code
6. Paste Claude's code

**Learning Tip:** 
- `local` = makes it private to this file
- `= {` = creating a table
- `return Constants` = sending the table out so other scripts can use it

---

## 📝 PROMPT 2: PlayerData Module (Save/Load System)

**Location in Roblox:** `ServerScriptService → ModuleScript called "PlayerData"`

**What this does:** Handles saving and loading player data (level, XP). Think of it as a "save file" system.

**Copy and paste this into Claude:**

```
Create a Roblox Lua ModuleScript for managing player data with DataStore.

Requirements:
1. Create functions to:
   - LoadPlayerData(player) - Gets saved data or creates new data
   - SavePlayerData(player, data) - Saves player data to DataStore
   
2. Data structure should be:
   {
       Level = 1,
       CurrentXP = 0,
       TotalXP = 0
   }

3. If player is new (no data), create with default values:
   - Level = 1
   - CurrentXP = 0
   - TotalXP = 0

4. Use DataStore2 for saving (or DataStoreService)
5. Use player.UserId as the key
6. Add error handling with pcall

7. Return a module with these functions:
   - LoadPlayerData(player)
   - SavePlayerData(player, data)

Add comments explaining what each function does.
Output ONLY code, no explanation.
```

**After Claude generates it:**

1. Copy the code
2. Right-click `ServerScriptService` → `ModuleScript`
3. Name it "PlayerData"
4. Paste Claude's code

**Learning Tips:**
- `pcall()` = "protected call" - runs code safely and catches errors
- `DataStore` = Roblox's built-in database for saving player info
- `player.UserId` = unique identifier for each player (like a social security number)

---

## 📝 PROMPT 3: Player Manager Script

**Location in Roblox:** `ServerScriptService → Script called "PlayerManager"`

**What this does:** Runs when players join/leave. Loads their data and saves it when they leave.

**Copy and paste this into Claude:**

```
Create a Roblox Lua server script for managing players joining and leaving.

Requirements:
1. Connect to Players service
2. When player joins:
   - Load their data using PlayerData module
   - Store in a global table called _G.PlayerStats
   
3. Structure:
   _G.PlayerStats[player.UserId] = {
       Level = data.Level,
       CurrentXP = data.CurrentXP,
       TotalXP = data.TotalXP
   }

4. When player leaves:
   - Save their data
   - Remove from _G.PlayerStats

5. Add error handling

6. Use these events:
   - game:GetService("Players").PlayerAdded:Connect(function(player)...end)
   - player.Leaving:Connect(function()...end)

7. Add comments explaining what each section does

Output ONLY code, no explanation.
```

**After Claude generates it:**

1. Copy the code
2. Right-click `ServerScriptService` → `Script` (NOT ModuleScript)
3. Name it "PlayerManager"
4. Paste Claude's code

**Learning Tips:**
- `game:GetService("Players")` = gets the Players service (Roblox service for managing players)
- `:Connect()` = listens for an event to happen
- `_G` = global table (all scripts can access it)
- `.PlayerAdded:Connect()` = fires when someone joins the game
- `player.Leaving:Connect()` = fires when someone leaves

---

## 📝 PROMPT 4: Leveling System Script

**Location in Roblox:** `ServerScriptService → Script called "LevelingSystem"`

**What this does:** The CORE of the game. Adds XP, checks for level ups, updates player stats.

**Copy and paste this into Claude:**

```
Create a Roblox Lua server script for the leveling system.

Requirements:
1. Create functions:
   - AddXP(player, amount) - Adds XP to player
   - CheckLevelUp(player) - Checks if they leveled up
   - LevelUp(player) - Handles level up logic
   
2. When AddXP is called:
   - Add amount to CurrentXP
   - Add amount to TotalXP
   - Call CheckLevelUp
   - Fire event to tell client to update UI

3. When CheckLevelUp:
   - If CurrentXP >= XP_PER_LEVEL:
     - Call LevelUp(player)
   - Else:
     - Just update UI

4. When LevelUp:
   - Increase Level by 1
   - Reset CurrentXP to 0
   - Show level up message
   - Fire LevelUpEvent

5. Create RemoteEvent called "HuntEvent" in StarterGui.MainMenu
6. When HuntEvent fires:
   - Call AddXP(player, BASE_XP_PER_HUNT)

7. Use Constants module for XP values
8. Add error handling

Output ONLY code, no explanation.
```

**After Claude generates it:**

1. Copy the code
2. Right-click `ServerScriptService` → `Script`
3. Name it "LevelingSystem"
4. Paste Claude's code

**Learning Tips:**
- `player.leaderstats` = Roblox way to store displayed stats
- `XP_PER_LEVEL` = comes from Constants module
- Events = way for server and client to communicate
- RemoteEvent = allows client (player's computer) to talk to server

---

## 📝 PROMPT 5: Main Menu UI Script (LocalScript)

**Location in Roblox:** `StarterGui → MainMenu → LocalScript called "MainMenuScript"`

**What this does:** Handles button clicks and sends messages to the server.

**Copy and paste this into Claude:**

```
Create a Roblox Lua LocalScript for the main menu UI.

Requirements:
1. This script runs on the CLIENT (player's computer)
2. Get references to UI elements:
   - LevelDisplay (TextLabel)
   - XPBar (ImageLabel or Frame for progress bar)
   - HuntButton (TextButton)
   - SettingsButton (TextButton)
   - SettingsPanel (Frame)

3. When HuntButton clicked:
   - Fire RemoteEvent "HuntEvent" to server
   - Show visual feedback (button changes color)
   - Play click sound (optional)

4. When SettingsButton clicked:
   - Show SettingsPanel
   - Play sound

5. Create RemoteEvent "HuntEvent" in MainMenu if not exists:
   local HuntEvent = game.StarterGui.MainMenu:WaitForChild("HuntEvent") or Instance.new("RemoteEvent")
   if not game.StarterGui.MainMenu:FindFirstChild("HuntEvent") then
       HuntEvent.Parent = game.StarterGui.MainMenu
   end

6. Connect HuntButton to fire HuntEvent:
   HuntButton.MouseButton1Click:Connect(function()
       HuntEvent:FireServer()
   end)

7. Add comments explaining each section

Output ONLY code, no explanation.
```

**After Claude generates it:**

1. Copy the code
2. In Roblox Studio, expand `StarterGui`
3. Right-click `MainMenu` (ScreenGui) → `LocalScript`
4. Name it "MainMenuScript"
5. Paste Claude's code

**Important:** 
- You MUST create the UI elements first (buttons, labels, etc.)
- Delete the default LocalScript that's in MainMenu

**Learning Tips:**
- `LocalScript` = runs on client side (player's computer) only
- `Script` = runs on server side (everyone sees it)
- `MouseButton1Click:Connect()` = fires when button is clicked
- `FireServer()` = sends message from client to server
- `:WaitForChild()` = waits for something to exist, then gets it

---

## 📝 PROMPT 6: UI Update Script (LocalScript)

**Location in Roblox:** `StarterGui → MainMenu → LocalScript called "UIUpdater"`

**What this does:** Updates the display (level, XP bar) when player data changes.

**Copy and paste this into Claude:**

```
Create a Roblox Lua LocalScript to update the main menu UI in real-time.

Requirements:
1. Get player's data from _G.PlayerStats[player.UserId]
2. Update LevelDisplay TextLabel with current level
3. Update XPBar with percentage filled:
   - Calculate: (CurrentXP / XP_PER_LEVEL) * 100
   - Set progress bar size based on percentage

4. Create a function UpdateUI():
   - Get current player
   - Get their stats from server
   - Update all displays
   - Make sure not to exceed 100%

5. Call UpdateUI() when:
   - Script first runs (initial display)
   - HuntEvent fires (after hunting)
   - Create RemoteEvent "UpdateUIEvent" and listen to it

6. Listen for UpdateUIEvent from server:
   local UpdateUIEvent = game.StarterGui.MainMenu:WaitForChild("UpdateUIEvent")
   UpdateUIEvent.OnClientEvent:Connect(function()
       UpdateUI()
   end)

7. Add error handling with pcall
8. Add comments

Output ONLY code, no explanation.
```

**After Claude generates it:**

1. Copy the code
2. Right-click `MainMenu` → `LocalScript`
3. Name it "UIUpdater"
4. Paste Claude's code

**Learning Tips:**
- LocalScript can access UI elements directly
- `OnClientEvent` = listening for server to send data
- Progress bar: multiply by 100 to get percentage
- Call UpdateUI() multiple times as data changes

---

## 📝 PROMPT 7: Settings Panel Script (LocalScript)

**Location in Roblox:** `StarterGui → MainMenu → SettingsPanel → LocalScript called "SettingsScript"`

**What this does:** Handles the settings menu (close button, reset data, exit game).

**Copy and paste this into Claude:**

```
Create a Roblox Lua LocalScript for the settings panel.

Requirements:
1. Get UI element references:
   - CloseButton
   - ResetButton
   - ExitButton
   - SettingsList (shows player info)

2. When CloseButton clicked:
   - Hide SettingsPanel
   - Animation: fade out over 0.3 seconds using TweenService

3. When ResetButton clicked:
   - Show confirmation dialog (use print or prompt)
   - If confirmed: tell server to reset data
   - Update UI after reset

4. When ExitButton clicked:
   - Kick the player using: game.Players.LocalPlayer:Kick("Thanks for playing!")

5. Display player info:
   - Player name
   - Current level
   - Total XP earned
   - Server player count
   - Uptime (optional)

6. Use TweenService for smooth animations:
   local TweenService = game:GetService("TweenService")
   local info = TweenInfo.new(0.3, Enum.EasingStyle.Quad)
   local tween = TweenService:Create(panel, info, {Transparency = 0})
   tween:Play()

7. Add comments

Output ONLY code, no explanation.
```

**After Claude generates it:**

1. Copy the code
2. Right-click `SettingsPanel` (Frame) → `LocalScript`
3. Name it "SettingsScript"
4. Paste Claude's code

**Learning Tips:**
- `TweenService` = smooth animations
- `TweenInfo.new(time, easing)` = animation settings
- `:Kick()` = removes player from game
- `game.Players.LocalPlayer` = the player using THIS computer

---

## 🎨 Design Implementation in Lua

After you get code from Claude, you need to SET the DESIGN properties in Lua:

### Example: Setting Button Colors
```lua
local HuntButton = game.StarterGui.MainMenu.HuntButton

-- Set colors (RGB values from Design Guide)
HuntButton.BackgroundColor3 = Color3.fromRGB(212, 175, 55)  -- Gold #D4AF37
HuntButton.TextColor3 = Color3.fromRGB(0, 0, 0)  -- Black text

-- Set size and position
HuntButton.Size = UDim2.new(0, 200, 0, 60)  -- 200x60 pixels
HuntButton.Position = UDim2.new(0.5, -100, 0.6, 0)  -- Center horizontally

-- Set text
HuntButton.Text = "HUNT"
HuntButton.Font = Enum.Font.GothamBold  -- Modern font
HuntButton.TextSize = 24

-- Set border
HuntButton.BorderSizePixel = 2
HuntButton.BorderColor3 = Color3.fromRGB(212, 175, 55)  -- Gold border
```

### Color Reference (Copy-Paste)
```lua
local COLORS = {
    DarkBG = Color3.fromRGB(15, 20, 25),      -- #0F1419
    SecondaryBG = Color3.fromRGB(26, 31, 46), -- #1A1F2E
    Gold = Color3.fromRGB(212, 175, 55),      -- #D4AF37
    LightText = Color3.fromRGB(232, 232, 232),-- #E8E8E8
    XPBar = Color3.fromRGB(52, 152, 219),     -- #3498DB
    Success = Color3.fromRGB(46, 204, 113),   -- #2ECC71
    Warning = Color3.fromRGB(231, 76, 60),    -- #E74C3C
    Hover = Color3.fromRGB(46, 62, 80)        -- #2E3E50
}
```

### Animations in Lua
```lua
local TweenService = game:GetService("TweenService")

-- Hover effect (scale up)
local hoverInfo = TweenInfo.new(
    0.2,  -- Duration: 0.2 seconds
    Enum.EasingStyle.Quad,
    Enum.EasingDirection.Out
)

HuntButton.MouseEnter:Connect(function()
    local tween = TweenService:Create(HuntButton, hoverInfo, {
        Size = UDim2.new(0, 210, 0, 63)  -- Slightly bigger
    })
    tween:Play()
end)

HuntButton.MouseLeave:Connect(function()
    local tween = TweenService:Create(HuntButton, hoverInfo, {
        Size = UDim2.new(0, 200, 0, 60)  -- Back to normal
    })
    tween:Play()
end)
```

---

## 📋 Order to Do Everything

**Step 1: Create UI Elements in Roblox Studio**
- [ ] Create ScreenGui called "MainMenu"
- [ ] Create TextLabel "LevelDisplay"
- [ ] Create Frame "XPBar"
- [ ] Create TextButton "HuntButton"
- [ ] Create TextButton "SettingsButton"
- [ ] Create Frame "SettingsPanel"
- [ ] Set basic colors and sizes

**Step 2: Generate Scripts with Claude**
- [ ] Prompt 1: Constants
- [ ] Prompt 2: PlayerData
- [ ] Prompt 3: PlayerManager
- [ ] Prompt 4: LevelingSystem
- [ ] Prompt 5: MainMenuScript
- [ ] Prompt 6: UIUpdater
- [ ] Prompt 7: SettingsScript

**Step 3: Apply Design in Lua**
- [ ] Set button colors and sizes
- [ ] Set fonts and text colors
- [ ] Add animations (hover effects)
- [ ] Style the panels

**Step 4: Test**
- [ ] Click Hunt button
- [ ] See XP increase
- [ ] See level up
- [ ] Open settings
- [ ] Save data

---

## 🐛 Common Errors & Fixes

**Error: "attempt to index nil with 'Level'"**
- Means the data isn't loaded yet
- Fix: Add wait before accessing: `wait(0.5)`

**Error: "attempt to call nil"**
- You're calling a function that doesn't exist
- Fix: Check module is required correctly: `local Constants = require(game.ServerScriptService.Constants)`

**Buttons not working**
- LocalScript might be in wrong place
- Fix: Make sure LocalScript is INSIDE StarterGui, not ServerScriptService

**UI not updating**
- RemoteEvent might not exist
- Fix: Create it manually in StarterGui.MainMenu

**Game crashes**
- Too many errors
- Fix: Check Output (View → Output) for red errors

---

## 💡 Tips for Learning

1. **Understand each prompt:** Read Claude's generated code and understand what it does
2. **Add comments:** Write comments explaining code you don't understand
3. **Test slowly:** Don't run everything at once, test each script individually
4. **Use print():** Add `print("Debug message")` to see if code is running
5. **Check Output:** Always look at Output panel for errors
6. **Ask Claude questions:** If you don't understand code, ask Claude to explain it

---

## 🔗 Useful Roblox API Reference

```lua
-- Get services
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")

-- Get current player (in LocalScript only)
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()

-- Get objects
local button = script.Parent.HuntButton
local label = script.Parent.LevelDisplay

-- Events
button.MouseButton1Click:Connect(function() end)  -- Button clicked
player.Leaving:Connect(function() end)  -- Player leaving
game.Players.PlayerAdded:Connect(function(player) end)  -- Player joined
```

---

Good luck! You've got this! 🚀

