Payload CMS 3, özellikle Next.js App Router ile derin entegrasyonu sayesinde modern web geliştirmenin en güçlü araçlarından biri haline geldi. JavaScript, React ve Next.js altyapınız, bu öğrenme sürecini çok hızlandıracak.

İşte size adım adım, temelden ileri seviyeye uzanan kapsamlı bir Payload CMS 3 öğrenme müfredatı:

---

### Payload CMS 3 Uzmanlık Müfredatı

**Hedef Kitle:** React, Next.js ve JavaScript bilen geliştiriciler.  
**Süre:** Yaklaşık 6-8 hafta (kendi hızınıza göre ayarlayabilirsiniz).  
**Yöntem:** Her modül teorik bilgi, dokümantasyon incelemesi ve pratik uygulama içerir.

---

### Modül 1: Temeller ve Felsefe (1. Hafta)

**Amaç:** Payload'ın ne olduğunu, rakiplerinden neden ayrıldığını ve temel mimarisini anlamak.

- **Konular:**
    - Headless CMS nedir? Payload'ın konumu (Contentful, Strapi, Sanity ile karşılaştırma).
    - **Payload 3'ün Devrimi:** Neden tamamen Next.js üzerine yeniden inşa edildi? App Router, React Server Components (RSC) ve Server Actions ile doğal uyum.
    - Yerel veritabanı (Local API) vs. REST/GraphQL API kavramı.
    - Temel kurulum: `create-payload-app` ile boş bir proje oluşturma.
    - Proje yapısının incelenmesi: `payload.config.ts`, `server.ts`, `app/(payload)` klasör yapısı.
    - Admin paneli tanıma.

- **Pratik:**
    - Sıfırdan bir Payload projesi oluşturun.
    - Admin paneline giriş yapın, varsayılan Users koleksiyonunu inceleyin.
    - `.env` dosyası ve `DATABASE_URI` yapılandırmasını öğrenin (SQLite ile başlayın).

