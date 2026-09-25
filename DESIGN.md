# Picorie Design System

> Web photobooth **Picorie** (by Reddie). Sumber: Figma *Photobooth-Reddie* → page **vibecode** (`node 2878:19158`).
> Semua nilai di dokumen ini diambil langsung dari layer Figma (fill, stroke, radius, padding, font).
> Nilai yang ditandai **≈** diestimasi dari render karena berupa aset vektor, bukan properti layer.

Visual sheet: [`picorie-design-system.html`](./picorie-design-system.html)

---

## 0. Prinsip desain

| Prinsip | Artinya di UI |
|---|---|
| **Desktop retro yang ramah** | Setiap layar adalah "jendela browser" dengan title bar kuning, traffic-light, address bar berbentuk pill, dan tab. User merasa sedang "membuka aplikasi" di komputer lama yang lucu. |
| **Garis tebal, warna hangat** | Outline maroon `#782B37` tebal (2–12px) di semua objek. Tidak ada garis abu-abu tipis untuk objek utama. |
| **Sticker & komik** | Hard shadow tanpa blur (`4px 4px 0`), ledakan komik (starburst) pink, halftone dots, dan border bergaya coretan tangan. |
| **Satu aksi utama per layar** | Setiap layar punya satu tombol kuning 3D (Start Photobooth / Next / Print). Semua hal lain adalah pendukung. |
| **Reddie adalah pemandu** | Mascot robot merah muncul di title bar (avatar 43×36) dan sebagai ilustrasi besar di onboarding/loading. |

### Alur layar (screen map)

| # | Layar | Frame Figma | Isi utama |
|---|---|---|---|
| 1 | Onboarding | `2878:19160` | Folder desktop, tombol **Start Photobooth**, logo "Welcome to PICORIE", Reddie |
| 2 | Choose Frame | `2878:19566` | Tab browser, grid frame template, panel **Selected Frame**, tombol Start |
| 3 | Create Template | `2878:19841` | Grid **layout card** (Layout A–E), panel Selected Frame, tombol **Next** |
| 4 | Choose Effect (×2) | `2878:20201`, `2878:20566` | Jendela berisi grid **sticker tile** 5×N + scrollbar, tombol **Next** |
| 5 | Camera | `2878:20958` | Jendela kamera bersarang, **shutter**, **pose tray**, **timer chip**, preview frame |
| 6 | Loading | `2878:21276` | Tumpukan 3 dialog "Reddie is cooking" + **segmented progress** |
| 7 | Result | `2878:21581` | Preview strip foto + jendela **QR** "Scan Me!" + tombol **Print** |

---

## 1. Foundation

### 1.1 Warna

#### Brand — Maroon & Rose
| Token | Hex | Dipakai untuk |
|---|---|---|
| `maroon-700` | `#782B37` | **Ink utama**: semua outline, teks tombol, teks address bar, ikon, hard shadow |
| `maroon-800` | `#60222C` | Outline body jendela gelap (Choose Effect) |
| `rose-500` | `#C06878` | Thumb scrollbar aktif, folder mauve |
| `rose-500b` | `#C26A78` | Segmen progress terisi (varian rose-500 di Figma; disarankan disatukan ke `#C06878`) |
| `dusty-400` | `#B99898` | Segmen progress kosong/idle |
| `blush-300` | `#F6B9C0` | Panggung pink (stage) di belakang jendela, starburst, halftone |

#### Sunshine — Kuning (aksi)
| Token | Hex | Dipakai untuk |
|---|---|---|
| `yellow-400` | `#FECE4E` | Fill tombol primary, title bar jendela |
| `yellow-300` | `#FCC86A` | Tab browser (inactive) |
| `yellow-100` | `#FFE6A4` | Tab browser (active / paling depan), hover lembut |
| `yellow-600` | `#EDAC00` | Border 8px tombol primary |
| `yellow-700` | `#C98F00` | "Bibir" 3D tombol (`0 5px 0`) |
| `amber-800` | `#8A5A00` | Teks timer (`05:00`) |

#### Accent
| Token | Hex | Dipakai untuk |
|---|---|---|
| `coral-500` | `#EB5C5D` | Judul display "Selected Frame" (selalu dengan outline maroon) |

