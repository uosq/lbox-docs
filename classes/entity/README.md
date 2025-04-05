---
description: >-
  Represents an entity in the game world. Make sure to not store entities long
  term, they can become invalid over time - their methods will return nil in
  that case.
---

# Entity

## This is not finished, there are so much methods that I decided to make the other stuff first

## Methods

### Generic

Able to use with most entities

<details>

<summary><mark style="color:blue;">IsValid</mark> ( )</summary>

* Returns whether the entity is valid. This is done automatically and all other functions will return nil if the entity is invalid.

- Return type: <mark style="color:yellow;">**boolean**</mark>

Example:

```lua
local me = entities.GetLocalPlayer()
if not me:IsValid() then
    print("localplayer is invalid!")
end
```

</details>

<details>

<summary><mark style="color:blue;">GetName</mark> ( )</summary>

* Returns the name string of the entity if its a player

- Return type: <mark style="color:yellow;">**string**</mark>?

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

print(me:GetName())
```

</details>

<details>

<summary><mark style="color:blue;">GetClass</mark> ( )</summary>

* Returns the class of the entity

- DONT BE CONFUSED WITH THE ACTUAL PLAYER's CLASS! (like spy, demoman, ... etc)

* this returns the entity's class (CTFPlayer, CObjectSentrygun, ... etc)

- Return type: <mark style="color:yellow;">**string**</mark>

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

print(me:GetClass())
```



</details>

<details>

<summary><mark style="color:blue;">GetIndex</mark> ( )</summary>

* Returns entity's index

- Return type: <mark style="color:yellow;">**integer**</mark>

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

print(me:GetIndex())
```

</details>

<details>

<summary><mark style="color:blue;">GetTeamNumber</mark> ( )</summary>

* Returns the entity's team number

- Return type: <mark style="color:yellow;">**integer**</mark>

Example:

{% code overflow="wrap" %}
```lua
local me = entities.GetLocalPlayer()
if not me then return end

local team = me:GetTeamNumber()
local text = team == 2 and "red team" or team == 3 and "blu team" or "spectator team"

print(text)
```
{% endcode %}

</details>

<details>

<summary><mark style="color:blue;">GetAbsOrigin</mark> ( )</summary>

* Returns the absolute position of the entity

- Return type: <mark style="color:yellow;">**Vector3**</mark>

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

print(me:GetAbsOrigin())
```

</details>

<details>

<summary><mark style="color:blue;">SetAbsOrigin</mark> ( origin: <mark style="color:red;">Vector3</mark> )</summary>

* Sets the absolute position of the entity

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

me:SetAbsOrigin(Vector3(200, 200, 200))
```

</details>

<details>

<summary><mark style="color:blue;">GetAbsAngles</mark> ( )</summary>

* Gets the absolute angles of the entity

- Return type: <mark style="color:yellow;">**Vector3**</mark>

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

local angle = me:GetAbsAngles()
print(angle)
```

</details>

<details>

<summary><mark style="color:blue;">SetAbsAngles</mark> ( angle: <mark style="color:red;"><strong>Vector3</strong></mark> )</summary>

* Sets the absolute angles of the entity

- <mark style="color:green;">FrameStageNotify might override this with whatever data gets received so you should use this in that callback</mark>

* This is really good for managing your own entities

Example:

{% code overflow="wrap" %}
```lua
local me = entities.GetLocalPlayer()
if not me then return end

local angles = Vector3(0, 0, 0)

local function FrameStageNotify(stage)
    --- we wait for the client to update the entity with whatever data was received so we can write after it
    if stage == E_ClientFrameStage.FRAME_NET_UPDATE_END then
        me:SetAbsAngles(angles)
    end
end

callbacks.Register("FrameStageNotify", FrameStageNotify)
```
{% endcode %}

</details>

<details>

<summary><mark style="color:blue;">GetHealth</mark> ( )</summary>

* Gets the health of the entity

- Return type: <mark style="color:yellow;">**integer**</mark>

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

local health = me:GetHealth()
print("Your health is " .. health)
```

</details>

<details>

<summary><mark style="color:blue;">GetMaxHealth</mark> ( )</summary>

* Gets the base MAX health of the entity (this is different from the MAX OVERHEALED health)

- Return type: <mark style="color:yellow;">**integer**</mark>

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

local maxhealth = me:GetMaxHealth()
print("Your max health is " .. maxhealth)
```

</details>

<details>

<summary><mark style="color:blue;">GetMins</mark> ( )</summary>

* This returns the mins of the entity

- You need to combine the return value of this with the origin

* Think of it like the position to the entity's bottom bounding box

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

local mins = me:GetMins()
local origin = me:GetAbsOrigin()
local pos = mins + origin
print(pos)
```

</details>

<details>

<summary><mark style="color:blue;">GetMaxs</mark> ( )</summary>

* This returns the maxs of the entity

- You need to combine the return value of this with the origin

* Think of it like the position to the entity's top bounding box

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

local maxs = me:GetMaxs()
local origin = me:GetAbsOrigin()
local top = maxs + origin
print(pos)
```

</details>

<details>

<summary><mark style="color:blue;">IsPlayer</mark> ( )</summary>

* Returns true if the entity is a player, or false if not

