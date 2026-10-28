# WuppyCMS Site — Design System

Bu dosya **müşteri sitesinin** tasarım sözleşmesidir. Tek doğruluk kaynağı
`src/styles/global.css` içindeki Tailwind 4 `@theme` token'larıdır. Bu belge
değerleri tekrar tanımlamaz; onları **kullanma biçimini** anlatır.

> **Kural:** Renk/radius/spacing için ham hex, `zinc-*`, `slate-*` gibi hazır
> paletler veya `style=""` kullanılmaz. Yalnızca token'lardan türeyen
> utility'ler (`bg-background`, `text-muted-foreground`, `border-border`,
> `rounded-xl`, `mt-section`…) kullanılır. Etkileşimli primitifler (Button,
> Badge, Input, Dialog…) **Bejamas UI**'dan gelir; elle yazılmaz.

---

## 1. Token kaynağı

```
src/styles/global.css   ← @theme + :root (tek kaynak)
```

Token değişikliği yalnız burada yapılır. Bir bileşende yeni renk gerekiyorsa
önce token eklenir, sonra utility kullanılır. `@theme` dışında custom CSS
yalnız `@layer base` temel kuralları için yazılır.

---

## 2. Renkler

| Token | Değer (oklch) | Kullanım |
| --- | --- | --- |
| `--color-background` | `0.16 0.004 260` | Sayfa zemini |
| `--color-foreground` | `0.97 0.003 260` | Ana metin |
| `--color-card` | `0.205 0.005 260` | Kart/panel yüzeyi |
| `--color-muted` | `0.27 0.005 260` | Sessiz zemin |
| `--color-muted-foreground` | `0.72 0.005 260` | İkincil metin |
| `--color-border` | `white / 12%` | Ayraç/kenar |
| `--color-input` | `white / 16%` | Form kenarı |
| `--color-primary` | `0.5772 0.2324 260` | Marka mavisi; CTA, link, vurgu |
| `--color-primary-foreground` | `0.977 0.013 260` | Primary üstü metin |
| `--color-destructive` | `0.62 0.21 25` | Hata/silme |

Örnek:

```astro
<section class="rounded-xl border border-border bg-card p-5">
  <p class="text-xs uppercase tracking-wide text-muted-foreground">Etiket</p>
  <a class="text-primary hover:underline" href="/blog">Yazı</a>
</section>
```

---

## 3. Tipografi

| Alan | Değer |
| --- | --- |
| Sans | Sistem sans (`font-sans`); şablonda Inter Variable |
| Mono | Sistem mono (`font-mono`); şablonda JetBrains Mono Variable |
| Gövde | `text-base leading-relaxed text-muted-foreground` |
| Başlık | `text-3xl/4xl font-semibold tracking-tight` |
| Mikro etiket | `text-xs uppercase tracking-[0.2em]` |
| Blog gövdesi | `prose prose-invert` (typography plugin) |

---

## 4. Radius

| Utility | Değer | Kullanım |
| --- | --- | --- |
| `rounded-sm` | 6px | Küçük rozet/kontrol |
| `rounded-md` | 8px | Input, küçük buton |
| `rounded-lg` | 10px | Buton |
| `rounded-xl` | 14px | Kart, bölüm yüzeyi |
| `rounded-2xl` | 18px | Büyük medya/hero yüzeyi |
| `rounded-full` | pill | Badge, avatar |

---

## 5. Spacing

Tailwind'in 4px ölçeği (`gap-2`, `p-4`, `mt-8`…) esastır. Anlamsal ekler:

| Token | Değer | Kullanım |
| --- | --- | --- |
| `--spacing-gutter` | 16px (`gap-gutter`, `px-gutter`) | Yatay boşluk |
| `--spacing-block` | 24px (`mt-block`, `gap-block`) | Bölüm içi blok aralığı |
| `--spacing-section` | 96px (`py-section`, `mt-section`) | Bölümler arası |
| `--spacing-hero` | 112px | Hero üst/alt |

Kurallar:

