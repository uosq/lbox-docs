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

> GetDataBitsLength()
> + Returns the length of the buffer in bits
> + You can use this to set or change the m_nLength when modifying a SendNetMsg callback
> + Return: **integer**

---

> GetDataBytesLength()
> + Returns the length of the buffer in bytes
> + You can use this to set or change the m_nLength when modifying a SendNetMsg callback
> + Its basically the same thing as **GetDataBitsLength()**
> + Return: **integer**

---

> Reset()
> + Resets the read position to the beginning of the buffer. This is useful if you want to read the buffer multiple times, but it is not necessary. 
> + This is basically SetCurBit(0)
> + Returns nothing

---

> ReadByte()
> + Reads 1 byte from the buffer, which means its reading 8 bits of information
> + Returns whatever info was in the 8 bits that were read
> + Return: **integer**

---

> ReadBit()
> + Reads 1 bit from the buffer
> + Returns either a 1 or a 0
> + Useful for TRUE or FALSE
> + Return: **integer**

---

**Good info to have about the next methods: When reading TF2's leaked source code, its good to remember a Word (ReadWord) is 16 bits, and generally you wont need to read 64 bits**

---

> ReadFloat( bitLength: integer )
> + **bitLength IS OPTIONAL, by default its 32 bits (or 4 bytes)**
> + Reads **N bytes** (default: 4) from the buffer and returns it as a float.
> + Returns the float read as first return value, and current bit position as second return value.
> + Return: **number**

---

> ReadInt( bitLength: integer )
> + **bitLength IS OPTIONAL, by default its 32 bits (or 4 bytes)**
> + Reads **N bytes** (default: 4) from the buffer and returns it as a float.
> + Returns the integer read as first return value, and current bit position as second return value.
> + Return: **number**

---

> ReadString( maxLength: integer )
> + Reads a string from the buffer
> + 