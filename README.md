# WuppyCMS Demo Sitesi

WuppyCMS şablonuyla kurulmuş örnek site. İçerik bu repoda yaşar; WuppyCMS'te
yapılan her kayıt gerçek bir commit'tir, build GitHub Actions'ta koşar.

Tasarım sözleşmesi: [`DESIGN_SYSTEM.md`](DESIGN_SYSTEM.md) — endüstriyel
Astro + Tailwind 4 + Bejamas UI sistemi (açık zemin, `#dd641e` turuncu,
Space Grotesk, keskin köşe). Token'lar `src/styles/global.css`ten gelir;
primitifler `src/ui` altındaki Bejamas portlarıdır.

## Yapı

| Yol | Ne var? |
| --- | --- |
| `src/content/blog/*.mdx` | Blog yazıları (frontmatter + MDX gövde) |
| `src/content/authors/*.md` | Yazarlar |
| `src/content.config.ts` | Zod şemaları — koleksiyonların gerçek kaynağı |
| `src/pages/index.astro` | Landing: hero, özellikler, süreç, blog, iletişim |
| `src/pages/blog/*` | Blog indeksi ve makale şablonu |
| `src/ui/*` | Bejamas UI primitifleri (NavigationMenu, Accordion, Tabs, Carousel) |
| `.reeyai/sites.jsonc` | Site tanımları (CMS buradan okur) |
| `.github/workflows/build.yml` | CI: her push'ta `pnpm build` |

## Geliştirme

```sh
pnpm install
pnpm dev      # http://localhost:4321
pnpm build
```
