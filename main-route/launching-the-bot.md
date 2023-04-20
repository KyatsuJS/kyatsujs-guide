---
description: In this page, you'll learn to create the base of a bot.
cover: ../.gitbook/assets/yingyi-xsu-s1.jpg
coverY: 0
---

# 🌱 Launching the bot

We won't go through 4 ways, there is a first code snippet:

{% tabs %}
{% tab title="JavaScript" %}
{% code title="index.js" lineNumbers="true" %}
```javascript
// Import the package
const kyatsujs = require("kyatsujs");

// Create an instance of the Kyatsu Client
const bot = kyatsujs.KyaClient.init("your token here");

// Launch the bot
void bot.login();
```
{% endcode %}
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

Now, let's explain what we wrote.

1. The first instruction, line 2, declares the constant `kyatsujs` that contains the package.
2. The second instruction, line 5, appeals the `init()` method from the `KyaClient` class. It returns a new instance of the latter.
3. Then, line 8, we appeal the method `login()` method from the `KyaClient` instance, to launch some data to Discord and the bot.

Note that the `void` keyword before the third instruction (line 8) isn't necessary. It's for code aesthetically.
