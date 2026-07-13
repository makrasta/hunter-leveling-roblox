# Complete Design Implementation - Ready-to-Use Lua Code

## 🎨 Color Palette Reference

Copy this to the TOP of your LocalScripts:

```lua
-- Color definitions (from Design Guide)
local COLORS = {
    DarkBG = Color3.fromRGB(15, 20, 25),        -- #0F1419 (Main background)
    SecondaryBG = Color3.fromRGB(26, 31, 46),   -- #1A1F2E (Secondary background)
    Gold = Color3.fromRGB(212, 175, 55),        -- #D4AF37 (Accent/highlights)
    LightText = Color3.fromRGB(232, 232, 232),  -- #E8E8E8 (Main text)
    DarkText = Color3.fromRGB(150, 150, 150),   -- #969696 (Secondary text)
    XPBar = Color3.fromRGB(52, 152, 219),       -- #3498DB (XP bar color)
    Success = Color3.fromRGB(46, 204, 113),     -- #2ECC71 (Level up/success)
    Warning = Color3.fromRGB(231, 76, 60),      -- #E74C3C (Delete/reset)
    Hover = Color3.fromRGB(46, 62, 80),         -- #2E3E50 (Hover state)
}
```

---

## 🖼️ DESIGN IMPLEMENTATION 1: Main Menu Background

**Location:** `StarterGui → MainMenu` (ScreenGui properties)

**What it looks like:**
- Full screen dark blue background
- Slightly lighter gradient at bottom
- Professional, clean look

**Copy-paste this code into a LocalScript in MainMenu:**

```lua
local MainMenu = script.Parent  -- The ScreenGui

-- Set background
MainMenu.BackgroundColor3 = Color3.fromRGB(15, 20, 25)  -- Dark blue #0F1419
MainMenu.BackgroundTransparency = 0
MainMenu.Size = UDim2.new(1, 0, 1, 0)  -- Full screen
```

---

## 🎮 DESIGN IMPLEMENTATION 2: Game Title

**Location:** `StarterGui → MainMenu → TextLabel called "TitleLabel"`

**What it looks like:**
```
HUNTER LEVELING
(Gold text, large, centered at top, glowing effect)
```

**Setup in Roblox Studio:**
1. Right-click `MainMenu` → Insert Object → TextLabel
2. Name it "TitleLabel"
3. Run this code in MainMenuScript:

```lua
local TitleLabel = script.Parent:WaitForChild("TitleLabel")

-- Text content
TitleLabel.Text = "HUNTER LEVELING"
TitleLabel.Font = Enum.Font.GothamBold  -- Modern font
TitleLabel.TextSize = 48
TitleLabel.TextColor3 = Color3.fromRGB(212, 175, 55)  -- Gold

-- Position (centered at top)
TitleLabel.Size = UDim2.new(0, 400, 0, 80)
TitleLabel.Position = UDim2.new(0.5, -200, 0.05, 0)  -- Center horizontally, 5% from top

-- Background (transparent so you see the main background)
TitleLabel.BackgroundTransparency = 1

-- Add stroke/outline (glow effect)
TitleLabel.TextStrokeTransparency = 0.7
TitleLabel.TextStrokeColor3 = Color3.fromRGB(212, 175, 55)  -- Gold glow
```

---

## 📊 DESIGN IMPLEMENTATION 3: Stats Display Box

**Location:** `StarterGui → MainMenu → Frame called "StatsBox"`

**What it looks like:**
```
┌─────────────────────┐
│ Level: 45           │
│ XP: 250 / 500       │
└─────────────────────┘
```

**Setup Instructions:**
1. Right-click `MainMenu` → Insert Object → Frame
2. Name it "StatsBox"
3. Inside StatsBox, create 2 TextLabels: "LevelText" and "XPText"
4. Run this code:

