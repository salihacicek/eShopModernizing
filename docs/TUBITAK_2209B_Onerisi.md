# TÜBİTAK 2209-B Araştırma Önerisi Formu (Taslak İçerik)

### 1. Amaç ve Hedefler
**Amaç:** Geleneksel monolitik mimariyle yazılmış kurumsal uygulamaların, modern bulut (cloud) ve hafif Linux tabanlı konteyner mimarilerine taşınması süreçlerini analiz etmek ve bu geçişi `eShopModernizing` projesi üzerinden uygulamalı göstermektir.
**Hedefler:**
1. Uygulamanın sadece "Lift-and-Shift" yöntemiyle taşınması yerine, mimari kısımlarının izole edilmesi.
2. Pilot bölge olarak "Catalog" modülünün .NET 8 Web API olarak yeniden yazılması.
3. Hantal Windows Container'lar yerine Linux tabanlı konteynerler kullanılarak kaynak (RAM/CPU) tasarrufu sağlanması.

### 2. Yenilikçi Yönü ve Teknolojik Değeri
Geleneksel modernizasyon projeleri genellikle "Lift and Shift" (olduğu gibi kopyalama) yapar. Bu projenin yenilikçi yönü, "Strangler Fig" yaklaşımını kullanarak legacy bir .NET sisteminin bir parçasını (Katalog modülü) koparıp, sıfırdan modern .NET 8 mimarisiyle yeniden yazarak sisteme entegre etmesidir. 

### 3. Yöntem
Araştırma kapsamında karma bir yöntem izlenecektir:
*   **Mimari Analiz:** Orijinal "eShopModernizing" (ASP.NET WebForms/WCF) kaynak kodları incelenecektir.
*   **Yeniden Geliştirme (Recreate):** Catalog modülü geleneksel yapıdan koparılıp güncel .NET 8 Web API'ye dönüştürülecektir.
*   **Konteynerleştirme ve Kıyaslama:** Yeni yazılan servis, hafif bir Alpine Linux Docker imajı kullanılarak ayağa kaldırılacak; eski Windows Container versiyonu ile RAM tüketimi, imaj boyutu (Örn: 6 GB vs 120 MB) ve yanıt süresi açısından kıyaslanacaktır.

### 4. İş-Zaman Çizelgesi
*   **1.-2. Hafta:** Proje organizasyonu ve literatür araştırması.
*   **3.-4. Hafta:** Orijinal kod tabanının analizi ve Catalog modülünün ayrıştırılması.
*   **5.-6. Hafta:** Catalog modülünün .NET 8 Web API olarak kodlanması ve Linux tabanlı Dockerfile yazılması.
*   **7.-8. Hafta:** Performans testlerinin (RAM/İmaj boyutu) yapılması ve raporlama.

### 5. Risk Yönetimi ve B Planları
*   **Risk 1:** Orijinal kodların bağımlı olduğu WCF/WebForms yapılarının, öğrenci bilgisayarlarında (özellikle Mac/Linux) "Windows Container" zorunluluğu nedeniyle çalıştırılamaması veya 10 GB'lık imajların bilgisayarları kilitlemesi.
    *   **Çözüm (B Planı):** Projenin başından itibaren "Lift and Shift" reddedilmiş olup, sorunlu modüller çapraz platform destekli .NET 8'e dönüştürülerek hafif Linux Container'larında çalıştırılacaktır.
*   **Risk 2:** Ekip içi senkronizasyon sorunları. Çözüm: GitHub ve Kanban aktif kullanılacaktır.

### 6. Araştırma Olanakları
Çalışma, takım üyelerinin şahsi bilgisayarları, GitHub ve Docker ekosistem araçları kullanılarak yürütülecektir.

### 7. Sanayi Odaklı Çıktılar ve Yaygın Etki
Bu projenin çıktısı, şirketlere "eski Windows tabanlı sistemlerinizi bulut dostu hafif Linux sistemlerine nasıl dönüştürürsünüz" sorusu için somut ve metriklerle kanıtlanmış bir rehber (proof of concept) niteliği taşıyacaktır.
