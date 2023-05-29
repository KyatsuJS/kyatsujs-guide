---
description: Let's build a simple Discord bot with some commands and events.
cover: >-
  https://images.unsplash.com/photo-1543872084-c7bd3822856f?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw5fHxjaXR5fGVufDB8fHx8MTY4NTM3NTA1NXww&ixlib=rb-4.0.3&q=85
coverY: -83
---

# Setting up our first program

## Reproducing the previous example

In the previous steps, we have seen how to create a bot and log it. Now, we will discover some features/services that allow us a couple of things. Let's copy  and edit it a bit to make it look cleaner with object destructuring.

<pre class="language-javascript" data-title="main.js" data-line-numbers><code class="lang-javascript"><strong>const { KyaClient } = require("kyatsujs");
</strong><strong>const { token } = require("./token.json");
</strong><strong>
</strong><strong>const bot = KyaClient.init(token);
</strong><strong>
</strong><strong>void bot.login();
</strong></code></pre>

Our bot is missing of content. Let's create a simple command !

## Create a first command

<pre class="language-javascript" data-title="main.js" data-line-numbers><code class="lang-javascript">const { KyaClient } = require("kyatsujs");
const { token } = require("./token.json");

const bot = KyaClient.init(token);

<strong>bot.Commands.add("ping", (command, interaction) => {
</strong><strong>    void interaction.reply("Pong!");
</strong><strong>}).load();
</strong>
void bot.login();
</code></pre>

First, we registered the command name. Then, we registered the function that will be called every time the command is triggered. The parameters of the function are a bit hard :&#x20;

* `command` represents the Command class instance, a KyatsuJS class that has some attributes and methods to manage a command. More info about this class here: [Command](https://kyatsujs-doc.vercel.app/classes/Command.html).
* `interaction` represents the Discord.js Interaction (Chat input or Context menu) class instance. More info about these classes here: [ChatInputCommandInteraction](https://discord.js.org/#/docs/discord.js/main/class/ChatInputCommandInteraction) | [ContextMenuCommandInteraction](https://discord.js.org/#/docs/discord.js/main/class/ContextMenuCommandInteraction).

## Handling events

If you tried the previous code, nothing should happen. Why ? It's because we have to tell our bot that we want it to listen to the different interactions that are triggered when it's online. How we do that ?

<pre class="language-javascript" data-title="main.js" data-line-numbers><code class="lang-javascript">const { KyaClient } = require("kyatsujs");
const { token } = require("./token.json");

const bot = KyaClient.init(token);

bot.Commands.add("ping", (command, interaction) => {
    void interaction.reply("Pong!");
}).load();

<strong>bot.Events.bindEvent("interactionCreate");
</strong>
void bot.login();
</code></pre>

This single line tells the bot that we bind it with the `interactionCreate` event.

Now, you know how to create a command and a simple bot. In the next sections, you'll see how to use with more accuracy the different available services and features of KyatsuJS. Happy coding !
