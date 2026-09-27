# Sektörel Projeler ve Mevcut Çalışmalar (Legacy'den Cloud'a Geçiş Örnekleri)

Bu alanda daha önce gerçekleştirilen ve bizim projemize ilham veren dünyadaki gerçek mühendislik projeleri şunlardır:

### 1. Netflix: Monolitik Yapıdan AWS Bulutuna Geçiş Projesi
*   **Mevcut Araştırma/Proje:** Netflix'in tek parça (monolitik) DVD kiralama yazılımından, günümüzdeki tamamen bulut tabanlı mikroservis altyapısına taşınma projesi.
*   **Kullanılan Yöntem:** *Chaos Engineering (Kaos Mühendisliği)*. Sistemi taşıyıp taşımadığını görmek için kasten kendi sunucularını çökertme testleri yapmışlardır.
*   **Teknik Yaklaşım:** Tüm sistemi API Gateway (İstek Yönlendirici) arkasında yüzlerce küçük servise bölmek.

### 2. Trendyol: Geleneksel .NET'ten Kubernetes'e Geçiş (Türkiye Örneği)
*   **Mevcut Araştırma/Proje:** Trendyol'un "Efsane Cuma" gibi yoğun günlerde çöken eski (legacy) monolitik altyapısını parçalara ayırarak mikroservislere taşıma projesi.
*   **Kullanılan Yöntem:** Sistemin tamamen durdurulmadan, parça parça (Strangler Fig yöntemiyle) yeni sisteme akıtılması.
*   **Teknik Yaklaşım:** *Event-Driven Architecture (Olay Güdümlü Mimari)*. Servislerin birbiriyle doğrudan değil, Kafka (mesaj kuyruğu) üzerinden haberleşerek çökme riskini sıfıra indirmesi.

### 3. Uber: DOMA (Domain Odaklı Mimari) Geçiş Projesi
*   **Mevcut Araştırma/Proje:** Uber'in ilk yıllarında yazdığı devasa eski Python kodunu, binlerce küçük Go dilinde yazılmış servise bölme operasyonu.
*   **Kullanılan Yöntem:** Mikroservislerin sayısının kontrolden çıkmasını engellemek için servislerin "Alanlara (Domain)" göre kümelenmesi.
*   **Teknik Yaklaşım:** Sadece ilgili servislerin birbirine erişebildiği "İzole Ağ Mimarisi". (Bizim eShop'taki Katalog ve Sepet izolasyonu gibi).

### 4. Amazon: Obelisk Monolith'ten Dağıtık Sisteme Geçiş
*   **Mevcut Araştırma/Proje:** Amazon.com'un 2001 yılında kod satırları o kadar büyüdü ki sistemi güncelleyemez hale geldiler. Bu devasa C++ altyapısını servis odaklı yapıya (SOA) taşıdılar.
*   **Kullanılan Yöntem:** *Two-Pizza Teams (İki Pizzayla Doyabilen Takımlar).* Teknolojik değişimden ziyade, her servise sadece 5-6 kişilik küçük bağımsız takımlar atayarak yönetim sorununu çözdüler.

### 5. Microsoft: "eShopOnContainers" Referans Projesi
*   **Mevcut Araştırma/Proje:** Bizim üzerinde çalıştığımız (eShopModernizing) projenin abisi sayılan, doğrudan sıfırdan mikroservis olarak yazılmış açık kaynaklı Microsoft projesidir.
*   **Kullanılan Yöntem:** Tam otomatize edilmiş CI/CD (Sürekli Entegrasyon) ve Container Orchestration (Konteyner Orkestrasyonu).
*   **Teknik Yaklaşım:** Uygulamanın veritabanı dahil her parçasını **Docker** içine hapsederek, platform bağımsız (ister Linux ister Windows sunucusunda) çalışabilir hale getirmek.
