---
description: In this page, you'll learn to create the base of a bot.
cover: ../.gitbook/assets/yingyi-xsu-s1.jpg
coverY: 0
---

# 🌱 Launch the bot

## Importation

We won't go through 4 ways, there is a first code snippet:

{% tabs %}
{% tab title="JavaScript" %}
<pre class="language-javascript" data-title="index.js" data-line-numbers><code class="lang-javascript">// Import the package
<strong>const kyatsujs = require("kyatsujs");
</strong>
// Create an instance of the Kyatsu Client
<strong>const bot = kyatsujs.KyaClient.init("your token here");
</strong>
// Launch the bot
<strong>void bot.login();
</strong></code></pre>
{% endtab %}

{% tab title="TypeScript" %}
{% code title="index.ts" lineNumbers="true" %}
```typescript
// Import the package
import {KyaClient} from "kyatsujs";

// Create an instance of the Kyatsu Client
const bot: KyaClient = KyaClient.init("your token goes here");

// Launch the bot
void bot.login();
```
{% endcode %}
{% endtab %}
{% endtabs %}

Of course, in the JavaScript version, you can also use destructured import:&#x20;

`const { KyaClient } = require("kyatsujs");`

## Explanation of our code

Now, let's explain what we wrote.

1. The first instruction, line 2, declares the constant `kyatsujs` that contains the package.
2. The second instruction, line 5, appeals the [`init()`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html#init) method from the [`KyaClient`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html) class. It returns a new instance of the latter.
3. Then, line 8, we appeal the method [`login()`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html#login) method from the [`KyaClient`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html) instance, to launch some data to Discord and the bot.

Note that the `void` keyword before the third instruction (line 8) isn't necessary. It's for code aesthetically.

{% hint style="info" %}
The [`init()`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html) method can be called before creating an instance of the Kyatsu Client because it's a static method that parse the passed arguments. This allows the developer to pass different types of parameters, without conflict the `KyaClient` class parameters.

For more informations about typings, check the [**Full Documentation**](https://kyatsujs-doc.vercel.app).
{% endhint %}

## Successful launching

Once your bot is launched, something should appear in the Run Console:

<pre><code><strong>...
</strong><strong>⟦KYATSU LOG⟧ Logged in as KyatsuJS#1234.
</strong>...
</code></pre>

This message warns us that the bot is launched. If something else show up instead of this log, consider that it's not normal and something turns wrong. Note that every log from the KyatsuJS package will be marked with `⟦KYATSU something⟧`.

