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
