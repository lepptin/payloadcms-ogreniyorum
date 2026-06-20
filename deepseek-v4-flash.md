Harika bir hedef belirlemişsiniz! JavaScript, React ve Next.js altyapınızla Payload CMS v3’ü öğrenmek için çok doğru bir yoldasınız. Payload v3, Next.js App Router ile tam uyumlu, headless bir CMS olarak modern web geliştirme için ideal. Aşağıda, sıfırdan ileri seviyeye kadar kapsamlı, haftalık bir müfredat planı hazırladım. Her hafta teorik bilgi, pratik alıştırmalar ve kaynaklar içeriyor.

---

## 🗓️ 8 Haftalık Kapsamlı Payload CMS v3 Müfredatı

### Hafta 1: Payload CMS’e Giriş ve Kurulum
**Amaç:** Payload’ın felsefesini, mimarisini anlamak ve ilk projeyi ayağa kaldırmak.

- **Teori:**
  - Headless CMS nedir? Payload’ın diğer CMS’lerden farkı (ör. Strapi, Sanity).
  - Payload v3’ün Next.js ile entegrasyonu (App Router, Server Components).
  - Temel kavramlar: Koleksiyon (Collection), Global, Alan (Field), Erişim Kontrolü.
- **Pratik:**
  - `npx create-payload-app` ile yeni bir proje oluşturma (Next.js + TypeScript seçeneği).
  - Geliştirme ortamını kurma: MongoDB (veya PostgreSQL) bağlantısı, `.env` ayarları.
  - Admin paneli arayüzünü inceleme: Koleksiyon listesi, düzenleme formu, medya yöneticisi.
