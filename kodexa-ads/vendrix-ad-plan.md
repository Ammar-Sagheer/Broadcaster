# Vendrix marketplace ad: full setup (Kodexa)

Everything needed to run the Meta ad for the Vendrix marketplace video.

---

## 1. Files (one ad, two versions)

| File | Size | Where it goes |
|---|---|---|
| `ad-market-4x5.mp4` | 4:5, 1080×1350, 17.7 s | **Feeds** (Facebook + Instagram). The reel plays inside a phone, next to "Your own Daraz-style marketplace" and 3 benefits. |
| `ad-market-9x16-safe.mp4` | 9:16, 1080×1920, 17.7 s | **Reels, Stories, Status.** The captions sit in the middle of the screen so Facebook's buttons can't cover them. It ends on the ad end card ("Get a quote in 2 minutes"). |

- **Organic reel** (for normal posting, not the ad): `vendrix.mp4`
- **Music:** an original track (Insomnia-style club beat, 128 BPM), made for this video. It's copyright-safe to boost and use in ads.

---

## 2. Before you start (important)
- [ ] **Fix the dead "Add to Cart" button** in the Today's Deals section on vendrixx.vercel.app. It has no action wired to it, and people from the ad will tap it.
- [ ] Make sure WhatsApp **+92 339 0391420** is linked to the Facebook Page (Page settings → Linked accounts → WhatsApp).
- [ ] Keep the phone nearby. Reply to every chat within 1 hour.

---

## 3. Campaign type

### Recommended: WhatsApp messages
A marketplace is an expensive project, so people want to talk before they buy. A WhatsApp chat is a stronger lead than a website visit, and it's cheap in Pakistan.

### Campaign level
| Setting | Value |
|---|---|
| Setup | **Manual** (not Recommended) |
| Objective | **Engagement** |
| Campaign name | Kodexa · Marketplace · WhatsApp |
| Special ad categories | None |
| Advantage campaign budget | **Off** (the budget is set on the ad set) |

### Ad set level
| Setting | Value |
|---|---|
| Conversion location | **Messaging apps → WhatsApp** (+92 339 0391420) |
| Performance goal | Maximise number of conversations |
| Budget | **Rs 500/day for 5 days** (minimum test: Rs 350/day for 3 days) |
| End date | set one (5 days from start) |
| Location | **Lahore, Karachi, Islamabad** (remove "Pakistan") |
| Age | 24 to 50 |
| Audience | Advantage+ audience, with suggestions: *small business owners, e-commerce, online shopping, Daraz, Shopify, entrepreneurship, retail* |
| Placements | Advantage+, or Manual with **Audience Network unticked** |

**WhatsApp greeting message** (message template):
```
Assalam o Alaikum! 👋 Kodexa here. Aap ko marketplace chahiye ya online store? Apna business batayein, hum demo aur fixed price bhejte hain.
```

### Alternative: send people to the website (Traffic)
Use this if you'd rather get website visits, like the first ad:
- **Objective:** Traffic
- **Conversion location:** Website
- **Performance goal:** **Landing page views** (not link clicks)
- **Pixel:** Kodexa Pixel (1824366032179710)
- **CTA:** Get quote
- **URL:** section 5
- Same budget, location, age, audience and placements as above

---

## 4. Ad level (step by step)
1. **Create ad → Manual upload → Single image or video.** **Untick "Multi-advertiser ads".**
2. **Media:**
   - Upload **`ad-market-4x5.mp4`** first.
   - In the crop / **Edit placements** step, click **Replace** on the **Vertical (9:16)** slot and choose **`ad-market-9x16-safe.mp4`**. Don't crop the 4:5.
   - Keep Square/Horizontal as Original. Ignore the horizontal warning.
3. **Image generation:** select **none** (the AI images had garbled text).
4. **Enhancements:** switch **everything OFF**:
   - Video touch-ups
   - Text improvements
   - Add details to ad layout
   - Essential enhancements (Relevant comments, Enhance CTA, Show spotlights, etc.)
   - Ignore the "Apply now / +2 points" nags. They switch Flexible media back on.
