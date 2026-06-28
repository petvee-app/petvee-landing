# CLAUDE.md — PetVee Landing Page 2026 Redesign
# For use with Claude Code (terminal)
# Repo: github.com/petvee-app/petvee-landing
# Deploy: GitHub Pages → petvee.app

---

## TASK

Completely redesign `index.html` to match the June 2026 app design refresh. The landing page must feel like a natural extension of the app — same colors, same typography, same design language. All CSS and JS must be inline (single HTML file). Push changes to `main` branch.

## CRITICAL CONSTRAINTS

- **DO NOT MODIFY**: `privacy.html`, `terms.html`, `CNAME` (contains `petvee.app`)
- **Single HTML file**: All CSS and JS inline — no build tools, no npm, no frameworks
- **External CDN allowed**: Google Fonts (Be Vietnam Pro), AOS (animate-on-scroll), Lucide Icons
- **Static hosting**: GitHub Pages — no server-side code
- **Mobile-first responsive**: Must look great on phone (375px), tablet (768px), and desktop (1440px)
- **Vietnamese primary language**: All copy in Vietnamese, diacritics must render correctly
- **Performance**: Lazy-load images below the fold, hero images eager. Target <3s first paint on 3G

---

## REPO STRUCTURE

```
petvee-landing/
├── index.html          ← REWRITE THIS (the main deliverable)
├── privacy.html        ← DO NOT MODIFY
├── terms.html          ← DO NOT MODIFY
├── CNAME               ← DO NOT MODIFY (contains: petvee.app)
├── CLAUDE.md           ← This file (spec reference)
├── README.md           ← Update briefly
└── images/
    ├── screenshot-home.png   ← App screenshot for hero (already cropped)
    └── mascots/              ← Transparent PNG mascot images
        ├── hero-duo.png
        ├── hero-duo-alt.png
        ├── mochi-worried.png
        ├── mochi-nighttime.png
        ├── mochi-confused.png
        ├── drvee-confident.png
        ├── mochi-relieved.png
        ├── feat-scanner.png
        ├── feat-chatbot.png
        ├── feat-checkin.png
        ├── feat-vaccine.png
        ├── feat-nutrition.png
        ├── feat-community.png
        ├── mochi-royal.png
        ├── celebration-highfive.png
        ├── banner-appstore.png
        └── gamify-streak.png
```

---

## COLOR SYSTEM (matches app exactly)

```css
/* ── Light mode ── */
--bg-cream:       #FFFAF3;    /* Page background */
--bg-white:       #FFFFFF;    /* Cards */
--bg-warm:        #FFF5EB;    /* Warm accent sections */

--text-heading:   #2D1B0E;    /* Dark warm brown headings */
--text-body:      #5C4033;    /* Body text */
--text-muted:     #A0785A;    /* Captions */

--orange-primary:  #FF6B35;   /* Primary brand */
--orange-light:    #FF8C42;   /* Gradient start */
--orange-lighter:  #FFAB76;   /* Gradient end */
--orange-bg:       #FFF1E6;   /* Orange tint bg */

--green-success:   #00B894;   /* Health/success */
--purple-premium:  #6C5CE7;   /* AI/premium */
--blue-info:       #0984E3;   /* Info */
--yellow-streak:   #FFD93D;   /* Gamification */
--red-alert:       #E74C3C;   /* Danger */

/* ── Dark sections (Problem, Pricing, Footer) ── */
--dark-navy:       #1A1A2E;   /* Dark background base */
--dark-card:       #2D2D44;   /* Dark card/header */
--dark-deep:       #0D1B2A;   /* Deepest dark */
--dark-gradient:   linear-gradient(135deg, #2D1B4E 0%, #1A1A2E 50%, #0D1B2A 100%);

/* ── Bento card colors (from app) ── */
--bento-mint:      linear-gradient(145deg, #E8F8F5, #D5F5E3);   /* Health */
--bento-lavender:  linear-gradient(145deg, #EBE4FF, #D6CCFF);   /* AI Scan */
--bento-peach:     linear-gradient(145deg, #FFF5E6, #FFECD2);   /* Tips */
--bento-amber:     linear-gradient(145deg, #FFF8E1, #FFECB3);   /* Gamification */

/* ── Primary CTA gradient (from app's btn-primary-gradient) ── */
--cta-gradient:    linear-gradient(135deg, #FF8C42 0%, #FF6B35 100%);
--cta-shadow:      0 4px 12px rgba(255, 107, 53, 0.25);
--cta-hover-shadow: 0 6px 16px rgba(255, 107, 53, 0.35);
```

