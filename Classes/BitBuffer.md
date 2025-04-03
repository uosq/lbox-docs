# BitBuffer

The BitBuffer object is used to read and write data that is usually sent over the network, compressed into a bitstream.

This is useful to manipulate data sent to the server, for example spoofing convars (console variables) like sv_cheats

### Constructor

```lua
BitBuffer()
```

Example:

```lua
--- create the buffer
local buffer = BitBuffer()
buffer:SetCurBit(0) --- sets the buffer's bit position to 0
buffer:WriteString("Hi mom!") --- writes "Hi mom!" to the buffer 
buffer:SetCurBit(0) --- sets the buffer's bit position to 0 (we wont do anything else with it here)

--- do something with the buffer here
--- like read it, in this case we need the bit as 0 so we know FOR SURE where we currently are with it BEFORE reading the buffer

buffer:Delete() -- !!!! DELETE THE BUFFER !!!!

--- in this case, we could have done something else like using buffer:WriteInt after WriteString, but as we ended 
```

### Methods

> [!NOTE]
> **Delete()**
> + **It's not deleted by Lua's garbage collection (WHY??? this is stupid)**
> + **You NEED to use delete after using the buffer** (we dont want any memory leaks, do we?)

> GetDataBitsLength()
> + Returns the length of the buffer in bits
> + You can use this to set or change the m_nLength when modifying a SendNetMsg callback
> + Return type: **integer**

---

> GetDataBytesLength()
> + Returns the length of the buffer in bytes
> + You can use this to set or change the m_nLength when modifying a SendNetMsg callback
> + Its basically the same thing as **GetDataBitsLength()**
> + Return type: **integer**

---

> Reset()
> + Resets the read position to the beginning of the buffer. This is useful if you want to read the buffer multiple times, but it is not necessary. 
> + This is basically SetCurBit(0)
> + Returns nothing

---

> GetCurBit()
> + Returns the current bit position
> + Return type: **integer**

---

> SetCurBit( position: **integer** )
> + Sets the current bit position
> + Return type: nothing :p

---

> #### **READ** Methods
>> ReadByte()
>> + Reads 1 byte from the buffer, which means its reading 8 bits of information
>> + Returns whatever info was in the 8 bits that were read
>> + Return type: **integer**
>>
>> ReadBit()
>> + Reads 1 bit from the buffer
>> + Returns either a 1 or a 0
>> + Useful for TRUE or FALSE
>> + Return type: **integer**
>>
>> ReadFloat( bitLength: integer )
>> + **bitLength IS OPTIONAL, by default its 32 bits (or 4 bytes)**
>> + Reads **N bits** (default: 4) from the buffer and returns it as a float.
>> + Returns the float read as first return value, and current bit position as second return value.
>> + Return type: **number**, current bit position (**number**)
>>
>> ReadInt( bitLength: integer )
>> + **bitLength IS OPTIONAL**
>> + Reads **N bits** (default: 32) from the buffer and returns it as a integer.
>> + Returns the integer read as first return value, and current bit position as second return value.
>> + Return type: **integer**, current bit position (**integer**)
>>
>> ReadString( maxLength: integer )
>> + Reads a string from the buffer
>> + maxLength is **NOT** optional
>> + Return type: **string**, current bit position (**integer**)

---

> #### **WRITE** Methods
>
> Be careful to **NOT** overflow the buffer
>> WriteByte( byte: **number** )
>> + Writes 1 byte to the buffer, which means its changing 8 bits of information
>>
>> WriteBit( bit: **integer** )
>> + Writes 1 bit to the buffer
>> + Either a 1 or a 0
>> + Useful for TRUE or FALSE
>> + Return type: nothing :p
>>
>> WriteByte( byte: **integer** )
>> + Writes 1 byte to the buffer
>> + Return type: nothing :p
>>
>> WriteFloat( value: **number**, bitLength: **integer** )
>> + **bitLength IS OPTIONAL, default its 32 bits**
>> + Writes **N bits** (default: 32) to the buffer
>> + Return type: nothing :p
>>
>> WriteInt( value: **integer** , bitLength: **integer** )
>> + **bitLength IS OPTIONAL**
>> + Writes **N bits** (default: 32) to the buffer
>> + Return type: nothing :p
>>
>> WriteString( text: **string** )
>> + Writes a string to the buffer
>> + Return type: nothing :p

---

### Examples

Changing clc_Move msg

```lua
local function SendNetMsg(msg)
   if msg:GetType() == 9 then --- clc_Move is 9
      local buffer = BitBuffer()

      buffer:WriteInt(2, 4) --- change new commands
      buffer:WriteInt(1, 3) --- change backup commands
      
      buffer:SetCurBit(0)
      msg:ReadFromBitBuffer(buffer)
      buffer:Delete()
   end
end

callbacks.Register("SendNetMsg", SendNetMsg)
```

---

Printing with bitbuffer

```lua
local buffer = BitBuffer()
buffer:WriteString("hi mom!")
buffer:SetCurBit(0)

local text = buffer:ReadString(7)
print(text)

--- dont forget to delete the buffer
buffer:Delete()
```