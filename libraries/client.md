---
description: Library used to get information about the client
---

# client

## Functions

### GetExtraInventorySlots

<details>

<summary><mark style="color:blue;">GetExtraInventorySlots</mark> ( )</summary>

Returns the number of extra inventory slots the user has

Return type: <mark style="color:yellow;">**integer**</mark>

Example:

```lua
print(client.GetExtraInventorySlots())
```

</details>

### IsFreeTrialAccount

<details>

<summary><mark style="color:blue;">IsFreeTrialAccount</mark> ( )</summary>

Returns whether the user is a free trial account

Which means it's not a premium account and cant speak in chat

Return type: <mark style="color:yellow;">**boolean**</mark>

Example:

```lua
if client.IsFreeTrialAccount() == true then
    print("Can't speak in chat :("
else
    print("Can speak in chat :)")
end
```

</details>

### HasCompetitiveAccess

<details>

<summary><mark style="color:blue;">HasCompetitiveAccess</mark> ( )</summary>

Returns whether the user can join matchmaking competitive matches

Return type: <mark style="color:yellow;">**boolean**</mark>

Example:

```lua
if client.HasCompetitiveAccess() == true then
    print("Woo hooo")
else
    print("Not woo hooo :(")
end
```

</details>

### IsInCoachesList <a href="#isincoacheslist" id="isincoacheslist"></a>

<details>

<summary><mark style="color:blue;">IsInCoachesList</mark> ( )</summary>

Returns whether the user is a coach or not

Return type: <mark style="color:yellow;">**boolean**</mark>

Example:

```lua
if client.IsInCoachesList() == true then
    print("Coach em")
else
    print("Nice")
end
```

</details>

### WorldToScreen <a href="#isincoacheslist" id="isincoacheslist"></a>

<details>

<summary><mark style="color:blue;">WorldToScreen</mark> (  worldPos: <a href="../classes/vector3.md"><mark style="color:red;"><strong>Vector3</strong></mark></a>, view: <a data-footnote-ref href="#user-content-fn-1"><mark style="color:red;"><strong>ViewSetup</strong></mark></a>? )</summary>

This translates 3D positions to 2D (screen position)

