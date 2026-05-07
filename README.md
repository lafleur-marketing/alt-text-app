# ALT TEXT APP — v1

A WordPress image toolkit by **LaFleur Marketing**. Browser-based, single-file HTML app that connects to any WordPress site via REST API and runs three diagnostic and repair modules powered by Claude Vision (Anthropic API).

🌐 **Live app**: https://lafleur-marketing.github.io/alt-text-app/

---

## What it does

| Module | Purpose |
|---|---|
| 🏷️ **ALT Text Generator** | Detects images in Posts, Pages, and any custom post type (incl. JetEngine CPTs) that lack ALT text. Uses Claude Vision to generate descriptive, SEO-friendly ALT text in English (max 125 chars), and writes it back via REST API. |
| 🔴 **Broken Image Detector** | Crawls all media URLs, flags 404s and connection errors. Generates a CSV report with image ID, filename, URL, status code, and which post/page uses it. |
| 📱 **Responsive Display Check** | Audits images for missing dimensions, missing `srcset` variants, oversized originals (>3000px), and hardcoded small `width` attributes inside post content. |

Each module runs independently — toggle them on/off before running. Results live in their own tab and export to CSV.

---

## How to use

### 1. Open the app
Go to https://lafleur-marketing.github.io/alt-text-app/

### 2. Get your credentials ready

You need three things:

| Field | Where to get it |
|---|---|
| **Site URL** | The full URL of the WordPress site (e.g. `https://example.com`) |
| **WordPress username** | The username you log in with (not the email) |
| **WP Application Password** | Generate at *WP Admin → Users → Profile → Application Passwords*. Format: `xxxx xxxx xxxx xxxx xxxx xxxx`. ⚠️ Shown only once — copy it immediately. |
| **Anthropic API key** | Create at [console.anthropic.com/keys](https://console.anthropic.com/keys). Format: `sk-ant-api03-...`. Required for Claude Vision. |

### 3. Choose scan mode

- **Full Site** — scans the entire Media Library.
- **By Content Type** — clicks *Detect Content Types* to auto-list all post types (Posts, Pages, JetEngine CPTs, etc.) and process only the images used in those.

### 4. Pick which modules to run, then click **Start**.

The app shows real-time progress in the activity log and a result table per tab. Each tab has its own CSV export button.

---

## Cost estimate (Anthropic API)

Using `claude-sonnet-4-6` (default), each image costs roughly **$0.004 USD**:

| Site size | Approx. cost |
|---|---:|
| 100 images | ~$0.40 |
| 500 images | ~$2.00 |
| 2,000 images | ~$8.00 |

Add Anthropic credits at [console.anthropic.com/billing](https://console.anthropic.com/billing). $5 covers a typical project.

---

## Security notes

- **The app runs 100% in your browser.** No data is sent anywhere except WordPress (your site) and Anthropic (Claude Vision).
- **No credentials are stored.** API keys, WP passwords, and URLs only live in memory while the tab is open.
- **The app cannot modify image files** — only the `alt_text` field on attachments. Reversible at any time.
- **Application Passwords are revocable** — if anything goes wrong, revoke from WP Admin → Users → Profile.

---

## Compatibility

- Any WordPress site with REST API enabled (5.6+ for Application Passwords).
- Tested on Kinsta, WP Engine, Pantheon, Cloudways, and shared hosting.
- Works with **JetEngine** custom post types (auto-detected).
- Works with multisite installs *if* the app is served from a real origin (this is why it's deployed to GitHub Pages, not run as `file://` local).
- Does **not** modify Elementor / Divi / WPBakery internal data — only standard `alt_text` and image metadata.

---

## Versions

- **v1** (May 2026) — Public release. Includes ALT Text Generator, Broken Image Detector, Responsive Check, multi-client config, JetEngine CPT auto-detection, retry logic for API rate limits, LaFleur branding.

---

## Troubleshooting

| Problem | Solution |
|---|---|
| `NetworkError` when scanning | Make sure you're using the GitHub Pages URL above, not a local file. Strict WordPress hosts reject `file://` origins. |
| `401 Unauthorized` | Username is the WP login name (not email). App Password format is `xxxx xxxx xxxx xxxx xxxx xxxx`. |
| `Overloaded` errors during ALT generation | Anthropic API congestion. The app auto-retries 3 times with backoff. If it still fails, click *Retry Failed Items* in the ALT tab after a few minutes. |
| Custom post types not detected | The site may have REST API disabled for that CPT. Add the CPT slug manually in the *Custom post type* field. |
| `model not found` from Anthropic | Your API key may be on an older account without access to `claude-sonnet-4-6`. Check console.anthropic.com → Settings. |

---

## Internal links

- 📂 Project source: `~/Projects/lafleur-kinsta/shared/alt-text-app/`
- 🐛 Issues: open at https://github.com/lafleur-marketing/alt-text-app/issues

---

Built with ☕ and ❤️ for LaFleur Marketing's client portfolio.