5. **Text:** add all 3 primary texts, then the headline, description and CTA below.
6. **Preview:** check the per-placement list. **Feeds** should show the beige 4:5 video; **Reels/Stories** the dark 9:16 video. The small preview panel sometimes wrongly shows the 9:16 in Feed. Trust the per-placement list, or use Share → preview on your phone.
7. **Publish.**

---

## 5. Ad copy (ready to paste)

**Primary text 1:**
```
Daraz jaisa apna marketplace? Humne bana ke dikha diya. ⚡

Bohat se sellers, ek website: deals with countdown, coupon codes, wishlist aur har seller ki apni shop.

Live demo dekhein, phir WhatsApp karein. Fixed price pehle, kaam baad mein.
```

**Primary text 2:**
```
We built a full electronics marketplace. ⚡
Many sellers, one store: live deals, coupons, wishlist and vendor shops with ratings.

Want one for your business? Get a fixed quote in 2 minutes.
```

**Primary text 3:**
```
Sirf online store nahi, poora marketplace. 🏪
Sellers apni shop khud chalate hain, aap commission kamate hain.

Kodexa design se launch tak sab banata hai. Aaj hi WhatsApp karein.
```

- **Headline:**
  ```
  Your own Daraz-style marketplace
  ```
- **Description:**
  ```
  Fixed price before we start
  ```
- **CTA button:**
  - WhatsApp campaign: **Send WhatsApp message**
  - Traffic campaign: **Get quote**
- **Website URL (Traffic campaign only):**
  ```
  https://kodexa.store/services/online-store?utm_source=meta&utm_medium=paid&utm_campaign=marketplace&utm_content=vendrix_video
  ```
- **Display link:** `kodexa.store`
- **Browser add-on:** None (the site has its own WhatsApp button)
- **Tracking:** Website events on with the Kodexa Pixel. Leave URL parameters empty; the UTMs are already in the link.

---

## 6. Checking results (after 3 days)
| Metric | Good | Action if bad |
|---|---|---|
| Cost per WhatsApp conversation | under Rs 150 | over Rs 300: change the hook or the audience |
| 3-second video views ÷ impressions | above 30% | below 20%: the first 2 seconds aren't stopping the scroll, so try a new hook |
| Link CTR (Traffic campaign) | above 1% | below 0.5%: change the primary text |
| Cost per landing page view (Traffic) | under Rs 15 | check the placements; turn off Audience Network |

- Pause the ad if it spends about **Rs 1,500 with zero conversations**.
- If it works: duplicate the ad set and raise the budget by about 20% every 2 days (not all at once).
- Reply fast. Meta ranks messaging ads lower when replies are slow.

---

## 7. Organic post (for the Page, separate from the ad)
Post `vendrix.mp4` as a **Reel** from the Kodexa page (the music is already inside).

**Description:**
```
We built a full electronics marketplace. ⚡

Vendrix is a multi-vendor store where many sellers sell on one website, like Daraz or Amazon:
📱 Shop by category and brand
🏷️ Featured, New Arrivals and On Sale in one tap
⏳ Live deals with a countdown timer
🎟️ Coupon codes, copied in one tap
🛒 Cart, wishlist and product compare
🏪 Sellers get their own shop page, ratings and sales

Want a marketplace or an online store for your business? We build it end to end.

💬 WhatsApp: +92 339 0391420
🌐 www.kodexa.store
🔗 Live demo: vendrixx.vercel.app

#Kodexa #Marketplace #OnlineStore #Ecommerce #WebDevelopment #MultiVendor #SmallBusinessPakistan #Pakistan
```

**First comment (pin it):**
```
Apna marketplace ya online store chahiye? "MARKETPLACE" likh ke WhatsApp karein: +92 339 0391420, hum free demo dikhayenge 👋
Live demo: vendrixx.vercel.app · www.kodexa.store
```

**Posting tips:**
- **Cover image:** the "We built a full electronics marketplace ⚡" hook frame, or the blue Deals countdown.
- **Timing:** weekday evening, 8 to 10 pm Pakistan time.
