---
description: >-
  Represents the context in which a model is being drawn in the DrawModel
  callback.
---

# DrawModelContext

## Methods

### Generic

Methods that you can use with basically any DrawModel callback

<details>

<summary><mark style="color:blue;">Execute</mark></summary>

* Draw the model immediately in the current state. Can be called multiple times

- Useful for stacking materials

Example:

```lua
local vmt = 
[[
UnlitGeneric
{
    $basetexture "vgui/white_addiive"
}
]]
local material = materials.Create("cool material", vmt)

local function DrawModel(dme)
    dme:Execute() --- draw original model
    
    --- now we change it to whatever we want
    dme:ForcedMaterialOverride(material)
    dme:SetColorModulation(1, 1, 0)
    dme:SetAlphaModulation(0.5)
    dme:Execute() --- run our modified Execute call above the original call
    --- makes a pretty cool highlight effect :p
end

callbacks.Register("DrawModel", DrawModel)
```

</details>

<details>

<summary><mark style="color:blue;">DrawExtraPass</mark></summary>

* Basically Execute() with another name, just use Execute() instead

</details>

<details>

<summary><mark style="color:blue;">GetModelName</mark></summary>

* Gets the model's name

- Return type: <mark style="color:yellow;">**string**</mark>

Example:

```lua
local function DrawModel(dme)
    local modelname = dme:GetModelName()
    
    if string.find( modelname, "c_weapons" ) then
        dme:SetColorModulation ( 1, 0, 0 )
    end
end

callbacks.Register("DrawModel", DrawModel)
```

</details>

<details>

<summary><mark style="color:blue;">GetEntity</mark></summary>

* Gets the entity linked with the drawn model

- <mark style="color:green;">It can be nil</mark>

* <mark style="color:green;">**If its nil, it's most likely a dynamic prop like the resupply cabinet, orange cone in itemtest, viewmodel weapon, etc**</mark>

- Return type: <mark style="color:yellow;">**Entity**</mark>?

Example:

```lua
local function DrawModel(dme)
    local entity = dme:GetEntity()
    if not entity:IsPlayer() then return end
    
    local player_name = entity:GetName()
    print(player_name)
end

callbacks.Register("DrawModel", DrawModel)
```

</details>

<details>

<summary><mark style="color:blue;">DepthRange</mark> ( zNear: <mark style="color:red;"><strong>number</strong></mark>, zFar: <mark style="color:red;"><strong>number</strong></mark> )</summary>

* <mark style="color:green;">Needs to be set to ( 0, 1 ) after drawing the model! like this:</mark> DepthRange(0, 1)

Example:

```lua
local function DrawModel(dme)
    local entity = dme:GetEntity()
    if not entity or not entity:IsPlayer() then return end
    
    --- make the player models show behind walls (classic wallhack)
    dme:DepthRange(0, 0.2)
end

callbacks.Register("DrawModel", DrawModel)
```

</details>

<details>

<summary><mark style="color:blue;">SuppressEngineLighting</mark> ( supress: <mark style="color:red;"><strong>boolean</strong></mark> )</summary>

* Suppresses engine lighting when drawing the model

Example:

```lua
local function DrawModel(dme)
    local entity = dme:GetEntity()
    if not entity or not entity:IsPlayer() then return end
    dme:SuppressEngineLighting(true)
end
```

</details>

<details>

<summary><mark style="color:blue;">ForcedMaterialOverride</mark> ( material: <a href="material/"><mark style="color:red;"><strong>Material</strong></mark></a>? )</summary>

* Change the parameter `material` to apply a different material to the drawn model

- Make `material` be nil to change it to the original material

Example:

```lua
local vmt =
[[
UnlitGeneric
{
    $basetexture "vgui/white_additive"
}
]]

local material = materials.Create("lolo", vmt)

local function DrawModel(dme)
    dme:ForcedMaterialOverride(material)
end

callbacks.Register("DrawModel", DrawModel)
```

</details>

### Lmaobox's

Methods that might do something when Lmaobox is doing something

<details>

<summary><mark style="color:blue;">IsDrawingAntiAim</mark></summary>

* Returns true when Lmaobox is drawing the Anti Aim indicator in this DrawModel callback

- Returns false when Lmaobox is not drawing the Anti Aim indicator in this DrawModel callback

* Return type: <mark style="color:yellow;">**boolean**</mark>

Example:

```lua
local function DrawModel(dme)
    if dme:IsDrawingAntiAim() then
        print("drawing antiaim :0")
    end
end

callbacks.Register("DrawModel", DrawModel)
```

</details>

<details>

<summary><mark style="color:blue;">IsDrawingBackTrack</mark></summary>

* Returns true when Lmaobox is drawing the Backtrack indicator in this DrawModel callback