```lua
local StatsBox = script.Parent:WaitForChild("StatsBox")
local LevelText = StatsBox:WaitForChild("LevelText")
local XPText = StatsBox:WaitForChild("XPText")

-- STATS BOX (Container)
StatsBox.BackgroundColor3 = Color3.fromRGB(26, 31, 46)  -- Dark gray #1A1F2E
StatsBox.BackgroundTransparency = 0
StatsBox.Size = UDim2.new(0, 350, 0, 100)
StatsBox.Position = UDim2.new(0.7, 0, 0.05, 0)  -- Top right

-- Stats Box Border
StatsBox.BorderSizePixel = 2
StatsBox.BorderColor3 = Color3.fromRGB(212, 175, 55)  -- Gold border

-- LEVEL TEXT
LevelText.Text = "Level: 45"
LevelText.Font = Enum.Font.GothamBold
LevelText.TextSize = 24
LevelText.TextColor3 = Color3.fromRGB(232, 232, 232)  -- Light text
LevelText.BackgroundTransparency = 1
LevelText.Size = UDim2.new(1, 0, 0.5, 0)
LevelText.Position = UDim2.new(0, 15, 0, 10)

-- XP TEXT
XPText.Text = "XP: 250 / 500"
XPText.Font = Enum.Font.GothamBold
XPText.TextSize = 18
XPText.TextColor3 = Color3.fromRGB(212, 175, 55)  -- Gold accent
XPText.BackgroundTransparency = 1
XPText.Size = UDim2.new(1, 0, 0.5, 0)
XPText.Position = UDim2.new(0, 15, 0.5, 0)

-- Function to update stats
local function UpdateStats(level, currentXP, maxXP)
    LevelText.Text = "Level: " .. level
    XPText.Text = "XP: " .. currentXP .. " / " .. maxXP
end

-- Example: Update to Level 50, 300 XP out of 500
UpdateStats(50, 300, 500)
```

---

## ⚡ DESIGN IMPLEMENTATION 4: XP Progress Bar

**Location:** `StarterGui → MainMenu → Frame called "XPBarContainer"`

**What it looks like:**
```
┌─────────────────────────────────────────┐
│░░░░░░░░░░░░░░░░░░░░░░░░░░░░��░░░░░░░░░░│
│ 250 / 500 XP                            │
└─────────────────────────────────────────┘
```

**Setup Instructions:**
1. Right-click `MainMenu` → Insert Object → Frame (name: "XPBarContainer")
2. Inside XPBarContainer, create another Frame (name: "XPBarFill")
3. Inside XPBarContainer, create TextLabel (name: "XPText")
4. Run this code:

```lua
local XPBarContainer = script.Parent:WaitForChild("XPBarContainer")
local XPBarFill = XPBarContainer:WaitForChild("XPBarFill")
local XPText = XPBarContainer:WaitForChild("XPText")

local TweenService = game:GetService("TweenService")

-- XP BAR CONTAINER (Background)
XPBarContainer.BackgroundColor3 = Color3.fromRGB(46, 62, 80)  -- Dark gray
XPBarContainer.BackgroundTransparency = 0
XPBarContainer.Size = UDim2.new(0, 800, 0, 40)
XPBarContainer.Position = UDim2.new(0.5, -400, 0.25, 0)  -- Centered
XPBarContainer.BorderSizePixel = 2
XPBarContainer.BorderColor3 = Color3.fromRGB(212, 175, 55)  -- Gold border

-- XP BAR FILL (The blue bar that grows)
XPBarFill.BackgroundColor3 = Color3.fromRGB(52, 152, 219)  -- Blue #3498DB
XPBarFill.BackgroundTransparency = 0
XPBarFill.Size = UDim2.new(0, 0, 1, 0)  -- Start empty
XPBarFill.Position = UDim2.new(0, 0, 0, 0)
XPBarFill.BorderSizePixel = 0

-- XP TEXT
XPText.Text = "0 / 500 XP"
XPText.Font = Enum.Font.GothamBold
XPText.TextSize = 16
XPText.TextColor3 = Color3.fromRGB(232, 232, 232)  -- Light text
XPText.BackgroundTransparency = 1
XPText.Size = UDim2.new(1, 0, 1, 0)

-- FUNCTION: Update XP bar smoothly
local function UpdateXPBar(currentXP, maxXP)
    -- Calculate percentage
    local percentage = math.min(currentXP / maxXP, 1.0)  -- Don't go over 100%
    
    -- Smooth animation
    local tweenInfo = TweenInfo.new(
        0.5,  -- Duration: 0.5 seconds
        Enum.EasingStyle.Quad,
        Enum.EasingDirection.Out
    )
    
    -- Animate the bar fill
    local tween = TweenService:Create(XPBarFill, tweenInfo, {
        Size = UDim2.new(percentage, 0, 1, 0)
    })
    tween:Play()
    
    -- Update text
    XPText.Text = currentXP .. " / " .. maxXP .. " XP"
end

-- Example: Set to 250 out of 500 XP
UpdateXPBar(250, 500)
```

