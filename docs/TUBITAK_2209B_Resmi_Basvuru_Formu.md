# TÜBİTAK 2209-B ARAŞTIRMA ÖNERİSİ FORMU

**Proje Adı:** Geleneksel (Legacy) Kurumsal Sistemlerin Strangler Fig Deseniyle Cloud-Native Mimarilere Taşınması: eShopModernizing Örneği

---

## 1. AMAÇ VE HEDEFLER
**Amaç:** 
Bu projenin temel amacı; günümüzde sanayide, bankacılıkta ve e-ticaret sektöründe yaygın olarak kullanılan ancak bakım maliyetleri yüksek olan geleneksel (monolitik) yazılımların, modern "Cloud-Native" (Bulut Doğuşlu) ve Linux tabanlı konteyner mimarilerine sıfır kesintiyle taşınması sürecini bilimsel metriklerle modellemektir. 

**Hedefler:**
1. Microsoft'un `eShopModernizing` referans projesi üzerinde yer alan eski (legacy) WCF/WebForms kod tabanının analiz edilmesi.
2. Sistemin tamamını "Lift-and-Shift" (olduğu gibi kopyalama) tembelliğiyle hantal Windows Konteynerlerine atmak yerine, pilot bölge olarak "Catalog (Ürün Kataloğu)" modülünün tespit edilmesi.
3. Seçilen modülün Strangler Fig deseniyle monolit yapıdan koparılarak güncel çapraz platform **.NET 8 RESTful Web API** yapısına dönüştürülmesi.
4. Yeni servisin çok hafif Linux (Alpine) konteynerlerinde (Docker) ayağa kaldırılarak, CI/CD (GitHub Actions) süreçleriyle otomatik dağıtımının yapılması.
5. Eski sistem (WCF & Windows Container) ile yeni sistemin (.NET 8 & Linux Container) RAM tüketimi, imaj boyutu ve yanıt süreleri açısından kıyaslanıp raporlanması.

---

## 2. YENİLİKÇİ YÖNÜ VE TEKNOLOJİK DEĞERİ
Endüstrideki geleneksel modernizasyon projeleri genellikle "Big Bang Rewrite" (sistemi çöpe atıp baştan yazma) veya "Lift and Shift" (mevcut spagetti kodu hiç değiştirmeden direkt sanal makineye/konteynere atma) stratejilerini uygular. Bu durum şirketler için yüksek maliyet, "Vendor Lock-in" ve büyük bir çökme riski barındırır. 

Bu projenin yenilikçi ve teknolojik yönü; eski koda dokunmadan sadece altyapıyı değiştirmeyi reddetmesidir. Proje, yazılım dünyasının altın standardı olan **"Strangler Fig" (Aşamalı Boğma)** yaklaşımını benimser. Orijinal WCF sistemine doğrudan dokunmadan, yeni oluşturulan modern (.NET 8) Linux tabanlı mikroservislerin eski sistemle entegre edilmesi, teknolojik açıdan kaynak tüketimini (CPU/RAM) dramatik ölçüde düşürecek yenilikçi bir mimari katkıdır.

---

## 3. YÖNTEM
Araştırma kapsamında şu adımlar (metodoloji) izlenecektir:
1. **Tersine Mühendislik (Reverse Engineering):** Orijinal `eShopModernizing` kaynak kodlarındaki bağımlılıklar analiz edilecektir.
2. **Mimari Ayrıştırma:** Veritabanı "Database-per-service" mantığına göre ayrıştırılacak ve Entity Framework Core (Code-First) kullanılarak yeniden modellenecektir.
3. **Yeniden Geliştirme (Recreate):** Eski WCF SOAP kontratları, modern JSON tabanlı DTO (Data Transfer Object) yapılarına çevrilecek ve REST API endpoint'leri yazılacaktır.
4. **Konteynerizasyon ve Orkestrasyon:** Geliştirilen modül için çok aşamalı (multi-stage) Dockerfile yazılacak ve `docker-compose.yml` ile orkestre edilecektir.
5. **Kıyaslama (Benchmark):** Postman Runner veya k6 kullanılarak yük testleri yapılacak; Linux vs Windows imaj boyutları (Örn: 150 MB vs 6 GB) tablo halinde bilimsel olarak raporlanacaktır.

---

