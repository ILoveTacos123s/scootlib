````md
---

## 🧩 Components & Methods

### 🪟 Window

```lua
Window:Page({ Name, Columns, SubPages })
Window:SetOpen(bool)
````

---

### 📄 Page

```lua
Page:SubPage({ Name, Columns })
Page:Turn(bool)
```

---

### 📄 SubPage

Same as Page (inherits Page methods)

---

### 📦 Section

```lua
Section:Toggle({ Name, Flag, Default, Callback })
Section:Button()
Section:Slider({ Name, Flag, Min, Max, Default, Suffix, Decimals, Callback })
Section:Dropdown({ Name, Flag, Items, Default, Multi, Callback })
Section:Label(Name)
Section:Textbox({ Name, Flag, Default, Placeholder, Numeric, Finished, Callback })
Section:Searchbox({ Name, Flag, Items, Default, Multi, Callback })
```

---

### 🔘 Toggle

```lua
Toggle:Get() -> boolean
Toggle:Set(bool)
Toggle:SetVisibility(bool)

Toggle:Colorpicker({ Flag, Default, Alpha, Callback })
Toggle:Keybind({ Flag, Default, Mode, Callback })
```

---

### 🔘 Button

```lua
Button:Add(name, callback)
Button:SetVisibility(bool)
```

---

### 🎚️ Slider

```lua
Slider:Get() -> number
Slider:Set(number)
Slider:SetVisibility(bool)
```

---

### 📋 Dropdown

```lua
Dropdown:Get() -> string/table
Dropdown:Set(value)
Dropdown:Add(option)
Dropdown:Remove(option)
Dropdown:Refresh(list)
Dropdown:SetVisibility(bool)
```

---

### 🏷️ Label

```lua
Label:SetText(string)
Label:SetVisibility(bool)

Label:Colorpicker({ Flag, Default, Alpha, Callback })
Label:Keybind({ Flag, Default, Mode, Callback })
```

---

### ⌨️ Textbox

```lua
Textbox:Get() -> string
Textbox:Set(string)
Textbox:SetVisibility(bool)
```

---

### 🔍 Searchbox

Same as Dropdown, but with built-in search and scrolling.

---

### ⌨️ Keybind

```lua
Keybind:Get() -> key, mode, toggled
Keybind:Set(key or table or mode)
Keybind:SetMode("Toggle"/"Hold"/"Always")
Keybind:Press(bool)
Keybind:SetVisibility(bool)
```

---

### 🎨 Colorpicker

```lua
Colorpicker:Set(color, alpha)
Colorpicker:Get() -> Color3, alpha
Colorpicker:SetOpen(bool)
Colorpicker:Update()
Colorpicker:SlidePalette(input)
Colorpicker:SlideHue(input)
Colorpicker:SlideAlpha(input)
```

---

## 🏳️ Flags System

```lua
local enabled = Library.Flags["MyToggleFlag"]
Library.SetFlags["MyToggleFlag"](true)
```

---

## 🎨 Theming

```lua
Library.Theme.Accent = Color3.fromRGB(255, 0, 0)
Library:ChangeTheme("Accent", Color3.fromRGB(255, 0, 0))
```

**Available Keys:**

* Background
* Border
* Inline
* Hovered Element
* Page Background
* Outline
* Element
* Gradient
* Text
* Text Stroke
* Placeholder Text
* Accent

---

## 💾 Config System

```lua
local json = Library:GetConfig()
writefile("config.json", json)

Library:LoadConfig(readfile("config.json"))
Library:DeleteConfig("config.json")
```

---

## 🔔 Additional Features

### Notifications

```lua
Library:Notification(title, description, durationSeconds)
```

---

### Watermark

```lua
local wm = Library:Watermark("My Script")
wm:SetVisibility(true)
```

---

### Keybind List

```lua
local list = Library:KeybindList()
list:Add(keyName, description, mode)
list:SetVisibility(bool)
```

---

### Inventory Viewer

```lua
local viewer = Library:InventoryViewer()
viewer:SetPlayer(player)
viewer:SetPlayerHealth(100)
viewer:SetPlayerDistance(50)
viewer:AddTool("ToolName", "rbxassetid")
viewer:RemoveAllTools()
```

---

## 🧠 Utilities

```lua
Library:Connect(event, callback, name)
Library:Disconnect(name)
Library:Thread(func)
Library:SafeCall(func, ...)
Library:Round(number, decimals)
Library:IsMouseOverFrame(frame)
Library:ToRich(text, color)
```

---

## 📝 Notes

* Automatically creates folders for configs/assets
* Images are cached on first use
* Mobile supported
* Fully draggable & resizable UI
* Use `Library:Unload()` to clean up

---

## 📌 Full Example

```lua
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
```

---

```
```