---

## 🔘 DESIGN IMPLEMENTATION 5: HUNT Button

**Location:** `StarterGui → MainMenu → TextButton called "HuntButton"`

**What it looks like:**
```
┌──────────────┐
│   HUNT       │  ← Gold button, centered
└──────────────┘
```

**Setup Instructions:**
1. Right-click `MainMenu` → Insert Object → TextButton
2. Name it "HuntButton"
3. Run this code:

```lua
local HuntButton = script.Parent:WaitForChild("HuntButton")
local TweenService = game:GetService("TweenService")

-- BUTTON PROPERTIES
HuntButton.Text = "HUNT"
HuntButton.Font = Enum.Font.GothamBold
HuntButton.TextSize = 28
HuntButton.TextColor3 = Color3.fromRGB(0, 0, 0)  -- Black text

-- BUTTON APPEARANCE (Normal state)
HuntButton.BackgroundColor3 = Color3.fromRGB(212, 175, 55)  -- Gold #D4AF37
HuntButton.BackgroundTransparency = 0
HuntButton.Size = UDim2.new(0, 200, 0, 60)
HuntButton.Position = UDim2.new(0.5, -100, 0.55, 0)  -- Centered, middle of screen
HuntButton.BorderSizePixel = 2
HuntButton.BorderColor3 = Color3.fromRGB(212, 175, 55)  -- Gold border

-- HOVER ANIMATION
HuntButton.MouseEnter:Connect(function()
    local hoverInfo = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(HuntButton, hoverInfo, {
        BackgroundColor3 = Color3.fromRGB(232, 194, 65),  -- Lighter gold
        Size = UDim2.new(0, 210, 0, 63)  -- Slightly bigger
    })
    tween:Play()
end)

-- HOVER LEAVE ANIMATION
HuntButton.MouseLeave:Connect(function()
    local normalInfo = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(HuntButton, normalInfo, {
        BackgroundColor3 = Color3.fromRGB(212, 175, 55),  -- Back to gold
        Size = UDim2.new(0, 200, 0, 60)  -- Back to normal
    })
    tween:Play()
end)

-- CLICK ANIMATION
HuntButton.MouseButton1Down:Connect(function()
    local clickInfo = TweenInfo.new(0.1, Enum.EasingStyle.Quad, Enum.EasingDirection.In)
    local tween = TweenService:Create(HuntButton, clickInfo, {
        BackgroundColor3 = Color3.fromRGB(168, 130, 30),  -- Darker gold
        Size = UDim2.new(0, 190, 0, 57)  -- Slightly smaller
    })
    tween:Play()
end)

-- RELEASE ANIMATION
HuntButton.MouseButton1Up:Connect(function()
    local releaseInfo = TweenInfo.new(0.1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(HuntButton, releaseInfo, {
        BackgroundColor3 = Color3.fromRGB(212, 175, 55),  -- Back to gold
        Size = UDim2.new(0, 200, 0, 60)  -- Back to normal
    })
    tween:Play()
end)

-- CLICK ACTION
HuntButton.MouseButton1Click:Connect(function()
    print("Hunt button clicked!")
    -- Fire event to server to add XP
    local HuntEvent = script.Parent:WaitForChild("HuntEvent")
    HuntEvent:FireServer()
end)
```

