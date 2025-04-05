---
description: One of the most important classes in the game
---

# UserCmd

Represents a user (movement) command about to be sent to the server.

## Fields

Can be modified directly

### tick\_count

The current tick number (<mark style="color:yellow;">**integer**</mark>)

### sendpacket

Whether the command should be sent to the server or choked[^1] (<mark style="color:yellow;">**boolean**</mark>)

### command\_number

The current command number (<mark style="color:yellow;">**integer**</mark>)

### viewangles

Local player's view angles (<mark style="color:yellow;">**Vector3**</mark>)

### forwardmove

The forward movement of the local player (<mark style="color:yellow;">**number**</mark>)

### sidemove

The sideways movement of the local player (<mark style="color:yellow;">**number**</mark>)

### upmove

The upward movement of the player (<mark style="color:yellow;">**number**</mark>)

### buttons

The buttons that are pressed. Masked with bits from [IN\_\*](usercmd-constants.md) enum (<mark style="color:yellow;">**integer / bit mask**</mark>)

### impulse

The impulse command that was issue (<mark style="color:yellow;">**integer**</mark>)

### weaponselect

The weapon id that is selected (<mark style="color:yellow;">**integer**</mark>)

### weaponsubtype

The subtype of the weapon (<mark style="color:yellow;">**integer**</mark>) ???

### random\_seed

The random seed of the command (<mark style="color:yellow;">**integer**</mark>)

### mousedx / mousedy

The x / y delta of the mouse (<mark style="color:yellow;">**integer**</mark>)

### hasbeenpredicted

Whether the command has been predicted (<mark style="color:yellow;">**boolean**</mark>)

## Methods

### SetViewAngles

<details>

<summary><mark style="color:blue;">SetViewAngles</mark> ( pitch: <mark style="color:yellow;"><strong>number</strong></mark>, yaw: <mark style="color:yellow;"><strong>number</strong></mark>, roll: <mark style="color:yellow;"><strong>number</strong></mark> )</summary>

Sets the view angles of the player

Same thing as just changing the field [viewangles](./#viewangles)

Example:

```lua
local function RandomViewAngles(cmd)
    cmd:SetViewAngles(engine.RandomFloat(-89, 89), engine.RandomFloat(-180, 180), engine.RandomFloat(0, 90))
    --- both do the same thing
    --- cmd.viewangles = Vector3(engine.RandomFloat(-89, 89), engine.RandomFloat(-180, 180), engine.RandomFloat(0, 90))
end

callbacks.Register("CreateMove", RandomViewAngles)
```

</details>

### GetViewAngles

<details>

<summary><mark style="color:blue;">GetViewAngles</mark> ( )</summary>

Returns local player's view angles (can be different from the engine's viewangles)

Return type: <mark style="color:yellow;">**Vector3**</mark>

</details>

### SetSendPacket

<details>

<summary><mark style="color:blue;">SetSendPacket</mark> ( willsend: <mark style="color:yellow;"><strong>boolean</strong></mark> )</summary>

This is the same thing as [sendpacket field](./#sendpacket)

Changes wether the packet will be sent to the server or choked

Example:

```lua
local MAX_CHOKED_COMMANDS = 21
local function ChokePacket(cmd)
    if clientstate:GetChokedCommands() < MAX_CHOKED_COMMANDS then
        cmd:SetSendPacket(false)
        --- same thing as this v
        --- cmd.sendpacket = false
    end
end

callbacks.Register("CreateMove", ChokePacket)
```

</details>

### SetButtons

<details>

<summary><mark style="color:blue;">SetButtons</mark> (  buttons: <mark style="color:yellow;"><strong>integer</strong></mark> )</summary>

Changes the buttons pressed in the current tick

Same thing as [cmd.buttons](./#buttons)

Example:

```lua
local function PreventShooting(cmd)
    local buttons = cmd:GetButtons()
    cmd:SetButtons(buttons & ~IN_ATTACK)
end

callbacks.Register("CreateMove", PreventShooting)
```

</details>

### GetButtons

<details>

<summary><mark style="color:blue;">GetButtons</mark> ( )</summary>

Returns the buttons pressed in this tick ([cmd.buttons](./#buttons))

Return type: <mark style="color:yellow;">**integer**</mark>

</details>

### SetForwardMove

<details>

<summary><mark style="color:blue;">SetForwardMove</mark> (  factor: <mark style="color:yellow;"><strong>integer</strong></mark> )</summary>

Changes the forward move integer in the current tick

Same thing as [cmd.forwardmove](./#forwardmove)

Example:

```lua
local function PreventForward(cmd)
    cmd:SetForwardMove(0)
end

callbacks.Register("CreateMove", PreventForward)
```

</details>

### GetForwardMove

<details>

<summary><mark style="color:blue;">GetForwardMove</mark> ( )</summary>

Returns the forward move integer in this tick ([cmd.forwardmove](./#forwardmove))

Return type: <mark style="color:yellow;">**integer**</mark>

</details>

### SetSideMove

<details>

<summary><mark style="color:blue;">SetSideMove</mark> (  factor: <mark style="color:yellow;"><strong>integer</strong></mark> )</summary>

Changes the side move integer in the current tick

Same thing as [cmd.sidemove](./#sidemove)

Example:

```lua
local function PreventSideMovement(cmd)
    cmd:SetSideMove(0)
end

callbacks.Register("CreateMove", PreventSideMovement)
```

</details>

### GetSideMove

<details>

<summary><mark style="color:blue;">GetSideMove</mark> ( )</summary>

Returns the sideways move integer in this tick ([cmd.sidemove](./#sidemove))

Return type: <mark style="color:yellow;">**integer**</mark>

</details>

### SetUpMove

<details>

<summary><mark style="color:blue;">SetUpMove</mark> (  factor: <mark style="color:yellow;"><strong>integer</strong></mark> )</summary>

Changes the up move integer in the current tick

Same thing as [cmd.upmove](./#upmove)

Example:

```lua
local function PreventUpMovement(cmd)
    cmd:SetUpMove(0)
end

callbacks.Register("CreateMove", PreventUpMovement)
```

</details>

### GetUpMove

<details>

<summary><mark style="color:blue;">GetUpMove</mark> ( )</summary>

Returns the upwards movement integer in this tick ([cmd.upmove](./#upmove))

Return type: <mark style="color:yellow;">**integer**</mark>

</details>

[^1]: A choked packet means that it will be sent next time we are sending packets, so this current one wont go to the server
