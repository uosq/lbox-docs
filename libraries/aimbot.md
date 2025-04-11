---
description: This can be used to interact with Lmaobox's aimbot
---

# aimbot

## Methods

### GetAimbotTarget

<details>

<summary><mark style="color:blue;">GetAimbotTarget</mark></summary>

This returns **0** if aimbot is not running

This returns **-1** if aimbot is running but has no target

If aimbot has a **target**, like a **player** or any **other entity**, it'll return the entity's index

Return type: <mark style="color:yellow;">**integer**</mark>

Example:

<pre class="language-lua" data-title="Print target&#x27;s name" data-overflow="wrap"><code class="lang-lua">local function CreateMove(cmd)
<strong>    local target = aimbot.GetAimbotTarget() --- returns -1 if not running or no target
</strong>
    --- world entity's index is 0, so we can skip it
    if target > 0 then
        local entity = entities.GetByIndex(target)
        if not entity then return end
        
        print("Target's name: " .. entity:GetName())
    end
end

callbacks.Register("CreateMove", CreateMove)
</code></pre>

</details>
