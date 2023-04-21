---
description: >-
  You have now you successfully launched your bot, you probably want to create
  some commands.
cover: ../.gitbook/assets/ying-yi-2px.jpg
coverY: 0
---

# 🕹 Creating commands

## Why should you use KyatsuJS to load commands ?

First, the commands' manager is a service from KyatsuJS that is fully optional. You can basically load these commands using the Discord.js methods.

If you want to use KyatsuJS one, just follow these steps !

{% hint style="info" %}
All the code snippets in this page are only in JavaScript.
{% endhint %}

## Create commands

### Command instantiation

The [`KyaClient`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html) class has a [`Commands`](https://kyatsujs-doc.vercel.app/classes/KyaClient.html#Commands) property that contains an instance of [`CommandsManager`](https://kyatsujs-doc.vercel.app/classes/CommandManager.html).

Now, we can use it to create a command:

{% code title="index.js" lineNumbers="true" %}
```javascript
// ...
const pingCommandData = {
    options: {
        name: "ping",
    }
};

const pingCommand = bot.Commands.create(pingCommandData);
```
{% endcode %}

Our constant `pingCommand` does now include an instance of [`Command`](https://kyatsujs-doc.vercel.app/classes/Command.html). To understand why the structure of `pingCommandData` seems weird, you can check all the structure and options possibles at the [`CommandOptions` interface](https://kyatsujs-doc.vercel.app/interfaces/CommandOptions.html). You can also pass a string if you just want to set a name for your command.

You are going to say, "hey, this command doesn't do anything !". We are going to set it ! Once we have our command instance, made with the previous method, or manually, we can register it to the commands' manager. We do it this way:

{% code title="index.js" lineNumbers="true" %}
```javascript
// ...
bot.Commands.add(pingCommand);
```
{% endcode %}

You can also directly use the [`add()`](https://kyatsujs-doc.vercel.app/classes/CommandManager.html#add) method with our command data. Separating the command instantiation and the adding may be useful if you need to dynamically change some information before register it. There is an example:

{% code title="index.js" lineNumbers="true" %}
```javascript
// ...
const pingCommandData = {
    options: {
        name: "ping",
    }
};

bot.Commands.add(pingCommandData);
```
{% endcode %}

But using this method could be rude and cause problems. So if you don't know exactly what you are doing, use the first one.

### Set callback function

Let's put into context, we have this code snippet:

{% code title="index.js" lineNumbers="true" %}
```javascript
// ...
const pingCommandData = {
    options: {
        name: "ping",
    }
};

const pingCommand = bot.Commands.create(pingCommandData);

/*
 * The magic will happen here.
 */

bot.Commands.add(pingCommand);
```
{% endcode %}

We want now to add a callback function to our ping command, that replies "Pong !". First, have a look on the type/structure our function must have at [`commandCallback`](https://kyatsujs-doc.vercel.app/types/commandCallback.html) type. Our two parameters must be:

* `command`: The command instance.
* `interaction`: The interaction associated with the command trigger.

We can now create our command:

{% code title="index.js" lineNumbers="true" %}
```javascript
const pingCommandAction = (command, interaction) => {
    interaction.reply("Pong !").catch(err => console.log(err));
};
```
{% endcode %}

And now, let's implement it in our main code, with the full code:

{% code title="index.js" lineNumbers="true" %}
```javascript
// ...
const pingCommandData = {
    options: {
        name: "ping",
    }
};

const pingCommand = bot.Commands.create(pingCommandData);

const pingCommandAction = (command, interaction) => {
    interaction.reply("Pong !").catch(err => console.log(err));
};

bot.Commands.add(pingCommand);
```
{% endcode %}

## Registering of our commands

Now, we added all our commands and want to send them to the Discord API for using them on Discord.

We can call the function [`load()`](https://kyatsujs-doc.vercel.app/classes/CommandManager.html#load) in the [`CommandManager`](https://kyatsujs-doc.vercel.app/classes/CommandManager.html). There is the full code:

{% code title="index.js" lineNumbers="true" %}
```javascript
// ...
const pingCommandData = {
    options: {
        name: "ping",
    }
};

const pingCommand = bot.Commands.create(pingCommandData);

const pingCommandAction = (command, interaction) => {
    interaction.reply("Pong !").catch(err => console.log(err));
};

bot.Commands.add(pingCommand);
bot.Commands.load();
```
{% endcode %}

Now, express your creativity and make beautiful handlers !

{% hint style="info" %}
Don't call the [`load()`](https://kyatsujs-doc.vercel.app/classes/CommandManager.html#load) method each time you restart your bot, unless if you did changes in the `options` object. This is for preventing `rateLimits` from Discord API.
{% endhint %}