---

## ⚙️ DESIGN IMPLEMENTATION 6: SETTINGS Button

**Location:** `StarterGui → MainMenu → TextButton called "SettingsButton"`

**What it looks like:**
```
┌──────────────┐
│  SETTINGS    │  ← Blue button, next to Hunt button
└──────────────┘
```

**Setup Instructions:**
1. Right-click `MainMenu` → Insert Object → TextButton
2. Name it "SettingsButton"
3. Run this code:

```lua
local SettingsButton = script.Parent:WaitForChild("SettingsButton")
local SettingsPanel = script.Parent:WaitForChild("SettingsPanel")
local TweenService = game:GetService("TweenService")

-- BUTTON PROPERTIES
SettingsButton.Text = "SETTINGS"
SettingsButton.Font = Enum.Font.GothamBold
SettingsButton.TextSize = 22
SettingsButton.TextColor3 = Color3.fromRGB(255, 255, 255)  -- White text

-- BUTTON APPEARANCE (Normal state)
SettingsButton.BackgroundColor3 = Color3.fromRGB(52, 152, 219)  -- Blue #3498DB
SettingsButton.BackgroundTransparency = 0
SettingsButton.Size = UDim2.new(0, 200, 0, 60)
SettingsButton.Position = UDim2.new(0.5, 110, 0.55, 0)  -- Right of Hunt button
SettingsButton.BorderSizePixel = 2
SettingsButton.BorderColor3 = Color3.fromRGB(52, 152, 219)  -- Blue border

-- HOVER ANIMATION
SettingsButton.MouseEnter:Connect(function()
    local hoverInfo = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(SettingsButton, hoverInfo, {
        BackgroundColor3 = Color3.fromRGB(93, 173, 226),  -- Lighter blue
        Size = UDim2.new(0, 210, 0, 63)
    })
    tween:Play()
end)

-- HOVER LEAVE ANIMATION
SettingsButton.MouseLeave:Connect(function()
    local normalInfo = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(SettingsButton, normalInfo, {
        BackgroundColor3 = Color3.fromRGB(52, 152, 219),
        Size = UDim2.new(0, 200, 0, 60)
    })
    tween:Play()
end)

-- CLICK ACTION
SettingsButton.MouseButton1Click:Connect(function()
    -- Show settings panel with animation
    SettingsPanel.Visible = true
    
    local slideInfo = TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(SettingsPanel, slideInfo, {
        Position = UDim2.new(0.5, -250, 0.5, -300)
    })
    tween:Play()
end)
```

---

## ⚙️ DESIGN IMPLEMENTATION 7: Settings Panel

**Location:** `StarterGui → MainMenu → Frame called "SettingsPanel"`

**What it looks like:**
```
┌────────────────────���─────────┐
│  SETTINGS PANEL          [X] │
├──────────────────────────────┤
│ Player: makrasta             │
│ Level: 45                    │
│ Total XP: 22,500             │
│ ─────────────────────────    │
│ Online: 1,234 Players        │
│ ┌────────────────────────┐   │
│ │  RESET DATA            │   │
│ └────────────────────────┘   │
│ ┌────────────────────────┐   │
│ │  EXIT GAME             │   │
│ └────────────────────────┘   │
└──────────────────────────────┘
```

**Setup Instructions:**
1. Right-click `MainMenu` → Insert Object → Frame
2. Name it "SettingsPanel"
3. Inside SettingsPanel, create:
   - TextLabel "Title" (for "SETTINGS PANEL")
   - TextButton "CloseButton" (X button)
   - TextLabel "PlayerInfo" (shows player details)
   - TextButton "ResetButton"
   - TextButton "ExitButton"
4. Run this code:

