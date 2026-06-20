JavaScript, React ve Next.js altyapınız olduğu için Payload CMS'i çok daha hızlı öğrenebilirsiniz. Ancak çoğu kişinin yaptığı hata, Payload'u "bir CMS" gibi öğrenmeye çalışmasıdır. Payload v3 aslında:

* Headless CMS
* Backend Framework
* Admin Panel Generator
* Authentication Server
* API Layer
* Next.js ile tam entegre Full-Stack Platform

olarak düşünülmelidir.

Bu nedenle eğitim planını "CMS kullanımı" değil, "Payload ile ürün geliştirme" perspektifinde hazırlamak daha doğru olur.

---

# PAYLOAD CMS V3 MASTERCLASS YOL HARİTASI

Toplam Süre:

* Temel Seviye → 2-3 hafta
* Orta Seviye → 4-6 hafta
* İleri Seviye → 6-8 hafta

Toplam:
Yaklaşık 3 aylık çalışma sonunda gerçek projeler geliştirebilecek seviyeye ulaşabilirsiniz.

---

# MODÜL 0

# Payload CMS Nedir?

Amaç:

Payload'un mimarisini anlamak.

## Öğrenilecek Konular

### Headless CMS nedir?

Karşılaştırma:

* WordPress
* Strapi
* Directus
* Payload

### Payload'ın Yapısı

```text
payload.config.ts

Collections
Globals

Admin UI

REST API
GraphQL API

Database

Hooks
Access Control

Jobs
Auth
Upload
```

### Payload v3 Yenilikleri

Özellikle:

* Next.js App Router entegrasyonu
* Server Components
* Turbopack desteği
* Monorepo yaklaşımı

---

# MODÜL 1

# Kurulum ve Proje Yapısı

Amaç:

Payload'ın oluşturduğu yapıyı anlamak.

## Uygulama

Yeni proje oluşturma:

```bash
npx create-payload-app
```

İncelenecek dosyalar:

```text
src/

payload.config.ts

collections/

globals/

app/

components/
```

### Öğrenilecek

payload.config.ts

Örnek:

```ts
export default buildConfig({
 collections: [],
 globals: [],
})
```

### Görev

Admin paneline giriş yap.

İlk koleksiyonunu oluştur.

---

# MODÜL 2

# Collections

Payload'un kalbi.

---

## Collection Nedir?

Örnek:

```ts
Users
Products
Orders
Posts
Categories
```

---

## Field Tipleri

### Text

```ts
{
  name: 'title',
  type: 'text'
}
```

### Number

### Date

### Email

### Select

### Checkbox

### Relationship

### Upload

### Blocks

### JSON

### Array

### Group

---

## Uygulama

Blog sistemi oluştur:

```text
Posts
Categories
Authors
```

---

# MODÜL 3

# Admin Panel Özelleştirme

Amaç:

Payload Admin'i anlamak.

---

## Sidebar

## Collection Label

## Default Columns

## Custom Views

## Custom Components

---

### Uygulama

Ürün yönetim ekranı tasarla.

---

# MODÜL 4

# Database Modelleme

Bu modül çok önemli.

Sizin süreç modelleme ilginizi düşünürsek özellikle burada derinleşmenizi öneririm.

---

## MongoDB

Payload'ın Mongo desteği

## PostgreSQL

Payload v3'ün önerdiği yapı

### İlişkiler

One To One

```text
User
Profile
```

One To Many

```text
Category
Posts
```

Many To Many

```text
Products
Tags
```

---

### Uygulama

E-Ticaret modeli oluştur.

```text
Users
Addresses
Orders
OrderItems
Products
Categories
```

---

# MODÜL 5

# Authentication

Bu modül sizin ERP entegrasyonlarınız için çok önemli.

---

## Auth Collection

```ts
auth: true
```

---

## Login

```http
/api/users/login
```

## Logout

```http
/api/users/logout
```

## Me

```http
/api/users/me
```

## Refresh Token

JWT yapısı

---

## External Authentication

Buraya özellikle odaklanın.

Payload v3:

```ts
auth: {
  strategies: []
}
```

Custom Strategy

LDAP

ERP

CRM

SSO

OAuth

---

### Proje

ERP kullanıcıları ile giriş.

---

# MODÜL 6

# Access Control

Payload'un en güçlü kısmı.

---

## Collection Access

```ts
access: {
  read: ...
  create: ...
  update: ...
  delete: ...
}
```

---

## Role Based Access

```text
Admin
Manager
Operator
Customer
```

---

## Field Level Access

```ts
salary
```

Sadece yöneticiler görebilsin.

---

### Proje

Kurumsal Personel Sistemi

---

