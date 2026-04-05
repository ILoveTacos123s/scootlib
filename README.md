Installation
lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/your-repo/scoot-ui/main.lua"))()
Quick Start
lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/your-repo/scoot-ui/main.lua"))()

-- Create main window
local Window = Library:Window({
    Logo = "77218680285262",   -- Roblox asset ID
    FadeTime = 0.3,            -- fade animation time
    Size = UDim2.new(0, 751, 0, 539)
})

-- Create watermark and keybind list (optional)
local Watermark = Library:Watermark("My Script")
local KeybindList = Library:KeybindList()

-- Add pages
local CombatPage = Window:Page({ Name = "Combat", SubPages = true })
local SettingsPage = Library:CreateSettingsPage(Window, Watermark, KeybindList) -- built-in settings

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
Library:Notification("Title", "Description here", 5) -- duration in seconds

-- Get flag values
local value = Library.Flags["EnableFeature"]
Components & Methods
Window
lua
Window:Page({ Name, Columns, SubPages }) -- returns Page
Window:SetOpen(bool) -- show/hide window
Page
lua
Page:SubPage({ Name, Columns }) -- returns SubPage
Page:Turn(bool) -- activate page
SubPage
Same as Page (SubPage inherits Page methods).

Section
lua
Section:Toggle({ Name, Flag, Default, Callback }) -- returns Toggle
Section:Button() -- returns Button
Section:Slider({ Name, Flag, Min, Max, Default, Suffix, Decimals, Callback }) -- returns Slider
Section:Dropdown({ Name, Flag, Items, Default, Multi, Callback }) -- returns Dropdown
Section:Label(Name) -- returns Label
Section:Textbox({ Name, Flag, Default, Placeholder, Numeric, Finished, Callback }) -- returns Textbox
Section:Searchbox({ Name, Flag, Items, Default, Multi, Callback }) -- returns Searchbox
Toggle
lua
Toggle:Get() -> boolean
Toggle:Set(bool)
Toggle:SetVisibility(bool)
Toggle:Colorpicker({ Flag, Default, Alpha, Callback }) -- returns Colorpicker (attached inline)
Toggle:Keybind({ Flag, Default, Mode, Callback }) -- returns Keybind (attached inline)
Button
lua
Button:Add(name, callback) -- creates a new button (can call multiple times)
Button:SetVisibility(bool)
Slider
lua
Slider:Get() -> number
Slider:Set(number)
Slider:SetVisibility(bool)
Dropdown
lua
Dropdown:Get() -> string/table (depending on Multi)
Dropdown:Set(value) -- string for single, table for multi
Dropdown:Add(option) -- adds option to dropdown
Dropdown:Remove(option)
Dropdown:Refresh(list) -- replaces all options
Dropdown:SetVisibility(bool)
Label
lua
Label:SetText(string)
Label:SetVisibility(bool)
Label:Colorpicker({ Flag, Default, Alpha, Callback }) -- inline colorpicker
Label:Keybind({ Flag, Default, Mode, Callback }) -- inline keybind
Textbox
lua
Textbox:Get() -> string
Textbox:Set(string)
Textbox:SetVisibility(bool)
Searchbox
Same as Dropdown, but with built-in search input and scrolling list. Good for large option sets.

Keybind
lua
Keybind:Get() -> key, mode, toggled
Keybind:Set(key or table or mode) -- e.g., Enum.KeyCode.R, {Key = Enum.KeyCode.R, Mode = "Hold"}, "Toggle"
Keybind:SetMode("Toggle"/"Hold"/"Always")
Keybind:Press(bool) -- manually trigger press (optional)
Keybind:SetVisibility(bool)
Colorpicker
lua
Colorpicker:Set(color, alpha) -- color can be Color3, hex string, or {r,g,b,a}
Colorpicker:Get() -> Color3, alpha
Colorpicker:SetOpen(bool)
Colorpicker:Update() -- refresh display
Colorpicker:SlidePalette(input) -- manual control
Colorpicker:SlideHue(input)
Colorpicker:SlideAlpha(input)
Flags System
All components accept a Flag parameter. Flags are stored in Library.Flags and can be accessed anywhere.

lua
-- Get flag value
local enabled = Library.Flags["MyToggleFlag"]

-- Set flag programmatically (updates UI automatically)
Library.SetFlags["MyToggleFlag"](true)
Theming
You can change theme colors at runtime:

lua
Library.Theme.Accent = Color3.fromRGB(255, 0, 0)
Library:ChangeTheme("Accent", Color3.fromRGB(255, 0, 0))
Available theme keys:

Background

Border

Inline

Hovered Element

Page Background

Outline

Element

Gradient

Text

Text Stroke

Placeholder Text

Accent

Config System
lua
-- Save current flags to file
local json = Library:GetConfig()
writefile("config.json", json)

-- Load from file
Library:LoadConfig(readfile("config.json"))

-- Delete config
Library:DeleteConfig("config.json")
Built-in Settings page automatically handles configs via Library:CreateSettingsPage().

Additional Features
Notification
lua
Library:Notification(title, description, durationSeconds)
Watermark
lua
local wm = Library:Watermark("My Script")
wm:SetVisibility(true/false)
Keybind List
lua
local list = Library:KeybindList()
list:Add(keyName, description, mode) -- automatically managed by Keybind components
list:SetVisibility(bool)
Inventory Viewer
lua
local viewer = Library:InventoryViewer()
viewer:SetPlayer(player) -- sets avatar and title
viewer:SetPlayerHealth(100)
viewer:SetPlayerDistance(50)
viewer:AddTool("ToolName", "rbxassetid")
viewer:RemoveAllTools()
Global Events & Utilities
lua
Library:Connect(event, callback, name) -- safe connection with cleanup
Library:Disconnect(name)
Library:Thread(func) -- run in coroutine
Library:SafeCall(func, ...) -- pcall wrapper
Library:Round(number, decimals)
Library:IsMouseOverFrame(frame) -- check if mouse is over a UI element
Library:ToRich(text, color) -- convert text to rich text with color
Notes
The library automatically creates folders for configs and assets.

Images are downloaded and cached on first use.

Mobile touch events are automatically mapped.

The UI is fully draggable and resizable.

Use Library:Unload() to clean up all connections and destroy the UI.

Example Full Script
lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/your-repo/scoot-ui/main.lua"))()
local Window = Library:Window({ Logo = "77218680285262" })
local Watermark = Library:Watermark("Example")
local KeybindList = Library:KeybindList()

local MainPage = Window:Page({ Name = "Main", SubPages = true })
local CombatSub = MainPage:SubPage({ Name = "Combat", Columns = 2 })

local CombatSection = CombatSub:Section({ Name = "Weapon", Side = 1 })

CombatSection:Toggle({
    Name = "Aimbot",
    Flag = "AimbotEnabled",
    Default = false,
    Callback = function(v)
        print("Aimbot:", v)
    end
}):Keybind({
    Flag = "AimbotKey",
    Default = Enum.KeyCode.X,
    Mode = "Hold"
})

CombatSection:Slider({
    Name = "Smoothness",
    Flag = "AimSmooth",
    Min = 1,
    Max = 10,
    Default = 5,
    Callback = function(v)
        print("Smoothness:", v)
    end
})

CombatSection:Dropdown({
    Name = "Target",
    Flag = "AimTarget",
    Items = {"Head", "Chest", "Legs"},
    Default = "Head"
})

Library:Notification("Loaded", "UI ready", 3)