```lua
local SettingsPanel = script.Parent:WaitForChild("SettingsPanel")
local CloseButton = SettingsPanel:WaitForChild("CloseButton")
local Title = SettingsPanel:WaitForChild("Title")
local PlayerInfo = SettingsPanel:WaitForChild("PlayerInfo")
local ResetButton = SettingsPanel:WaitForChild("ResetButton")
local ExitButton = SettingsPanel:WaitForChild("ExitButton")

local TweenService = game:GetService("TweenService")

-- PANEL CONTAINER
SettingsPanel.BackgroundColor3 = Color3.fromRGB(26, 31, 46)  -- Dark gray #1A1F2E
SettingsPanel.BackgroundTransparency = 0
SettingsPanel.Size = UDim2.new(0, 500, 0, 600)
SettingsPanel.Position = UDim2.new(0.5, -250, 0.5, -300)  -- Centered
SettingsPanel.BorderSizePixel = 2
SettingsPanel.BorderColor3 = Color3.fromRGB(212, 175, 55)  -- Gold border
SettingsPanel.Visible = false  -- Hidden by default

-- TITLE
Title.Text = "SETTINGS"
Title.Font = Enum.Font.GothamBold
Title.TextSize = 28
Title.TextColor3 = Color3.fromRGB(232, 232, 232)
Title.BackgroundTransparency = 1
Title.Size = UDim2.new(1, -50, 0, 50)
Title.Position = UDim2.new(0, 20, 0, 10)

-- CLOSE BUTTON (X)
CloseButton.Text = "✕"
CloseButton.Font = Enum.Font.GothamBold
CloseButton.TextSize = 24
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.BackgroundColor3 = Color3.fromRGB(231, 76, 60)  -- Red #E74C3C
CloseButton.BackgroundTransparency = 0
CloseButton.Size = UDim2.new(0, 40, 0, 40)
CloseButton.Position = UDim2.new(1, -50, 0, 10)
CloseButton.BorderSizePixel = 0

-- Close button hover
CloseButton.MouseEnter:Connect(function()
    local hoverInfo = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(CloseButton, hoverInfo, {
        BackgroundColor3 = Color3.fromRGB(192, 57, 43)  -- Darker red
    })
    tween:Play()
end)

CloseButton.MouseLeave:Connect(function()
    local normalInfo = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(CloseButton, normalInfo, {
        BackgroundColor3 = Color3.fromRGB(231, 76, 60)  -- Red
    })
    tween:Play()
end)

-- CLOSE BUTTON ACTION
CloseButton.MouseButton1Click:Connect(function()
    local slideInfo = TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(SettingsPanel, slideInfo, {
        Position = UDim2.new(0.5, -250, 0.5, -500)  -- Slide out
    })
    tween:Play()
    tween.Completed:Connect(function()
        SettingsPanel.Visible = false
    end)
end)

-- PLAYER INFO TEXT
PlayerInfo.Text = "Player: makrasta\nLevel: 45\nTotal XP: 22,500\n\nOnline: 1,234 Players"
PlayerInfo.Font = Enum.Font.GothamBold
PlayerInfo.TextSize = 16
PlayerInfo.TextColor3 = Color3.fromRGB(232, 232, 232)
PlayerInfo.BackgroundColor3 = Color3.fromRGB(15, 20, 25)  -- Dark background
PlayerInfo.BackgroundTransparency = 0.5
PlayerInfo.Size = UDim2.new(0.9, 0, 0.3, 0)
PlayerInfo.Position = UDim2.new(0.05, 0, 0.08, 50)
PlayerInfo.TextWrapped = true
PlayerInfo.BorderSizePixel = 1
PlayerInfo.BorderColor3 = Color3.fromRGB(212, 175, 55)  -- Gold border

-- RESET BUTTON
ResetButton.Text = "RESET DATA"
ResetButton.Font = Enum.Font.GothamBold
ResetButton.TextSize = 18
ResetButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ResetButton.BackgroundColor3 = Color3.fromRGB(231, 76, 60)  -- Red
ResetButton.BackgroundTransparency = 0
ResetButton.Size = UDim2.new(0.9, 0, 0.12, 0)
ResetButton.Position = UDim2.new(0.05, 0, 0.45, 0)
ResetButton.BorderSizePixel = 1
ResetButton.BorderColor3 = Color3.fromRGB(231, 76, 60)

-- Reset button hover
ResetButton.MouseEnter:Connect(function()
    local hoverInfo = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(ResetButton, hoverInfo, {
        BackgroundColor3 = Color3.fromRGB(192, 57, 43),
        Size = UDim2.new(0.9, 0, 0.13, 0)
    })
    tween:Play()
end)

ResetButton.MouseLeave:Connect(function()
    local normalInfo = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(ResetButton, normalInfo, {
        BackgroundColor3 = Color3.fromRGB(231, 76, 60),
        Size = UDim2.new(0.9, 0, 0.12, 0)
    })
    tween:Play()
end)

-- EXIT BUTTON
ExitButton.Text = "EXIT GAME"
ExitButton.Font = Enum.Font.GothamBold
ExitButton.TextSize = 18
ExitButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ExitButton.BackgroundColor3 = Color3.fromRGB(149, 165, 166)  -- Gray
ExitButton.BackgroundTransparency = 0
ExitButton.Size = UDim2.new(0.9, 0, 0.12, 0)
ExitButton.Position = UDim2.new(0.05, 0, 0.60, 0)
ExitButton.BorderSizePixel = 1
ExitButton.BorderColor3 = Color3.fromRGB(149, 165, 166)

-- Exit button hover
ExitButton.MouseEnter:Connect(function()
    local hoverInfo = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(ExitButton, hoverInfo, {
        BackgroundColor3 = Color3.fromRGB(108, 117, 125),
        Size = UDim2.new(0.9, 0, 0.13, 0)
    })
    tween:Play()
end)

ExitButton.MouseLeave:Connect(function()
    local normalInfo = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
    local tween = TweenService:Create(ExitButton, normalInfo, {
        BackgroundColor3 = Color3.fromRGB(149, 165, 166),
        Size = UDim2.new(0.9, 0, 0.12, 0)
    })
    tween:Play()
end)

-- EXIT GAME ACTION
ExitButton.MouseButton1Click:Connect(function()
    game.Players.LocalPlayer:Kick("Thanks for playing!")
end)
```

