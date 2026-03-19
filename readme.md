# Compkiller UI Library

**A modern, clean, and powerful UI library for Roblox scripts.**

Created by **4lpaca**  
Press **Left Alt** to open/close the UI (default keybind).

---

## ✨ Features

- Sleek modern Roblox UI with smooth animations
- Built-in **Config System** (auto-save/load with `Flag`)
- Notification system
- Dynamic **Watermark** with live time/date
- Multiple tab layouts:
  - Normal (Double sections)
  - Single tab
  - Container tabs (nested tabs)
- Full theme system (6 built-in + custom colors)
- Risky feature highlighting
- Responsive elements (sub-options, keybinds, helpers)
- Loading screen
- Easy-to-use API

---

## 📥 Installation

```luau
local Compkiller = loadstring(game:HttpGet("https://raw.githubusercontent.com/4lpaca-pin/CompKiller/refs/heads/main/src/source.luau"))()
```
## 🚀 Quick Start Example

```luau
local Compkiller = loadstring(game:HttpGet("https://raw.githubusercontent.com/4lpaca-pin/CompKiller/refs/heads/main/src/source.luau"))()

-- Notification System
local Notifier = Compkiller.newNotify()

-- Config Manager
local ConfigManager = Compkiller:ConfigManager({
    Directory = "Compkiller-UI",
    Config = "MyConfig"
})

-- Loader
Compkiller:Loader("rbxassetid://120245531583106", 2.5).yield()

-- Main Window
local Window = Compkiller.new({
    Name = "COMPKILLER",
    Keybind = "LeftAlt",
    Logo = "rbxassetid://120245531583106",
    Scale = Compkiller.Scale.Window, -- or leave blank for auto-scale
    TextSize = 15,
})

-- Notification
Notifier.new({
    Title = "Notification",
    Content = "Thank you for using Compkiller UI!",
    Duration = 10,
    Icon = "rbxassetid://120245531583106"
})

-- Watermark
local Watermark = Window:Watermark()
Watermark:AddText({ Icon = "user", Text = "4lpaca" })
Watermark:AddText({ Icon = "clock", Text = Compkiller:GetDate() })

local TimeLabel = Watermark:AddText({ Icon = "timer", Text = "TIME" })
task.spawn(function()
    while true do
        task.wait()
        TimeLabel:SetText(Compkiller:GetTimeNow())
    end
end)

Watermark:AddText({ Icon = "server", Text = Compkiller.Version })

-- Example Tab
Window:DrawCategory({ Name = "Example" })
local Tab = Window:DrawTab({
    Name = "Example Tab",
    Icon = "apple",
    EnableScrolling = true
})

local Section = Tab:DrawSection({
    Name = "Section",
    Position = "left"
})

Section:AddToggle({
    Name = "Toggle",
    Flag = "Toggle_Example",
    Default = false,
    Callback = print,
})
```
---
# 📖 Full API Documentation

## 1. Notifications
```luau
local Notifier = Compkiller.newNotify()

Notifier.new({
    Title = "Title",
    Content = "Message",
    Duration = 5,           -- seconds
    Icon = "rbxassetid://..."
})
```
## 2. Config Manager
```luau
local ConfigManager = Compkiller:ConfigManager({
    Directory = "FolderName",
    Config = "DefaultConfigName"
})
```
## 3. Loader

```luau
Compkiller:Loader("rbxassetid://...", 2.5).yield() -- shows loading animation
```

## 4. Window Creation

```luau
local Window = Compkiller.new({
    Name = "Window Title",
    Keybind = "LeftAlt",
    Logo = "rbxassetid://...",
    Scale = Compkiller.Scale.Window, -- optional
    TextSize = 15,
})
```

## 5. Watermark

```lua
local wm = Window:Watermark()
wm:AddText({ Icon = "icon-name", Text = "value" })
-- Use .SetText() on returned object for live updates
```

## 6. Tabs & Sections

```lua
local Tab = Window:DrawTab({
    Name = "Tab Name",
    Icon = "lucide-icon",      -- e.g. "apple", "settings-3"
    EnableScrolling = true,
    Type = "Double"            -- "Double" (default) or "Single"
})

local Section = Tab:DrawSection({
    Name = "Section Title",
    Position = "left"          -- or "right"
})
```
## Container Tabs:
```lua
local Container = Window:DrawContainerTab({ Name = "Tools", Icon = "contact" })
local SubTab = Container:DrawTab({ Name = "Sub Tab", Type = "Double" })
```

## 7. UI Elements (add to any Section)
## Toggle

```lua
Section:AddToggle({
    Name = "Toggle",
    Flag = "MyToggle",      -- saves to config
    Default = false,
    Risky = false,          -- red highlight
    Callback = function(v) end
})
```
## Keybind
```lua
Section:AddKeybind({
    Name = "Keybind",
    Default = "LeftAlt",
    Flag = "KeyFlag",
    Callback = function() end
})
```
## Slider
```lua
Section:AddSlider({
    Name = "Slider",
    Min = 0,
    Max = 100,
    Default = 50,
    Round = 0,
    Flag = "SliderFlag",
    Callback = function(v) end
})
```
## ColorPicker
```lua
Section:AddColorPicker({
    Name = "Color",
    Default = Color3.fromRGB(0, 255, 140),
    Flag = "ColorFlag",
    Callback = function(c) end
})
```
## Dropdown
```lua
Section:AddDropdown({
    Name = "Dropdown",
    Default = "Head",           -- string or table (Multi)
    Multi = false,
    Flag = "DropdownFlag",
    Values = {"Head", "Body", "Arms", "Legs"},
    Callback = function(v) end
})
```
## Button 
```lua
Section:AddButton({
    Name = "Click Me",
    Callback = function() print("Clicked!") end
})
```
## Paragraph
```lua
Section:AddParagraph({
    Title = "Title",
    Content = "Multi-line text\nSupports \\n"
})
```
## TextBox
```lua
Section:AddTextBox({
    Name = "TextBox",
    Placeholder = "Type here...",
    Default = "Hello",
    Numeric = false, -- when true, Callback receives a number (digits + decimal only)
    Callback = function(value) end
})
```

## 8. Themes & Colors
```lua
-- Built-in themes
Compkiller:SetTheme("Default")
Compkiller:SetTheme("Dark Green")
Compkiller:SetTheme("Dark Blue")
Compkiller:SetTheme("Purple Rose")
Compkiller:SetTheme("Skeet")
Compkiller:SetTheme("Midnight")

-- Custom colors
Compkiller.Colors.Highlight = Color3.fromRGB(255, 0, 100)
Compkiller:RefreshCurrentColor()

-- Get current theme
print(Compkiller:GetTheme()) -- returns table (copy to clipboard with button)

-- Get version
print(Compkiller:GetVersion()) -- returns version string e.g. "2.7"
```

## 9. Config Tab (Recommended)
```lua
local ConfigUI = Window:DrawConfig({
    Name = "Config",
    Icon = "folder",
    Config = ConfigManager
})
ConfigUI:Init()
```

# 📌 Important Notes
- Flag = Requires config saving
- Element without flag will not save
- Risky = True makes the element red (dangerous options)
- Type = "Single" removes left/right section
- All colors are live-updatable with :RefreshCurrentColor()

## Changelog
- 2026-03-19: Improved `TextBox` focus/hover visuals, added `Numeric` documentation (and fixed legacy `Numberic` support), and added a pressed-state animation to `Button`.

# Credits

Developer: 4lpaca
Modified: ziozindex
Made with ❤️ for the Roblox scripting community.
