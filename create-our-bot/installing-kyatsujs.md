---
description: Steps to install the KyatsuJS package and start using it.
cover: >-
  https://images.unsplash.com/photo-1495954380655-01609180eda3?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwxMHx8Y2l0eXxlbnwwfHx8fDE2ODUzNzUwNTV8MA&ixlib=rb-4.0.3&q=85
coverY: 336
---

# Installing KyatsuJS

## Install the NPM package

If you never did this before, here is how to install any package using NPM or other package manager:

```bash
npm install kyatsujs@latest
```

Then, wait until the download is finished. More files will be added in your project root:

<div align="left">

<figure><img src="https://media.botmarket.ovh/x0ncof.png" alt="" width="375"><figcaption></figcaption></figure>

</div>

You shall see a new property in your package.json where appears the versions of the different dependencies (packages) your project uses. Congrats !

## Our first program with the package

Open the main.js file and be ready to write the first line of code. If you didn't, take a look on the [Prerequisites page](prerequesites.md), it will be crucial to understand what we'll write.

The added code snippet will be highlighted.

### 1. Importing the package

<pre class="language-javascript" data-title="main.js" data-line-numbers data-full-width="false"><code class="lang-javascript"><strong>const KyatsuJS = require("kyatsujs");
</strong></code></pre>

### 2. Creating an instance of a KyatsuJS Client class

<pre class="language-javascript" data-title="main.js" data-line-numbers><code class="lang-javascript">const KyatsuJS = require("kyatsujs");

<strong>const botInstance = KyatsuJS.KyaClient.init("Token");
</strong></code></pre>

### 3. Linking our bot token

Go back to the Discord Developer Portal and navigate over the Bot tab. You can see the token section. Reset it and copy the new you see, you won't be able to copy it again after you closed this page !

<div align="left">

<figure><img src="https://media.botmarket.ovh/d2ai33.png" alt=""><figcaption></figcaption></figure>

</div>

Then, paste it in your code. For the example, a false token will be used. Replace it by yours instead. Our finale code looks like that:

<pre class="language-javascript" data-title="main.js" data-line-numbers><code class="lang-javascript">const KyatsuJS = require("kyatsujs");

const botInstance = KyatsuJS.KyaClient.init("abcde.fghij.klmno.13579");

<strong>void botInstance.login();
</strong></code></pre>

The 5th line tells the compiler that we want to log in the bot (it will connect it with Discord, and it will be online !). The void keyword is fully optional but tells that we don't care about the promised return of the login function.

Congratulations, you can now start a Discord bot with KyatsuJS. :)