#### Surface & Neutral
| Token | Hex | Dipakai untuk |
|---|---|---|
| `canvas` | `#F8F4ED` | Background halaman (paling belakang) |
| `white` | `#FFFFFF` | Body jendela, card, pill address bar |
| `neutral-50` | `#FAFAFA` | Track scrollbar |
| `placeholder` | `#F2F2F7` | Slot foto kosong di layout card |
| `hairline` | `#D2D2D7` | Border tipis frame preview dalam card |
| `slate-200` | `#E2E8F0` | Border frame preview (Layout A–C) |
| `neutral-300` | `#D4D4D4` | Thumb scrollbar netral |
| `camera-off` | `#CCCCCC` | Viewfinder kamera saat belum aktif (white + 20% black) |

#### Text
| Token | Hex | Dipakai untuk |
|---|---|---|
| `text-strong` | `#0F172A` (slate-900) | Judul card ("Layout A") |
| `text-muted` | `#64748B` (slate-500) | Meta card ("2 Pose") |
| `text-subtle` | `#94A3B8` (slate-400) | Helper ("Scan QR or Print") |
| `text-ink` | `#782B37` | Teks di atas kuning/putih |

#### Window controls (traffic light) ≈
| Token | Hex |
|---|---|
| `dot-close` | `#EC4B4B` ≈ |
| `dot-min` | `#E8B21C` ≈ |
| `dot-max` | `#34B556` ≈ |

#### Semantic mapping
```css
--color-bg:            var(--canvas);        /* #F8F4ED */
--color-stage:         var(--blush-300);     /* #F6B9C0 */
--color-surface:       #FFFFFF;
--color-chrome:        var(--yellow-400);    /* title bar */
--color-ink:           var(--maroon-700);    /* outline + teks utama */
--color-action:        var(--yellow-400);
--color-action-border: var(--yellow-600);
--color-action-lip:    var(--yellow-700);
--color-selected:      var(--rose-500);
--color-display:       var(--coral-500);
```

#### Kontras (WCAG 2.1)
| Pasangan | Rasio | Status |
|---|---|---|
| Maroon on White | 9.55 : 1 | ✅ AAA |
| Maroon on Canvas | 8.71 : 1 | ✅ AAA |
| Maroon on Yellow-400 | 6.44 : 1 | ✅ AA (AAA untuk teks besar) |
| Maroon on Yellow-100 | 7.78 : 1 | ✅ AAA |
| Maroon on Blush | 5.74 : 1 | ✅ AA |
| Slate-500 on White | 4.76 : 1 | ✅ AA |
| Amber-800 on White | 5.93 : 1 | ✅ AA |
| Coral on White | 3.38 : 1 | ⚠️ Hanya teks besar (≥24px) — wajib pakai outline maroon |
| Slate-400 on White | 2.56 : 1 | ❌ Jangan untuk info penting; ganti `slate-500` bila teks wajib dibaca |
| White on Yellow-300 (teks tab) | 1.54 : 1 | ❌ Teks tab putih **wajib** diberi stroke maroon 2–3px (seperti di Figma) atau ganti ke teks maroon |

---

### 1.2 Tipografi

| Peran | Family | Sumber | Fallback |
|---|---|---|---|
| Display | **Block Berthold** (Regular) | Komersial — self-host `@font-face` | `"Lilita One", "Baloo 2", system-ui` |
| UI / Button / Label | **Baloo 2** (500, 700) | Google Fonts | `"Nunito", system-ui, sans-serif` |
| Content / Card | **Poppins** (500, 700) | Google Fonts | `system-ui, sans-serif` |

Token Figma: `typography/font-size/text-5 = 18px`, `text-7 = 22px`, `text-8 = 24px`, `font-weight/font-bold = 700`, `font-weight/font-medium = 500`, `letter-spacing/letter-spacing-5 = 0`.

