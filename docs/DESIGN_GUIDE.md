# Hunter Leveling Game - Design Guide

## 🎨 Design Philosophy
- **Modern gaming aesthetic**
- **Hunter x Hunter inspired** (dark, sleek, professional)
- **Clean and minimal** (not cluttered)
- **Smooth animations** (modern feel)
- **Professional color scheme**

---

## 🎭 Color Palette

### Primary Colors
- **Deep Dark Blue:** `#0F1419` (Main background)
- **Hunter Gold:** `#D4AF37` (Accent, highlights, important text)
- **Dark Gray:** `#1A1F2E` (Secondary background)
- **Light Text:** `#E8E8E8` (Main text, readable)

### Secondary Colors
- **Success Green:** `#2ECC71` (Level up, achievements)
- **XP Blue:** `#3498DB` (XP bar color)
- **Warning Red:** `#E74C3C` (Alerts, errors)
- **Hover Highlight:** `#2E3E50` (Button hover state)

### Color Code Reference
```
Background:      #0F1419
Secondary BG:    #1A1F2E
Accent (Gold):   #D4AF37
Text (Light):    #E8E8E8
XP Bar:          #3498DB
Success:         #2ECC71
```

---

## 🔤 Typography

### Font Choices
- **Title Font:** "GothamBold" or "Orbitron" (futuristic, modern)
- **Body Font:** "Segoe UI" or "Roboto" (clean, readable)
- **Game Title:** Large, Bold, Gold color

### Font Sizes
- **Main Title (Hunter Leveling):** 48px, Bold, Gold
- **Level Display:** 36px, Bold, White
- **Button Text:** 20px, Bold, White
- **XP Text:** 16px, Normal, Light Gray
- **Settings Label:** 18px, Normal, Light Gray

---

## 📐 Main Menu Layout

```
┌─────────────────────────────────────────┐
│                                         │
│     HUNTER LEVELING                     │  ← Title (Gold, Large)
│                                         │
│  ┌─────────────────────────────────┐   │
│  │  Level: 45              XP: 250 │   │  ← Stats display (Top right)
│  └─────────────────────────────────┘   │
│                                         │
│  ┌─────────────────────────────────┐   │
│  │░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░│   │  ← XP Bar (Blue gradient)
│  │ 250 / 500 XP                    │   │
│  └─────────────────────────────────┘   │
│                                         │
│      ┌──────────────┐  ┌──────────────┐│
│      │ HUNT         │  │ SETTINGS     ││  ← Buttons (Large, Gold border)
│      └──────────────┘  └──────────────┘│
│                                         │
│  [HuntButton slides up on hover]        │
│  [SettingsButton slides right on hover] │
│                                         │
└─────────────────────────────────────────┘
```

---

## 🎯 Main Menu Components

### 1. **Background**
- Color: `#0F1419` (Deep dark blue)
- Texture: Slight gradient (slightly lighter at bottom)
- Size: Full screen (1920x1080 or scaled)

### 2. **Game Title**
- Text: "HUNTER LEVELING"
- Font: Orbitron, 48px, Bold
- Color: `#D4AF37` (Gold)
- Position: Top center, with padding
- Effect: Subtle glow effect (semi-transparent gold shadow)

### 3. **Stats Display Box**
- Background: `#1A1F2E` (Dark gray)
- Border: 2px `#D4AF37` (Gold)
- Border Radius: 8px
- Padding: 15px
- Position: Top right

**Inside Stats Box:**
```
Level: 45          XP Progress: 50%
(White text)       (Gold accent)
```

### 4. **XP Progress Bar**
- Background: `#2E3E50` (Dark gray)
- Fill Color: `#3498DB` (Blue gradient left to right)
- Border: 1px `#D4AF37` (Gold)
- Border Radius: 4px
- Height: 30px
- Width: 80% of screen
- Text Inside: "250 / 500 XP" (White, centered)

**Smooth Animation:**
- XP bar fills smoothly over 0.5 seconds
- Glowing effect when filling

### 5. **HUNT Button**
- Shape: Rectangle with rounded corners
- Background: `#D4AF37` (Gold)
- Text: "HUNT" (Bold, Black text, 24px)
- Border Radius: 8px
- Width: 200px, Height: 60px
- Position: Center, slightly below XP bar

**Hover State:**
- Background: Lighter gold `#E8C041`
- Scale up slightly (1.05x)
- Shadow appears beneath

**Click State:**
- Background: Darker gold `#B8941F`
- Scale down slightly (0.95x)

### 6. **SETTINGS Button**
- Shape: Rectangle with rounded corners
- Background: `#3498DB` (Blue)
- Text: "SETTINGS" (Bold, White, 24px)
- Border Radius: 8px
- Width: 200px, Height: 60px
- Position: Right of HUNT button, same row

**Hover State:**
- Background: Lighter blue `#5DADE2`
- Scale up slightly (1.05x)
- Shadow appears beneath

**Click State:**
- Background: Darker blue `#2E86C1`
- Scale down slightly (0.95x)

---

## ⚙️ Settings Panel Design

```
┌─────────────────────────────────────────┐
│         SETTINGS PANEL                  │  ← Title (White, Large)
│                                    [X]  │  ← Close button (Top right)
├─────────────────────────────────────────┤
│                                         │
│  Player: makrasta                       │  ← Player info
│  Level: 45                              │
│  Total XP: 22500                        │
│                                         │
│  ─────────────────────────────────      │  ← Divider
│                                         │
│  Server Status                          │
│  Players Online: 1,234                  │
│  Server Uptime: 48h 32m                 │
│                                         │
│  ─────────────────────────────────      │
│                                         │
│    ┌──────────────────────────────────┐ │
│    │ RESET DATA                       │ │  ← Buttons
│    └──────────────────────────────────┘ │
│                                         │
│    ┌──────────────────────────────────┐ │
│    │ EXIT GAME                        │ │
│    └──────────────────────────────────┘ │
│                                         │
└─────────────────────────────────────────┘
```

