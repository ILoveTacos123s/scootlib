```markdown
# Scoot UI Library

A modern, feature-rich UI library for Roblox exploits. Built with performance and customization in mind.

## Installation

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/your-repo/scoot-ui/main.lua"))()
```

## Quick Start

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/your-repo/scoot-ui/main.lua"))()

-- Create main window
local Window = Library:Window({
    Logo = "77218680285262",   -- Roblox asset ID
    FadeTime = 0.3,
    Size = UDim2.new(0, 751, 0, 539)
})

-- Create watermark and keybind list (optional)
local Watermark = Library:Watermark("My Script")
local KeybindList = Library:KeybindList()

-- Add pages
local CombatPage = Window:Page({ Name = "Combat", SubPages = true })
local SettingsPage = Library:CreateSettingsPage(Window, Watermark, KeybindList)

-- Add a subpage
local WeaponsSub = CombatPage:SubPage({ Name = "Weapons", Columns = 2 })

-- Add a section
local MainSection = WeaponsSub:Section({ Name = "Main", Side = 1 })

-- Add components
MainSection:Toggle({
    Name = "Enabled",
    Flag = "EnableFeature",
    Default = true,
    Callback = function(value)
        print("Toggle:", value)
    end
})

MainSection:Slider({
    Name = "Speed",
    Flag = "SpeedValue",
    Min = 0,
    Max = 100,
    Default = 50,
    Suffix = "%",
    Callback = function(value)
        print("Slider:", value)
    end
})

local btn = MainSection:Button()
btn:Add("Click Me", function()
    print("Button clicked")
end)

MainSection:Dropdown({
    Name = "Mode",
    Flag = "ModeSelect",
    Items = {"Auto", "Semi", "Manual"},
    Default = "Auto",
    Callback = function(value)
        print("Dropdown:", value)
    end
})

MainSection:Textbox({
    Name = "Username",
    Flag = "UserName",
    Placeholder = "Enter name...",
    Callback = function(value)
        print("Textbox:", value)
    end
})

MainSection:Label("Status"):Colorpicker({
    Flag = "StatusColor",
    Default = Color3.fromRGB(255, 0, 0),
    Callback = function(color)
        print("Color changed:", color)
    end
})

MainSection:Label("Hotkey"):Keybind({
    Flag = "MyKeybind",
    Default = Enum.KeyCode.R,
    Mode = "Toggle", -- "Toggle", "Hold", or "Always"
    Callback = function(toggled)
        print("Keybind toggled:", toggled)
    end
})

-- Notifications
Library:Notification("Title", "Description here", 5)

-- Get flag values
local value = Library.Flags["EnableFeature"]
```

## Components & Methods

### Window
```lua
Window:Page({ Name, Columns, SubPages }) -- returns Page
Window:SetOpen(bool)
```

### Page
```lua
Page:SubPage({ Name, Columns }) -- returns SubPage
Page:Turn(bool)
```

### SubPage
Same as Page.

### Section
```lua
Section:Toggle({ Name, Flag, Default, Callback }) -- returns Toggle
Section:Button() -- returns Button
Section:Slider({ Name, Flag, Min, Max, Default, Suffix, Decimals, Callback }) -- returns Slider
Section:Dropdown({ Name, Flag, Items, Default, Multi, Callback }) -- returns Dropdown
Section:Label(Name) -- returns Label
Section:Textbox({ Name, Flag, Default, Placeholder, Numeric, Finished, Callback }) -- returns Textbox
Section:Searchbox({ Name, Flag, Items, Default, Multi, Callback }) -- returns Searchbox
```

### Toggle
```lua
Toggle:Get() -> boolean
Toggle:Set(bool)
Toggle:SetVisibility(bool)
Toggle:Colorpicker({ Flag, Default, Alpha, Callback }) -- returns Colorpicker
Toggle:Keybind({ Flag, Default, Mode, Callback }) -- returns Keybind
```

### Button
```lua
Button:Add(name, callback) -- creates a new button
Button:SetVisibility(bool)
```

### Slider
```lua
Slider:Get() -> number
Slider:Set(number)
Slider:SetVisibility(bool)
```

### Dropdown
```lua
Dropdown