---

## ✨ BONUS: Level Up Animation

**When player levels up, show this celebration animation:**

```lua
-- Add this to your UIUpdater script when level increases
local function LevelUpAnimation(newLevel)
    local LevelDisplay = script.Parent:WaitForChild("LevelDisplay")
    local TweenService = game:GetService("TweenService")
    
    -- Play level up animation
    local celebrateInfo = TweenInfo.new(
        0.5,
        Enum.EasingStyle.Back,
        Enum.EasingDirection.Out
    )
    
    -- Scale up and glow
    local tween = TweenService:Create(LevelDisplay, celebrateInfo, {
        Size = UDim2.new(0, 250, 0, 100),
        TextColor3 = Color3.fromRGB(46, 204, 113)  -- Green success color
    })
    tween:Play()
    
    -- Change text
    LevelDisplay.Text = "LEVEL UP!\n" .. newLevel
    
    -- Reset after animation
    tween.Completed:Connect(function()
        wait(1)
        LevelDisplay.TextColor3 = Color3.fromRGB(232, 232, 232)  -- Back to white
        LevelDisplay.Size = UDim2.new(0, 200, 0, 80)
        LevelDisplay.Text = "Level: " .. newLevel
    end)
end

-- Call it like this when level increases:
LevelUpAnimation(46)  -- Show "LEVEL UP! 46"
```

---

## 🎨 Complete Main Menu Setup (All-in-One)

If you want everything at once, create a single LocalScript in MainMenu with this:

