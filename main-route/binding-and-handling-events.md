---
description: You probably want to know how to configure your event handler.
cover: ../.gitbook/assets/5956.jpg
coverY: 160
---

# ❗ Binding & handling events

## Basics & Introduction

KyatsuJS can handle few default events. These events are listed [**here**](https://kyatsujs-doc.vercel.app/types/availableEvent.html). As commands, Kyatsu Client includes its own [`EventManager`](https://kyatsujs-doc.vercel.app/classes/EventManager.html) class instance in the [`Events`](https://kyatsujs.gitbook.io/guides/main-route/binding-and-handling-events) attributes. Few methods allow us to manage events to bind, and to customize.

### Default case

If no event is configured, it can handle the defaults event listed above. There are the two functions defined for each:

{% tabs %}
{% tab title="JavaScript" %}
{% code title="events.js" lineNumbers="true" %}
```javascript
// Ready event
bot.on('ready', client => {
  log(`Logged in as ${client.resolved.user.tag}.`);
});

// Interaction create event
bot.on(
  'interactionCreate',
  async (client, interaction) => {
    if (interaction.isChatInputCommand() || interaction.isContextMenuCommand()) {
      const command = client.Commands.getCommand(interaction.commandName);
      if (!command) return;
      await command.run(interaction);
    }
  }
);
```
{% endcode %}

We advise you to check the TypeScript version, in the next tab, for a better understanding of this code.
{% endtab %}

{% tab title="TypeScript" %}
<pre class="language-typescript" data-title="events.ts" data-line-numbers><code class="lang-typescript"><strong>// Ready event
</strong><strong>bot.on('ready', (client: KyaClient): void => {
</strong>  log(`Logged in as ${(client.resolved as Client&#x3C;true>).user.tag}.`);
});

// Interaction create event
bot.on(
  'interactionCreate',
  async (client: KyaClient, interaction: BaseInteraction): Promise&#x3C;void> => {
    if (interaction.isChatInputCommand() || interaction.isContextMenuCommand()) {
      const command: Command | undefined = client.Commands.getCommand(interaction.commandName);
      if (!command) return;
      await command.run(interaction);
    }
  }
);
</code></pre>
{% endtab %}
{% endtabs %}

### Which event is executed if none is specified ?

When you want to use event manager from KyaClient, you can encounter 3 cases:

1. If any event is specified, **only the `ready` one** will be executed using the default function.
2. If you specify an event that **is considered** as default, you can avoid passing your own function, and it will use the default one.
3. If you specify an event that is **NOT considered** as default, you MUST pass your own function.

## Configure your events

Now, after having told how events can be handled, let's show you why you are here. It's important to read the section above to understand what we will do below.

### Binding a default event

<pre class="language-javascript" data-title="events.js" data-line-numbers><code class="lang-javascript">// ...
<strong>bot.Events.bindEvent("interactionCreate");
</strong></code></pre>

### Binding an event using your own function

That method works for default events and not default events.

<pre class="language-javascript" data-title="events.js" data-line-numbers><code class="lang-javascript">// ...
<strong>bot.Events.bindEvent("interactionCreate", (client, interaction) => {
</strong><strong>    // Some code here
</strong><strong>});
</strong></code></pre>

The function passed as argument must contain the client parameter first. The `client` parameter will be a `KyaClient` instance once the event is triggered. Then, the following parameters are the same as the Discord.js event.

## Removing events

If you don't want some events to be triggered, you can unbind them with the following code:

<pre class="language-javascript" data-title="events.js" data-line-numbers><code class="lang-javascript">// ...
<strong>bot.Events.unbindEvent("interactionCreate");
</strong></code></pre>

Unbinding events removes completely the event, and this latter won't be listened at all.

## Undesirable effects

Some unknown consequences could appear if I don't note them here.

First, once the bot is logged in, binding and/or unbinding events has any impact ! The bot loads the bound events when the logging function is triggered.

We advise you to keep the ready event bound, even if you want to change the callback function (you can), for being notified when the "pre-logged in" phase switch to the "logged in" phase.
