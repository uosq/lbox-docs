---
description: >-
  The BitBuffer object is used to read and write data that is usually sent over
  the network, compressed into a bitstream.
---

# BitBuffer

This is useful to manipulate data sent to the server, for example spoofing convars (console variables)  values like sv\_cheats to their default instead of whatever we have

### Constructor

```lua
BitBuffer()
```

{% code title="Example" overflow="wrap" %}
```lua
--- create the buffer
local buffer = BitBuffer()
buffer:WriteString("Hi mom!") --- writes "Hi mom!" to the buffer 
buffer:SetCurBit(0) --- sets the buffer's bit position to 0 (we wont do anything else with it here)

--- do something with the buffer here
--- like read it, in this case we need the bit as 0 so we know FOR SURE where we currently are with it BEFORE reading the buffer

buffer:Delete() -- !!!! DELETE THE BUFFER !!!!

--- in this case, we could have done something else like using buffer:WriteInt after WriteString
```
{% endcode %}

### Methods

<details>

<summary><mark style="color:green;">Delete</mark></summary>

You <mark style="color:yellow;">SHOULD</mark> use this after using the buffer (You dont want any memory leaks, do you?)

</details>

<details>

<summary><mark style="color:blue;">GetDataBitsLength</mark></summary>

Returns the length of the buffer in bits

You can use this to set or change the m\_nLength when modifying a SendNetMsg callback

Return type: <mark style="color:yellow;">**integer**</mark>

</details>

<details>

<summary><mark style="color:blue;">GetDataBytesLength</mark></summary>

Returns the length of the buffer in bytes

Its basically the same thing as **GetDataBitsLength()**

Return type: <mark style="color:yellow;">**integer**</mark>

</details>

<details>

<summary><mark style="color:blue;">Reset</mark></summary>

Resets the read position to the beginning of the buffer.

This is useful if you want to read the buffer multiple times, but it is not necessary.

This is basically <mark style="color:blue;">SetCurBit</mark>(0)

</details>

<details>

<summary><mark style="color:blue;">GetCurBit</mark></summary>

Returns the current bit position

Return type: <mark style="color:yellow;">**integer**</mark>

</details>

<details>

<summary><mark style="color:blue;">SetCurBit</mark> ( position: <mark style="color:red;"><strong>integer</strong></mark> )</summary>

Sets the current bit position

</details>

### Read Methods

<details>

<summary><mark style="color:blue;">ReadByte</mark></summary>

Reads 1 byte from the buffer, which means its reading 8 bits of information

Returns whatever info was in the 8 bits that were read

It starts from the current bit position

Return type: <mark style="color:yellow;">**integer**</mark>

</details>

<details>

<summary><mark style="color:blue;">ReadBit</mark></summary>

Reads 1 bit from the buffer

Starts at the current bit position

Return type: <mark style="color:yellow;">**integer**</mark>

</details>

<details>

<summary><mark style="color:blue;">ReadFloat</mark> ( bitLength: <mark style="color:red;"><strong>integer</strong></mark> )</summary>

<mark style="color:green;">bitLength IS OPTIONAL, default is</mark> <mark style="color:green;"></mark><mark style="color:green;">**32**</mark> <mark style="color:green;"></mark><mark style="color:green;">bits</mark>

Reads **N bits** (default: 32) from the buffer and returns it as a number.

Return type: <mark style="color:yellow;">**number**</mark>

</details>

<details>

<summary><mark style="color:blue;">ReadInt</mark> ( bitLength: <mark style="color:red;"><strong>integer</strong></mark> )</summary>

<mark style="color:green;">bitLength IS OPTIONAL, default is</mark> <mark style="color:green;"></mark><mark style="color:green;">**32**</mark> <mark style="color:green;"></mark><mark style="color:green;">bits</mark>

Reads **N bits** (default: 32) from the buffer and returns it as a integer.

Return type: <mark style="color:yellow;">**integer**</mark>

</details>

<details>

<summary><mark style="color:blue;">ReadString</mark> ( maxLength: <mark style="color:red;"><strong>integer</strong></mark> )</summary>

Reads a string from the buffer

<mark style="color:green;">maxLength is</mark> <mark style="color:green;"></mark><mark style="color:green;">**NOT**</mark> <mark style="color:green;"></mark><mark style="color:green;">optional</mark>

Return type: <mark style="color:yellow;">**string**</mark>

</details>

### Write Methods

Be careful to **NOT** overflow the buffer

<details>

<summary><mark style="color:blue;">WriteByte</mark> ( value: <mark style="color:red;"><strong>number</strong></mark> )</summary>

Writes 1 byte to the buffer, which means its changing 8 bits of information in the current bit position

</details>

<details>

<summary><mark style="color:blue;">WriteInt</mark> ( value: <mark style="color:red;"><strong>number</strong></mark> )</summary>

Writes 1 integer to the buffer in the current bit position

</details>

<details>

<summary><mark style="color:blue;">WriteFloat</mark> ( value: <mark style="color:red;"><strong>number</strong></mark>, bitLength: <mark style="color:red;"><strong>integer</strong></mark> )</summary>

Writes a float number to the buffer with the <mark style="color:green;">**OPTIONAL**</mark> bitLength (default is 32)

</details>

<details>

<summary><mark style="color:blue;">WriteString</mark> ( text: <mark style="color:red;"><strong>string</strong></mark> )</summary>

Writes the text to the buffer

</details>

### Examples

{% code title="Changing clc_Move msg" %}
```lua
local function SendNetMsg(msg)
   if msg:GetType() == 9 then --- clc_Move is 9
      local buffer = BitBuffer() --- create new BitBuffer

      buffer:WriteInt(2, 4) --- change new commands
      buffer:WriteInt(1, 3) --- change backup commands
      
      buffer:SetCurBit(0)
      msg:ReadFromBitBuffer(buffer)
      buffer:Delete() --- delete our BitBuffer
   end
end

callbacks.Register("SendNetMsg", SendNetMsg)
```
{% endcode %}
