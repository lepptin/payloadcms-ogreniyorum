# 🎓 Payload CMS v3 - Kapsamlı Öğrenme Müfredatı

Payload CMS v3, **Next.js App Router** üzerine inşa edilmiş, TypeScript-first bir headless CMS'tir. v2'den çok farklı bir mimariye sahiptir. Aşağıdaki müfredat, JavaScript/React/Next.js bilginiz olduğunu varsayarak sıfırdan ileri seviyeye kadar götürür.

---

## 📚 FAZA 0: ÖN HAZIRLIK (1-2 Hafta)

### 0.1 — Payload v3'ün Felsefesini Anlamak
- Neden Next.js-native? v2 vs v3 mimari farkları
- "Code-first" yaklaşım: Config-as-code felsefesi
- Self-hosted vs SaaS karşılaştırması
- TypeScript ile "typesafe CMS" konsepti

### 0.2 — Geliştirme Ortamı
```bash
npx create-payload-app -n my-project
```
- Node.js 20+ ve pnpm/yarn/npm
- Proje yapısını tanımak:
  ```
  src/
    app/(payload)/     → Admin panel route'ları
    app/(frontend)/    → Public Next.js route'ları
    collections/       → Veri modelleri
    payload.config.ts  → Ana konfigürasyon
  ```

### 0.3 — Temel Next.js App Router Hatırlatması
- Server Components vs Client Components
- Route handlers
- Server Actions
- Middleware kavramı (Payload auth için kritik)

---

## 📚 FAZA 1: TEMEL KAVRAMLAR (2-3 Hafta)

### 1.1 — İlk Collection Oluşturma
```typescript
// src/collections/Posts.ts
import { CollectionConfig } from 'payload'

export const Posts: CollectionConfig = {
  slug: 'posts',
  fields: [
    { name: 'title', type: 'text', required: true },
    { name: 'content', type: 'richText' },
    { name: 'publishedAt', type: 'date' },
  ],
}
```

**Öğrenilecekler:**
- `CollectionConfig` tipi
- Field tipleri (text, textarea, number, checkbox, date)
- `slug`, `labels`, `admin` metadata
- `payload.config.ts`'e collection ekleme

### 1.2 — Alan (Field) Tipleri Derinlemesine
| Field Tipi | Kullanım |
|---|---|
| `text` | Başlık, kısa metin |
| `textarea` | Uzun düz metin |
| `richText` | Lexical editor (slate yerine) |
| `number` | Sayısal veri |
| `checkbox` | Boolean |
| `select` | Enum / dropdown |
| `radio` | Tek seçim |
| `date` | Tarih |
| `email` | E-posta validasyonu |
| `upload` | Dosya yükleme |
| `relationship` | İlişki kurma |
| `array` | Tekrarlı alanlar |
| `blocks` | Dinamik içerik blokları |
| `group` | Alan gruplama |

### 1.3 — Admin Panelini Keşfetmek
- `/admin` URL'si
- Otomatik CRUD UI
- Field-level admin konfigürasyonu
- List view özelleştirme

---

## 📚 FAZA 2: VERİ İLİŞKİLERİ VE YAPISI (2 Hafta)

### 2.1 — Relationship (İlişki) Alanları
```typescript
{
  name: 'author',
  type: 'relationship',
  relationTo: 'users',
  hasMany: false,
}
```
- `relationTo`: Tek veya çoklu collection
- `hasMany`: Tekil vs çoklu ilişki
- `filterOptions`: Koşullu seçim
- Polymorphic ilişkiler

### 2.2 — Upload Collection (Medya Yönetimi)
```typescript
export const Media: CollectionConfig = {
  slug: 'media',
  upload: {
    staticDir: 'media',
    imageSizes: [
      { name: 'thumbnail', width: 400 },
      { name: 'card', width: 768 },
    ],
    mimeTypes: ['image/*'],
  },
  fields: [
    { name: 'alt', type: 'text', required: true },
  ],
}
```
- Görsel boyutlandırma
- S3 / Cloudinary / R2 adapter'ları
- Focal point (odak noktası)

### 2.3 — Blocks (Dinamik Sayfa Yapıları)
```typescript
{
  name: 'layout',
  type: 'blocks',
  blocks: [
    HeroBlock,
    ContentBlock,
    CTABlock,
  ],
}
```
- Block-based page builder mantığı
- Her bloğun ayrı tipi
- Frontend'de blokları render etme

### 2.4 — Array & Group Fields
- Tekrarlayan veri yapıları
- Nested formlar
- Validation kuralları

---

