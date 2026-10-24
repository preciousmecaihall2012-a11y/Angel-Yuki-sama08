# Yuki Archive ♡

A coquette-blue, AO3-inspired fanfiction website starter with a profile and skin customization studio. This version is immediately testable in your browser and includes:
- Browse/search demo stories
- Publish demo stories and chapters
- Read works and add comments
- Kudos and bookmarks
- Author profile page
- Blue, rose, lavender, and midnight themes
- Browser-saved theme preferences and demo content
- Profile picture and banner uploads (image resized in-browser)
- Profile bio and decorative sticker styles
- Optional site background image and custom CSS with a live profile preview
- Guest mode: guests can publish demo works but have no edit/recovery rights
- Google sign-in integration scaffold using Supabase Auth

## Try it locally now
1. Download and unzip this folder.
2. Open `index.html` in a modern browser.
3. Try Browse, Post a story, Read & comment, Bookmark, and Skin studio.

**Demo limitation:** Without backend configuration, posts/comments/bookmarks are stored only in the current browser's local storage. Guest mode is temporary; refreshing or leaving ends the guest session. Guest-published works have no edit/recovery feature. The Google button intentionally opens setup guidance instead of pretending to authenticate. No Google password is ever requested or stored by this app.

## Publish the static demo on GitHub Pages
1. Create a public repository on https://github.com/new (e.g. `yuki-archive`).
2. Upload `index.html`, `styles.css`, `app.js`, and `README.md` to the repository root.
3. In the repository, open Settings → Pages.
4. Choose “Deploy from a branch”, select `main` and `/(root)`, then Save.
5. Wait for the Pages URL to appear.

GitHub Pages hosts the front end only. It does not provide user accounts, shared data, or a database.

## Enable real Google login (free Supabase setup)
You need to create your own Supabase project and Google OAuth credentials. Never paste a Google client secret into front-end code.

### A. Create a Supabase project
1. Go to https://supabase.com and create a project.
2. In Project Settings → API, copy the Project URL and the publishable/anon key.
3. In `app.js`, fill in `SUPABASE_URL` and `SUPABASE_ANON_KEY` near the top. The publishable/anon key is designed for front-end use only when your database has correct Row Level Security (RLS) policies. Never use a service-role key in the browser.

### B. Configure Google as an OAuth provider
1. In Supabase, open Authentication → Sign In / Providers → Google and follow the current setup instructions.
2. In Google Cloud Console, create/configure an OAuth client for a Web application. Add the callback URL shown by Supabase to the Google OAuth client's Authorized redirect URIs.
3. In Supabase Authentication → URL Configuration, set the Site URL to your deployed GitHub Pages URL. Add that URL (and your local test URL if applicable) to the allowed Redirect URLs.
4. Save and test “Continue with Google”.

OAuth setup screens change over time; follow the callback URL and instructions shown in your own Supabase dashboard. Do not share client secrets.

## Important next engineering step: real shared stories
This starter uses local storage for stories, comments, kudos, and bookmarks. For a public community, create Supabase tables for profiles, works, chapters, comments, kudos, bookmarks, and follows. Enable RLS on every user-owned table. Enforce that only a signed-in author can create/update/delete their own works; only signed-in users can comment; validate ratings/tags and add rate limits/moderation. Do not expose private emails or secrets in public profiles.

The provided Google sign-in scaffold handles OAuth identity/session, but it does **not yet sync stories or comments to Supabase**. Don't advertise this as a fully multi-user archive until the database schema, RLS policies, and shared CRUD operations are implemented and tested.

## Suggested next steps
1. Set up real Google sign-in.
2. Create profile/work/chapter/comment tables and RLS policies.
3. Sync works, comments, kudos, bookmarks, and profiles with Supabase.
4. Add report/block/moderation tools and clear content-rating/warning requirements.
5. Implement secure custom skins. If you later allow custom CSS, sandbox and sanitize it; never let arbitrary user HTML run in other users' browsers.


## Profile and skin studio
Open **My profile → Decorate profile** to upload a profile picture and banner, set a bio, choose decorative stickers, add a background photo, or write custom CSS. The profile studio previews the banner/avatar and saves choices in the same browser. In this static demo, uploaded images and customizations are not uploaded to a shared server and will not follow you to another device. Use trusted CSS only. The CSS is inserted as CSS only; HTML and JavaScript are not executed.
