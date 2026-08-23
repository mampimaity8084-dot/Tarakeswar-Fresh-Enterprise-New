TARAKESWAR FRESH FISH — RAZORPAY STANDARD CHECKOUT
==================================================

Already added to this package:
1) netlify/functions/create-order.js
2) netlify/functions/verify-payment.js
3) netlify.toml
4) Razorpay Checkout flow in index.html

SECURITY
--------
Never put RAZORPAY_KEY_SECRET inside index.html or any browser JavaScript.
The site reads Razorpay credentials only from Netlify Environment Variables.

Required Netlify Environment Variables:
RAZORPAY_KEY_ID
RAZORPAY_KEY_SECRET

DEPLOY
------
Upload this entire project folder/ZIP to the SAME Netlify project where those variables are configured.
After deploy, check Netlify -> Functions. You should see:
- create-order
- verify-payment

TEST
----
1. Open customer site.
2. Add a product -> Checkout / Order.
3. Choose COD + Advance or Full Online.
4. Tap Pay & Confirm Order.
5. Razorpay Standard Checkout should open.
6. Complete a Razorpay TEST payment.
7. Only after server-side signature verification will the Supabase order be created and the Order Confirmed screen appear.
8. If payment is cancelled/failed, no Supabase order is placed and no WhatsApp confirmation is produced.

IMPORTANT
---------
You are currently using Razorpay TEST keys, so this package is for testing until you replace them with LIVE keys in Netlify.
Razorpay-enabled payment methods (UPI/cards/netbanking/wallets etc.) depend on what Razorpay enables for your account.
