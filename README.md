# Jyoti's Cafe House — single-page website + owner dashboard

## What is included
- One `index.html` for the public café website and private owner dashboard (`#admin`); there is no separate admin page.
- Actual menu list and prices restored from the earlier version, with the supplied food photos in `assets/`.
- Supabase is the source of truth for menu records and customer reviews.
- Visitors can submit reviews; they stay pending until the owner approves them.
- Owner can select multiple pending reviews and approve or delete them in bulk (delete is permanent).

## Setup
1. Create a free Supabase project.
2. In Supabase SQL Editor, run `supabase_setup.sql` once.
3. In Supabase Project Settings → API, copy the Project URL and public anon/publishable key.
4. Put the Project URL and public anon/publishable key in `config.js` (not `index.html`). Never use a `service_role` or secret key. Optionally add hours, address, phone and WhatsApp there too.
5. In Supabase Authentication → Users, create the owner login using an email you control and a strong unique password.
6. Copy the user's UUID, then run in SQL Editor: `insert into public.cafe_review_admins(user_id) values ('YOUR-AUTH-USER-UUID');` using the actual UUID.
7. Upload `index.html`, `config.js`, and the entire `assets/` folder (`supabase_setup.sql` is optional) to the root of the same GitHub repository. Keep `assets/` alongside `index.html` so the real food photos load.
8. Open the published site and test menu/review submission. For the owner dashboard, open the same site and click **Owner login** in the footer (or append `#admin` to the URL).

## Menu images
The food photos are local files in `assets/`. Menu names, prices, descriptions, image paths, availability and order are read from Supabase `cafe_menu_items` table. If you rename an asset file, update its `image_url` in Supabase too.

## Security
- Only the public anon/publishable key belongs in the website.
- Supabase RLS keeps pending reviews hidden from the public and allows only UUIDs listed in `cafe_review_admins` to approve/reject reviews.
- Do not use the sample test password from chat as a permanent password.

## Zomato
Order link: https://zomato.onelink.me/xqzv/ffnzlzh7

## Day-to-day
- Change a price, mark something sold out (`is_available` = false) or reorder (`sort_order`) in Supabase → Table Editor → `cafe_menu_items`. No code changes needed.
- If Supabase is unreachable, the site shows a built-in copy of the menu from `index.html`.
- Re-running `supabase_setup.sql` is safe; it no longer overwrites menu edits.

## Known to-do
Mango and Strawberry Milkshake currently reuse the pineapple and Oreo photos. Add real photos to `assets/` and update their `image_url` in Supabase.
