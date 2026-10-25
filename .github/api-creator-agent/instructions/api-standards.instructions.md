---
applyTo: "**/*.java,**/pom.xml,**/*.gradle,**/*.gradle.kts,**/application*.yml,**/application*.yaml,**/application*.properties"
---

# API standartları

- Java 17 ve Spring Boot 3.5.x kullan. Var olan uyumlu 3.5.x sürümünü koru; depo/template bağımlılık yönetimini izle. Jakarta validation/persistence kullan.
- Referans proje yolu `<TEMPLATE_PROJECT_PATH>` yer tutucusudur; gerçek yolu kullanıcı sağlar. Paket, adlandırma, modül, endpoint ve kod biçiminde template'i izle. Template veya `references/sql/parameter` altındaki DDL'leri düzenleme.
- Onion Architecture uygula: domain merkezde; application kullanım senaryolarını ve portları; infrastructure JPA/JDBC adaptörlerini; presentation controller'ları barındırır. Bağımlılıklar içeri yönelir; domain/application controller veya somut altyapı adaptörlerine bağımlı olmaz.
- Template'in JPA entity yerleşimini koru; dış katman bağımlılığı yaratma. Application portu üzerinden persistence erişimi sağla; gerekiyorsa infrastructure repository adaptörü ekle. Gereksiz interface/implementation veya katman üretme. Template ile Onion zorunluluğu çelişiyorsa sessizce mimari değiştirme; engeli netleştir.
- Her tablo için ayrı controller, service, repository, entity, manuel mapper, CreateRequest, UpdateRequest ve Response DTO oluştur; mevcut eşdeğerleri geliştir. Genel CRUD süper sınıflarıyla tablo sözleşmelerini gizleme.
- Controller HTTP, request validation ve response dönüşümünü; service iş kurallarını ve transaction sınırlarını; repository veri erişimini yönetir. Controller'dan doğrudan repository çağırma.
- Basit CRUD ve dinamik filtrelemeyi Spring Data JPA/Specification ile yap. JDBC'yi yalnızca JPA ile makul biçimde ifade edilemeyen karmaşık sorgularda kullan; parametreleri bağla, kullanıcı girdisini SQL'e birleştirme.
- Mapping manueldir; MapStruct/ModelMapper ekleme. Entity'yi API response olarak döndürme; kontrolsüz request-to-entity property kopyalama yapma.
- Var olan ortak `ApiResponse<T>` sözleşmesini kullan. Yoksa template stilinde data, başarı bilgisi, mesaj ve hata ayrıntılarını taşıyan tek ortak sözleşme tanımla; liste metadata'sını data içinde tut. Hataları HTTP 200 ile maskeleme.
- Bean Validation kullan; sınırları DDL ve doğrulanmış iş kurallarından çıkar. Veritabanı constraint'leriyle birlikte çalış; benzersizlik ön kontrolünü yarış durumlarına karşı yeterli sayma.
- Merkezi `@RestControllerAdvice` kullan veya mevcut handler'ı genişlet: validation/geçersiz sorgu 400, bulunamayan veya pasif kayıt 404, doğrulanmış constraint çatışması 409, beklenmeyen hata 500. SQL, stack trace ve hassas bilgileri response'a yazma.
- Yazma işlemleri transaction içinde; okumalar uygun yerde readOnly olsun. Oracle tiplerini DDL precision/scale ve template'e göre eşle; ondalık hassasiyetini kaybetme. Anahtar stratejisi, timezone veya ilişki türetme.
- Cache sadece açık kullanıcı isteğiyle eklenir; istenirse yazma/silme sonrası invalidation uygula.
- Birim testi üretme. İlgili derleme kontrolünü test çalıştırmadan yap; yapmadığın kontrolü yapılmış gibi bildirme. Alakasız dosyaları, bağımlılıkları ve API sözleşmelerini değiştirme.
