# Gelecek Hafta Sunumu (Alan Araştırması) - Taslak Metinler

## Slayt 1: Konu ve Problem Tanımı
*   **Seçilen Proje Yönü:** Proje 01 - Legacy sistemden modern mimariye geçiş.
*   **Alt Konu:** Monolitik yapıdaki geleneksel bir e-ticaret (eShop) uygulamasının Container (Konteyner) teknolojileriyle modernize edilmesi.
*   **Temel Problem:** Kurumsal firmaların eski kod altyapılarına bağımlı kalması; bu sistemlerin yeni özellikler eklemeye kapalı, ölçeklenmesi zor ve sunucu maliyetlerinin yüksek olması.

## Slayt 2: Literatür ve Mevcut Çalışmalar
*(research/Literatur.md dosyasındaki 5 kaynağı baz alarak anlatacaksınız. Anahtar kelimelerimiz: Monolith to Microservices, Strangler Fig Pattern, Containerization)*
*(Ayrıca `research/Sektorel_Projeler.md` dosyasındaki Netflix, Trendyol, Uber gibi gerçek dünya projelerini de bu slaytta mevcut çalışmalar olarak anlatacaksınız.)*

## Slayt 3: Benzer Araç ve Sistemler
*   **AWS App2Container / Azure Migrate:** 
    *   *Güçlü yönleri:* Otomatik kod taraması ve hızlı container imajı oluşturma.
    *   *Sınırlılıkları:* Çok kompleks sistemlerde tam bağımsızlık sağlayamaması.
*   **Bizim Projemizin Farkı (Gerçek Modernizasyon):** Otomatik araçların yaptığı basit "Lift-and-Shift" (olduğu gibi taşıma) mantığını reddediyoruz. Eski kodu doğrudan hantal Windows Container'lara atmak yerine, mimariyi inceleyip izole bir yapı kuracağız.

## Slayt 4: Repository İncelemesi (eShopModernizing)
*   **Yazılım Mimarisi:** Geleneksel Monolitik ve N-Tier Mimari.
*   **Teknoloji Yığını:** 
    *   *Mevcut Hali:* .NET Framework 4.x, ASP.NET WebForms / WCF.
    *   *Dönüştürülecek Hali:* .NET 8 Web API, Hafif Linux (Alpine) Container'lar.
*   **Takımın Odaklanacağı Bölüm:** Sadece "Catalog (Ürün Kataloğu)" modülü.

## Slayt 5: Kullanılacak Teknolojiler ve Araçlar
*   **Programlama Dilleri:** C#, SQL.
*   **Kütüphane ve Framework'ler:** .NET 8, Entity Framework Core.
*   **Geliştirme & Test Araçları:** Visual Studio / VS Code, Docker Desktop.
*   **Yöntemler:** Strangler Fig Deseni, Linux Containerization.

## Slayt 6: Takımın Katkısı ve Proje Kapsamı
*   **Takımın Özgün Katkısı (Rota A):** Orijinal reponun yaptığı gibi kodları sadece Windows Docker içine koymak (Lift-and-Shift) **değildir**. Özgün katkımız; Catalog modülünü geleneksel yapıdan koparıp, güncel **.NET 8 Web API** olarak yeniden yazmak ve hantal Windows imajları yerine **hafif Linux Container'larında** ayağa kaldırmaktır.
*   **Kıyaslama:** Proje sonunda eski WCF/Windows Container versiyonu ile bizim yazdığımız yeni .NET 8/Linux Container versiyonunun RAM tüketimi ve imaj boyutu karşılaştırılacaktır.

## Slayt 7: Repository URL ve Ekip
*   Takım GitHub Linki: `https://github.com/salihacicek/eShopModernizing`
*   GitHub Projects Kanban Tahtası başarıyla kurulmuş ve iş dağılımları eklenmiştir.