# MODÜL 7

# Hooks

Payload'u framework yapan kısım.

---

## beforeValidate

## beforeChange

## afterChange

## afterRead

## afterDelete

---

Örnek:

```ts
afterChange
```

Sipariş oluşunca:

```text
Stok düş
Mail gönder
ERP entegrasyonu
```

---

### Proje

Sipariş yönetim sistemi.

---

# MODÜL 8

# Relationship ve Veri Modelleme

Burada MongoDB düşünmeyin.

Domain Modelleme düşünün.

---

Örnek:

```text
Sipariş
 ├─ Sipariş Kalemi
 ├─ Müşteri
 ├─ Adres
 └─ Ödeme
```

Payload'ta nasıl modellenir?

---

### Uygulama

Tam e-ticaret şeması.

---

# MODÜL 9

# Upload Sistemi

---

## Upload Collection

```ts
upload: true
```

---

## Görsel İşleme

```ts
imageSizes
```

---

## S3

Payload + AWS

---

## MinIO

Payload + Self Hosted

---

### Proje

Ürün resim sistemi.

---

# MODÜL 10

# Globals

Tek kayıtlı veriler.

---

Örnek:

```text
Site Settings

SEO

Footer

Header

Company Info
```

---

### Proje

Kurumsal site ayarları.

---

# MODÜL 11

# Blocks

Payload'un en güçlü özelliklerinden biri.

---

## Dynamic Page Builder

```text
Hero

Banner

FAQ

Gallery

Video
```

---

### Uygulama

Landing Page Builder

---

# MODÜL 12

# API Katmanı

---

## REST API

```http
/api/posts
```

---

## GraphQL

```graphql
query {
 posts {}
}
```

---

## Local API

Payload'un en güçlü özelliği.

```ts
payload.find()
```

---

### Proje

Headless blog.

---

# MODÜL 13

# Next.js Entegrasyonu

Sizin mevcut deneyiminiz nedeniyle kritik modül.

---

## Server Components

## Server Actions

## ISR

## SSR

## SSG

---

Payload ile veri çekme:

```ts
getPayload()
```

---

### Uygulama

Blog Frontend

---

# MODÜL 14

# Multi Tenant Sistemler

Kurumsal projeler için.

---

```text
Firma A

Firma B

Firma C
```

Tek Payload.

---

### Access Control

Tenant bazlı filtreleme.

---

# MODÜL 15

# Jobs & Background Tasks

---

Payload Jobs

Cron

Queue

Worker

---

### Proje

Gece raporlama sistemi.

---

# MODÜL 16

# Plugin Geliştirme

---

Custom Field

Custom Admin UI

Custom Package

---

### Proje

Kendi Payload Plugin'inizi yazın.

---

# MODÜL 17

# Enterprise Mimari

Bu aşamada artık Payload kullanıcısı değil Payload mimarı olursunuz.

---

## DDD

Sizin süreç simülasyonu (SODOS) çalışmalarınız için özellikle önemli.

### Domain

```text
Process
SubProcess
Activity
WorkStep
```

### Collection Mapping

### Aggregate

### Event

### Workflow

---

# KAPSTONE PROJELER

## Proje 1

Blog Sistemi

Öğrenilenler:

* Collections
* Globals
* Upload
* Next.js

---

## Proje 2

E-Ticaret Backend

Öğrenilenler:

* Relationships
* Hooks
* Access
* Auth

---

## Proje 3

ERP Kullanıcı Entegrasyonu

Öğrenilenler:

* Custom Auth Strategy
* Access Control
* Hooks

---

## Proje 4

SODOS Benzeri Süreç Yönetimi

Domain:

```text
Process
SubProcess
Activity
WorkStep
```

Öğrenilenler:

* Domain Modeling
* Workflow
* Access
* Jobs
* Events

```

Sizin geçmiş konuşmalarınıza bakınca en verimli sıra şu olur:

1. Collections
2. Relationships
3. Auth
4. Access Control
5. Hooks
6. Local API
7. Next.js Integration
8. Blocks
9. Jobs
10. Multi Tenant
11. Plugin Development

Çünkü şu anda zaten Next.js, veri modelleme, ERP entegrasyonu ve süreç yönetimi konularında deneyiminiz var. Bu nedenle Payload'u bir CMS olarak değil, "Next.js üzerinde çalışan backend framework" olarak öğrenmeniz size çok daha fazla değer sağlayacaktır. Özellikle ERP entegrasyonu ve SODOS projenizdeki süreç hiyerarşilerini Payload koleksiyonları, access control, hooks ve jobs yapılarıyla modellemek ileri seviye bir öğrenme projesi olacaktır.
```