---

## TYPOGRAPHY (matches app)

```css
/* Be Vietnam Pro — chosen for Vietnamese diacritical rendering */
@import url('https://fonts.googleapis.com/css2?family=Be+Vietnam+Pro:ital,wght@0,400;0,500;0,600;0,700;0,800;1,400&display=swap');

body { font-family: 'Be Vietnam Pro', sans-serif; color: #5C4033; }

/* Desktop scale */
.hero-headline     { font-size: 56px; font-weight: 800; letter-spacing: -0.02em; line-height: 1.1; color: #2D1B0E; }
.hero-subheadline   { font-size: 24px; font-weight: 500; line-height: 1.5; color: #5C4033; }
.section-title      { font-size: 36px; font-weight: 700; letter-spacing: -0.01em; color: #2D1B0E; }
.section-subtitle   { font-size: 18px; font-weight: 400; line-height: 1.7; color: #5C4033; }
.card-title         { font-size: 20px; font-weight: 700; }
.body-text          { font-size: 17px; font-weight: 400; line-height: 1.7; }
.small-text         { font-size: 14px; font-weight: 400; }
.cta-text           { font-size: 16px; font-weight: 700; font-family: 'Be Vietnam Pro', sans-serif; }

/* Mobile (max-width: 768px) */
.hero-headline      { font-size: 36px; }
.hero-subheadline   { font-size: 18px; }
.section-title      { font-size: 28px; }
.card-title         { font-size: 18px; }
.body-text          { font-size: 16px; }
```

---

## PAGE SECTIONS — Alternating Light/Dark Rhythm

Section order with background colors:

1. **NAVBAR** — transparent → frosted glass on scroll
2. **HERO** — cream `#FFFAF3` (light)
3. **PROBLEM** — dark gradient `#2D1B4E → #1A1A2E → #0D1B2A` (dark)
4. **SOLUTION** — warm cream `#FFF5EB` (light)
5. **FEATURES** — white `#FFFFFF` (light)
6. **PRICING** — dark gradient (same as Problem) (dark)
7. **CTA** — warm gradient `#FFF8F0 → #FFE8D6` (light)
8. **FOOTER** — dark navy `#1A1A2E` (dark)

This alternating rhythm creates visual contrast — not everything cream from top to bottom.

---

### Section 1: NAVBAR (sticky)

```
Design: Frosted glass, matches app's header-dark-band style
- Background: transparent initially → on scroll (>50px), transition to:
  rgba(26, 26, 46, 0.95) with backdrop-filter: blur(20px)
- Logo: "PV" icon + "PetVee" text in cream #FFFAF0 (always visible)
- Nav links (right): Tính năng | Bảng giá | Tải app
  - Color: rgba(255,255,255,0.7) → hover: #FFFFFF
- Mobile: hamburger → dropdown with same frosted dark background
- Height: 72px, z-index: 1000
- Transition: background 0.3s ease, box-shadow 0.3s ease
```

### Section 2: HERO (cream background)

```
Background: #FFFAF3
Layout: Two columns on desktop, stacked on mobile
- Left column (60%):
  - Kinetic headline: "Thấu hiểu chân tình" — each word fades in with 0.15s stagger
  - Sub-headline: "Chăm sóc trọn niềm tin."
  - Body: "Ứng dụng AI chăm sóc sức khoẻ thú cưng đầu tiên tại Việt Nam. Quét bệnh, hỏi bác sĩ AI, theo dõi sức khoẻ mỗi ngày."
  - CTA button: "Dùng thử miễn phí" (gradient CTA style)
  - Trust badges: "🐕 5,000+ sen đã tin dùng" | "⭐ 4.9 đánh giá" | "🏥 AI bác sĩ 24/7"
    (these are aspirational/marketing numbers)
- Right column (40%):
  - Phone mockup frame containing screenshot-home.png
  - Floating mascot: hero-duo.png (Dr. Vee + Mochi together) positioned
    overlapping bottom-left of phone, slight bounce animation
  - Phone has subtle shadow and 5-degree tilt

Mobile: Stack vertically — headline → phone mockup → CTA
```

