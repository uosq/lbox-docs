---
description: >-
  Library that helps making useful callbacks so your script can react to most
  things
---

# callbacks

## sCallbacks

They aren't functions, all the callback's parameters are passed to the actual function that you register

Callbacks can be called in different situations, for example CreateMove gets called \~67 times per second, but Draw gets called every frame. Some might not even be called at all like ServerCmdKeyValue that only runs when you use a item like noisemaker or buy a upgrade in MvM.

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

{% code title="Example from official docs" fullWidth="false" %}
```lua
--- source: https://lmaobox.net/lua/Lua_Classes/UserMessage/#example
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

callbacks.Register("DispatchUserMessage", myCoolMessageHook)
```
{% endcode %}

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
