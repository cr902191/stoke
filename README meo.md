# STOKE — setup guide

This is a static site (`index.html`) with a real, working cart and checkout built in via **Snipcart** — no backend or server code needed, so it works directly on GitHub Pages.

## What's already working
- Add to bag / cart drawer / quantity editing
- Checkout flow (address, shipping, payment)
- Order confirmation emails
- The 4 products are wired up with real prices ($34 / $89 / $58 / $42)

## What you need to do before it processes real orders

### 1. Create a free Snipcart account
Go to https://app.snipcart.com/register and sign up. You start in **test mode** automatically — you can click through the whole cart/checkout flow with fake card numbers before anything is live.

### 2. Get your API key and drop it in
In the Snipcart dashboard: **Store Configuration → API Keys**, copy the **Public Test API Key**.

In `index.html`, find this line near the bottom:
```html
<div hidden id="snipcart" data-config-modal-style="side" data-api-key="YOUR_SNIPCART_PUBLIC_API_KEY"></div>
```
Replace `YOUR_SNIPCART_PUBLIC_API_KEY` with the key you copied.

### 3. Connect a payment processor
Still in the Snipcart dashboard: **Store Configuration → Payment**. Connect **Stripe** or **PayPal** (both take a few clicks, no code). This is what actually charges the customer's card.

### 4. Set up shipping and tax
**Store Configuration → Shipping** — set a flat rate, free-shipping threshold, or connect a carrier.
**Store Configuration → Taxes** — set rates for wherever you're shipping from/to.

### 5. Add product photos
Right now the product cards use custom illustrations, not photos. When you have real photos (from your supplier or your own shoot), drop them into an `/images` folder in this repo and update the `data-item-image` attribute on each button in `index.html` to point to the file, e.g.:
```html
data-item-image="images/pocket-ember.jpg"
```

### 6. Go live
When you're ready to accept real payments, switch to your **Live** API key (same place you got the test one) and swap it into `data-api-key`.

## Deploying to GitHub Pages
1. Push this repo to GitHub.
2. Repo → **Settings → Pages** → set source to your main branch, root folder.
3. Your site will be live at `https://<your-username>.github.io/<repo-name>/`.

## Adding suppliers later
When you connect a real supplier (dropshipping app, manual fulfillment, etc.), you only need to update the four products' `data-item-*` attributes in `index.html` (price, name, description, image) or add new product cards using the same pattern — the cart and checkout logic doesn't change.

## Costs to know about
Snipcart is free to test. Once live, they take a small percentage per transaction (check current pricing at snipcart.com/pricing) — separate from whatever Stripe/PayPal charges for processing.
