# Proje Mimarisi ve Görev Dağılımı (Sorumluluk Matrisi)

## 1. Proje Nedir ve Neyi "Recreate" Ediyoruz?

### Orijinal Proje (eShopModernizing) Nedir?
Microsoft tarafından hazırlanan `eShopModernizing`, 2000'li yıllardan kalma geleneksel (legacy) kurumsal sistemleri temsil eden bir e-ticaret arka ofis (backoffice) uygulamasıdır.

**Orijinal mimari şu bileşenlerden oluşur:**
*   **Monolitik & Eski Altyapı:** ASP.NET WebForms, ASP.NET MVC (.NET Framework 4.x) ve SOAP tabanlı bir WCF (Windows Communication Foundation) servis katmanı.
*   **Veritabanı:** SQL Server üzerinde koşan ilişkisel ürün kataloğu (Product Catalog).
*   **Microsoft'un Çözümü (Lift-and-Shift):** Kodu hiç değiştirmeden, IIS sunucusunu ve .NET Framework'ü devasa Windows Container imajlarına paketleyip buluta veya Docker'a atmak.

### Bizim "Recreate" Edeceğimiz Proje Nedir?
Orijinal repo 2024'te arşivlendi ve salt Windows Container kullandığı için pratikte hantal, platform bağımlı ve maliyetlidir. Biz projeyi birebir kopyalamak yerine **Modern Yazılım Mühendisliği Standartlarına** göre yeniden inşa ediyoruz:

| Eski Mimari (Lift-and-Shift) | Recreate Edilen Yeni Mimari (Rota A) |
| :--- | :--- |
| .NET Framework + WCF (SOAP) | **.NET 8 / 9 RESTful Web API** |
| Windows Containers (~8-10 GB) | **Linux Alpine Containers (~150 MB)** |
| Monolitik Veritabanı Bağımlılığı | **Repository Pattern + EF Core Code-First** |
| Elle / Batch Script ile Dağıtım | **CI/CD Pipeline (GitHub Actions) + Docker Compose** |

**Bu çalışmanın somut çıktısı:** Strangler Fig Deseni uygulanarak eski WCF servisinden koparılan, platform bağımsız (Linux/Mac/Windows), hafif ve test edilebilir bir Modern Catalog Mikroservisi ve Yönetim Paneli olacaktır.

---

## 2. 5 Kişilik Görev Dağılımı ve Sorumluluk Matrisi
Projenin takvimini riske atmamak için mimariyi 5 bağımsız ama birbiriyle entegre modüle bölüyoruz:

### 👤 1. Kişi: Backend & API Mimarı (Çekirdek Servis)
**Görev:** Eski WCF/MVC içindeki ürün kataloğu mantığını modern bir REST API'ye taşımak.
*   .NET Web API projesini açmak, `CatalogController` endpoint'lerini yazmak (GET /api/catalog, POST, PUT, DELETE).
*   Eski WCF SOAP kontratlarını JSON tabanlı DTO (Data Transfer Object) yapılarına çevirmek.
*   Swagger/OpenAPI entegrasyonu ile API dokümantasyonunu hazır etmek.

### 👤 2. Kişi: Veri Katmanı & Veritabanı Sorumlusu (Data Engineering)
**Görev:** Eski veritabanı şemasını modern ORM yapısına taşımak ve mock/seed verileri yönetmek.
*   Entity Framework Core (EF Core) modellerini (`CatalogItem`, `CatalogType`, `CatalogBrand`) oluşturmak.
*   Code-First Migration altyapısını kurmak.
*   Docker üzerinde koşacak SQL Server / PostgreSQL konteynerini yapılandırmak ve test verilerini yükleyen seed mekanizmasını yazmak.

### 👤 3. Kişi: Frontend & Arayüz Geliştiricisi (İstemci Deneyimi)
**Görev:** Eski WebForms/MVC arayüzünü modern, responsive bir yönetim paneline dönüştürmek.
*   Teknolojiyi seçmek (Hafif bir ASP.NET Core Razor Pages, Blazor veya React/Vue).
*   Ürün listeleme, sayfalama, filtreleme, yeni ürün ekleme ve silme ekranlarını kodlamak.
*   1. Kişinin hazırladığı REST API endpoint'lerini tüketmek (HTTP client entegrasyonu).

### 👤 4. Kişi: DevOps & Konteynerizasyon Uzmanı (Altyapı)
**Görev:** Tüm projeyi işletim sisteminden bağımsız tek komutla çalışır hale getirmek.
*   API ve Frontend için çok aşamalı (multi-stage build) hafif Linux Dockerfile dosyalarını yazmak.
*   Veritabanı, Backend ve Frontend'i birbirine bağlayan `docker-compose.yml` dosyasını yapılandırmak (`docker compose up --build` ile sistemin tek seferde ayağa kalkması).
*   GitHub Actions ile kod her push edildiğinde imajları derleyen basit bir CI pipeline kurmak.

### 👤 5. Kişi: Test, Kıyaslama (Benchmark) & Akademik Raporlama
**Görev:** Projenin akademik/teknik değerini sayısallaştırmak ve TÜBİTAK/Sunum çıktılarını üretmek.
*   API için birim (Unit) ve entegrasyon testlerini hazırlamak.
*   Performans Kıyaslaması: Orijinal Windows Container (literatür verisi) ile yeni Linux Container arasındaki imaj boyutu (MB), RAM tüketimi ve API yanıt sürelerini (k6 veya Postman Runner ile) ölçüp grafiklere dökmek.
*   Sunum slaytlarını, mimari şemaları ve TÜBİTAK proje formundaki metinleri derlemek.
