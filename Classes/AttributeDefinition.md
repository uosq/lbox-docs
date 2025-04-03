# AttributeDefinition

## Has information on the desired attribute

##### this doesn't have a function to get the attribute's value in case we need it

---

### Methods

> GetName()
> + Returns the name
> + There isn't much else to say
> + Return: **string**

---

> GetID()
> + Returns the ID
> + Use this
> + Return: **integer**

---

> IsStoredAsInteger()
> + Returns true if the attribute is stored as an integer. For numeric attibutes, false means it is stored as a float.

### Examples

```lua
--- easier to read like this
local function EnumAttributes(attrDef)
   local name = attrDef:GetName() --- this is a string!
   local id = attrDef:GetID() --- this is a integer!
   local text = name .. tostring(id) --- fuses together name and id
   print(text) --- outputs the text to the console
end

--- our actual function
itemschema.EnumerateAttributes(EnumAttributes)
```