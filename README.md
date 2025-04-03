# Custom Docs

Most of the info here was taken from the **official documentation** OR from my experience using the API

**Methods are called directly from the object**

Called with :

Example:

```lua
local buffer = BitBuffer()
buffer:SetCurBit(0)
buffer:WriteInt(120)
buffer:SetCurBit(0)
```

**Functions are called from a library**

Called with .

Example:

```lua
local pi = math.pi
```