### Section 3: PROBLEM (dark gradient background)

```
Background: linear-gradient(135deg, #2D1B4E 0%, #1A1A2E 50%, #0D1B2A 100%)
Title: "Sen ơi, boss đang cần gì?" (cream #FFF5E6 text)
Subtitle: "Mỗi ngày, hàng ngàn sen Việt Nam đang gặp những vấn đề này..."

3 problem cards in a row (staggered AOS fade-up):
  Card 1: mochi-worried.png
    Title: "Không biết boss bị gì"
    Text: "Triệu chứng lạ nhưng chưa đến mức đi khám? Google cho kết quả lung tung?"
    
  Card 2: mochi-confused.png
    Title: "Quên lịch tiêm, khám định kỳ"
    Text: "Lịch vaccine, tẩy giun, khám tổng quát — sen nào nhớ nổi?"
    
  Card 3: mochi-nighttime.png
    Title: "Nửa đêm boss ốm, không biết hỏi ai"
    Text: "Phòng khám đóng cửa, hotline không ai nghe — cần lời khuyên ngay lập tức."

Card style:
  - Background: rgba(255,255,255,0.05)
  - Border: 1px solid rgba(255,255,255,0.08)
  - Border-radius: 20px
  - Backdrop-filter: blur(10px)
  - Mascot image floats at top of card (80px height, transparent background)
  - Text color: #FFF5E6 (title), rgba(255,255,255,0.7) (body)

Mobile: Stack cards vertically
```

### Section 4: SOLUTION (warm cream background)

```
Background: linear-gradient(180deg, #FFF5EB 0%, #FFFAF3 100%)
Title: "PetVee — Bác sĩ AI trong túi sen" (#2D1B0E)
Subtitle: "Một ứng dụng, tất cả những gì boss cần."

Layout: Text left + mascot right (drvee-confident.png, large, ~300px)
Dr. Vee mascot has subtle bounce animation

3 solution bullets with icons:
  ✨ "Quét bệnh AI — chỉ cần chụp ảnh, biết ngay tình trạng"
  💬 "Hỏi bác sĩ AI 24/7 — câu trả lời chuyên môn, bằng tiếng Việt"  
  📊 "Theo dõi sức khoẻ mỗi ngày — check-in, nhắc lịch, biểu đồ trend"

Mobile: Mascot on top, text below
```

### Section 5: FEATURES (white background, bento grid)

```
Background: #FFFFFF
Title: "Tính năng nổi bật" (#2D1B0E)

Bento grid layout (matches app's home-bento-grid style):
  Row 1: AI Scanner (full width, featured — biggest card)
  Row 2: AI Chatbot (50%) + Daily Check-in (50%)
  Row 3: Vaccine Reminders (50%) + Nutrition (50%)
  Row 4: Community (full width)

Card design (matches app bento-card style):
  - Border-radius: 18px
  - Padding: 24px
  - Each card has its OWN background color identity:
    
    AI Scanner → bento-lavender: linear-gradient(145deg, #EBE4FF, #D6CCFF)
      - feat-scanner.png floating right
      - Title in purple #6C5CE7
      - Left accent bar (4px gradient purple)
      
    AI Chatbot → bento-mint: linear-gradient(145deg, #E8F8F5, #D5F5E3)
      - feat-chatbot.png floating right
      - Title in green #00B894
      
    Check-in → bento-peach: linear-gradient(145deg, #FFF5E6, #FFECD2)
      - feat-checkin.png floating right
      - Title in orange #FF6B35
      
    Vaccines → bento-amber: linear-gradient(145deg, #FFF8E1, #FFECB3)
      - feat-vaccine.png floating right
      - Title in warm brown #8B6914
    
    Nutrition → bento-mint (lighter variant)
      - feat-nutrition.png floating right
      - Title in green #00B894
      
    Community → gradient: linear-gradient(145deg, #FFF0F5, #FFE4EE)
      - feat-community.png floating right
      - Title in pink/warm #E84393

Cards have box-shadow: 0 2px 10px rgba(0,0,0,0.05)
Each card has small text description below the title
AOS: stagger fade-up with 100ms delay between cards
```

### Section 6: PRICING (dark gradient background)

