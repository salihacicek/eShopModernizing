# Gelecek Hafta Sunumu (Alan Araştırması) - Taslak Metinler

*(Bu içerikleri PowerPoint veya Canva slaytlarınıza bölerek kopyalayabilirsiniz.)*

## Slayt 1: Konu ve Problem Tanımı
*   **Seçilen Proje Yönü:** Proje 01 - Legacy sistemden modern mimariye geçiş (From Legacy to Modern).
*   **Alt Konu:** Monolitik yapıdaki geleneksel bir e-ticaret (eShop) uygulamasının Container (Konteyner) teknolojileriyle modernize edilmesi.
*   **Temel Problem:** Kurumsal firmaların eski kod altyapılarına bağımlı kalması; bu sistemlerin yeni özellikler eklemeye kapalı, ölçeklenmesi zor ve sunucu maliyetlerinin yüksek olması.
*   **Önemi:** Bu problemin çözülmesi, şirketlerin piyasadaki yeniliklere hızlı adapte olmasını (Time-to-market), bulut teknolojilerinin nimetlerinden faydalanmasını ve çökme risklerini minimize etmesini sağlar.

## Slayt 2: Literatür ve Mevcut Çalışmalar
*(Ayrıca `research/Sektorel_Projeler.md` dosyasındaki Netflix, Trendyol, Uber gibi gerçek dünya projelerini de bu slaytta mevcut çalışmalar olarak anlatacaksınız.)*
*(Bunu `research/Literatur.md` dosyasındaki 5 kaynağı baz alarak anlatacaksınız. Anahtar kelimelerimiz: Monolith to Microservices, Strangler Fig Pattern, Containerization)*

## Slayt 3: Benzer Araç ve Sistemler
Piyasada modernizasyon amaçlı kullanılan araçlar şunlardır:
*   **AWS App2Container / Azure Migrate:** 
    *   *Güçlü yönleri:* Otomatik kod taraması ve hızlı container imajı oluşturma.
    *   *Sınırlılıkları / Eksik Yönleri:* Çok kompleks (spagetti kod) sistemlerde tam bağımsızlık sağlayamaması ve "Vendor Lock-in" (Sadece tek bulut markasına bağımlılık) yaratması.
*   **Bizim Projemizin Farkı (Özgün Katkı):** Mevcut otomasyon araçlarının kör noktası olan kod içi bağımlılıkları manuel analizle ayırarak daha temiz bir geçiş mimarisi tasarlamak. 

## Slayt 4: Repository İncelemesi (eShopModernizing)
*   **Yazılım Mimarisi:** Geleneksel Monolitik ve N-Tier (Çok Katmanlı) Mimari.
*   **Teknoloji Yığını:** 
    *   *Eski Yapı:* .NET Framework 4.x, ASP.NET WebForms / MVC, WCF.
    *   *Hedeflenen Yapı:* .NET Core / .NET 8, Docker, Windows/Linux Containers.
*   **Temel Bileşenler:** Catalog (Katalog), Basket (Sepet), Identity (Kimlik/Giriş), Ordering (Sipariş).
*   **Takımın Odaklanacağı Bölüm:** Tüm sistemi baştan yapmak yerine, pilot bölge olarak *Catalog (Ürün Kataloğu)* modülünün kopartılarak Docker imajına dönüştürülmesi hedeflenmektedir.

## Slayt 5: Kullanılacak Teknolojiler ve Araçlar
*   **Programlama Dilleri:** C#, SQL.
*   **Kütüphane ve Framework'ler:** .NET, Entity Framework, ASP.NET Core.
*   **Geliştirme & Test Araçları:** Visual Studio / VS Code, Docker Desktop, Git, GitHub Actions.
*   **Yöntemler:** Agile (Iterative Development), Reverse Engineering, Containerization.

## Slayt 6: Takımın Katkısı ve Proje Kapsamı
*   **Takımın Özgün Katkısı:** Uygulamayı sadece teknik olarak Docker içine koymak (Lift-and-Shift) değil, mimariyi cloud-native mantığına uygun şekilde izole edilebilir hale getirmek.
*   **Kapsam Dahilinde:** Web Frontend ve Catalog API'sinin modernize edilmesi.
*   **Kapsam Dışında Bırakılanlar:** Ödeme (Payment) sistemlerinin gerçek banka entegrasyonu ve çok karmaşık Event-Bus haberleşme mekanizmaları bilinçli olarak proje kapsamı dışında (kısıt) bırakılmıştır.

## Slayt 7: Repository URL ve Ekip
*   Takım GitHub Linki: `https://github.com/salihacicek/eShopModernizing`
*   GitHub Projects Kanban Tahtası başarıyla kurulmuş ve iş dağılımları eklenmiştir.
