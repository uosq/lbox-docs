---
description: Has information on the desired attribute
---

# Attribute Definition

### Methods

<details>

<summary><mark style="color:blue;">GetName</mark></summary>

* Returns the name
* Return type: <mark style="color:yellow;">**string**</mark>

</details>

<details>

<summary><mark style="color:blue;">GetID</mark></summary>

* Returns the ID of the attribute
* Return type: <mark style="color:yellow;">**integer**</mark>

</details>

<details>

<summary><mark style="color:blue;">IsStoredAsInteger</mark></summary>

* Returns true if the attribute is stored as an integer. For numeric attibutes, false means it is stored as a float.
* Return type: <mark style="color:yellow;">**boolean**</mark>

</details>

### Examples

<pre class="language-lua" data-full-width="false"><code class="lang-lua">--- easier to read like this
local function EnumAttributes(attrDef)
<strong>   local name = attrDef:GetName() --- this is a string!
</strong>   local id = attrDef:GetID() --- this is a integer!

   local text = name .. tostring(id) --- fuses together name and id
   print(text) --- outputs the text to the console
end

--- our actual function
itemschema.EnumerateAttributes(EnumAttributes)
</code></pre>
