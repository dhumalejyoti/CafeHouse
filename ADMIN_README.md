# Jyoti's Cafe House — owner review admin page

The `admin.html` page provides Supabase email/password login, a pending-review queue, selection checkboxes, bulk approve, bulk reject, approve-all-pending and reject-all-pending. Reject means permanently delete.

## Setup (do this before using the page)

1. In Supabase, open **Authentication → Users** and create the owner's account with an email and strong password. If email confirmation is enabled, confirm the account before signing in.
2. In **Project Settings / API**, copy the Project URL and public publishable key (or legacy `anon` key). Never use `service_role` or a secret key in frontend files.
3. Edit **both** `index.html` and `admin.html` and replace `PASTE_YOUR_SUPABASE_PROJECT_URL_HERE` and `PASTE_YOUR_SUPABASE_ANON_KEY_HERE` with those same public values.
4. Open **SQL Editor** and run all of `admin_setup.sql`.
5. In **Authentication → Users**, copy the owner's UUID. In SQL Editor, run this with the actual UUID:

   ```sql
   INSERT INTO public.cafe_review_admins (user_id)
   VALUES ('PASTE-THE-REAL-AUTH-USER-UUID-HERE');
   ```

   Do not leave the placeholder UUID. Only add trusted owner/admin accounts to this table.
6. Upload/commit `admin.html` and `admin_setup.sql` to the same GitHub Pages repository as `index.html`, at the repository root. Ensure `index.html` and `admin.html` use the same Supabase URL and public key.
7. Open `https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/admin.html` and sign in with the owner Auth account. Do not link this admin page prominently on the public café site.
8. Submit a test review from the public website. It should appear in the admin queue as pending. Approve it and verify it appears on the public site. Test reject only with a disposable test review.

## Security notes

- Authentication alone is not enough; the `cafe_review_admins` allowlist and row-level security policies are what authorize moderation.
- The `admin_setup.sql` policies assume the original public policies in `supabase_setup.sql` are in place. Visitors can still insert only pending reviews and read approved reviews; only allowlisted authenticated users can see all reviews, update approval, or delete.
- Do not expose a service-role/secret key in HTML, JavaScript, GitHub, or QR codes.
- Bulk reject permanently deletes the selected pending rows. Bulk actions require confirmation.
- Use a strong unique password, and never share the admin URL credentials with customers.
