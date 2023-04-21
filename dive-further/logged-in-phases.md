---
description: >-
  If you want to add some specific functions, relatives to the bot phase, this
  page will help you.
cover: ../.gitbook/assets/ying-yi956-72px.jpg
coverY: 105
---

# ⏳ Logged in phases

{% hint style="warning" %}
In this Dive Further category, we will spare the laborious explanations and get to the heart of the matter. Bring the documentation nearby, you'll need it.
{% endhint %}

## What phases are

Contextualization: when I made the KyatsuJS package, I encountered a problem that will cause some issues to you, developers. First, have a look at this code:

<pre class="language-javascript" data-title="index.js" data-line-numbers><code class="lang-javascript">const { KyaClient } = require("kyatsujs");
const { token } = require("./token.json");

const client = KyaClient.init(token);

client.Events.bindEvent("interactionCreate");

client.Commands
    .add("ping", (command, interaction) => {
        interaction.reply("Pong!");
    })
    .load();

void client.login();

// The problem is here:
<strong>console.log(client.resolved.guilds.cache);
</strong></code></pre>

The login method, line 14, is an asynchronous one. The problem is, as long as the bot is not fully logged in, you can't call the Discord.js\<Client> methods on it, like view guilds or users. However, if your code is displayed in a single file, you probably don't want to break your head making an asynchronous function that includes your source code.

You probably don't want to set your code in a `then()` method too.

<details>

<summary>Example of <code>then()</code> method use</summary>

```javascript
// ...
void bot.login().then(str => {
    console.log(bot.resolved.guilds.cache);
    
    // If your code is long, it will become unreadable with many indents.
    // It can cause problem with the outside of your code (synchronous issues).
});
```

</details>

So, phases are a concept that designates the phase before the bot is ready, and after it's ready.

This concept is now explained, we can show our prepared solution.

## Avoiding methods

{% hint style="info" %}
This problem is for people who make a pretty simple Kyatsu bot, in a single file. We recommand you to use a clean project tree, with a good organization.
{% endhint %}

We can tell the Kyatsu Client that we want a piece of code to be executed before the bot is logged in, and a piece of code to be executed after. The first one isn't necessary, you could just put your code above the login method.

### Set the prepare function

(This is fully optional) You just have to call the [`prepare()`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html#prepare) method in the [`KyaClient`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html) instance.

<pre class="language-javascript" data-title="index.js" data-line-numbers><code class="lang-javascript">const { KyaClient } = require("kyatsujs");
const { token } = require("./token.json");

const client = KyaClient.init(token);

// Here
<strong>client.prepare((kyacli, bot) => {
</strong><strong>    kyacli.Events.bindEvent("interactionCreate");
</strong><strong>    
</strong><strong>    kyacli.Commands
</strong><strong>        .add("ping", (command, interaction) => {
</strong><strong>            interaction.reply("Pong!");
</strong><strong>        })
</strong><strong>        .load();
</strong><strong>});
</strong>
void client.login();
</code></pre>

As you can see, the prepare method can help to structure a bit of our code. The parameters here are the same for the [`prepare()`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html#prepare) and the [`run()`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html#run) methods.

* `kyacli` is the [`KyaClient`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html) instance. Use a different parameter name as the instance one, stored in a constant. It allows you to make the difference easier between these two, and to avoid severe JavaScript compilation issues.
* `bot` is the Discord.js Client (`bot` = [`kyacli.resolved`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html#resolved)) instance; **before the login** if the method is [`prepare()`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html#prepare), **after the login** if the method is [`run()`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html#run).

### Set the run function

The [`run()`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html#run) function uses the same syntax as the [`prepare()`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html#prepare) one. There is an example, the fixed version of our previous mistake:

<pre class="language-javascript" data-title="index.js" data-line-numbers><code class="lang-javascript">const { KyaClient } = require("kyatsujs");
const { token } = require("./token.json");

const client = KyaClient.init(token);

client.prepare((kyacli, bot) => {
    kyacli.Events.bindEvent("interactionCreate");
    
    kyacli.Commands
        .add("ping", (command, interaction) => {
            interaction.reply("Pong!");
        })
        .load();
});

// Here
<strong>client.run((kyacli, bot) => {
</strong><strong>    console.log(bot.guilds.cache);
</strong><strong>});
</strong>
void client.login();
</code></pre>

{% hint style="danger" %}
* The run method is called **after the events are listened**. So you can't change event bindings.
* This is called also **after the commands are loaded**.
{% endhint %}

You can find more information about these two methods syntax here: [`systemFunction`](https://kyatsujs-doc.vercel.app/types/systemFunction.html).