## 4. PROJE YÖNETİMİ VE İŞ PAKETLERİ (İş-Zaman Çizelgesi)

Çalışma, her biri farklı bir mühendislik disiplinini (API, Data, Frontend, DevOps, Test) temsil eden 5 İş Paketine (İP) bölünmüştür:

*   **İP-1: Backend ve API Mimarisinin Kurulması (1.-3. Hafta):** Eski WCF mantığının modern REST API'ye taşınması ve Swagger entegrasyonu.
*   **İP-2: Veri Katmanının (Data Engineering) Yenilenmesi (2.-4. Hafta):** SQL Server şemasının EF Core ile modernizasyonu ve seed data (test verisi) yazılımı.
*   **İP-3: Arayüz (Frontend) Entegrasyonu (4.-6. Hafta):** Ayrıştırılan yeni Catalog API'sinin, arayüz tarafından (HTTP Client ile) tüketilmesi.
*   **İP-4: DevOps ve Konteynerizasyon Altyapısı (5.-7. Hafta):** Linux Dockerfile dosyalarının yazılması, Docker Compose ve GitHub Actions (CI/CD) kurulumu.
*   **İP-5: Test, Benchmark ve Akademik Raporlama (7.-8. Hafta):** Birim testlerin yazılması, RAM/Hız metriklerinin ölçülmesi ve TÜBİTAK/Ders final raporunun derlenmesi.

### Risk Yönetimi ve B Planı
*   **Risk:** Orijinal kodların bağımlı olduğu WCF yapılarının, öğrenci bilgisayarlarında (Mac/Linux) "Windows Container" zorunluluğu nedeniyle çalıştırılamaması veya 10 GB'lık baz imajların donanımı kilitlemesi.
*   **B Planı (Uygulanacak Çözüm):** Projede "Lift and Shift" tamamen reddedilmiş olup; sorunlu modüller donanım dostu, çapraz platform destekli .NET 8 altyapısına dönüştürülerek 150 MB'lık Alpine Linux konteynerlerinde çalıştırılacaktır.

---

## 5. ARAŞTIRMA OLANAKLARI
Proje, tamamen açık kaynaklı ve endüstri standardı araçlar kullanılarak yürütülecektir:
*   **Donanım:** Takım üyelerine ait Mac/Windows bireysel çalışma istasyonları.
*   **Yazılım & Çatılar:** .NET 8 SDK, Entity Framework Core, Docker Desktop.
*   **İşbirliği ve CI/CD:** GitHub (Sürüm Kontrolü), GitHub Projects (Kanban/Agile proje yönetimi), GitHub Actions (Otomasyon).
*   **Editörler:** Visual Studio 2022 ve Visual Studio Code.

---

## 6. SANAYİ ODAKLI ÇIKTILAR VE YAYGIN ETKİ
Yazılım modernizasyonu, günümüzde bankacılık, e-ticaret ve telekomünikasyon sanayisinin en büyük (ve en maliyetli) BT (IT) problemidir. Kurumlar, monolitik sistemlerini buluta taşırken donanım israfı ve çökme riskleri yaşarlar. 
Bu projenin çıktısı; sanayi kuruluşlarına "eski Windows tabanlı hantal sistemlerinizi, sistemi durdurmadan hafif Linux sistemlerine nasıl dönüştürürsünüz?" sorusu için, bizzat kod üzerinde metriklerle kanıtlanmış bir **Kavram Kanıtı (Proof of Concept)** rehberi sunacaktır. 

---

## 7. KAYNAKLAR
1. Fowler, M. (2004). *Strangler Fig Application*. MartinFowler.com. (Mimari geçiş stratejisi referansı).
2. Richardson, C. (2018). *Microservices Patterns: With Examples in Java*. Manning Publications. (Database-per-service ayrıştırma deseni referansı).
3. Microsoft Architecture. (2023). *Modernize existing .NET applications with Cloud and Windows Containers*. (Orijinal referans ve antipattern tespiti).
4. Pahl, C. (2015). *Containerization and the PaaS Cloud*. IEEE Cloud Computing. (Linux konteynerlerin performans kanıtı).
5. Jamshidi, P., et al. (2018). *Microservices: The Journey So Far and Challenges Ahead*. IEEE Software. (Risk yönetimi ve geçiş sorunları analizi).
