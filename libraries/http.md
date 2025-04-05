---
description: Http library
---

# http

## Functions

<details>

<summary><mark style="color:blue;">Get</mark> ( url: <mark style="color:red;"><strong>string</strong></mark> )</summary>

* Returns whatever the request url returns as a string

Example:

<pre class="language-lua"><code class="lang-lua"><strong>local fact = http.Get("https://catfact.ninja/fact")
</strong>print(fact)
</code></pre>

</details>

<details>

<summary><mark style="color:blue;">GetAsync</mark> ( url: <mark style="color:red;"><strong>string</strong></mark>, callback: <mark style="color:red;"><strong>fun(response: string)</strong></mark> )</summary>

* Doesn't return anything

- <mark style="color:green;">CURRENTLY ONLY ON BETA BUILD</mark>

* when the url returns something, it'll pass it to the "response" parameter of the callback

Example:

<pre class="language-lua"><code class="lang-lua">local function print_fact(fact)
    print(fact)
end

<strong>http.GetAsync("https://catfact.ninja/fact", print_fact)
</strong></code></pre>

</details>
