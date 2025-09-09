# APB Promo Block (Test Build)

A minimal, dependency-free **WordPress plugin** used for testing how a custom promo block behaves on real posts.  
It automatically appends your hand-crafted HTML under single posts, safely stores that HTML in **Base64** (to survive WAF/ModSecurity filters), and wires up **copy-to-clipboard** buttons for promo codes. Designed to be small, transparent, and easy to tweak.

---

## Why this exists

When you store raw HTML inside `wp_options`, many hosts run filters that silently strip or empty the content. That makes it hard to run realistic UI tests on production-like data.  
**APB Promo Block** stores the HTML as Base64 in the options table, decodes it at render time, and leaves your exact markup intact. Result: deterministic tests with your real layout and styles.

---

For a concrete, production-like layout and structure, see a working page in the wild: https://all-promokod-bonus.ru/promokody/on-x-casino-promokod-i-bonusy

## Features

- **Auto-append under single posts** (toggleable in settings).
- **Admin settings page** with Base64 storage of raw HTML (WAF-friendly).
- **Per-card copy buttons**: add `<button class="apb-copy" data-code="PROMO_CODE">…</button>` next to the promo code line; the JS binds automatically.
- **Default promo fallback** via settings if a button has no `data-code`.
- **Shortcode** for manual placement: `[apb_promo_block]`.
- **No external dependencies**: vanilla JS + a tiny CSS file.
- **Theme-agnostic**: styles are scoped to the plugin wrapper.

> Example card pattern we test with: Logo → “Overview” pill → perks → line  
> `Promo code: PROMO_CODE` **+** a **Copy** button placed right after the code for clarity.

---

## Quick start

1. Copy the folder `apb-promo-block/` into `wp-content/plugins/`.
2. Activate **APB Promo Block** in **WP Admin → Plugins**.
3. Go to **Settings → APB Promo Block**.
4. Paste your HTML block into the textarea and set a default promo (e.g., `PROMO_CODE`).
5. Open any single post on the front end and verify the block is appended.

> If you prefer manual placement, disable auto-append and put the shortcode  
> wherever you need it: `[apb_promo_block]`.

---

## Example HTML you can paste


<section class="apb-grid">
  <article class="apb-card">
    <div class="apb-card__head">
      <div class="apb-card__logo">
        <img src="" alt="BRAND" loading="lazy">
      </div>
      <a class="apb-chip apb-chip--brand" href="" rel="nofollow">Overview</a>
    </div>
    <h3 class="apb-card__title">BRAND</h3>
    <ul class="apb-card__perks">
      <li>🎁 100% bonus</li>
      <li>🎰 100 spins</li>
    </ul>
    <div class="apb-card__code">
      Promo code: <b>PROMO_CODE</b>
      <button class="apb-copy" type="button" data-code="PROMO_CODE" aria-label="Copy promo code">Copy</button>
    </div>
  </article>
  <!-- Duplicate <article> for other brands; change logo/link as needed -->
</section>
