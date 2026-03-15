# GTM Advanced Attribution Script

## Overview

This repository contains a **Custom HTML script for Google Tag Manager (GTM)** that captures advanced attribution across all traffic channels. It tracks both **session-level** and **first-touch attribution**, including:

- Email campaigns
- Messaging apps (WhatsApp, Slack, Discord, iMessage, etc.)
- AI / LLM traffic (ChatGPT, Claude, Perplexity, etc.)
- Developer and community traffic (GitHub, StackOverflow, HackerNews, Product Hunt)
- Organic search
- Referral traffic

The script is **fully ES5-compatible**, safe for any GTM implementation, and does **not interfere with existing dataLayer keys or tags**. Paid traffic (gclid, fbclid, and other ad parameters) is ignored to preserve clean attribution.

---

## Features

- Session-level and first-touch attribution tracking
- Channel classification: organic, social, email, messaging, AI, developer/community, referral
- Safe for GTM: all keys are prefixed with `attr_`
- Stores session attribution in `sessionStorage` and first-touch in `localStorage`
- Optional hash-based UTM detection for copied links
- Fully ES5-compatible for browser and GTM support

---

## Setup Instructions

### 1. Add the Custom HTML Tag

1. In GTM, go to **Tags → New → Custom HTML**  
2. Paste the **ES5 attribution script** from this repository  
3. Set **Trigger → All Pages → Initialization**  
4. Save and publish the tag  

> This ensures the script runs early on every page and computes attribution correctly.

---

### 2. Set up the GA4 Event Tag

1. **Tag Type:** GA4 Event  
2. **Configuration Tag:** Select your main GA4 Configuration tag  
3. **Event Name:** `attr_attribution_ready`  
4. **Trigger:** Custom Event → Event name = `attr_attribution_ready`  
5. **Event Parameters:** Map dataLayer keys as follows:

| GA4 Event Parameter | dataLayer Variable |
|--------------------|------------------|
| session_source      | attr_session_source |
| session_medium      | attr_session_medium |
| session_campaign    | attr_session_campaign |
| first_source        | attr_first_source |
| first_medium        | attr_first_medium |
| first_campaign      | attr_first_campaign |

6. Save and publish the tag  

> This ensures GA4 captures both **session** and **first-touch attribution** after the Custom HTML script runs.

---

### 3. Optional Notes

- Prefixed keys (`attr_`) prevent conflicts with existing GTM or dataLayer variables.  
- Paid traffic is ignored, ensuring clean first-touch and session attribution for organic and other channels.  
- Messaging app traffic is detected using user agent fingerprinting for iOS and Android apps.  
- The script handles URL hash-based UTMs for links shared via copy/paste.  

---

## Example Workflow

1. User lands on your site via a shared link in WhatsApp, Slack, or email  
2. Custom HTML script runs → detects source and medium based on referrer or link  
3. Session and first-touch attribution are stored in **sessionStorage** and **localStorage**  
4. Script pushes `attr_attribution_ready` to the dataLayer  
5. GA4 Event Tag triggers on `attr_attribution_ready` → records all `attr_` parameters  

---

## Browser & GTM Compatibility

- Fully compatible with GTM Custom HTML tags  
- Works in all modern browsers (Chrome, Firefox, Safari, Edge)  
- ES5 syntax ensures **no issues with older GTM engines**  

---

## License

MIT License – free to use and modify for your projects.
