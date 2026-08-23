TARAKESWAR FRESH FISH — V6 FINAL LAUNCH
========================================

WHAT THIS BUILD DOES
--------------------
1. Customer, Admin and Delivery continue to use the same old Supabase project.
2. Legacy V4/V4.3/V5/V5.1/V5.2 runtime scripts are bundled into ONE runtime file and loaded once.
3. Existing customer AI, visual search, smart reorder, partner/family, automation, payment and delivery layers are retained.
4. AI Product Studio lets Admin upload a product photo and get an editable Bengali catalog draft.
5. AI Product Studio can save an approved product to Supabase fish table.
6. Customer AI can return safe add-to-cart actions. Payment/refund/cancellation remain confirmation-controlled.
7. Browser Bengali voice input is available for AI ordering where supported by the browser.
8. Customer fish/offers/order views continue to use Supabase Realtime where the project has Realtime enabled.
9. Backup/Restore and WhatsApp functions remain server-side and require Admin authentication.
10. Transparent logo asset remains the canonical logo.

IMPORTANT: AI PRICE SAFETY
--------------------------
A product photo cannot reliably tell the exact selling price. AI therefore suggests name/category/description and only uses price/stock hints supplied by Admin. Admin must approve price and stock before saving.

NETLIFY ENVIRONMENT VARIABLES
-----------------------------
Required for backend:
SUPABASE_URL
SUPABASE_SERVICE_ROLE_KEY
ADMIN_EMAILS

Razorpay:
RAZORPAY_KEY_ID
RAZORPAY_KEY_SECRET

AI:
OPENAI_API_KEY
OPENAI_MODEL=gpt-5.6-luna

WhatsApp (optional until Meta setup is complete):
WHATSAPP_ACCESS_TOKEN
WHATSAPP_PHONE_NUMBER_ID
WHATSAPP_GRAPH_VERSION
WHATSAPP_GROUP_ID

Push (optional):
VAPID_PUBLIC_KEY
VAPID_PRIVATE_KEY
VAPID_SUBJECT

DO NOT put service role, Razorpay secret, OpenAI key or WhatsApp access token in browser files.

SUPABASE STEPS
--------------
1. Keep the existing Supabase project.
2. Run the existing V5/V5.3 migration/setup files that your current project already uses.
3. Then run V6_MASTER_MIGRATION.sql once.
4. Confirm Storage bucket product-images exists and is public for read.
5. Authentication -> URL Configuration: add the NEW Netlify site URL and its admin.html/delivery.html redirect URLs as required by your login flow.
6. Keep RLS enabled. Backend service role is only used by Netlify Functions.

NEW NETLIFY DEPLOY
------------------
1. Extract this ZIP.
2. Deploy the extracted root folder to the new Netlify project.
3. Add the environment variables above.
4. Redeploy after environment variables are saved.
5. Open /, /admin.html and /delivery.html.
6. Test Admin login first.

FIRST TEST ORDER
----------------
Customer -> product -> Add -> Checkout -> Razorpay test -> verify-payment -> Admin order -> Delivery queue -> OTP -> Delivered.

AI PRODUCT STUDIO
-----------------
Admin -> AI Product Studio -> upload photo -> Analyze & Draft -> review/edit price/stock -> Approve & Save.
For many products, use the CSV template as a bulk starting point. Product photos can be added/updated after the catalog data is approved.

AUTOMATION PRINCIPLE
--------------------
Realtime is preferred over blind 5-10 second page reloads. Sensitive actions remain approval controlled. Failed integrations should show an exception message rather than silently pretending success.

KNOWN EXTERNAL DEPENDENCIES
---------------------------
- Razorpay account/configuration
- Supabase Realtime/Auth/Storage/RLS configuration
- OpenAI API key and billing/quota
- Meta WhatsApp Business/Cloud API eligibility and credentials
- Browser support for SpeechRecognition
- Device permission for Delivery GPS
- Network connectivity