## 📚 FAZA 3: VERİTABANI VE ADAPTERLAR (1-2 Hafta)

### 3.1 — Veritabanı Seçimi
| Adapter | Kullanım Alanı |
|---|---|
| **MongoDB** (Mongoose) | Esnek şema, hızlı prototyping |
| **PostgreSQL** (Drizzle) | İlişkisel veri, production |
| **SQLite** (Drizzle) | Küçük projeler, edge deployment |
| **Supabase** | Auth + DB combo |

### 3.2 — Drizzle Adapter (Postgres) Detayları
```typescript
import { postgresAdapter } from '@payloadcms/db-postgres'

export default buildConfig({
  db: postgresAdapter({
    pool: { connectionString: process.env.DATABASE_URI }
  }),
})
```
- Migration sistemi (`payload migrate`)
- Schema push vs migrations
- Drizzle Studio ile inceleme

### 3.3 — Çoklu Veritabanı Stratejileri
- Dev/Staging/Prod farklı DB'ler
- Seed data oluşturma
- Backup stratejileri

---

## 📚 FAZA 4: ERİŞİM KONTROLÜ (Access Control) (2 Hafta)

### 4.1 — Auth Sistemi
```typescript
export const Users: CollectionConfig = {
  slug: 'users',
  auth: true,
  fields: [
    { name: 'role', type: 'select', options: ['admin', 'editor'] }
  ],
}
```
- `auth: true` ile collection'ı kullanıcı collection'ına çevirme
- JWT session stratejisi
- HTTP-only cookie'ler
- `req.user` API

### 4.2 — Access Function Yazma
```typescript
import { Access } from 'payload'

export const isAdmin: Access = ({ req: { user } }) => {
  return user?.role === 'admin'
}

export const isOwnerOrAdmin: Access = ({ req: { user } }) => {
  if (user?.role === 'admin') return true
  return { author: { equals: user?.id } }
}
```

### 4.3 — Access Tipleri
- `create`, `read`, `update`, `delete` — operasyon bazlı
- `read` için field-level read access
- `admin` field erişimi
- Unauthenticated access tanımı (`() => true`)

### 4.4 — Rol Bazlı Hiyerarşi
- Custom user roles
- Permission'ları merkezileştirme (`src/access/`)
- Collection-level vs field-level

---

## 📚 FAZA 5: HOOKS (YAŞAM DÖNGÜSÜ) (2-3 Hafta)

### 5.1 — Hook Çeşitleri
```typescript
{
  slug: 'posts',
  hooks: {
    beforeChange: [beforeChangeHook],
    afterChange: [afterChangeHook],
    beforeRead: [beforeReadHook],
    afterRead: [afterReadHook],
    beforeDelete: [beforeDeleteHook],
    afterDelete: [afterDeleteHook],
  }
}
```

### 5.2 — Yaygın Hook Kalıpları
- **Slug otomatik üretimi** (beforeValidate)
- **Tarih damgası** (beforeChange)
- **Revalidation** (afterChange) — Next.js cache temizleme
- **Loglama** (afterChange)
- **Side-effect tetikleme** (email, webhook)

### 5.3 — Field-Level Hooks
```typescript
{
  name: 'password',
  type: 'text',
  hooks: {
    beforeChange: [hashPassword],
  }
}
```

### 5.4 — Async Pattern'ler
- Promise handling
- Error propagation
- Transaction context (`req.transactionID`)

---

## 📚 FAZA 6: API'LERİ KULLANMA (2-3 Hafta)

### 6.1 — Local API (Server-side)
```typescript
import { getPayload } from 'payload'
import config from '@payload-config'

const payload = await getPayload({ config })
const posts = await payload.find({
  collection: 'posts',
  where: { status: { equals: 'published' } },
  limit: 10,
  depth: 2,
})
```
- **En performanslı** erişim yöntemi
- Server Components ve Server Actions'ta kullanım
- `find`, `findByID`, `create`, `update`, `delete`

### 6.2 — REST API
- `/api/posts` endpointleri
- Query parametreleri: `?where[status][equals]=published`
- Sort, limit, depth, populate
- Custom endpoints oluşturma:
```typescript
endpoints: [
  {
    path: '/stats',
    method: 'get',
    handler: async (req) => { ... }
  }
]
```

### 6.3 — GraphQL API
- Otomatik GraphQL schema üretimi
- Playground erişimi
- Query/mutation yazımı

### 6.4 — Query (Where) Operatörleri
- `equals`, `not_equals`, `greater_than`, `like`, `in`
- AND/OR mantığı
- Nested where clauses

---

