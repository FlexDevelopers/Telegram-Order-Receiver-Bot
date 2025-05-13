# Telegram Order Receiver Bot

A simple and lightweight Telegram bot that receives order messages from a web form. Built with HTML & Javascript.


## Features

- Sends new order details to your Telegram with Inline Buttons & Thumbnails

- Fully customizable message format

## Demo

**Use case:** An online store sends order info to this bot, and it automatically acknowledges the order.

## Tech Stack

- HTML, CSS & JS
- Telegram Bot API

## Requirements

- Get your bot token from @BotFather.
- Get your chat ID(For recive messages)


## Example: HTML Form Integration

You can integrate this bot with any website using a basic HTML form:
```html
<!DOCTYPE html>
<html>
<head>
  <title>Order Product</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; background: #eef2f7; }
    form { background: white; padding: 25px; max-width: 400px; margin: auto; border-radius: 12px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); }
    input, select, textarea, button {
      width: 100%; padding: 10px; margin: 10px 0; border-radius: 6px; border: 1px solid #ccc;
    }
    button { background: #1c93e3; color: white; font-weight: bold; border: none; cursor: pointer; }
    h2 { text-align: center; }
  </style>
</head>
<body>

<h2>Order a Product</h2>

<form id="orderForm">
  <input type="text" id="name" placeholder="Your Name" required>
  <input type="text" id="phone" placeholder="Phone Number" required>

  <select id="product" required>
    <option value="">Select Product</option>
    <option value="T-Shirt - Rs.1500|https://cdn.pixabay.com/photo/2024/05/05/05/34/ai-generated-8740242_1280.jpg">T-Shirt</option>
    <option value="Shoes - Rs.3500|https://cdn.pixabay.com/photo/2016/12/11/12/41/shoes-1899327_1280.jpg">Shoes</option>
    <option value="Watch - Rs.5000|https://cdn.pixabay.com/photo/2017/03/20/15/13/wrist-watch-2159351_1280.jpg">Watch</option>
  </select>

  <textarea id="address" placeholder="Delivery Address" required></textarea>

  <button type="submit">Place Order</button>
</form>

<script>
  const botToken = ''; // Replace with your bot token
  const chatId = '';     // Replace with your Telegram user/chat ID

  document.getElementById('orderForm').addEventListener('submit', function(e) {
    e.preventDefault();

    const name = document.getElementById('name').value.trim();
    const phone = document.getElementById('phone').value.trim();
    const selected = document.getElementById('product').value;
    const [product, imageUrl] = selected.split('|');
    const address = document.getElementById('address').value.trim();
    const timestamp = new Date().toLocaleString();

    const caption = `
🛒 *New Order Received!*

👤 *Name:* ${name}
📞 *Phone:* ${phone}
📦 *Product:* ${product}
📍 *Address:* ${address}
🕒 *Time:* ${timestamp}
    `;

    fetch(`https://api.telegram.org/bot${botToken}/sendPhoto`, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        chat_id: chatId,
        photo: imageUrl,
        caption: caption,
        parse_mode: "Markdown",
        reply_markup: {
          inline_keyboard: [
            [
              { text: "✅ Mark as Done", callback_data: "mark_done" }
            ]
          ]
        }
      })
    })
    .then(res => res.json())
    .then(data => {
      if (data.ok) {
        alert("Order submitted successfully!");
        document.getElementById('orderForm').reset();
      } else {
        console.error(data);
        alert("Telegram Error: " + data.description);
      }
    })
    .catch(err => {
      alert("Failed to send order. Check bot settings or connection.");
      console.error(err);
    });
  });
</script>

</body>
</html>
```

## Example Bot Reply
```
🛒 *New Order Received!*

👤 *Name:* THARU
📞 *Phone:* 077xxxxxx
📦 *Product:* T-shirt
📍 *Address:* Kurunegala
🕒 *Time:* 12/05/2025, 12:08
```


## License

This project is licensed under the MIT License.

---

**Made with love for small businesses.**
