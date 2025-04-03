---
description: >-
  Represents an entity in the game world. Make sure to not store entities long
  term, they can become invalid over time - their methods will return nil in
  that case.
---

# Entity



## Methods

<details>

<summary><mark style="color:blue;">IsValid</mark></summary>

Returns whether the entity is valid. This is done automatically and all other functions will return nil if the entity is invalid.

Return type: <mark style="color:yellow;">**boolean**</mark>

Example:

```lua
local player = entities.GetLocalPlayer()
if not player:IsValid() then print("localplayer is invalid!") end
```

</details>

<details>

<summary><mark style="color:blue;">GetName</mark></summary>

Returns the name string of the entity if its a player

Return type: <mark style="color:yellow;">**string**</mark>?

Example:

```lua
local player = entities.GetLocalPlayer()
if not player then return end

print(player:GetName())
```

</details>

<details>

<summary><mark style="color:blue;">GetClass</mark></summary>

Returns the class of the entity

DONT BE CONFUSED WITH THE ACTUAL PLAYER's CLASS! (like spy, demoman, ... etc)

this returns the entity's class (CTFPlayer, CObjectSentrygun, ... etc)

Return type: <mark style="color:yellow;">**string**</mark>

Example:

```lua
local player = entities.GetLocalPlayer()
if not player then return end

print(player:GetClass())
```



</details>

<details>

<summary><mark style="color:blue;">GetIndex</mark></summary>

Returns entity's index

Return type: <mark style="color:yellow;">**integer**</mark>

Example:

```lua
local player = entities.GetLocalPlayer()
if not player then return end

print(player:GetIndex())
```

</details>

<details>

<summary><mark style="color:blue;">GetTeamNumber</mark></summary>

Returns the entity's team number

Return type: <mark style="color:yellow;">**integer**</mark>

Example:

{% code overflow="wrap" %}
```lua
local player = entities.GetLocalPlayer()
if not player then return end

local team = player:GetTeamNumber()
local text = team == 2 and "red team" or team == 3 and "blu team" or "spectator team"

print(text)
```
{% endcode %}

</details>

<details>

<summary><mark style="color:blue;">GetAbsOrigin</mark></summary>

Returns the absolute position of the entity

Return type: <mark style="color:yellow;">**Vector3**</mark>

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

print(me:GetAbsOrigin())
```

</details>

<details>

<summary><mark style="color:blue;">SetAbsOrigin</mark> ( origin: <mark style="color:red;">Vector3</mark> )</summary>

Sets the absolute position of the entity

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

me:SetAbsOrigin(Vector3(200, 200, 200))
```

</details>