## 📚 FAZA 7: FRONTEND ENTEGRASYONU (2-3 Hafta)

### 7.1 — Server Components ile Veri Çekme
```typescript
// app/(frontend)/blog/page.tsx
import { getPayload } from 'payload'
import config from '@payload-config'

export default async function BlogPage() {
  const payload = await getPayload({ config })
  const { docs } = await payload.find({ collection: 'posts' })
  return <PostList posts={docs} />
}
```

### 7.2 — Server Actions ile Form İşlemleri
```typescript
async function createPost(formData: FormData) {
  'use server'
  const payload = await getPayload({ config })
  await payload.create({
    collection: 'posts',
    data: { title: formData.get('title') as string }
  })
  revalidatePath('/blog')
}
```

### 7.3 — Live Preview (Önizleme)
- Next.js draftMode() entegrasyonu
- Anlık içerik önizleme
- `payload.generatePreviewPath` kullanımı

### 7.4 — SEO ve Metadata
- Dynamic metadata generation
- Open Graph
- Sitemap.xml üretimi

### 7.5 — Arama ve Filtreleme
- Full-text search (Postgres)
- Custom search endpointleri
- Tag/category filtreleme

---

## 📚 FAZA 8: GELİŞMİŞ ÖZELLİKLER (3-4 Hafta)

### 8.1 — Versiyonlama (Versions)
```typescript
versions: {
  drafts: {
    autosave: true,
    schedulePublish: true,
  },
  maxPerDoc: 25,
}
```
- Draft sistemi
- Autosave davranışı
- Zamanlanmış yayınlama
- `_status` field kullanımı

### 8.2 — Yerelleştirme (i18n)
```typescript
i18n: {
  supportedLanguages: { en, tr, de }
}

fields: [
  {
    name: 'title',
    type: 'text',
    localized: true,
  }
]
```
- Locale-aware sorgular
- Frontend'de locale routing

### 8.3 — Custom Field Components
```typescript
{
  name: 'colorPicker',
  type: 'text',
  admin: {
    components: {
      Field: '@/components/ColorPickerField',
    }
  }
}
```
- React component olarak custom field
- Server vs Client component kararı
- Field state yönetimi

### 8.4 — Custom Views (Admin UI Genişletme)
- Tamamen custom admin sayfaları
- Nav linkleri ekleme
- Custom dashboard bileşenleri

### 8.5 — Custom Endpoints
- REST endpointleri
- Webhook altyapısı
- Third-party API entegrasyonları

---

## 📚 FAZA 9: PLUGİN EKOSİSTEMİ (2 Hafta)

### 9.1 — Resmi Payload Plugin'leri
- `@payloadcms/plugin-form-builder`
- `@payloadcms/plugin-seo`
- `@payloadcms/plugin-nested-docs`
- `@payloadcms/plugin-redirects`
- `@payloadcms/plugin-stripe`
- `@payloadcms/plugin-sentry`

### 9.2 — Plugin Kurulumu
```typescript
import { seoPlugin } from '@payloadcms/plugin-seo'

plugins: [
  seoPlugin({
    collections: ['posts', 'pages'],
    uploadsCollection: 'media',
  })
]
```

### 9.3 — Custom Plugin Yazma
- Plugin yapısı (`(options) => (config) => config`)
- Field ekleme
- Collection ekleme
- Hook manipülasyonu

---

## 📚 FAZA 10: AUTH VE GÜVENLİK (2 Hafta)

### 10.1 — Gelişmiş Auth Stratejileri
- Email verification
- Password reset
- Magic link auth (custom strategy)
- OAuth (Google, GitHub) — custom strategy
- 2FA / TOTP

### 10.2 — Custom Auth Strategy
```typescript
// authStrategies: [
//   { name: 'google', authenticate: ... }
// ]
```
- JWT strategy customization
- Cookie ayarları (`sameSite`, `secure`)
- Session expiration

### 10.3 — Rate Limiting
- Brute-force koruması
- Custom rate limit middleware

### 10.4 — CORS ve CSRF
- Payload'ın built-in korumaları
- Frontend origin ayarları
- Production CSP

---

## 📚 FAZA 11: DEPLOYMENT VE PRODÜKSİYON (2-3 Hafta)

### 11.1 — Build Süreci
```bash
npm run build
payload migrate
```
- Next.js build aşamaları
- Static vs dynamic admin
- Bundle analizi

### 11.2 — Deployment Platformları
| Platform | Notlar |
|---|---|
| **Vercel** | Next.js ile mükemmel entegrasyon |
| **Railway** | Postgres ile kolay setup |
| **Render** | Hem DB hem app |
| **Self-hosted** | Docker + VPS |
| **Fly.io** | Edge deployment |
| **Netlify** | Serverless functions |