#### Type scale
| Token | Font | Size / Line | Weight | Tracking | Warna | Contoh di Figma |
|---|---|---|---|---|---|---|
| `display-xl` | Block Berthold | 58 / 65 | 400 | 2px | Coral + stroke maroon | "Selected Frame" |
| `display-lg` | Block Berthold | 40 / normal | 400 | 0, UPPERCASE | Maroon | "WELCOME TO" |
| `title` | Poppins | 24 / normal | 700 | 0 | slate-900 | "Layout A" |
| `button-lg` (`text-8`) | Baloo 2 | 24 / normal | 700 | 0 | Maroon | "Start Photobooth", timer "05:00" (amber) |
| `button` (`text-7`) | Baloo 2 | 22 / normal | 700 | 0 | Maroon | "Next", "Print" |
| `helper` (`text-7`) | Baloo 2 | 22 / normal | 500 | 0 | slate-400 | "Scan QR or Print" |
| `label-loud` | Baloo 2 | 20 / normal | 700 | 2px | White + stroke maroon | "Loading..." |
| `body` (`text-5`) | Baloo 2 | 18 / normal | 700 | 0 | Maroon | "Ready to make new memories?", "Reddie is cooking" |
| `tab` (`text-5`) | Baloo 2 | 18 / normal | 700 | 1px | White + stroke maroon | "Choose Frame" |
| `meta` | Poppins | 16 / normal | 500 | 0 | slate-500 | "2 Pose" |
| `caption` | Baloo 2 | 16 / normal | 700 | 0 | Black | label folder "reddie" |

> `line-height: normal` di Figma ≈ 1.2–1.35 tergantung font. Untuk implementasi gunakan `1.25` untuk Baloo 2 dan `1.3` untuk Poppins.

---

### 1.3 Spacing

Grid dasar **4px**. Nilai di luar kelipatan 4 (6, 10, 14, 35) memang dipakai di Figma dan tetap didokumentasikan sebagai token.

| Token | px | Dipakai untuk |
|---|---|---|
| `space-1` | 4 | Gap tray ikon, gap judul↔meta card, padding tray |
| `space-1.5` | 6 | Gap slot foto dalam layout frame |
| `space-2` | 8 | Padding vertikal address pill, gap slot (Layout A–C) |
| `space-2.5` | 10 | Padding icon tile, gap segmen progress |
| `space-3` | 12 | Padding frame preview, gap folder ikon↔label |
| `space-3.5` | 14 | Gap isi layout card, padding vertikal title bar |
| `space-4` | 16 | Padding horizontal address pill & dialog title bar, gap ikon nav (15) |
| `space-5` | 20 | Padding layout card, padding QR |
| `space-6` | 24 | Gap sticker grid, gap panel "Selected Frame", padding sticker window |
| `space-7` | 28 | Overlap tab (−28), inset konten dari body jendela (29.5) |
| `space-9` | 35 | Padding horizontal title bar jendela |
| `space-10` | 40 | Gap title bar QR, inset kamera (39.5) |
| `space-16` | 64 | Inset konten onboarding (63.5) |

Layout: artboard **1920×1080**, stage pink **1538×896** (radius 64, border 12), jendela utama **1498×856** di tengah stage (inset 20px).

---

### 1.4 Radius

| Token | px | Dipakai untuk |
|---|---|---|
| `radius-2xs` | 2 | Segmen progress |
| `radius-xs` | 4 | Sticker window, pose tray, icon tile, slot foto kotak (layout E) |
| `radius-sm` | 5 | Track progress |
| `radius-md` | 8 | Frame preview dalam card (layout E) |
| `radius-lg` | 16 | Slot foto (layout A–C) |
| `radius-tab` | 18 | Sudut tab browser |
| `radius-xl` | 20 | Address pill, timer chip, QR image, frame preview |
| `radius-2xl` | 28 | Layout card |
| `radius-dialog` | 31 | Dialog kecil (Reddie is cooking) |
| `radius-window` | 54 | Jendela utama (atas & bawah) |
| `radius-stage` | 64 | Stage pink |
| `radius-pill` | 999 | Tombol primary, slot foto bulat (100) |

### 1.5 Stroke / Border

| Token | px | Dipakai untuk |
|---|---|---|
| `stroke-hair` | 1 | Icon tile, segmen progress, scrollbar, frame preview |
| `stroke-thin` | 2 | Address pill, timer chip, sticker window, pose tray |
| `stroke-card` | 3 | Layout card, QR, track progress aktif |
| `stroke-window` | 5 | Title bar, body jendela, tab, dialog |
| `stroke-button` | 8 | Tombol primary (`yellow-600`) |
| `stroke-stage` | 12 | Stage pink |

Semua stroke objek memakai **maroon-700** kecuali tombol (yellow-600) dan hairline di dalam card.

### 1.6 Elevation / Shadow