```lua
-- COMPLETE MAIN MENU SETUP

local MainMenu = script.Parent
local TweenService = game:GetService("TweenService")

-- COLOR PALETTE
local COLORS = {
    DarkBG = Color3.fromRGB(15, 20, 25),
    SecondaryBG = Color3.fromRGB(26, 31, 46),
    Gold = Color3.fromRGB(212, 175, 55),
    LightText = Color3.fromRGB(232, 232, 232),
    DarkText = Color3.fromRGB(150, 150, 150),
    XPBar = Color3.fromRGB(52, 152, 219),
    Success = Color3.fromRGB(46, 204, 113),
    Warning = Color3.fromRGB(231, 76, 60),
}

-- SETUP MAIN BACKGROUND
MainMenu.BackgroundColor3 = COLORS.DarkBG
MainMenu.BackgroundTransparency = 0

-- Get or create UI elements
local function GetOrCreate(parent, name, className)
    local existing = parent:FindFirstChild(name)
    if existing then
        return existing
    end
    local new = Instance.new(className)
    new.Name = name
    new.Parent = parent
    return new
end

-- CREATE TITLE
local Title = GetOrCreate(MainMenu, "Title", "TextLabel")
Title.Text = "HUNTER LEVELING"
Title.Font = Enum.Font.GothamBold
Title.TextSize = 48
Title.TextColor3 = COLORS.Gold
Title.BackgroundTransparency = 1
Title.Size = UDim2.new(0, 400, 0, 80)
Title.Position = UDim2.new(0.5, -200, 0.05, 0)

-- CREATE HUNT BUTTON
local HuntButton = GetOrCreate(MainMenu, "HuntButton", "TextButton")
HuntButton.Text = "HUNT"
HuntButton.Font = Enum.Font.GothamBold
HuntButton.TextSize = 28
HuntButton.TextColor3 = Color3.fromRGB(0, 0, 0)
HuntButton.BackgroundColor3 = COLORS.Gold
HuntButton.Size = UDim2.new(0, 200, 0, 60)
HuntButton.Position = UDim2.new(0.5, -100, 0.55, 0)
HuntButton.BorderSizePixel = 2
HuntButton.BorderColor3 = COLORS.Gold

-- CREATE SETTINGS BUTTON
local SettingsButton = GetOrCreate(MainMenu, "SettingsButton", "TextButton")
SettingsButton.Text = "SETTINGS"
SettingsButton.Font = Enum.Font.GothamBold
SettingsButton.TextSize = 22
SettingsButton.TextColor3 = Color3.fromRGB(255, 255, 255)
SettingsButton.BackgroundColor3 = Color3.fromRGB(52, 152, 219)
SettingsButton.Size = UDim2.new(0, 200, 0, 60)
SettingsButton.Position = UDim2.new(0.5, 110, 0.55, 0)
SettingsButton.BorderSizePixel = 2
SettingsButton.BorderColor3 = Color3.fromRGB(52, 152, 219)

-- ADD ANIMATIONS
local function AddHoverEffect(button, normalColor, hoverColor)
    button.MouseEnter:Connect(function()
        local info = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
        local tween = TweenService:Create(button, info, {
            BackgroundColor3 = hoverColor,
            Size = UDim2.new(button.Size.X.Scale, button.Size.X.Offset + 10, button.Size.Y.Scale, button.Size.Y.Offset + 3)
        })
        tween:Play()
    end)
    
    button.MouseLeave:Connect(function()
        local info = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
        local tween = TweenService:Create(button, info, {
            BackgroundColor3 = normalColor,
            Size = UDim2.new(button.Size.X.Scale, button.Size.X.Offset - 10, button.Size.Y.Scale, button.Size.Y.Offset - 3)
        })
        tween:Play()
    end)
end

AddHoverEffect(HuntButton, COLORS.Gold, Color3.fromRGB(232, 194, 65))
AddHoverEffect(SettingsButton, Color3.fromRGB(52, 152, 219), Color3.fromRGB(93, 173, 226))

print("Main menu setup complete!")
```

---

## 📋 Implementation Checklist

- [ ] Background color set
- [ ] Title created and styled
- [ ] Hunt button created with hover effect
- [ ] Settings button created with hover effect
- [ ] Stats box created
- [ ] XP bar container and fill created
- [ ] XP bar update function working
- [ ] Settings panel created
- [ ] Close button (X) works
- [ ] Level up animation ready
- [ ] All animations smooth and working

Good luck! Your game is going to look professional! 🚀

