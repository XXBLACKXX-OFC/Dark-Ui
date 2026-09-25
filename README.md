# Dark Library Ui / Black Hub

A modern Roblox UI library with progressive rendering, customizable theme, and a full set of controls.

---

## Features

- Progressive loading (`Rendering`)
- Enable / disable tabs from a simple table
- Custom floating open/close button with circular logo
- Notifications
- Search (global + per page)
- Draggable main window and floating button
- Clean dark theme (white accents)

---

## Installation

```lua
local Library = loadstring(game:HttpGet("YOUR_RAW_UI_LIBRARY_URL"))()
```

Or load from a local file:

```lua
local Library = loadstring(readfile("Ui-Library.luau"))()
```

---

## Quick Start

```lua
local Library = loadstring(game:HttpGet("YOUR_RAW_UI_LIBRARY_URL"))()

local Window = Library:CreateWindow({
    Title = "Black Hub",
    Desc = "- Blox Fruits",
    Image = "rbxassetid://127598561744166",
    Rendering = "true" -- "true" = progressive | "false" = instant
})

local Tab = Window:AddTab("Main")
local Section = Tab:AddLeftGroupbox("General")

Section:AddToggle("MyToggle", {
    Title = "Enable Feature",
    Default = false,
    Callback = function(Value)
        print(Value)
    end
})
```

---

## CreateWindow

| Option | Type | Description |
|--------|------|-------------|
| `Title` | string | Main hub title |
| `Desc` | string | Subtitle next to the title |
| `Image` | string | Logo asset (`rbxassetid://...`) used on the floating button and header |
| `Rendering` | string / bool | `"true"` = load tabs/elements one by one (250ms). `"false"` = load everything instantly |

---

## Tabs System

Control which tabs appear using a simple table:

```lua
local Tabs = {
    TabCommunity = "true",
    TabShop = "true",
    TabMain = "false"  -- this tab will not be created
}

local function IsTab(name)
    local v = Tabs[name]
    return v == true or v == "true"
end

if IsTab("TabCommunity") then
    local TabCommunity = Window:AddTab("Community")
    -- ...
end
```

- `"true"` / `true` → tab is created  
- `"false"` / `false` → tab is skipped  

---

## Controls

### AddTab

```lua
local Tab = Window:AddTab("Main")
```

### AddLeftGroupbox / AddRightGroupbox / AddSection

```lua
local Section = Tab:AddLeftGroupbox("General")
-- or
local Section = Tab:AddRightGroupbox("Settings")
-- or
local Section = Tab:AddSection("Name")
```

---

### AddToggle

```lua
Section:AddToggle("ToggleId", {
    Title = "Option Name",
    Default = false,
    Callback = function(Value)
        print("Toggle:", Value)
    end
})
```

---

### AddButton

```lua
Section:AddButton({
    Title = "Click Me",
    Callback = function()
        print("Clicked")
    end
})
```

---

### AddSlider

```lua
Section:AddSlider({
    Title = "Value",
    Min = 100,
    Max = 1000,
    Default = 100,
    Precise = false,
    Callback = function(Value)
        print("Slider:", Value)
    end
})
```

| Option | Description |
|--------|-------------|
| `Min` | Minimum value |
| `Max` | Maximum value |
| `Default` | Starting value |
| `Precise` | Use decimal values when `true` |

---

### AddDropdown (Single)

```lua
Section:AddDropdown("DropdownId", {
    Title = "Select Island",
    Values = {"Island 1", "Island 2", "Island 3", "Island 4"},
    Default = "Island 1",
    Multi = false,
    Search = false,
    Callback = function(Value)
        print("Selected:", Value)
    end
})
```

### AddDropdown (Multi)

```lua
Section:AddDropdown("MultiId", {
    Title = "Select Island",
    Values = {"Island 1", "Island 2", "Island 3", "Island 4"},
    Default = {"Island 1"},
    Multi = true,
    Callback = function(Value)
        print("Selected list:", Value)
    end
})
```

| Option | Description |
|--------|-------------|
| `Values` | List of options |
| `Default` | String (single) or table (multi) |
| `Multi` | `true` = multi-select |
| `Search` | `true` = searchable dropdown |

---

### AddInput

```lua
Section:AddInput("InputId", {
    Title = "Write the He wants",
    Placeholder = "Type here...",
    Default = "",
    Callback = function(Text)
        print("Input:", Text)
    end
})
```

---

### AddKeyBind

```lua
Section:AddKeyBind({
    Title = "Menu Key",
    Default = Enum.KeyCode.RightShift,
    Mode = "Toggle", -- "Toggle" or "Hold"
    Callback = function(Value)
        print("Keybind:", Value)
    end
})
```

---

### AddLabel

```lua
Section:AddLabel("Status: true")
```

---

### AddParagraph

```lua
Section:AddParagraph("Example")
Section:AddParagraph("Example:", "Line 1\nLine 2\nLine 3")
```

---

### AddSeperator

```lua
Section:AddSeperator("Info")
```

---

### AddLinkInvite

Special control with banner, circular photo and a copy-link button.

```lua
Section:AddLinkInvite({
    Title = "Discord Invite",
    Banner = "100023306258643",      -- banner image id
    Photo = "80861671332748",       -- circular photo id
    Link = "https://discord.gg/example",
    Button = "Join Server",         -- button text (customizable)
    Callback = function(link)
        print("Copied:", link)
    end
})
```

| Option | Description |
|--------|-------------|
| `Banner` | Roblox image id for the banner |
| `Photo` | Roblox image id for the circular avatar |
| `Link` | Invite URL (copied on click) |
| `Button` | Button label (e.g. `"Join Server"`, `"Click To Copy"`) |

---

## Notifications

```lua
Library:Notify({
    Title = "Ready",
    Desc = "UI fully loaded!",
    Duration = 3
})
```

---

## Other Methods

```lua
Library:ToggleUI()   -- show / hide main UI
Library:DestroyUI()  -- destroy all library GUIs
```

Floating button (bottom-left) also toggles the UI and is draggable.

---

## Full Example Structure

```text
Window
├── Tab: Community
│   └── Section: Invite
│       └── AddLinkInvite (banner + photo + copy button)
│
├── Tab: Shop
│   └── Section: Buy
│       ├── Buttons: Buy Sword, Buy Fight Styles, Buy Guns, Buy Fruits
│       ├── Dropdown (single): Select Island
│       └── Toggle: Teleport to Island
│
└── Tab: Main
    └── Section: Teleport
        ├── Dropdown (multi): Select Island
        ├── Toggle: Teleport Island
        ├── Seperator: Info
        ├── Paragraphs
        ├── Label: Status: true
        ├── Slider: 100 – 1000
        └── Input: Write the He wants
```

---

## Theme

Default accent colors are white / light gray on a dark background.  
Logo and title are set via `CreateWindow` (`Image`, `Title`, `Desc`).

---

## License

Use freely for your hubs and scripts. Credit appreciated but not required.