| Token | Nilai | Dipakai untuk |
|---|---|---|
| `shadow-button` | `0 5px 0 #C98F00, 0 10px 18px rgba(60,10,10,.20)` | Tombol primary (efek 3D) |
| `shadow-sticker` | `4px 4px 0 #782B37` | Sticker window, pose tray |
| `shadow-chip` | `3px 2px 0 #782B37` | Timer chip |
| `shadow-sticker-dark` | `4px 4px 0 #000` | Track progress (idle) |
| `shadow-mini` | `2px 2px 0 #000` | Segmen progress |
| `shadow-soft` | `0 4px 5px rgba(0,0,0,.04)` | Frame preview di layout card |

> Aturan: **hard shadow tanpa blur** untuk objek bergaya sticker; blur hanya dipakai di tombol primary (agar "melayang").

### 1.7 Ikonografi

| Ikon | Set | Ukuran | Warna |
|---|---|---|---|
| arrow-left / arrow-right | vuesax/linear | 26 | maroon |
| undo-alt (refresh) | Line Awesome solid | 22 | maroon |
| add (tab baru) | vuesax/linear | 32 | maroon |
| minus / square / times | vuesax/linear, LA solid | 26 / 26 / 22 | maroon |
| star | Iconly/Curved/Bold | 24 (UI), 100 (sticker) | maroon / black |

Stroke ikon linear 1.5px, ujung membulat.

### 1.8 Motif & ilustrasi

- **Stage pink** `#F6B9C0` + border 12px maroon, radius 64 — "meja" tempat jendela diletakkan.
- **Starburst** (ledakan komik) pink di pojok kanan atas, keluar dari stage.
- **Halftone dots** pink transparan di sudut kiri bawah & di dalam jendela.
- **Speed lines** (garis radial) di belakang Reddie.
- **Border coretan tangan**: outline jendela di render Figma bergerigi halus (tekstur sketsa). Di web bisa ditiru dengan SVG `feTurbulence` + `feDisplacementMap` pada outline, intensitas rendah.
- **Folder desktop** 144×95 dalam 4 warna: blush `#F5B8C4`≈, cream `#FDF3DC`≈, mauve `#C26A78`, yellow `#FECE4E`.
- **Reddie**: avatar title bar 43×36; ilustrasi besar ±740px di onboarding.

---

## 2. Components

Setiap komponen punya 4 state wajib: **default · hover · active (pressed/selected) · disabled**, plus **focus-visible** untuk keyboard.
State hover/active/disabled tidak ada di file Figma. Yang ditulis di bawah adalah **usulan** yang diturunkan dari token di atas agar tetap konsisten.

### 2.1 Button / Primary (3D pill)
Anatomi: pill `radius 999` · fill `yellow-400` · border `8px yellow-600` · shadow `shadow-button` · label Baloo 2 Bold maroon.

| Size | Tinggi | Lebar di Figma | Label |
|---|---|---|---|
| `lg` | 80 | 280 | 24px (Start Photobooth) |
| `md` | 61 | 280–427 | 22px (Next, Print) |

| State | Spec |
|---|---|
| Default | seperti anatomi |
| Hover | `translateY(-2px)`, lip `0 7px 0 #C98F00`, fill `#FFD866` |
| Active | `translateY(5px)`, lip `0 0 0`, blur shadow hilang, fill `#F5C43A` |
| Disabled | fill `#F3E6C3`, border `#E6D5A6`, teks `#B79AA0`, tanpa shadow, `cursor:not-allowed` |
| Focus | outline `3px maroon` offset 4px |

### 2.2 Window (Browser Window)
- **Title bar**: tinggi 73 · fill `yellow-400` · border 5 maroon · radius atas 54 · padding `14 35` · `space-between`.
  - Kiri: traffic light (3 dot, 112×24) **atau** nav icons (arrow-left, arrow-right, undo; gap 15).
  - Tengah: Address pill.
  - Kanan: avatar Reddie 43×36.
- **Body**: fill white · border 5 maroon · radius bawah 54 · `overflow: clip`.
- Varian: `window/main` (1498×856), `window/nested` (kamera, 1082 lebar), `window/card` (QR 499×680, sticker 824×784).

