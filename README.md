# GA4 Attribution UTM Injector

Automatically improves GA4 attribution by injecting missing UTM parameters before analytics loads.  
This helps reduce **Unassigned**, **Direct**, and **(not set)** traffic while preserving paid attribution.

The logic runs client-side and classifies traffic such as:

- Organic search  
- Social  
- Email  
- Messaging apps  
- AI tools (ChatGPT, Perplexity, etc.)  
- Dark social  
- Direct shares  

Paid traffic identifiers like `gclid`, `fbclid`, and `msclkid` are preserved.

---

# What This Fixes

This improves attribution for:

- Unassigned traffic  
- (not set) source / medium  
- Dark social traffic  
- Email clicks without UTMs  
- Messaging apps (Slack, WhatsApp, SMS)  
- AI tools and LLM referrals  
- iOS / Android share sheet traffic  

---

# How It Works

1. Script runs before GA4 loads  
2. Checks if UTMs already exist  
3. Checks for paid click IDs  
4. Detects referrer or missing referrer  
5. Classifies traffic source + medium  
6. Injects UTM parameters  
7. GA4 reads proper attribution  

No redirects. No reloads. No performance impact.

---

# Installation

### Step 1

Add the script from:

```
/src/ga4-attribution.js
```

into Google Tag Manager as a **Custom HTML tag**

---

### Step 2

Trigger:

```
Initialization - All Pages
```

This ensures it fires **before GA4 config tag**

---

### Step 3

Ensure tag order:

1. Attribution script  
2. GA4 config tag  
3. GA4 event tags  

---

# Example Improvements

Before:

```
Direct / (none)
Unassigned
(not set)
```

After:

```
ios_share / dark_social
chatgpt.com / ai
mail.google.com / email
reddit.com / social
google.com / organic
```

---

# Paid Traffic Protection

The script does nothing when these are present:

- gclid  
- gbraid  
- wbraid  
- fbclid  
- msclkid  
- ttclid  
- twclid  
- li_fat_id  
- any *clid  
- any *clickid  

This ensures Google Ads attribution is never overwritten.

---

# Performance

- No redirects  
- No reloads  
- No layout shift  
- Runs in <1ms  
- Uses history.replaceState  

---

# Expected Impact

Reduces:

- Unassigned traffic  
- Direct traffic  
- (not set)  

Improves:

- Dark social attribution  
- Email attribution  
- Messaging attribution  
- AI referral tracking  
- Organic vs referral accuracy  

---

# License

MIT