- **Alıştırma:** Basit bir `Posts` koleksiyonu oluşturun (title, content, status alanları). Admin panelinden birkaç post ekleyin.
- **Kaynaklar:**
  - [Payload Resmi Dokümantasyonu](https://payloadcms.com/docs)
  - [Payload v3 Quick Start](https://payloadcms.com/docs/getting-started/quick-start)

---

### Hafta 2: Koleksiyonlar ve Alanlar (Fields) Derinlemesine
**Amaç:** Koleksiyon yapılandırmasını ve tüm alan türlerini öğrenmek.

- **Teori:**
  - Koleksiyon yapılandırması: `slug`, `fields`, `admin`, `access`, `hooks`.
  - Alan türleri: `text`, `textarea`, `richText`, `number`, `select`, `checkbox`, `date`, `relationship`, `array`, `blocks`, `group`, `upload`, `code`, `json`, `ui`.
  - Özel alanlar (custom fields) oluşturma: `Field` tipi, `admin` özellikleri.
- **Pratik:**
  - `Categories` koleksiyonu oluşturun (name, description, parent relationship).
  - `Posts` koleksiyonuna `category` (relationship), `tags` (array of text), `publishedAt` (date) ekleyin.
  - Rich Text alanını özelleştirin (toolbar, admin settings).
- **Alıştırma:** Bir `Authors` koleksiyonu oluşturun (name, avatar upload, bio rich text). `Posts` ile `author` ilişkisi kurun.
- **Kaynaklar:**
  - [Payload Fields Dokümantasyonu](https://payloadcms.com/docs/fields/overview)
  - [Rich Text Alanı](https://payloadcms.com/docs/fields/rich-text)

---

### Hafta 3: Global’ler, Versiyonlama ve Draft/Publish
**Amaç:** Global veri yönetimi, içerik sürümleme ve yayın akışını kavramak.

- **Teori:**
  - Global nedir? Koleksiyondan farkı (tekil veri, örn. site ayarları, header/footer).
  - Versiyonlama (versioning): Otomatik geçmiş, geri alma, karşılaştırma.
  - Draft/Publish sistemi: `status` alanı, `draft` ve `published` durumları.
- **Pratik:**
  - `SiteSettings` global’i oluşturun (site adı, logo upload, sosyal medya linkleri).
  - `Posts` koleksiyonunda versiyonlama ve draft/publish’i etkinleştirin.
  - Admin panelinde versiyon geçmişini inceleyin, geri alma işlemi yapın.
- **Alıştırma:** `Navigation` global’i oluşturun (menü öğeleri array, her öğe için label ve link). Admin’den menüyü düzenleyin.
- **Kaynaklar:**
  - [Global Dokümantasyonu](https://payloadcms.com/docs/globals/overview)
  - [Versiyonlama](https://payloadcms.com/docs/versions/overview)

---

### Hafta 4: Erişim Kontrolü ve Yetkilendirme
**Amaç:** Kullanıcı rolleri, izinler ve API güvenliğini yönetmek.

- **Teori:**
  - Payload’ın erişim kontrol modeli: `access` fonksiyonları (read, create, update, delete, admin).
  - Kullanıcı koleksiyonu (`users`): varsayılan alanlar, özel alan ekleme.
  - Rol tabanlı erişim: `roles` alanı, `access` fonksiyonlarında rol kontrolü.
  - API anahtarları (API keys) ve public erişim.
- **Pratik:**
  - `users` koleksiyonuna `role` select alanı ekleyin (admin, editor, viewer).
  - `Posts` koleksiyonunda `access` fonksiyonları yazın: sadece admin ve editor create/update yapabilsin, viewer sadece published postları görebilsin.
  - Public API’den postları çekmek için `readAccess`’i public yapın.
- **Alıştırma:** Bir `Comments` koleksiyonu oluşturun. Sadece giriş yapmış kullanıcılar yorum ekleyebilsin, admin tüm yorumları silebilsin.
- **Kaynaklar:**
  - [Access Control Dokümantasyonu](https://payloadcms.com/docs/access-control/overview)
  - [Kullanıcı Yönetimi](https://payloadcms.com/docs/authentication/overview)

---

### Hafta 5: Medya Yönetimi ve Dosya İşlemleri
**Amaç:** Resim, video ve diğer dosyaları yüklemek, dönüştürmek ve sunmak.

- **Teori:**
  - `upload` alanı: resim boyutlandırma (image sizes), format dönüşümü, kırpma.
  - Medya koleksiyonu (`media`): varsayılan alanlar, özel alan ekleme.
  - Dosya depolama: yerel disk, S3, Cloudinary, Google Cloud Storage.
  - Admin panelinde medya yöneticisi.
- **Pratik:**
  - `media` koleksiyonuna `altText` ve `caption` alanları ekleyin.
  - Resim yükleme sırasında otomatik thumbnail oluşturma (ör. 400x400, 800x800).
  - S3 entegrasyonu için `payload.config`’e storage ayarlarını ekleyin.
- **Alıştırma:** `Posts` koleksiyonundaki `featuredImage` alanını `upload` tipine çevirin. Admin panelinden resim yükleyin ve ön yüzde gösterin.
- **Kaynaklar:**
  - [Upload Alanı](https://payloadcms.com/docs/fields/upload)
  - [Medya Depolama](https://payloadcms.com/docs/upload/storage)

---

### Hafta 6: Next.js ile Ön Yüz Geliştirme
**Amaç:** Payload API’sini kullanarak Next.js uygulamasında içerik çekme ve görüntüleme.

- **Teori:**
  - Payload REST API ve GraphQL API (v3’te GraphQL desteği).
  - Next.js App Router ile veri çekme: `fetch` veya Payload SDK (payloadcms/payload-client).
  - Server Components vs Client Components: hangi durumda hangisi kullanılır.
  - Dinamik routing: `[slug]` sayfaları, `generateStaticParams` ile SSG.
- **Pratik:**
  - `payloadcms/payload-client` SDK’sını kurun ve bir `getPosts` fonksiyonu yazın.
  - Ana sayfada post listesini gösterin (title, excerpt, featuredImage).
  - `posts/[slug]` sayfası oluşturun, post detayını getirin.
  - `revalidate` ile ISR (Incremental Static Regeneration) ekleyin.
- **Alıştırma:** `SiteSettings` global’ini kullanarak header ve footer’ı tüm sayfalarda gösterin. `Navigation` global’inden menüyü çekin.
- **Kaynaklar:**
  - [Payload REST API](https://payloadcms.com/docs/rest-api/overview)
  - [Payload Client SDK](https://github.com/payloadcms/payload-client)
  - [Next.js Data Fetching](https://nextjs.org/docs/app/building-your-application/data-fetching)

---

### Hafta 7: İleri Düzey Özellikler
**Amaç:** Webhook’lar, eklentiler, özel bileşenler ve performans optimizasyonu.

- **Teori:**
  - Webhook’lar: koleksiyon olaylarına (create, update, delete) tetiklenen HTTP istekleri.
  - Payload eklentileri (plugins): mevcut eklentiler (SEO, form builder, cloud storage) ve özel eklenti yazma.
  - Özel admin bileşenleri (custom components): admin panelinde özel UI elemanları (ör. özel bir dashboard widget).
  - Performans: sorgu optimizasyonu, `depth` parametresi, `limit` ve `page`.
- **Pratik:**
  - `Posts` koleksiyonuna bir webhook ekleyin: post yayınlandığında bir Slack kanalına bildirim gönderin (ör. Zapier veya kendi endpoint’iniz).
  - `payload-seo` eklentisini kurun ve postlara SEO meta alanları ekleyin.
  - Admin panelinde özel bir “Dashboard” bileşeni oluşturun (ör. son 10 post ve istatistikler).
- **Alıştırma:** Kendi eklentinizi yazın: post oluşturulduğunda otomatik olarak bir `slug` oluşturan basit bir eklenti.
- **Kaynaklar:**
  - [Webhook Dokümantasyonu](https://payloadcms.com/docs/webhooks/overview)
  - [Payload Eklentileri](https://payloadcms.com/docs/plugins/overview)
  - [Özel Bileşenler](https://payloadcms.com/docs/admin/custom-components)

---

### Hafta 8: Deployment, Production ve Proje Tamamlama
**Amaç:** Projeyi canlıya almak, performans ve güvenlik ayarlarını yapmak.

- **Teori:**
  - Deployment seçenekleri: Vercel, Railway, DigitalOcean, AWS.
  - Environment değişkenleri, secret yönetimi.
  - MongoDB Atlas veya PostgreSQL (production veritabanı).
  - SSL, CORS, rate limiting.
  - Loglama ve hata izleme (Sentry, LogRocket).
- **Pratik:**
  - Projeyi Vercel’e deploy edin (Next.js + Payload aynı projede).
  - MongoDB Atlas’a bağlanın.
  - `.env.production` dosyası oluşturun, `PAYLOAD_SECRET`, `DATABASE_URI` gibi değişkenleri ayarlayın.
  - Admin panelini password korumalı yapın (zaten varsayılan).
- **Alıştırma:** Tüm haftalardaki çalışmaları birleştirerek tam bir blog sitesi (veya portföy sitesi) oluşturun. Canlıya alın ve test edin.
- **Kaynaklar:**
  - [Payload Deployment Guide](https://payloadcms.com/docs/deployment/overview)
  - [Vercel Deployment](https://payloadcms.com/docs/deployment/vercel)

---

## 🧠 Ek Öneriler

- **Proje Tabanlı Öğrenme:** Her hafta sonunda küçük bir proje parçası ekleyin. 8. haftada tüm parçaları birleştirip tam bir uygulama çıkarın.
- **Payload Discord Topluluğu:** [Payload Discord](https://discord.gg/payload) – sorularınızı sorun, örnek projeleri inceleyin.
- **Örnek Projeler:** GitHub’da `payloadcms/payload` reposundaki `examples` klasörünü inceleyin (örn. `nextjs`, `custom-server`).
- **TypeScript Kullanımı:** Payload v3 TypeScript ile yazılmıştır. Tip güvenliğinden maksimum faydalanmak için projenizde TypeScript kullanın.
- **Test Yazma:** Koleksiyonlarınız ve API’niz için testler ekleyin (Jest, Playwright). Payload’ın test yardımcıları mevcut.

---

Bu müfredatı takip ederek 8 hafta içinde Payload CMS v3’ü profesyonel düzeyde öğrenebilirsiniz. Her hafta en az 10-15 saat ayırmanızı öneririm. Başarılar! 🚀