- Return type: <mark style="color:yellow;">**boolean**</mark>

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

print(me:IsPlayer()) --- yes
```

</details>

<details>

<summary><mark style="color:blue;">IsWeapon</mark> ( )</summary>

* Returns true if the entity is a weapon, and false if not

- Return type: <mark style="color:yellow;">**boolean**</mark>

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

print(me:IsWeapon())
```

</details>

<details>

<summary><mark style="color:blue;">IsAlive</mark> ( )</summary>

* Returns true if the entity is alive

- <mark style="color:green;">**THIS MIGHT GIVE A FALSE POSITIVE! Resupply cabinet, some other props, whatever building a engineer is holding in his arms IS ALIVE! Consider using GetHealth for them**</mark>

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

print(me:IsAlive())
```

</details>

<details>

<summary><mark style="color:blue;">EstimateAbsVelocity</mark> ( )</summary>

* Returns the estimated absolute velocity of the entity

- Return type: <mark style="color:yellow;">**Vector3**</mark>

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

print("Your velocity is " .. me:EstimateAbsVelocity())
```

</details>

<details>

<summary><mark style="color:blue;">GetMoveType</mark> ( )</summary>

* Returns the move type of the entity

- Learn more about it [here](move-types.md)

* Return type: <mark style="color:yellow;">**integer**</mark>

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

local movetype = me:GetMoveType()
print(movetype)
```

</details>

<details>

<summary><mark style="color:blue;">HitboxSurroundingBox</mark> ( )</summary>

* Returns the hitbox surrounding box of the entity as table of [Vector3](https://lmaobox.net/lua/Lua_Classes/Vector3) mins and maxs

- Return type: { \[1]: <mark style="color:red;">**Vector3**</mark>, \[2]: <mark style="color:red;">**Vector3**</mark> }

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

local box = me:HitboxSurroundingBox()
print(box)
```

</details>

<details>

<summary><mark style="color:blue;">EntitySpaceHitboxSurroundingBox</mark> ( )</summary>

* Returns the hitbox surrounding box of the entity in entity space as table of [Vector3](https://lmaobox.net/lua/Lua_Classes/Vector3) mins and maxs

- Its relative, like <mark style="color:blue;">GetMins</mark> and <mark style="color:blue;">GetMaxs</mark>

* Return type: { \[1]: <mark style="color:red;">**Vector3**</mark>, \[2]: <mark style="color:red;">**Vector3**</mark> }

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

local box = me:EntitySpaceHitboxSurroundingBox()
print(box)
```

</details>

<details>

<summary><mark style="color:blue;">SetupBones</mark> ( boneMask: <mark style="color:red;"><strong>integer</strong></mark>?, currentTime: <mark style="color:red;">number</mark>? )</summary>

* Both boneMask and currentTime are optional, you can just do it without changing any of them

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

local bones = me:SetupBones()
for i, v in pairs (bones) do
    print(i, v)
end
```

</details>

<details>

<summary><del>GetHitboxes ( currentTime: <mark style="color:red;"><strong>number</strong></mark>? )</del> Deprecated: use SetupBones instead!</summary>

* currentTime can be nil or just dont change it

- Returns world-transformed hitboxes of the entity as table of tables, each containing 2 entries of [Vector3](https://lmaobox.net/lua/Lua_Classes/Vector3): mins and maxs positions of each hitbox

Example table

| Hitbox Index | Mins & Maxs table                              |
| ------------ | ---------------------------------------------- |
| 1            | \[1]: Vector3(1, 2, 3), \[2]: Vector3(4, 5, 6) |
| 2            | \[1]: Vector3(7, 8, 9), \[2]: Vector3(0, 1, 2) |

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

local hitboxes = me:GetHitboxes()
for i, v in pairs (hitboxes) do
    print(i,v)
end
```

</details>

### Player methods

These are only available for Player entities (class CTFPlayer)

<details>

<summary><mark style="color:blue;">GetMaxBuffedHealth</mark> ( )</summary>

* Gets the max health a overhealed player can have, for example heavy will be 450

- Return type: <mark style="color:yellow;">**integer**</mark>

Example:

```lua
local me = entities.GetLocalPlayer()
if not me then return end

local maxbuffed = me:GetMaxBuffedHealth()
print("Your max overheal health is " .. maxbuffed)
```

</details>

### Attachments

These are usually entities attached to another entity, for example cosmetics from players

<details>

<summary><mark style="color:blue;">GetMoveChild</mark> ( )</summary>

* Returns the first entity attached to the entity

- Return type: <mark style="color:yellow;">**entity**</mark>?

</details>

<details>

<summary><mark style="color:blue;">GetMovePeer</mark> ( )</summary>

* Returns the next entity attached to the entity

- Return type: <mark style="color:yellow;">**entity**</mark>?

</details>

<details>

<summary>How to use both GetMoveChild and GetMovePeer</summary>

```lua
local me = entities.GetLocalPlayer()
if not me then return end

--- this is not the best way, but if it works it works
local moveChild = me:GetMoveChild()
--- until moveChild turns nil, this will run
while moveChild do
    --- do something here :p
    
    --- get the next attachment from the list
    moveChild = moveChild:GetMovePeer()
end
```

</details>

