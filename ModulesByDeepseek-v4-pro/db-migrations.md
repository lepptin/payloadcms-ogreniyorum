### 1. Payload CMS 3 ile Migration İş Akışı

Payload, migration'ları yönetmek için güçlü bir CLI (Komut Satırı Arayüzü) sunar.

**Temel Komutlar:**

*   **`pnpm payload migrate:create <isim>`**: Yeni bir migration dosyası oluşturur.
*   **`pnpm payload migrate`**: Henüz çalıştırılmamış tüm migration'ları sırayla uygular.
*   **`pnpm payload migrate:status`**: Hangi migration'ların uygulandığını ve hangilerinin beklemede olduğunu gösterir.

### 2. Pratik: Örnek Senaryolar ile Adım Adım Migration

Şimdi, sizin yaşadığınız senaryoyu ve diğer yaygın durumları ele alalım.

#### **Varsayımlar:**
*   Projenizin `package.json` dosyasında `"payload": "cross-env PAYLOAD_CONFIG_PATH=src/payload.config.ts payload"` komutu tanımlı.
*   Migration dosyaları varsayılan olarak `src/migrations` klasöründe saklanır.

#### **Senaryo 1: Koleksiyona Yeni Bir Alan Eklemek**

Diyelim ki `Posts` koleksiyonunuza `summary` adında yeni bir metin alanı eklediniz.

1.  **Değişikliği Yapın**: `Posts` koleksiyonunun tanımına `summary` alanını ekleyin.
2.  **Migration Oluşturun**:
    ```bash
    pnpm payload migrate:create add_summary_to_posts
    ```
    Bu komut, `src/migrations` klasöründe zaman damgalı (`timestamp_add_summary_to_posts.ts`) bir dosya oluşturacaktır.
3.  **Migration Dosyasını İnceleyin (ve Gerekirse Düzenleyin)**:
    Oluşturulan dosya genellikle Drizzle tarafından otomatik olarak doldurulur. İçeriği şuna benzer:
    ```typescript
    import { MigrateUpArgs, MigrateDownArgs } from '@payloadcms/db-sqlite'

    export async function up({ payload, req }: MigrateUpArgs): Promise<void> {
      // Drizzle, `summary` alanını eklemek için gerekli SQL komutlarını buraya yazar.
      // Örn: ALTER TABLE posts ADD COLUMN summary text;
    }

    export async function down({ payload, req }: MigrateDownArgs): Promise<void> {
      // Geri almak için gerekli SQL komutları.
      // Örn: ALTER TABLE posts DROP COLUMN summary;
    }
    ```
    Çoğu durumda bu dosyayı elle değiştirmenize gerek yoktur, Drizzle sizin için hazırlar.
4.  **Migration'u Uygulayın**:
    ```bash
    pnpm payload migrate
    ```
    Bu komut, yeni oluşturulan migration'u çalıştırarak `posts` tablosuna `summary` sütununu ekler.

**Artık veritabanınızı silmeden, güvenle şema değişikliği yapmış oldunuz.**

#### **Senaryo 2: Bir Alanın Adını Değiştirmek (Breaking Change)**

Payload 3'ün bazı sürümlerinde, sütun adları `camelCase`'den `snake_case`'e çevrilmiştir. Bu tür kritik değişikliklerde migration şarttır.

1.  **Değişikliği Yapın**: Koleksiyondaki alanın adını değiştirin (örneğin, `selectReadOnly` -> `select_read_only`).
2.  **Migration Oluşturun**:
    ```bash
    pnpm payload migrate:create rename_select_column
    ```
3.  **Migration'u Uygulayın**:
    ```bash
    pnpm payload migrate
    ```
    Bu işlem, sütun adını güvenle yeniden adlandıracaktır.

#### **Senaryo 3: Mevcut Bir Özelliği Aktifleştirmek (Örn: Versiyonlama)**

Diyelim ki bir koleksiyon için `versions` özelliğini `true` yaptınız.

1.  **Değişikliği Yapın**: Koleksiyon tanımına `versions: true` ekleyin.
2.  **Migration Oluşturun**:
    ```bash
    pnpm payload migrate:create enable_versions_for_posts
    ```
3.  **Migration'u Uygulayın**:
    ```bash
    pnpm payload migrate
    ```
    Bu migration, versiyonları saklamak için gerekli yeni tabloları ve ilişkileri oluşturacaktır.

### 3. Özet ve En İyi Pratikler

*   **Development (Geliştirme)**: `push` özelliğini (`pnpm dev`) **yalnızca** hızlı prototipleme için kullanın. Şema değişikliklerini migration ile yapmaya alışın.
*   **Production (Canlı)**: `push`'u **kesinlikle kullanmayın**. Tüm şema değişikliklerini migration dosyaları oluşturarak ve `pnpm payload migrate` komutuyla uygulayarak yapın.
*   **Versiyon Kontrolü**: Tüm migration dosyalarınızı (örn: `src/migrations` klasörünü) Git gibi bir versiyon kontrol sistemine ekleyin. Böylece tüm ekip aynı şema geçmişine sahip olur.
*   **Hata Durumunda**: Eğer bir migration sırasında hata alırsanız, `pnpm payload migrate:down` ile son migration'u geri alabilir, hatayı düzelttikten sonra tekrar `pnpm payload migrate` çalıştırabilirsiniz.

### Sonuç

Mevcut yönteminiz olan veritabanını silip yeniden oluşturmak, acil durumlar için geçerli bir kurtarma yöntemi olabilir. Ancak **üretken bir geliştirme süreci için migration kullanımı zorunludur**. Bu sayede hem yerel ortamınızda zamandan tasarruf eder hem de uygulamanızı canlıya almaya hazır hale getirirsiniz.