- Returns false when Lmaobox is not drawing the Backtrack indicator in this DrawModel callback

* Return type: <mark style="color:yellow;">**boolean**</mark>

Example:

```lua
local function DrawModel(dme)
    if dme:IsDrawingBackTrack() then
        print("drawing backtrack :3")
    end
end

callbacks.Register("DrawModel", DrawModel)
```

</details>

<details>

<summary><mark style="color:blue;">IsDrawingGlow</mark></summary>

* Returns true when Lmaobox is drawing the Glow indicator in this DrawModel callback

- Returns false when Lmaobox is not drawing the Glow indicator in this DrawModel callback

* Return type: <mark style="color:yellow;">**boolean**</mark>

Example:

```lua
local function DrawModel(dme)
    if dme:IsDrawingBackTrack() then
        print("drawing glow :D")
    end
end

callbacks.Register("DrawModel", DrawModel)
```

</details>

### RenderView

<details>

<summary><mark style="color:blue;">SetColorModulation</mark> ( red: <mark style="color:red;"><strong>integer</strong></mark>, green: <mark style="color:green;"><strong>integer</strong></mark>, blue: <mark style="color:blue;"><strong>integer</strong></mark> )</summary>

* You will probably use this

- Changes the color of the drawn model to whatever you want

* <mark style="color:green;">**red, green and blue parameters are all in the \[0, 1] range**</mark>

Example:

```lua
local red_team = 2

local function ChangePlayerColor(dme)
    local entity = dme:GetEntity()
    if not entity or not entity:IsPlayer() then return end
    
    if entity:GetTeamNumber() == red_team then
        dme:SetColorModulation ( 1, 0, 0 )
        else
        dme:SetColorModulation ( 0, 1, 1 )
    end
end

callbacks.Register("DrawModel", DrawModel)
```

</details>

<details>

<summary><mark style="color:blue;">SetAlphaModulation</mark> ( alpha: <mark style="color:red;"><strong>number</strong></mark> )</summary>

* Sets the alpha modulation of the model

- You will probably use this

* <mark style="color:green;">**alpha is in the \[0, 1] range**</mark>

Example:

```lua
local function MakePlayersTransparent(dme)
    local entity = dme:GetEntity()
    if not entity or not entity:IsPlayer() then return end
    
    render.OverrideDepthEnable ( true, true )
    dme:SetAlphaModulation ( 0.5 )
    dme:Execute()
    render.OverrideDepthEnable ( false, false )
end

callbacks.Register("DrawModel", MakePlayersTransparent)
```

</details>

### StudioRender

<details>

<summary><mark style="color:blue;">StudioSetColorModulation</mark> ( red: <mark style="color:red;"><strong>integer</strong></mark>, green: <mark style="color:green;"><strong>integer</strong></mark>, blue: <mark style="color:blue;"><strong>integer</strong></mark> )</summary>

* Changes the color of the drawn studio model to whatever you want

- <mark style="color:green;">**red, green and blue parameters are all in the \[0, 1] range**</mark>

Same thing as [SetColorModulation](drawmodelcontext.md#setcolormodulation-red-integer-green-integer-blue-integer)

</details>

<details>

<summary><mark style="color:blue;">StudioSetAlphaModulation</mark> ( alpha: <mark style="color:red;"><strong>number</strong></mark> )</summary>

* Sets the alpha modulation of the studio model

- <mark style="color:green;">**alpha is in the \[0, 1] range**</mark>

Same thing as [SetAlphaModulation](drawmodelcontext.md#setalphamodulation-alpha-number)

</details>

### Examples

<details>

<summary>Basic chams</summary>

```lua
local vmt = 
[[
UnlitGeneric
{
    $basetexture "vgui/white_addiive"
}
]]
local material = materials.Create("not chams", vmt)
local red_team = 2

local red_color = {255, 0, 0}
local blu_color = {0, 255, 255}

--- the function DrawModel callback will call when it wants to draw a model
local function DrawChams(dme)
    local entity = dme:GetEntity()
    if not entity or not entity:IsPlayer() then return end
    
    --- cool little trick that is basically a IF statement on a variable
    local color = entity:GetTeamNumber() == red_team and red_color or blu_color
    dme:ForcedMaterialOverride(material)

    --- we divide by 255 because we need them to be in the [0, 1] range
    dme:SetColorModulation( color[1]/255, color[2]/255, color[3]/255 )
    
    --- we dont need to run dme:Execute() because we are already changing
    --- the drawn material
    --- unless you want 2 Execute calls for the same thing :p
    --- as this callback is already 1 Execute call
end

callbacks.Register("DrawModel", "my cool chams", DrawChams)
```

</details>