### Settings Panel Components

**Panel Container:**
- Background: `#1A1F2E` (Dark gray)
- Border: 2px `#D4AF37` (Gold)
- Border Radius: 10px
- Width: 500px, Height: 600px
- Position: Center of screen
- Shadow: Large shadow effect (professional depth)

**Close Button (X):**
- Size: 30x30px
- Background: `#E74C3C` (Red)
- Text: "X" (White, bold)
- Border Radius: 50% (circle)
- Position: Top right corner
- Hover: Darker red `#C0392B`

**Section Headers:**
- Color: `#D4AF37` (Gold)
- Font: Bold, 18px
- Underline: 1px gold line

**Text Content:**
- Color: `#E8E8E8` (Light)
- Font: Regular, 14px
- Line spacing: 1.5

**Dividers:**
- 1px line, `#D4AF37` (Gold)
- 40% opacity
- Margin: 20px top/bottom

**Reset Data Button:**
- Background: `#E74C3C` (Red)
- Text: "RESET DATA" (White, Bold)
- Width: 400px, Height: 50px
- Border Radius: 8px
- Hover: Lighter red, scale up

**Exit Game Button:**
- Background: `#95A5A6` (Gray)
- Text: "EXIT GAME" (White, Bold)
- Width: 400px, Height: 50px
- Border Radius: 8px
- Hover: Darker gray, scale up

---

## ✨ Animation & Effects

### Button Animations
```lua
-- Hover Animation (0.2 seconds)
Scale: 1.0 → 1.05
Shadow: None → Medium shadow

-- Click Animation (0.1 seconds)
Scale: 1.05 → 0.95
Background: Lighter → Darker

-- Release Animation (0.15 seconds)
Scale: 0.95 → 1.0
```

### XP Bar Animation
```lua
-- Fill Animation (0.5 seconds)
Width: Current% → New%
Glow effect: Pulsing gold outline

-- Level Up Animation (1 second)
Scale: 1.0 → 1.15 → 1.0
Color flash: Gold → Original
Sound: Level up sound (optional)
```

### Panel Slide In Animation
```lua
-- Settings Panel (0.3 seconds)
Opacity: 0 → 1.0
Position: Slide from right
```

---

## 🎮 UI States

### Button States

**Normal:**
- Opacity: 1.0
- Scale: 1.0
- Cursor: Default

**Hover:**
- Opacity: 0.9
- Scale: 1.05
- Shadow: Yes
- Cursor: Pointer hand

**Clicked:**
- Opacity: 0.8
- Scale: 0.95
- Color: Darker shade

**Disabled:**
- Opacity: 0.5
- Scale: 1.0
- Cursor: Not allowed

---

## 📱 Responsive Design

### For Different Screen Sizes

**Large (1920x1080):**
- Button size: 200x60px
- Font sizes: As listed
- Padding: 20px

**Medium (1280x720):**
- Scale all elements by 0.85x
- Button size: 170x51px
- Adjust padding: 15px

**Small (800x600):**
- Scale all elements by 0.7x
- Stack buttons vertically if needed
- Reduce padding: 10px

---

## 🎨 Visual Hierarchy

**Most Important → Least Important:**
1. HUNT Button (Gold, large, center)
2. Level Display (Large, prominent)
3. Game Title (Top, eye-catching)
4. XP Bar (Progress, informative)
5. SETTINGS Button (Secondary action)
6. Stats display (Reference info)

---

## 📦 Assets You Need to Create

### Images/Textures
- [ ] Background texture (gradient or pattern)
- [ ] Button backgrounds (or use simple colored rectangles)
- [ ] XP bar fill gradient
- [ ] Settings icon
- [ ] Hunter x Hunter themed icons (sword, trophy, etc.)
- [ ] Panel background texture

### Sounds (Optional)
- [ ] Button click sound (short, crisp)
- [ ] Level up sound (celebration sound)
- [ ] XP gain sound (subtle ping)

### Fonts to Download
- [ ] Orbitron (Title font) - Google Fonts
- [ ] Roboto (Body font) - Google Fonts

---

## 🛠️ Implementation Checklist

- [ ] Create background with correct colors
- [ ] Add Game Title text
- [ ] Create Stats Display box with border
- [ ] Create XP Progress bar
- [ ] Create HUNT button with hover effects
- [ ] Create SETTINGS button
- [ ] Design Settings Panel
- [ ] Add all animations (TweenService)
- [ ] Test on different screen sizes
- [ ] Add sound effects
- [ ] Polish and refine

---

## 💡 Design Tips

1. **Keep it Clean:** Don't overcrowd the UI
2. **Use Gold Sparingly:** It's the accent, not the main color
3. **Contrast:** Make sure text is readable on backgrounds
4. **Consistency:** Use the same colors throughout
5. **Smooth Animations:** Users love smooth, professional feel
6. **Feedback:** Every click should have visual feedback
7. **Testing:** Test on actual Roblox to see how it looks

---

## 🔗 HxH Design Inspiration

- Dark, mysterious atmosphere
- Gold/yellow accents (Hunter insignia style)
- Clean, professional UI
- Smooth, quality animations
- Minimal but impactful design