```
Background: linear-gradient(135deg, #2D1B4E 0%, #1A1A2E 50%, #0D1B2A 100%)
Title: "Bảng giá" (cream #FFF5E6)
Subtitle: "Bắt đầu miễn phí. Nâng cấp khi boss cần thêm."

3 pricing cards side by side (desktop), stacked (mobile):

  FREE:
    - Background: rgba(255,255,255,0.05), border: 1px solid rgba(255,255,255,0.1)
    - Title: "Miễn phí" in white
    - Price: "0đ"
    - Features:
      ✓ Check-in hàng ngày
      ✓ Nhắc lịch vaccine
      ✓ Cộng đồng sen
      ✓ 3 lần quét AI/tháng
      ✓ 5 câu hỏi bác sĩ AI/tháng

  GÓI CHĂM (recommended):
    - Background: rgba(255,255,255,0.08), border: 2px solid #FF6B35
    - "PHỔ BIẾN" badge (yellow #FFD93D bg, dark text)
    - Title: "Gói Chăm" in orange #FF6B35
    - Price: "49.000đ/tháng"
    - Features: everything free +
      ✓ Quét AI không giới hạn
      ✓ 30 câu hỏi bác sĩ AI/tháng
      ✓ Lịch sử sức khoẻ chi tiết
      ✓ Xuất PDF báo cáo

  GÓI YÊU:
    - Background: linear-gradient(135deg, #FF6B35, #FF8C5A), no border needed
    - "HOT" badge
    - Title: "Gói Yêu" in white
    - Price: "99.000đ/tháng"
    - Features: everything Gói Chăm +
      ✓ Bác sĩ AI không giới hạn
      ✓ Ưu tiên phản hồi nhanh
      ✓ Tư vấn dinh dưỡng AI
      ✓ Badge VIP trong cộng đồng

  Each card: border-radius: 20px, padding: 32px
  CTA button at bottom of each card
```

### Section 7: CTA (warm gradient)

```
Background: linear-gradient(180deg, #FFF8F0 0%, #FFE8D6 100%)
Center-aligned

Mascot: celebration-highfive.png (Dr. Vee + Mochi high-fiving, ~200px)
Title: "Tải PetVee — Miễn phí!" (#2D1B0E, 800 weight)
Subtitle: "Có mặt trên iOS và Android" (#6B5A4A)

CTA button: "Tải app ngay 🐾" (gradient, large, with paw emoji)
  Style: btn-cta-gradient from app CSS

Below CTA: "Hoặc dùng ngay trên web → petvee.lovable.app" (smaller link)
```

### Section 8: FOOTER (dark navy)

```
Background: #1A1A2E
Layout: 3 columns on desktop, stacked on mobile

Column 1: Logo + tagline
  - "PV PetVee" 
  - "Thấu hiểu chân tình – Chăm sóc trọn niềm tin."
  - "© 2026 PetVee. All rights reserved."

Column 2: Links
  - Tính năng
  - Bảng giá
  - Chính sách bảo mật (→ /privacy.html)
  - Điều khoản sử dụng (→ /terms.html)

Column 3: Contact
  - 📧 hello@petvee.app
  - 🌐 petvee.app
  - Social icons: Facebook, TikTok (placeholder links)

Text colors: rgba(255,255,255,0.8) titles, rgba(255,255,255,0.4) body
Link hover: #FF6B35
Divider line at top: 1px solid rgba(255,255,255,0.06)
```

---

## MASCOT IMAGE RULES