### 2.3 Tab (Browser Tab)
Tinggi 63 · border 5 maroon · radius `35/18` (tab pertama) atau `18/18` · padding `17 35` · overlap `-28px` · teks Baloo 2 Bold 18, tracking 1, white + stroke maroon · ikon close 22.

| State | Spec |
|---|---|
| Default (inactive) | fill `yellow-300` `#FCC86A`, z-index di belakang |
| Hover | fill `#FDD68A`, naik `-2px` |
| Active (current) | fill `yellow-100` `#FFE6A4`, z-index paling depan |
| Disabled | fill `#F1E7CF`, teks `#D9C9C0` tanpa stroke, ikon close disembunyikan |
| Tab "+" | lebar 100, ikon add 32, fill `yellow-100` |

### 2.4 Address Pill (prompt bar)
White · border 2 maroon · radius 20 · padding `8 16` · lebar 352–710 · teks body maroon + ikon star 24.

| State | Spec |
|---|---|
| Default | seperti anatomi |
| Hover | border 2 maroon + `shadow-chip` |
| Active / Focus | background `yellow-100`, `shadow-sticker` |
| Disabled | background `#F4EFEA`, teks & ikon `#B79AA0` |

### 2.5 Icon Button (nav / window controls)
Ikon 22–26px maroon, hit area min 40×40.
Hover: lingkaran `yellow-100`. Active: lingkaran `yellow-600` + `scale(.92)`. Disabled: opacity 35%.

### 2.6 Traffic Light
3 dot Ø≈18 dengan outline 1.5 maroon, gap 8. Hover pada grup: tampilkan glyph (×, –, +) maroon.

### 2.7 Layout Card
304×480 · white · border 3 maroon · radius 28 · padding 20 · gap 14.
Isi: frame preview (border 1 `slate-200` / `hairline`, radius 20/8, padding 12, gap 8/6) + slot `placeholder` (radius 16 / 4 / 100) · judul `title` · meta `meta`.

| State | Spec |
|---|---|
| Default | seperti anatomi |
| Hover | `translate(-2px,-2px)` + `shadow-sticker` |
| Active (selected) | border 3 `rose-500`, ring luar 3px `blush-300`, badge ✓ maroon di pojok |
| Disabled | opacity 45%, slot `#F7F7F9`, `cursor:not-allowed`, badge "Soon" |

### 2.8 Sticker / Effect Tile
Padding 10 · border 1 maroon · radius 4 (hanya sudut tertentu di Figma) · ikon 100. Grid gap 24 di dalam sticker window (border 2 maroon, radius 4, `shadow-sticker`).

| State | Spec |
|---|---|
| Default | white |
| Hover | background `yellow-100` |
| Active (selected) | background `blush-300`, border 2 maroon, `shadow-mini` maroon |
| Disabled | ikon opacity 30% |

### 2.9 Pose Tray
White · border 2 maroon · radius 4 · padding `10 4 4` · gap 4 · `shadow-sticker`. Berisi slot 44×44 (border 1, ikon star 24). Slot terisi = star hitam; slot kosong = star outline.

### 2.10 Timer Chip
280 lebar · white · border 2 maroon · radius 20 · padding `8 24` · `shadow-chip` · teks `button-lg` warna `amber-800` + star.
State warning (<10 detik) usulan: teks `coral-500`, animasi pulse.

### 2.11 Shutter Button
Lingkaran Ø83 di bawah viewfinder, fill `#A6A6A6`≈.
Hover: fill white + ring 4 maroon. Active: `scale(.9)`. Disabled: opacity 40%.

### 2.12 Segmented Progress
Track: white · radius 5 · padding `8 11` · border 1 black (idle) → 3 maroon (aktif). Segmen 27×45 · radius 2 · gap 10 · `shadow-mini`.
Segmen kosong `dusty-400`, terisi `rose-500b` dengan border maroon. Label "Loading..." `label-loud`.

### 2.13 Dialog (Reddie is cooking)
Lebar 631 · title bar yellow-400, border 5, radius atas 31, padding `14 16`, ikon minus/square/times · body white 175 tinggi, radius bawah 31. Bisa ditumpuk 3 dengan offset `16px, 12px`.

### 2.14 Scrollbar
Track 15 lebar · `neutral-50` · border 1 maroon. Thumb 13 lebar · radius 24 · `rose-500` (aktif) atau `neutral-300` (netral).

