# Telegram Order Receiver Bot

A simple and lightweight Telegram bot that receives order messages from a web form. Built with HTML & Javascript.


## Features

- Accepts orders from an HTML form or API request
- Sends new order details to your Telegram
- Fully customizable message format

## Demo

**Use case:** An online store sends order info to this bot, and it automatically acknowledges the order.

## Tech Stack

- Node.js
- Telegram Bot API
- Express.js (for handling POST requests from forms)

## Example

```bash

BOT_TOKEN=your_telegram_bot_token
ADMIN_CHAT_ID=your_telegram_chat_id

> Get your bot token from @BotFather.

Use @userinfobot to get your chat ID.
```

Example: HTML Form Integration

You can integrate this bot with any website using a basic HTML form and fetch:

<form onsubmit="sendOrder(event)">
  <input type="text" name="name" placeholder="Your Name" required />
  <input type="text" name="product" placeholder="Product Name" required />
  <button type="submit">Send Order</button>
</form>

<script>
function sendOrder(e) {
  e.preventDefault();
  const form = new FormData(e.target);
  fetch("https://your-server.com/order", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({
      name: form.get("name"),
      product: form.get("product")
    }),
  });
}
</script>

Example Bot Reply

When the bot receives an order:

New Order Received:

Name: John Doe
Product: T-shirt

Thank you for your order, John! We'll get back to you shortly.

Deployment Options

You can host this bot on any Node.js-friendly platform, such as:

Pella

Render

Railway

Vercel (via serverless functions)

Glitch


License

This project is licensed under the MIT License.


---

Made with love for small businesses.