- All mascot images are **transparent PNGs** — they float directly on section backgrounds
- **NO border, NO box-shadow, NO border-radius** on mascot images
- **NO card wrapper** around mascot images — they sit directly on backgrounds
- **Background: transparent** on both img elements and parent containers
- Hero mascot: loaded eagerly (not lazy)
- All other mascots: `loading="lazy"`
- If a mascot PNG file is missing, gracefully hide that image slot (don't break layout)
- Recommended max display size: 200-300px width for section mascots, 80-100px for card mascots

---

## ANIMATION

- **AOS** (Animate on Scroll): Load from CDN
  ```html
  <link href="https://cdn.jsdelivr.net/npm/aos@2.3.4/dist/aos.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/aos@2.3.4/dist/aos.min.js"></script>
  ```
  - Cards and sections: `data-aos="fade-up"`
  - Problem cards: stagger `data-aos-delay="100"`, `200`, `300`
  - Feature bento cards: stagger similarly
  - AOS config: `AOS.init({ duration: 600, once: true, offset: 80 });`

- **Hero kinetic text**: JS splits headline into `<span>` per word on DOMContentLoaded
  ```css
  @keyframes wordFadeIn {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }
  /* Each word span gets animation-delay: calc(var(--i) * 0.15s) */
  ```

- **Navbar**: JS scroll listener adds `.scrolled` class after 50px scroll
  - `.scrolled { background: rgba(26,26,46,0.95); backdrop-filter: blur(20px); box-shadow: 0 2px 20px rgba(0,0,0,0.15); }`

- **Mascot bounce**: CSS keyframes, subtle 2s ease-in-out infinite
  ```css
  @keyframes mascot-bounce {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-6px); }
  }
  ```
  Apply to hero mascot only. Respect `prefers-reduced-motion`.

- **No heavy animation libraries** — keep page lightweight

---

## CTA BUTTON STYLE (matches app exactly)

```css
.btn-cta {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 16px 32px;
  background: linear-gradient(135deg, #FF8C42 0%, #FF6B35 100%);
  color: #FFFFFF;
  font-family: 'Be Vietnam Pro', sans-serif;
  font-weight: 700;
  font-size: 16px;
  border: none;
  border-radius: 16px;
  box-shadow: 0 4px 12px rgba(255, 107, 53, 0.25);
  cursor: pointer;
  text-decoration: none;
  transition: transform 0.15s ease, box-shadow 0.15s ease;
}
.btn-cta:hover {
  box-shadow: 0 6px 16px rgba(255, 107, 53, 0.35);
  transform: translateY(-1px);
}
.btn-cta:active {
  transform: scale(0.98);
}
```

---

## PERFORMANCE

- Compress mascot PNGs if >500KB each (use `optipng` or `pngquant` if available)
- Lazy-load ALL images below the fold: `loading="lazy"`
- Hero images (screenshot + hero-duo mascot): NOT lazy — load eagerly
- Add `width` and `height` attributes to all images to prevent layout shift
- Keep total page weight under 5MB
- Target: <3s first paint on throttled 3G

---

## META / SEO / OG

```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PetVee — Ứng dụng AI chăm sóc sức khoẻ thú cưng đầu tiên tại Việt Nam</title>
<meta name="description" content="Quét bệnh AI, hỏi bác sĩ AI 24/7, theo dõi sức khoẻ thú cưng mỗi ngày. Tải miễn phí.">
<meta property="og:title" content="PetVee — AI chăm sóc sức khoẻ thú cưng">
<meta property="og:description" content="Ứng dụng AI đầu tiên tại Việt Nam. Quét bệnh, hỏi bác sĩ AI, theo dõi sức khoẻ mỗi ngày.">
<meta property="og:image" content="https://petvee.app/images/og-image.png">
<meta property="og:url" content="https://petvee.app">
<meta property="og:type" content="website">
<meta property="og:locale" content="vi_VN">
<link rel="icon" type="image/svg+xml" href="favicon.svg">
```

---

## CHECKLIST BEFORE PUSH

- [ ] All mascot PNGs render with transparent backgrounds (no cream rectangles visible)
- [ ] Hero kinetic text animation plays on page load
- [ ] Dark sections (Problem, Pricing) create clear visual contrast with light sections
- [ ] All CTA buttons use orange gradient with hover lift effect
- [ ] Feature bento grid is responsive (2 columns on tablet, 1 column on mobile)
- [ ] Navbar transitions from transparent to frosted dark glass on scroll
- [ ] AOS animations fire correctly on scroll (each card, each section)
- [ ] Privacy link (footer) → `/privacy.html` works
- [ ] Terms link (footer) → `/terms.html` works
- [ ] Page loads under 3s on throttled connection
- [ ] No console errors
- [ ] Vietnamese diacritics render correctly everywhere (ă, ắ, ổ, ệ, ư, ờ, etc.)
- [ ] Phone mockup screenshot-home.png is visible in hero
- [ ] Mobile hamburger menu works and closes on link click
- [ ] Footer email: hello@petvee.app
- [ ] `<html lang="vi">` is set
