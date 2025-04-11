---
description: >-
  Library that helps making useful callbacks so your script can react to most
  things
---

# callbacks

## Callbacks

They aren't functions, all the callback's parameters are passed to the actual function that you register

Callbacks can be called in different situations, for example CreateMove gets called \~67 times per second, but Draw gets called every frame. Some might not even be called at all like ServerCmdKeyValue that only runs when you use a item like noisemaker or buy a upgrade in MvM.

<details>

<summary>Unload ( )</summary>

This is called when the script is being unloaded, either by the lmaobox menu or by another script

Called before actually being unloaded, so you can still use your variables

Example:

```lua
local junkvar1 = 1239842389047
local junkvar2 = 12842389174

local function Unload()
    print("Script is being unloaded!")
    junkvar1 = nil
    junkvar2 = nil
    collectgarbage("collect")
end

callbacks.Register("Unload", Unload)
```

</details>

<details>

<summary>CreateMove ( cmd: <a href="../classes/usercmd/"><mark style="color:purple;"><strong>UserCmd</strong></mark></a> )</summary>

Useful for processing & changing input and movement

Example:

<pre class="language-lua"><code class="lang-lua">local function IsShooting(cmd)
    if (cmd.buttons &#x26; IN_ATTACK) ~= 0 then
        --- local player is shooting
        --- do something :3
    end
end

<strong>callbacks.Register("CreateMove", IsShooting)
</strong></code></pre>

</details>

<details>

<summary>Draw ( )</summary>

Useful for drawing stuff to the screen

You might want to check the draw library

Example:

<pre class="language-lua"><code class="lang-lua">local font = draw.CreateFont("TF2 BUILD", 12, 1000)

local function DrawText()
    local x, y = 50, 20
    draw.SetFont(font)
    draw.Color(255, 255, 255, 255)
    draw.TextShadow(x, y, "hi mom!")
end

<strong>callbacks.Register("Draw", DrawText)
</strong></code></pre>

</details>

<details>

<summary>DrawModel ( context: <a href="../classes/drawmodelcontext.md"><mark style="color:purple;"><strong>DrawModelContext</strong></mark></a> )</summary>

Useful to change how the models are drawn

Example:

```lua
local function MakeModelsRed(context)
    local entity = context:GetEntity()
    if not entity or not entity:IsPlayer() then return end
    
    context:SetColorModulation(1, 0, 0)
end

callbacks.Register("DrawModel", MakeModelsRed)
```

</details>

<details>

<summary>DrawStaticProps ( info: <a data-footnote-ref href="#user-content-fn-1"><mark style="color:purple;"><strong>StaticPropRenderInfo</strong></mark></a> )</summary>

This is useful to change how static props look

Although we have exactly only half the functions working (there are only 2 of them)

And the other half that works, im not sure if it really works :p

Example:

<pre class="language-lua"><code class="lang-lua">local function MakePropsBlue(info)
    info:StudioSetColorModulation(1, 0, 0)
end

<strong>callbacks.Register("DrawStaticProps", MakePropsBlue)
</strong></code></pre>

</details>

<details>

<summary>FireGameEvent ( event: <a data-footnote-ref href="#user-content-fn-2"><mark style="color:purple;"><strong>GameEvent</strong></mark></a> )</summary>

Useful to react to certain events in the game, like a player's death for example

You might want to take a look at the [Game Events](https://wiki.alliedmods.net/Team_Fortress_2_Events) page

Example:

```lua
local function PlayerDeath(event)
    if event:GetName() == "player_death" then
        local victim_index = event:GetInt("victim_entindex")
        local victim = entities.GetByIndex(victim_index)
        if not victim then return end
        
        print(victim:GetName() .. " has died")
    end
end

callbacks.Register("FireGameEvent", PlayerDeath)
```

</details>

<details>

<summary>DispatchUserMessage ( msg: <a data-footnote-ref href="#user-content-fn-2"><mark style="color:purple;"><strong>UserMessage</strong></mark></a> )</summary>

It's useful for buying stuff in MvM and other things :p&#x20;

To find user messages, I recommend looking at the TF2's source code

Example:

<pre class="language-lua" data-title="Example from official docs" data-full-width="false"><code class="lang-lua">--- source: https://lmaobox.net/lua/Lua_Classes/UserMessage/#example
local function myCoolMessageHook(msg)

    if msg:GetID() == SayText2 then 
        local bf = msg:GetBitBuffer()

        bf:SetCurBit(8)-- skip 1 byte of not useful data

        local chatType = bf:ReadString(256)
        local playerName = bf:ReadString(256)
        local message = bf:ReadString(256)

        print("Player " .. playerName .. " said " .. message)
    end

end

<strong>callbacks.Register("DispatchUserMessage", myCoolMessageHook)
</strong></code></pre>

</details>

<details>

<summary>SendStringCmd ( cmd: <a data-footnote-ref href="#user-content-fn-3"><mark style="color:purple;"><strong>StringCmd</strong></mark></a> )</summary>

Called when console command is sent to server, like for example when using chat it'll pass the message to the cmd parameter

Example:

```lua
local function PrintMessages(cmd)
    local text = cmd:Get()
    if string.find(text, 'say "') then
        print(text)
        cmd:Set("echo hi mom!") --- change the command from for example, 'say "hi dad"' to "echo hi mom!"
    end
end

callbacks.Register("SendStringCmd", PrintMessages)
```

</details>

<details>

<summary>FrameStageNotify ( stage: <a data-footnote-ref href="#user-content-fn-4"><mark style="color:purple;"><strong>E_ClientFrameStage</strong></mark></a> )</summary>

This gets called when when rendering starts/ends, when starting/nding to receive a network update, etc.

Used to be PostPropUpdate but its deprecated, so use `stage == E_ClientFrameStage.NETWORK_UPDATE_START`  if you want the same thing

Example:

```lua
local position = nil

local function GetLocalPlayerPosition()
    local player = entities.GetLocalPlayer()
    if not player then position = nil return end
    
    position = player:GetAbsOrigin()
    print("The new localplayer position is " .. tostring(position))
end

local function FrameStageNotify(stage)
    if stage == E_ClientFrameStage.NETWORK_UPDATE_START then
        GetLocalPlayerPosition()
    end
end

callbacks.Register("FrameStageNotify", FrameStageNotify)
```

</details>

<details>

<summary>RenderView ( setup: <a data-footnote-ref href="#user-content-fn-5"><mark style="color:purple;"><strong>ViewSetup</strong></mark></a> )</summary>

This is called before the view of the local player is rendered

Its used to change your fov, angles, etc

Example:

```lua
local function ChangeFOV(setup)
    setup.fov = 120
end

callbacks.Register("RenderView", ChangeFOV)
```

</details>

<details>

<summary>PostRenderView ( setup: <a data-footnote-ref href="#user-content-fn-5"><mark style="color:purple;"><strong>ViewSetup</strong></mark></a> )</summary>

This is called after the view of the local player is rendered

Its used to make custom cameras

Example:

{% code title="Example from official doc" %}
```lua
--- source: https://lmaobox.net/lua/Lua_Libraries/render/#examples
local camW = 400
local camH = 300
local cameraTexture = materials.CreateTextureRenderTarget( "cameraTexture123", camW, camH )
local cameraMaterial = materials.Create( "cameraMaterial123", [[
    UnlitGeneric
    {
        $basetexture    "cameraTexture123"
    }
]] )

callbacks.Register("PostRenderView", function(view)
    customView = view
    customView.angles = EulerAngles(customView.angles.x, customView.angles.y + 180, customView.angles.z)

    render.Push3DView( customView, E_ClearFlags.VIEW_CLEAR_COLOR | E_ClearFlags.VIEW_CLEAR_DEPTH, cameraTexture )
    render.ViewDrawScene( true, true, customView )
    render.PopView()
    render.DrawScreenSpaceRectangle( cameraMaterial, 300, 300, camW, camH, 0, 0, camW, camH, camW, camH )
end)
```
{% endcode %}

</details>

<details>

<summary>ServerCmdKeyValues ( keyvalues: <a data-footnote-ref href="#user-content-fn-6"><mark style="color:purple;"><strong>StringCmd</strong></mark></a> )</summary>

Called when the client sends a keyvalues message to the server. Keyvalues are a way of sending data to the server, and are used for many things, such as sending MVM Upgrades, using items, and more

Example:

```lua
local function ServerCmdKeyValues(keyvalues)
    local text = keyvalues:Get()
    print(text)
end

callbacks.Register("ServerCmdKeyValues", ServerCmdKeyValues)
```

</details>

<details>

<summary>OnFakeUncrate ( crate: <a data-footnote-ref href="#user-content-fn-7"><mark style="color:purple;"><strong>Item</strong></mark></a>, crateLootList: <mark style="color:purple;"><strong>table</strong></mark> )</summary>

Honestly everything in this specific callback was taken from the official lua doc, I have never used this one

Called when a fake crate is to be uncrated. This is called before the crate is actually uncrated. You can return a table of items that will be shown as uncrated. The loot list is useful as a reference for what items can be uncrated in this crate, but you can create any items you want.

Example:

{% code title="Example from official lua doc" %}
```lua
--- source: https://lmaobox.net/lua/Lua_Callbacks/#examples

--- OnFakeUncrate gets called when user is unboxing a fake crate with a fake key, 
--- both could be created by our skinchanger and via CreateFakeItem method
callbacks.Register( "OnFakeUncrate", "abcd", function( itemCrate, lootTable )
    print( "OnFakeUncrate" )
    print( "itemCrate Name: " .. itemCrate:GetName() )

    for i = 1, #lootTable do
        print( "lootTable[" .. i .. "] Name: " .. lootTable[i]:GetName() )
    end

    return lootTable
end )

--- modify unboxing to always unbox rainbow flamethrower (15090)
callbacks.Register( "OnFakeUncrate", "abcd", function( itemCrate, lootTable )
    print( "OnFakeUncrate crate: " .. itemCrate:GetName() )

    local myLootTable = {}
    myLootTable[1] = itemschema.GetItemDefinitionByID(15090)

    return myLootTable
end )
```
{% endcode %}

</details>

<details>

<summary>OnLobbyUpdated ( lobby: <a data-footnote-ref href="#user-content-fn-8"><mark style="color:purple;"><strong>GameServerLobby</strong></mark></a> )</summary>

Called when the lobby is found or updated

Is called before deciding if you're gonna join the game or not, so you can decide for the game :)

Example:

```lua
---@param lobby GameServerLobby
local function OnLobbyUpdated(lobby)
   for i, member in pairs (lobby:GetMembers()) do
      print(member:GetName() .. " " .. member:GetSteamID())
   end
end

callbacks.Register("OnLobbyUpdated", OnLobbyUpdated)
```

</details>

<details>

<summary>SetRichPresence ( key: <mark style="color:purple;"><strong>string</strong></mark>, value: <mark style="color:purple;"><strong>string</strong></mark> )</summary>

This is **NOT** discord rich presence, its for steam friend list!

Allows you to change the rich presence in the friend list

{% code overflow="wrap" %}
```lua
--- this changes the state to casual, so even if we're on a community server it will look like we're playing a casual match :)

---@param key string
---@param value string?
---@return string?
local function SetRichPresence(key, value)
   if key == "state" then
      return "PlayingCasual"
   end

   return nil
end

callbacks.Register("SetRichPresence", SetRichPresence)
```
{% endcode %}

</details>

<details>

<summary>SendNetMsg ( msg: <a data-footnote-ref href="#user-content-fn-9"><mark style="color:purple;"><strong>NetMessage</strong></mark></a>, isreliable: <mark style="color:purple;"><strong>boolean</strong></mark>, isvoice: <mark style="color:purple;"><strong>boolean</strong></mark> )</summary>

Called when the client wants to send a <mark style="color:purple;">**NetMessage**</mark> to the server, you can use this callback to intercept that and decide if you want to send it. It's possible to change the message data so we can do some light amount of tom foolery with the server like spoofing convar values

You might want to check the leaked 2020 TF2 source code for the net messages and to see how they write & read them

You might want to see how the BitBuffer class works, it is really important for this

Example:

```lua
local clc_move = 9

---@param msg NetMessage
---@param isreliable boolean
---@param isvoice boolean
local function SendNetMessage(msg, isreliable, isvoice)
   if msg:GetType() == clc_move then
      local buffer = BitBuffer()
      msg:WriteToBitBuffer(buffer)

      --- skip 6 useless bits
      buffer:SetCurBit(6)

      local newcommands, backupcommands
      newcommands = buffer:ReadInt(4)
      backupcommands = buffer:ReadInt(3)

      local formattedtext = string.format("new cmds: %s, backup cmds: %s", newcommands, backupcommands)
      print(formattedtext)

      buffer:Delete()
   end

   return true
end

callbacks.Register("SendNetMsg", SendNetMessage)
```

</details>

<details>

<summary>DoPostScreenSpaceEffects ( )</summary>

Called after the screen space effects are drawn in the screen

This is useful for drawing custom glows and other stuff

Example:

i have no good example, sorry

was never able to make stuff with this callback work

</details>

#### GCSendMessage and GCRetrieveMessage exist, but I have no idea what they do. Even the example in the official lua documentation explains nothing <a href="#gcsendmessage-typeidinteger-datastringcmd" id="gcsendmessage-typeidinteger-datastringcmd"></a>

## Methods

### Register

<details>

<summary>Register ( id: <mark style="color:yellow;"><strong>string</strong></mark>, name: <mark style="color:yellow;"><strong>string</strong></mark>, func: <mark style="color:yellow;"><strong>function</strong></mark> )</summary>

* You can use this to register a function (`func`) that gets called when a certain callback (`id`) runs

- The <mark style="color:green;">name</mark> parameter is a unique identifier so you can stop a registered function to stop at any time

Example:

<pre class="language-lua" data-title="Print hi on Draw callback"><code class="lang-lua">local function PrintHi()
    print("hi mom!")
end

<strong>callbacks.Register("Draw", "hi dad", PrintHi)
</strong></code></pre>

</details>

<details>

<summary>Register ( id: <mark style="color:yellow;"><strong>string</strong></mark>, func: <mark style="color:yellow;"><strong>function</strong></mark> )</summary>

* You can use this to register a function (`func`) that gets called when a certain callback (`id`) runs

Example:

<pre class="language-lua"><code class="lang-lua">local function PrintHi()
    print("hi mom!")
end

<strong>callbacks.Register("Draw", PrintHi)
</strong></code></pre>

</details>

### Unregister

<details>

<summary>Unregister ( id: <mark style="color:yellow;"><strong>string</strong></mark>, name: <mark style="color:yellow;"><strong>string</strong></mark> )</summary>

* Stops a registered callback id (<mark style="color:green;">**name**</mark>) from running

Example:

```lua
callbacks.Unregister("Draw", "hi dad")
```

</details>

[^1]: <mark style="color:purple;">**I have to add this class later**</mark>

[^2]: I didn't make the class page yet

[^3]: <mark style="color:purple;">**Class page still not made**</mark>

[^4]: I still need to make this page

[^5]: Still have to make this page

[^6]: Gotta make the page

[^7]: As always, I still have to make this page :(

[^8]: Still gotta make this page, nice

[^9]: I particularly love this class, but I still haven't made the page :p