### 11.3 — Environment Variables
- Secret yönetimi
- Database URL'leri
- S3/cloud storage keys
- `.env` dosya yapısı

### 11.4 — Production Checklist
- HTTPS zorunlu
- Admin URL'i özelleştir (`/manage` vb.)
- Database backup stratejisi
- Monitoring (Sentry, LogRocket)
- Performance: ISR, caching

### 11.5 — CI/CD
- GitHub Actions ile test
- Otomatik migration
- Preview deployments

---

## 📚 FAZA 12: TEST VE PERFORMANS (2 Hafta)

### 12.1 — Test Stratejileri
- **Unit tests**: Vitest ile hook/function testleri
- **Integration tests**: Payload test utils
- **E2E tests**: Playwright ile admin UI
- API endpoint testleri

### 12.2 — Payload Test Helpers
```typescript
import { initPayloadInt } from 'payload'

beforeAll(async () => {
  await initPayloadInt(config)
})
```

### 12.3 — Performans Optimizasyonu
- `depth` kullanımını minimize etme
- Select: sadece gerekli field'lar
- Database indexleme
- Image optimization
- Caching stratejileri

---

## 📚 FAZA 13: PROJELER (Uygulama) (4-6 Hafta)

### 🛠️ Proje 1: Blog Sistemi (1-2 Hafta)
- Posts + Categories + Tags + Authors
- Rich text editör
- Image upload
- SEO plugin
- Frontend: Next.js blog sayfaları

### 🛠️ Proje 2: E-Ticaret CMS (2 Hafta)
- Products, Categories, Orders
- Stripe entegrasyonu
- Variant'lar (array field)
- Inventory tracking
- Custom hooks

### 🛠️ Proje 3: Çok Kiracılı (Multi-tenant) SaaS (2 Hafta)
- Tenant bazlı veri ayrımı
- Custom access control
- Subdomain routing
- Custom admin

### 🛠️ Proje 4: Real-world Production App (2+ Hafta)
- Auth, payments, multi-language
- Webhook entegrasyonları
- Email bildirimleri
- Full deployment

---

## 🎯 ALT TOPIC'LERİN HIZLI HARİTASI

```
Payload CMS v3
├── Konfigürasyon
│   ├── collections
│   ├── globals
│   ├── fields
│   └── access
├── Veri Katmanı
│   ├── adapters (Postgres/Mongo/SQLite)
│   ├── hooks
│   └── migrations
├── API Katmanı
│   ├── Local API
│   ├── REST
│   └── GraphQL
├── Auth & Güvenlik
│   ├── strategies
│   ├── access control
│   └── rate limiting
├── Admin UI
│   ├── custom fields
│   ├── custom views
│   └── plugins
├── Next.js Entegrasyonu
│   ├── Server Components
│   ├── Server Actions
│   ├── Live Preview
│   └── Revalidation
└── Production
    ├── deployment
    ├── monitoring
    └── testing
```

---

## 📖 ÖNERİLEN KAYNAKLAR

### Resmi
- 📘 [Payload Docs v3](https://payloadcms.com/docs)
- 📘 [Next.js + Payload blog yazıları](https://payloadcms.com/blog)
- 💻 Payload GitHub örnekleri

### Topluluk
- 💬 Payload Discord
- 🎥 YouTube: "Payload CMS v3" araması
- 🐦 Payload Twitter/X güncellemeleri
- 📦 Payload Templates (resmi starter'lar)

---

## ⏱️ Tahmini Toplam Süre

| Profil | Süre |
|---|---|
| Yoğun (haftada 15-20 saat) | **12-16 hafta** |
| Orta (haftada 8-10 saat) | **20-24 hafta** |
| Rahat (haftada 4-5 saat) | **30-40 hafta** |

---

## 💡 Önerilen Çalışma Yöntemi

1. **Her faza %80 teorik + %20 pratik** oranıyla başla
2. **Her konuyu bitirince** küçük bir deneme yap
3. **Faza 13'teki projeler** öğrendiklerini pekiştirecek
4. **Takıldığında** Payload'ın source code'una GitHub'dan bak — açık kaynak ve okunabilir
5. **TypeScript bilgini güçlendir** — v3 ile neredeyse zorunlu

Hangi fazadan başlamak istiyorsun? İstersen herhangi bir fazayı daha da detaylı açabilirim, örnek projelerle birlikte kodlayabiliriz. 🚀
