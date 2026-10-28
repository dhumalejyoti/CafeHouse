# Jyoti's Cafe House — simple website

This is a lightweight single-page café website with:
- Mobile-friendly home page
- Menu cards with photos, descriptions and prices
- Zomato order buttons
- Customer reviews that remain hidden until you approve them
- Free static hosting compatibility (GitHub Pages)

## Important before publishing
The menu has now been transcribed from the Zomato screenshots supplied by the café owner. Prices and visible item names have been added, and the supplied product photos are stored in `assets/`. A few screenshot descriptions were clipped and shortened; some drink photos may be approximate because the supplied product-photo set does not clearly label every drink.

## Connect review storage (Supabase free tier)
1. Create a project at https://supabase.com/.
2. Open **SQL Editor**, paste the contents of `supabase_setup.sql`, and run it.
3. Go to **Project Settings → API** (or the API keys page in the current dashboard).
4. Copy the Project URL and the public `anon` / publishable key.
5. In `index.html`, replace:
   - `PASTE_YOUR_SUPABASE_PROJECT_URL_HERE`
   - `PASTE_YOUR_SUPABASE_ANON_KEY_HERE`
6. Do **not** put a `service_role` key in the website.

### Approve customer reviews
1. Open Supabase → Table Editor → `cafe_reviews`.
2. Check new submissions where `approved` is `false`.
3. Change `approved` to `true` only for reviews you want displayed.
4. The website displays approved reviews and their average rating.

The SQL uses row-level security: public visitors can read approved reviews and insert pending reviews, but cannot approve, edit, or delete them.

## Publish free with GitHub Pages
1. Create/sign in to a GitHub account.
2. Create a public repository, e.g. `jyotis-cafe-house`.
3. Upload `index.html` and `supabase_setup.sql` (the SQL file is for your setup; it need not be on the website).
4. In repository **Settings → Pages**, choose deploy from the `main` branch and `/ (root)`.
5. GitHub will show a free `https://YOUR-USERNAME.github.io/jyotis-cafe-house/` address.
6. Test the website on a phone and scan the QR code generated for that exact address.

## QR code for packaging
After publishing, generate a QR code that points to:
`https://YOUR-USERNAME.github.io/jyotis-cafe-house/#reviews`
Use the final live URL before printing stickers. If you rename the repository or change the published address later, the QR code may need reprinting.

## Photos
The website uses the food photos supplied in the uploaded ZIP, stored in `assets/`. Some milkshake photos are reused where an exact drink-photo match was not clear.

## Note
The Supabase free tier's limits and policies can change. For a small home café, it is usually enough to get started, but check current limits in your account.