- **Kaynaklar:**
    - [Payload CMS Resmi Dokümantasyonu - Başlangıç](https://payloadcms.com/docs/getting-started/installation)
    - [Payload 3.0 Duyuru Blog Yazısı](https://payloadcms.com/blog/payload-3-0)

---

### Modül 2: Konfigürasyon ve Koleksiyonlar (1-2. Hafta)

**Amaç:** Payload'ın kalbi olan konfigürasyon dosyasını ve koleksiyonları derinlemesine öğrenmek.

- **Konular:**
    - `payload.config.ts` detaylı incelenmesi.
    - **Koleksiyonlar (Collections):**
        - Alan tipleri (Fields): text, number, date, richText, upload, relationship, array, blocks, JSON, vb.
        - Alan doğrulama (validation), varsayılan değerler, zorunluluk.
        - `hooks` (beforeChange, afterChange, beforeRead, afterRead, vb.).
        - `access` kontrolü (create, read, update, delete - CRUD).
        - `admin` panel özelleştirmeleri (grup, açıklama, liste görünümü).
    - **Globals:** Tekil veri yapıları (site ayarları, header/footer).
    - **Upload Koleksiyonları:** Medya yönetimi, boyut sınırları, mime-type kontrolü.

- **Pratik Proje: "Blog Sistemi"**
    - `Posts` koleksiyonu: title, slug (auto-generate), author (relationship), content (richText), featuredImage (upload), tags (array), status (select).
    - `Categories` koleksiyonu: name, slug.
    - `Media` upload koleksiyonu.
    - `SiteSettings` global'i: site adı, logo, sosyal medya linkleri.
    - Admin panelinde listelere özel sütunlar ekleyin, filtreleme ve arama yapılandırın.

- **Kaynaklar:**
    - [Koleksiyon Konfigürasyonu](https://payloadcms.com/docs/configuration/collections)
    - [Alanlar (Fields)](https://payloadcms.com/docs/fields/overview)
    - [Globals](https://payloadcms.com/docs/configuration/globals)

---

### Modül 3: Next.js Entegrasyonu ve Frontend (2-3. Hafta)

**Amaç:** Payload'ı Next.js App Router ile sorunsuzca kullanarak içerikleri görüntülemek.

- **Konular:**
    - **Local API:** `payload.find()`, `payload.findByID()`, `payload.create()` metodlarının Server Components içinde doğrudan kullanımı. Veritabanına ek bir HTTP isteği olmadan erişmenin gücü.
    - **React Server Components (RSC) ile Veri Çekme:** Async component'ler.
    - **Live Preview:** Admin panelde içerik düzenlerken anlık önizleme. `useLivePreview` hook'u.
    - **Şablonlar (Templates):** Sayfa yapılarını oluşturmak için Blocks ve Array alanlarının frontend'de render edilmesi.
    - **Dinamik Rota Oluşturma:** `generateStaticParams` ile koleksiyon slug'larına göre sayfa üretme.
    - **Zengin Metin (Rich Text) Render:** `@payloadcms/richtext-lexical` paketi ile özel render fonksiyonları.

- **Pratik Proje: "Blog Frontend"**
    - Ana sayfa: son blog yazılarını listeleyin.
    - Kategori sayfası: kategoriye ait yazıları filtreleyin.
    - Blog detay sayfası: `[slug]` rotası, zengin metin içeriğini render edin.
    - Admin panelde "Preview" butonu ile canlı önizleme çalıştırın.
    - `SiteSettings` global'inden header/footer bilgilerini çekip layout'a ekleyin.

- **Kaynaklar:**
    - [Next.js Entegrasyonu](https://payloadcms.com/docs/nextjs/overview)
    - [Local API](https://payloadcms.com/docs/local-api/overview)
    - [Live Preview](https://payloadcms.com/docs/live-preview/overview)

---

### Modül 4: Yetkilendirme, Kimlik Doğrulama ve Erişim Kontrolü (3. Hafta)

**Amaç:** Çok kullanıcılı, roller ve izinlere dayalı güvenli bir sistem kurmak.

- **Konular:**
    - `Users` koleksiyonu ve `auth` özelliği (email, password, token tabanlı).
    - **Erişim Kontrolü (Access Control):** Koleksiyon, global ve alan seviyesinde fonksiyon tabanlı erişim.
    - Roller ve izinler: `admin`, `editor`, `public` gibi özel roller tanımlama.
    - `beforeChange` hook'u ile otomatik rol atama.
    - Next.js middleware ile korumalı rotalar.
    - Frontend'de kullanıcı girişi/kaydı için Server Actions kullanımı.

- **Pratik:**
    - `Users` koleksiyonuna `role` alanı ekleyin (admin, editor, user).
    - `Posts` koleksiyonunda: sadece `admin` ve `editor` oluşturabilsin, `user` sadece kendi yazısını güncelleyebilsin.
    - `/dashboard` rotasını sadece giriş yapmış kullanıcılara açın.
    - Kullanıcı kaydı ve girişi için formlar oluşturun.

- **Kaynaklar:**
    - [Kimlik Doğrulama](https://payloadcms.com/docs/authentication/overview)
    - [Erişim Kontrolü](https://payloadcms.com/docs/access-control/overview)

---

### Modül 5: Plugin Sistemi ve Özelleştirmeler (4. Hafta)

**Amaç:** Payload'ın modüler yapısını kullanarak hazır plugin'leri entegre etmek ve kendi plugin'lerinizi yazmak.

- **Konular:**
    - Resmi plugin'ler: `@payloadcms/plugin-seo`, `@payloadcms/plugin-nested-docs`, `@payloadcms/plugin-form-builder`, `@payloadcms/plugin-search`.
    - SEO plugin'i: meta title, description, og:image alanlarını otomatik eklemek.
    - Nested Docs: sayfa ağaç yapısı (parent/child).
    - **Özel Plugin Yazımı:** `createPlugin` fonksiyonu, plugin yapısı, koleksiyon/global/alan ekleme, hook'ları genişletme.
    - **Özel Bileşenler (Custom Components):** Admin panelinde özel React bileşenleri kullanma (alan bileşeni, görünüm bileşeni).

- **Pratik:**
    - Blog projesine SEO plugin'ini entegre edin.
    - Sayfalar için Nested Docs plugin'ini kurun, admin panelde ağaç görünümü oluşturun.
    - Basit bir "Newsletter" plugin'i yazın: `Subscribers` koleksiyonu, admin panelde özel bir dashboard widget'ı.

- **Kaynaklar:**
    - [Resmi Plugin'ler](https://payloadcms.com/docs/plugins/overview)
    - [Özel Plugin Geliştirme](https://payloadcms.com/docs/plugins/custom)

---

### Modül 6: İleri Seviye Veritabanı ve Mimari (5. Hafta)

**Amaç:** Payload'ın veritabanı katmanını, ilişkileri ve performans optimizasyonlarını anlamak.

- **Konular:**
    - **Drizzle ORM:** Payload 3'ün temelindeki ORM. Ham SQL sorguları yazma, migration'lar.
    - Veritabanı seçimi: SQLite (geliştirme) vs. PostgreSQL (production).
    - **İlişkiler:** one-to-one, one-to-many, many-to-many. `hasMany`, `relationTo` kullanımı.
    - Derin popülasyon (deep population) ve performans etkileri.
    - `payload.db` ile doğrudan Drizzle işlemleri.
    - **Versiyonlama ve Taslaklar:** `versions` özelliği ile içerik geçmişi, taslak/otomatik kaydetme.
    - **Localizasyon (i18n):** Çok dilli içerik yönetimi, alan seviyesinde çeviri.

- **Pratik:**
    - Blog'u PostgreSQL'e taşıyın, migration oluşturun.
    - `Posts` koleksiyonuna `versions` ve `drafts` özelliğini ekleyin.
    - İçerikleri iki dilde (TR/EN) yönetmek için localizasyon kurun.
    - Karmaşık bir ilişki: `Products` -> `Categories` -> `Brands` (çoklu ilişkiler).

- **Kaynaklar:**
    - [Veritabanı](https://payloadcms.com/docs/database/overview)
    - [Versiyonlar](https://payloadcms.com/docs/versions/overview)
    - [Localizasyon](https://payloadcms.com/docs/localization/overview)

---

### Modül 7: Deployment, DevOps ve Production Best Practices (6. Hafta)

**Amaç:** Payload projesini canlıya almak, ölçeklendirmek ve güvenli hale getirmek.

- **Konular:**
    - **Deployment Seçenekleri:** Vercel, Railway, DigitalOcean, kendi VPS'iniz.
    - **Vercel Deployment:** Next.js ile tek repo, serverless fonksiyonlar, blob storage (Medya için).
    - **Ortam Değişkenleri:** `PAYLOAD_SECRET`, veritabanı bağlantıları, API anahtarları.
    - **Medya Depolama:** `@payloadcms/storage-s3` veya `@payloadcms/storage-vercel` ile bulut depolama.
    - **E-posta Ayarları:** SMTP veya Resend entegrasyonu (şifre sıfırlama, bildirimler).
    - **Hata İzleme ve Loglama:** Sentry, Pino logger.
    - **CI/CD:** GitHub Actions ile otomatik deployment.

- **Pratik:**
    - Blog projesini Vercel'e deploy edin.
    - Medya dosyalarını Vercel Blob Storage'a yönlendirin.
    - Resend ile e-posta gönderimini yapılandırın.
    - Temel bir GitHub Actions workflow'u oluşturun.

- **Kaynaklar:**
    - [Production Deployment](https://payloadcms.com/docs/production/deployment)
    - [Cloud Storage](https://payloadcms.com/docs/cloud-storage/overview)
    - [Email](https://payloadcms.com/docs/email/overview)

---

### Modül 8: Gerçek Dünya Projesi ve İleri Teknikler (7-8. Hafta)

**Amaç:** Tüm öğrendiklerinizi birleştirerek kompleks, production-ready bir proje inşa etmek.

- **Proje Önerisi: "Çok Dilli E-ticaret İçerik Yönetimi"**
    - `Products` koleksiyonu: çoklu dil, versiyonlama, fiyat, stok, medya galerisi, ilişkili ürünler.
    - `Orders` koleksiyonu: kullanıcı ilişkisi, sipariş durumu, özel hook'lar (stok düşme).
    - `Pages` koleksiyonu: Blocks ile esnek sayfa yapısı (Hero, Ürün Grid, Metin+Resim, CTA).
    - Özel admin panel bileşenleri: Sipariş grafiği, stok uyarıları.
    - Frontend: Next.js ile statik/dinamik sayfalar, ürün filtreleme, sepet (local state), Stripe ödeme entegrasyonu.
    - **İleri Hook Kullanımı:** `afterChange` hook'u ile Elasticsearch/Search plugin'e veri gönderme.
    - **Webhook'lar:** İçerik değişikliklerinde dış servisleri tetikleme.

- **Kaynaklar:**
    - [Payload E-ticaret Şablonu](https://github.com/payloadcms/payload/tree/main/templates/ecommerce)
    - [Payload Examples](https://github.com/payloadcms/payload/tree/main/examples)

---

### Öğrenme Kaynakları ve Topluluk

- **Resmi Dokümantasyon:** [payloadcms.com/docs](https://payloadcms.com/docs) (Başucu kaynağınız bu olmalı).
- **Payload YouTube Kanalı:** Özellikle 3.0 tanıtım videoları ve canlı yayınlar.
- **GitHub Deposu:** [payloadcms/payload](https://github.com/payloadcms/payload) (Örnekleri, şablonları inceleyin).
- **Payload Discord Topluluğu:** Sorularınız için en hızlı destek.
- **Next.js Dokümantasyonu:** App Router, Server Components ve Server Actions konularını sürekli taze tutun.

---

### Önemli İpuçları

1.  **Local API'yi Sevin:** Payload 3'ün en büyük gücü, veritabanına doğrudan erişimdir. Next.js Server Components içinde `payload.find()` kullanmak, ayrı bir REST API katmanına olan ihtiyacı ortadan kaldırır.
2.  **TypeScript'in Gücünü Kullanın:** Payload, koleksiyon konfigürasyonlarınızdan otomatik tip üretir. `import { Post } from '@/payload-types'` ile tam tip güvenliği elde edersiniz.
3.  **Admin Panelini Özelleştirmekten Çekinmeyin:** İhtiyacınız olan her yere özel React bileşenleri enjekte edebilirsiniz.
4.  **Toplulukla Etkileşimde Kalın:** Payload hızla gelişiyor, Discord'da yeni özellikleri ve en iyi uygulamaları takip edin.

Bu müfredat, sizi Payload CMS 3 ile production seviyesinde projeler geliştirebilecek bir uzman haline getirecek şekilde tasarlandı. Her modüldeki pratikleri mutlaka yapın, çünkü Payload'ı gerçekten anlamanın yolu kod yazmaktan geçiyor. Başarılar!
