```markdown
# Scoot UI Library

A modern, feature-rich UI library for Roblox exploits. Built with performance and customization in mind.

## Installation

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/ILoveTacos123s/scootlib/refs/heads/main/scootuilib.lua"))()
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