Return type: <mark style="color:yellow;">**{ \[**</mark>[<mark style="color:yellow;">**1**</mark>](#user-content-fn-2)[^2]<mark style="color:yellow;">**]: integer, \[**</mark>[<mark style="color:yellow;">**2**</mark>](#user-content-fn-3)[^3]<mark style="color:yellow;">**]: integer }**</mark> | this return type is a bit special, it returns a table with the x and y as respectively 1 and 2 index

Example:

<pre class="language-lua" data-title="Basic ESP"><code class="lang-lua">local font = draw.CreateFont("TF2 BUILD", 16, 1000)

local function ESP()
   --- if esc or console is open or we are not connected to a server, then dont draw the esp
   if engine:IsGameUIVisible() or engine:Con_IsVisible() or engine:GetServerIP() == "" then
      return
   end

   local players = entities.FindByClass("CTFPlayer")

   for _, player in pairs (players) do
      --- skip dormant and dead players
      if player:IsDormant() or not player:IsAlive() then goto continue end

      local position = player:GetAbsOrigin()
      local mins, maxs = player:GetMins(), player:GetMaxs()

      --- same as dividing by 2 the mins + maxs
      local center = position + ((mins + maxs) * 0.5)

      --- convert the 3D space to our screen's coordinates
<strong>      local screen_position = client.WorldToScreen(center)
</strong>
      --- when nil it means it is behind us so we dont need to draw them
      if screen_position == nil then goto continue end

      --- makes it easier for us to understand what each of the indexes is
      local x, y = screen_position[1], screen_position[2]
      local name = player:GetName()
      local color = player:GetTeamNumber() == 2 and {255, 0, 0, 255} or {0, 255, 255, 255}

      draw.SetFont(font)
      local text_width, text_height = draw.GetTextSize(name)

      --- centering it in the middle of the player
      x = x - math.floor(text_width * 0.5)
      y = y - math.floor(text_height * 0.5)

      draw.Color(table.unpack(color))
      draw.SetFont(font)
      draw.TextShadow(x, y, name)
      ::continue::
   end
end

callbacks.Register("Draw", ESP)
</code></pre>

</details>

### Command <a href="#isincoacheslist" id="isincoacheslist"></a>

<details>

<summary><mark style="color:blue;">Command</mark> ( cmd: <mark style="color:red;"><strong>string</strong></mark> )</summary>

Runs the command

Same thing as using it in the console, but automated

Example:

```lua
client.Command('say "hi dad!"')
```

</details>

### ChatSay <a href="#isincoacheslist" id="isincoacheslist"></a>

<details>

<summary><mark style="color:blue;">ChatSay</mark> ( message: <mark style="color:red;"><strong>string</strong></mark> )</summary>

Say text in the chat, not much else to explain :p&#x20;

Example:

```lua
client.ChatSay("hi mom!")
```

</details>

### ChatTeamSay <a href="#isincoacheslist" id="isincoacheslist"></a>

<details>

<summary><mark style="color:blue;">ChatTeamSay</mark> ( message: <mark style="color:red;"><strong>string</strong></mark> )</summary>

Say text in the team's chat, there is really not much else to say about it

Example:

```lua
client.ChatTeamSay("hi guys")
```

</details>

### GetPlayerNameByIndex <a href="#isincoacheslist" id="isincoacheslist"></a>

<details>

<summary><mark style="color:blue;">GetPlayerNameByIndex</mark> ( index: <mark style="color:red;"><strong>integer</strong></mark> )</summary>

Returns the player's name

Honestly its better to just get the player entity and get the name directly

Return type: <mark style="color:yellow;">**string**</mark>

Example:

```lua
print(client.GetPlayerNameByIndex(2))
```

</details>

### GetPlayerNameByUserID <a href="#getplayernamebyuserid-useridinteger" id="getplayernamebyuserid-useridinteger"></a>

<details>

<summary><mark style="color:blue;">GetPlayerNameByUserID</mark> ( userID: <mark style="color:red;"><strong>integer</strong></mark> )</summary>

Returns the player's name

Honestly its better to just get the player entity and get the name directly

Return type: <mark style="color:yellow;">**string**</mark>

Example:

```lua
client.GetPlayerNameByUserID(14276)
```

</details>

### GetPlayerInfo <a href="#isincoacheslist" id="isincoacheslist"></a>

<details>

<summary><mark style="color:blue;">GetPlayerInfo</mark> ( index: <mark style="color:red;"><strong>integer</strong></mark> )</summary>

Returns cool info about the player

Return type: {  Name: <mark style="color:yellow;">**string**</mark>, UserID: <mark style="color:yellow;">**number**</mark>, SteamID: <mark style="color:yellow;">**string**</mark>, IsBot: <mark style="color:yellow;">**boolean**</mark>, IsHLTV: <mark style="color:yellow;">**boolean**</mark> }

Example:

```lua
local info = client.GetPlayerInfo(clien.GetLocalPlayerIndex())
print(info.UserID)
```

</details>

### GetPlayerView <a href="#isincoacheslist" id="isincoacheslist"></a>

<details>

<summary><mark style="color:blue;">GetPlayerView</mark> ( )</summary>

Returns the player's renderview setup

Return type: [<mark style="color:yellow;">**ViewSetup**</mark>](#user-content-fn-4)[^4]

Example:

```lua
print(client.GetPlayerView().width)
```

</details>

### GetLocalPlayerIndex <a href="#isincoacheslist" id="isincoacheslist"></a>

<details>

<summary><mark style="color:blue;">GetLocalPlayerIndex</mark> ( )</summary>

This returns the local player's index

Return type: <mark style="color:yellow;">**integer**</mark>

Example:

```lua
local index = client.GetLocalPlayerIndex()
local player = entities.GetByIndex(index)

if player then
    print(player:GetName())
end
```

</details>

### GetConVar <a href="#isincoacheslist" id="isincoacheslist"></a>

<details>

<summary><mark style="color:blue;">GetConVar</mark> ( convar: <mark style="color:red;"><strong>string</strong></mark> )</summary>

This returns the convar's value

Return type: <mark style="color:yellow;">**integer**</mark>, <mark style="color:yellow;">**number**</mark>, <mark style="color:yellow;">**string**</mark>

Example:

```lua
local mat_wireframe = client.GetConVar("mat_wireframe")
print(mat_wireframe)
```

</details>

### SetConVar <a href="#isincoacheslist" id="isincoacheslist"></a>

<details>

<summary><mark style="color:blue;">SetConVar</mark> ( convar: <mark style="color:red;"><strong>string</strong></mark>, value:  <mark style="color:red;"><strong>integer</strong></mark> or <mark style="color:red;"><strong>number</strong></mark> or <mark style="color:red;"><strong>string</strong></mark> )</summary>

Changes the convar value to whatever you want

Example:

```lua
client.SetConVar("mat_wireframe", 1)
```

</details>

### RemoveConVarProtection <a href="#isincoacheslist" id="isincoacheslist"></a>

<details>

<summary><mark style="color:blue;">RemoveConVarProtection</mark> ( convar: <mark style="color:red;"><strong>string</strong></mark> )</summary>

Removes the convar protection, which means if i was hidden then it will appear&#x20;

For example, cl\_interpolate is protected and cant be changed in the console, but using this you can make it appear and be changable[^5]

```lua
client.RemoveConVarProtection("cl_interpolate")
```

</details>

### ChatPrintf <a href="#isincoacheslist" id="isincoacheslist"></a>

<details>

<summary><mark style="color:blue;">ChatPrintf</mark> ( message: <mark style="color:red;"><strong>string</strong></mark> )</summary>

This prints a message in chat, only you can see it

custom colors:

* `\x01` - White color
* `\x02` - Old color
* `\x03` - Player name color
* `\x04` - Location color
* `\x05` - Achievement color
* `\x06` - Black color
* `\x07` - Custom color, read from next 6 characters as HEX
* `\x08` - Custom color with alpha, read from next 8 characters as HEX

Example:

```lua
client.ChatPrintf("hi bro!")
```

</details>

### Localize <a href="#isincoacheslist" id="isincoacheslist"></a>

<details>

<summary><mark style="color:blue;">Localize</mark> (  key: <mark style="color:red;"><strong>string</strong></mark> )</summary>

Returns a localized string. The localizable strings usually start with a `#` character, but there are exceptions. Will return nil on failure.

Return type: <mark style="color:yellow;">**true**</mark>?

Example:

i apologize i dont have any example :(

</details>

[^1]: <mark style="color:red;">I still have to make this class page</mark>

[^2]: The X coordinate

[^3]: The Y coordinate

[^4]: Yet to be made the class page :(

[^5]: is this a real word?
