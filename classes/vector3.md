---
description: Is a point in 3D space, can mean a lot of things
---

# Vector3

## Constructor

{% tabs %}
{% tab title="Overloads" %}
* <mark style="color:purple;">Vector3</mark> (x, y, z)
* <mark style="color:purple;">Vector3</mark> () is equal to <mark style="color:purple;">Vector3</mark>(0, 0, 0)
{% endtab %}

{% tab title="Examples" %}
```lua
local allzeros = Vector3()
print(allzeros)

local hidad = Vector3(10, 50, 0)
print(hidad)
```
{% endtab %}
{% endtabs %}

## Fields

### x

The X coordinate (<mark style="color:yellow;">**number**</mark>)

### y

The Y coordinate (<mark style="color:yellow;">**number**</mark>)

### z

The Z coordinate (<mark style="color:yellow;">**number**</mark>)

## Methods

### Unpack

<details>

<summary><mark style="color:blue;">Unpack</mark> ( )</summary>

Returns the X, Y, and Z coordinates as separate variables

Return type: <mark style="color:yellow;">**number**</mark>, <mark style="color:yellow;">**number**</mark>, <mark style="color:yellow;">**number**</mark>

Example:

<pre class="language-lua"><code class="lang-lua">local position = Vector3(10, 50, 20)
<strong>local x, y, z = position:Unpack()
</strong>print(x, y, z)
</code></pre>

</details>

### Length

<details>

<summary><mark style="color:blue;">Length</mark> ( )</summary>

Returns the length of the vector.

Return type: <mark style="color:yellow;">**number**</mark>

Example:

<pre class="language-lua"><code class="lang-lua">local position = Vector3(10, 50, 20)
<strong>local length = position:Length()
</strong>print(length)
</code></pre>

</details>

### LengthSqr

<details>

<summary><mark style="color:blue;">LengthSqr</mark> ( )</summary>

Returns the squared length of the vector.

Return type: <mark style="color:yellow;">**number**</mark>

Example:

<pre class="language-lua"><code class="lang-lua">local position = Vector3(10, 50, 20)
<strong>local length = position:LengthSqr()
</strong>print(length)
</code></pre>

</details>

### Length2D

<details>

<summary><mark style="color:blue;">Length2D</mark> ( )</summary>

Returns the length in 2 dimensions (x, y) of the vector.

Return type: <mark style="color:yellow;">**number**</mark>

Example:

<pre class="language-lua"><code class="lang-lua">local position = Vector3(10, 50, 20)
<strong>local length = position:Length2D()
</strong>print(length)
</code></pre>

</details>

### Length2DSqr

<details>

<summary><mark style="color:blue;">Length2DSqr</mark> ( )</summary>

Returns the squared length in 2 dimensions (x, y) of the vector.

Return type: <mark style="color:yellow;">**number**</mark>

Example:

<pre class="language-lua"><code class="lang-lua">local position = Vector3(10, 50, 20)
<strong>local length = position:Length2DSqr()
</strong>print(length)
</code></pre>

</details>

### Dot

<details>

<summary><mark style="color:blue;">Dot</mark> ( vec: <mark style="color:yellow;"><strong>Vector3</strong></mark> )</summary>

Returns the dot product

Return type: <mark style="color:yellow;">**number**</mark>

Example:

```lua
local position1 = Vector3(10, 50, 20)
local position2 = Vector3(0, 20, 10)
local dot = position1:Dot(position2)
print(dot)
```

</details>

### Cross

<details>

<summary><mark style="color:blue;">Cross</mark> ( vec: <mark style="color:yellow;"><strong>Vector3</strong></mark> )</summary>

Returns the cross product between current vector and the vec parameter

Return type: <mark style="color:yellow;">**Vector3**</mark>

Example:

```lua
local position1 = Vector3(10, 50, 20)
local position2 = Vector3(0, 20, 10)
local cross = position1:Cross(position2)
print(cross)
```

</details>

### Clear

<details>

<summary><mark style="color:blue;">Clear</mark> ( )</summary>

Clears the vector, making it (0, 0, 0)

Return type: <mark style="color:yellow;">Vector3</mark> i am not sure if it returns anything

Example:

```lua
local position = Vector3(10, 50, 20)
position:Clear()
```

</details>

### Normalize

<details>

<summary><mark style="color:blue;">Normalize</mark> ( )</summary>

Normalizes the vector, making it have length 1 but go in the same direction

Return type: <mark style="color:yellow;">**Vector3**</mark>

Example:

```lua
local position = Vector3(10, 50, 20)
local normalized = position:Normalize()
print(normalized)
```

</details>

### Right

<details>

<summary><mark style="color:blue;">Right</mark> ( )</summary>

Returns the right of the vector

Return type: <mark style="color:yellow;">**Vector3**</mark>

Example:

```lua
local position = Vector3(10, 50, 20)
local right = position:Right()
print(right)
```

</details>

### Up

<details>

<summary><mark style="color:blue;">Up</mark> ( )</summary>

Returns the up of the vector

Return type: <mark style="color:yellow;">**Vector3**</mark>

Example:

```lua
local position = Vector3(10, 50, 20)
local up = position:Up()
print(up)
```

</details>

### Vectors

<details>

<summary><mark style="color:blue;">Vectors</mark> ( )</summary>

Returns the forward, right and up of the vector

Return type: <mark style="color:yellow;">**Vector3**</mark>, <mark style="color:yellow;">**Vector3**</mark>, <mark style="color:yellow;">**Vector3**</mark>

Example:

```lua
local position = Vector3(10, 50, 20)
local forward, right, up = position:Vectors()
print(forward, right, up)
```

</details>
