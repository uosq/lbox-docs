---
description: This can be used to interact with Lmaobox's aimbot
---

# aimbot

## Methods

<details>

<summary><mark style="color:blue;">GetAimbotTarget</mark></summary>

This returns **-1** if aimbot has no target

If aimbot has a **target**, like a **player** or any **other entity**, it'll return the entity's index

Return type: <mark style="color:yellow;">**integer**</mark>

Example:

{% code title="Print target's name" overflow="wrap" %}
```lua
local function CreateMove(cmd)
    local target = aimbot.GetAimbotTarget() --- returns -1 if not running or no target

    --- world entity's index is 0, so we can skip it
    if target > 0 then
        local entity = entities.GetByIndex(target)
        if not entity then return end
        
        print("Target's name: " .. entity:GetName())
    end
end

callbacks.Register("CreateMove", CreateMove)
```
{% endcode %}

</details>