- Bölümler arası: `mt-section` / `py-section`.
- Kart içi: `p-5`/`p-6`, kartlar arası `gap-4`.
- Başlık–metin: `mt-3`/`mt-4`.
- Buton grubu: `flex flex-wrap gap-3`.

---

## 6. Button — Bejamas UI

Kaynak: `src/components/ui/button/` (Bejamas registry portu).

| Varyant | Kullanım |
| --- | --- |
| `default` | Ana CTA; Kumo mavisi degrade, `--button-primary-*` token'ları |
| `secondary` | İkincil CTA; çerçeveli |
| `outline` | Nötr eylem |
| `ghost` | Araç çubuğu/ikon |
| `destructive` | Silme |

Boyutlar: `sm` 32px · `default` 36px · `lg` 40px · `icon*`.

```astro
---
import { Button } from "../components/ui/button";
---
<Button as="a" href="#posts">Yazıları oku</Button>
<Button as="a" href="#about" variant="secondary">Hakkımızda</Button>
```

Primary buton rengi **yalnız** `--color-primary` ve türevlerinden
(`--button-primary-grad-top/bottom`, `--button-primary-ring/gloss`) gelir.

---

## 7. Badge — Bejamas UI

```astro
---
import { Badge } from "../components/ui/badge";
---
<Badge variant="outline" shape="pill">Astro + Tailwind 4</Badge>
```

Varyantlar: `default`, `secondary`, `outline`, `destructive`. Durum/etiket
için pill biçimi tercih edilir.

---

## 8. Bölüm ve kart deseni

Referans: `src/components/sections/About.astro`

```astro
<section class="mt-section">
  <p class="text-xs font-medium uppercase tracking-[0.2em] text-primary">Hakkımızda</p>
  <h2 class="mt-3 text-3xl font-semibold tracking-tight">Başlık</h2>
  <p class="mt-4 max-w-2xl text-base leading-relaxed text-muted-foreground">Açıklama</p>
  <div class="mt-block grid gap-4 sm:grid-cols-3">
    <div class="rounded-xl border border-border bg-card p-5">…</div>
  </div>
</section>
```

- Bölüm kimliği: `id` + isteğe bağlı `data-reeyai-section`.
- İçerik hedefi: `data-reeyai-content` / `data-reeyai-field` (CMS element seçici).
- Kart: `rounded-xl border border-border bg-card p-5`.
- İkon/medya yüzeyi: `rounded-lg overflow-hidden border border-border`.

---

## 9. Bejamas UI kuralı

- Yeni primitif: `npx bejamas add <ad>` → `src/components/ui/<ad>/`.
- Elle buton/input/dialog yazılmaz; shadcn/Radix/Headless UI'dan kopyalanmaz.
- Kurulu primitif tekrar kurulmaz; `src/components/ui` altındaki kullanılır.
- Stil Tailwind 4 utility'leri + token'lardır; bileşene gömülü renk yoktur.

Mevcut: **Button, Badge**. İhtiyaç doğdukça aynı CLI ile eklenir.

---

## 10. Erişilebilirlik ve etkileşim

- Odak görünür: Bejamas primitifleri `focus-visible:ring-*` taşır.
- İkon-only kontrollerde `aria-label` + `title`.
- Renk tek başına anlam taşımaz; metin/ikonla desteklenir.
- `scroll-behavior: smooth` base katmanındadır; hareket azaltma tercihinde
  tarayıcı davranışı korunur.
- Metin kontrastı: `text-foreground` / `text-muted-foreground`; primary üzerinde
  `text-primary-foreground`.

---

## 11. Yapılmaması gerekenler

- `bg-zinc-950`, `text-gray-400`, `border-slate-800` gibi ham paletler.
- `style="color: #..."`, bileşen içi `<style>` (yalnız `global.css` istisna).
- Bölüm aralıklarını `mt-[73px]` gibi keyfî değerlerle vermek; `mt-section` kullan.
- Aynı görsel işi yapan yeni bir buton/kart primitifi yazmak.
- Token'ı atlayıp degrade/renk uydurmak.
