# Jyoti's Cafe House — single-page website + owner dashboard

## What is included
- One `index.html` for the public café website and private owner dashboard (`#admin`); there is no separate admin page.
- Actual menu list and prices restored from the earlier version, with the supplied food photos in `assets/`.
- Supabase is the source of truth for menu records and customer reviews.
- Visitors can submit reviews; they stay pending until the owner approves them.
- Owner can select multiple pending reviews and approve or reject them in bulk.

## Setup
1. Create a free Supabase project.
2. In Supabase SQL Editor, run `supabase_setup.sql` once.
3. In Supabase Project Settings → API, copy the Project URL and public anon/publishable key.
4. Edit `index.html` and replace `PASTE_YOUR_SUPABASE_PROJECT_URL_HERE` and `PASTE_YOUR_SUPABASE_ANON_KEY_HERE`. Do not use a `service_role` or secret key.
5. In Supabase Authentication → Users, create the owner login using an email you control and a strong unique password.
6. Copy the user's UUID, then run in SQL Editor: `insert into public.cafe_review_admins(user_id) values ('YOUR-AUTH-USER-UUID');` using the actual UUID.
7. Upload `index.html`, `supabase_setup.sql` (optional to publish), and the entire `assets/` folder to the root of the same GitHub repository. Keep `assets/` alongside `index.html` so the real food photos load.
8. Open the published site and test menu/review submission. For the owner dashboard, open the same site and click **Owner login** (or append `#admin` to the URL).

## Menu images
The food photos are local files in `assets/`. Menu names, prices, descriptions, image paths, availability and order are read from Supabase `cafe_menu_items` table. If you rename an asset file, update its `image_url` in Supabase too.

## Security
- Only the public anon/publishable key belongs in the website.
- Supabase RLS keeps pending reviews hidden from the public and allows only UUIDs listed in `cafe_review_admins` to approve/reject reviews.
- Do not use the sample test password from chat as a permanent password.

## Zomato
Order link: https://zomato.onelink.me/xqzv/ffnzlzh7