### 2.15 Folder (desktop icon)
Ikon 144×95 + label `caption`, gap 12. Hover: `translateY(-3px)`. Selected: label diberi highlight `yellow-100` radius 4. Disabled: opacity 40%.

### 2.16 QR Card
QR 413×413 · border 3 maroon · radius 20. Di bawahnya helper "Scan QR or Print" lalu tombol primary Print (427×61).

---

## 3. Pola layout

| Pola | Struktur |
|---|---|
| **Stage + Window** | Canvas `#F8F4ED` → stage pink (1538×896) → window 1498×856 di tengah. Starburst & halftone sebagai dekor di luar window. |
| **Grid + Sidebar** (Choose Frame / Create Template) | Grid 3 kolom card 304px, gap 44, inset 29.5 · scrollbar vertikal · sidebar 290px berisi judul display, card terpilih, tombol Next (gap 24). |
| **Centered Card Window** (Choose Effect / Result) | Window 824×784 atau 499×680 di tengah stage, konten grid sticker atau QR, tombol primary di bawah. |
| **Nested Window** (Camera) | Window utama → window kamera 1082 lebar di kiri + kolom kanan 280 (timer, preview strip, Next). Pose tray di bawah kamera. |
| **Stacked Dialog** (Loading) | 3 dialog 631 ditumpuk, offset 16/12, di tengah stage kecil 717×303. |

## 4. Do & Don't

- ✅ Satu tombol kuning per layar. ❌ Dua tombol primary bersebelahan.
- ✅ Outline selalu maroon. ❌ Outline hitam/abu untuk objek utama (kecuali loading track idle yang ada di Figma).
- ✅ Hard shadow `4px 4px 0` untuk sticker. ❌ Drop shadow blur besar di card.
- ✅ Teks putih hanya dengan stroke maroon. ❌ Teks putih polos di atas kuning.
- ✅ Coral hanya untuk judul display ≥40px. ❌ Coral untuk body text.

## 5. CSS token (siap pakai)

```css
:root {
  /* color */
  --maroon-700:#782B37; --maroon-800:#60222C; --rose-500:#C06878; --rose-500b:#C26A78;
  --dusty-400:#B99898; --blush-300:#F6B9C0;
  --yellow-100:#FFE6A4; --yellow-300:#FCC86A; --yellow-400:#FECE4E; --yellow-600:#EDAC00;
  --yellow-700:#C98F00; --amber-800:#8A5A00; --coral-500:#EB5C5D;
  --canvas:#F8F4ED; --white:#FFFFFF; --neutral-50:#FAFAFA; --placeholder:#F2F2F7;
  --hairline:#D2D2D7; --slate-200:#E2E8F0; --neutral-300:#D4D4D4;
  --slate-900:#0F172A; --slate-500:#64748B; --slate-400:#94A3B8;

  /* type */
  --font-display:"Block Berthold","Lilita One","Baloo 2",system-ui,sans-serif;
  --font-ui:"Baloo 2","Nunito",system-ui,sans-serif;
  --font-content:"Poppins",system-ui,sans-serif;
  --text-5:18px; --text-7:22px; --text-8:24px;

  /* spacing */
  --space-1:4px; --space-1-5:6px; --space-2:8px; --space-2-5:10px; --space-3:12px;
  --space-3-5:14px; --space-4:16px; --space-5:20px; --space-6:24px; --space-7:28px;
  --space-9:35px; --space-10:40px; --space-16:64px;

  /* radius */
  --radius-2xs:2px; --radius-xs:4px; --radius-sm:5px; --radius-md:8px; --radius-lg:16px;
  --radius-tab:18px; --radius-xl:20px; --radius-2xl:28px; --radius-dialog:31px;
  --radius-window:54px; --radius-stage:64px; --radius-pill:999px;

  /* stroke */
  --stroke-hair:1px; --stroke-thin:2px; --stroke-card:3px; --stroke-window:5px;
  --stroke-button:8px; --stroke-stage:12px;

  /* shadow */
  --shadow-button:0 5px 0 #C98F00, 0 10px 18px rgba(60,10,10,.2);
  --shadow-sticker:4px 4px 0 #782B37;
  --shadow-chip:3px 2px 0 #782B37;
  --shadow-mini:2px 2px 0 #000;
  --shadow-soft:0 4px 5px rgba(0,0,0,.04);
}
```
