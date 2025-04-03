---
description: Represents a material in source engine
---

# Material

For more information, see how [VMT files are made](https://developer.valvesoftware.com/wiki/VMT)

## Methods

<details>

<summary><mark style="color:blue;">GetName</mark></summary>

Returns the material name

Return type: <mark style="color:yellow;">**string**</mark>



Example

```lua
local material = materials.Find("white")
local name = material:GetName()
print(name)
```

</details>

<details>

<summary><mark style="color:blue;">GetTextureGroupName</mark></summary>

Returns group the material is part of

See the [texture groups](texture-groups.md) and use the values you want



Example:

```lua
local material = materials.Find("white")
local group = material:GetTextureGroupName()
print(group)
```

</details>

<details>

<summary><mark style="color:blue;">SetMaterialVarFlag</mark> ( flag: <mark style="color:red;"><strong>integer</strong></mark>, set: <mark style="color:red;"><strong>boolean</strong></mark> )</summary>

Change a material variable flag, see [Material Flags](https://developer.valvesoftware.com/wiki/Material_Flags) for a list of flags. The flag is the integer value of the flag enum, not the string name.

example:

```lua
local material = materials.Find("white")
material:SetMaterialVarFlag(E_MaterialFlag.MATERIAL_VAR_NO_DRAW, true)
```

</details>

<details>

<summary><mark style="color:blue;">SetShaderParam</mark> ( param: <mark style="color:red;"><strong>string</strong></mark>,  value: <mark style="color:red;"><strong>integer|number|Vector3|string</strong></mark>)</summary>

The value can be a integer, a number, a Vector3 or a string

Set a shader parameter, see [Shader Parameters](https://developer.valvesoftware.com/wiki/Category:List_of_Shader_Parameters) for a list of parameters. Supported values are



Example:

```lua
local material = materials.Find("white")
material:SetShaderParam("$color2", Vector3(1, 0, 0))
```

</details>

### Methods that dont work

<details>

<summary><mark style="color:blue;">ColorModulate</mark> ( red: <mark style="color:red;"><strong>number</strong></mark>, green: <mark style="color:red;"><strong>number</strong></mark>, blue: <mark style="color:red;"><strong>number</strong></mark> )</summary>

Modulate the color of the given material

<mark style="color:green;">**All the parameters should be in the \[0, 1] range**</mark>

</details>

<details>

<summary><mark style="color:blue;">AlphaModulate</mark> ( alpha: <mark style="color:red;"><strong>number</strong></mark> ) </summary>

Modulate transparency of material by given alpha value

<mark style="color:green;">Uses the \[0, 1] range</mark>

</details>

### Suggestions for lbox

Add a way to get materials properties, for example like this

<details>

<summary><mark style="color:blue;">GetShaderParam</mark> ( param: <mark style="color:red;"><strong>string</strong></mark> )</summary>

Can return one of them

* a Vector3 (for parameters that have 3 values like $color2)
* a number (for parameters that return a float)
* a integer (for parameters that return a int)
* a string (for parameters that return a string, like $basetexture)

```lua
local material = materials.Find("white")

--- returns: Vector3
local color2 = material:GetShaderParam("$color2")

--- returns: string ( for example, "vgui/white_additive" )
local basetexture = material:GetShaderParam("$basetexture")

--- returns: integer
local translucent = material:GetShaderParam("$translucent")

--- returns: number (alpha is in the [0, 1] range)
local alpha = material:GetShaderParam("$alpha")
```

</details>

