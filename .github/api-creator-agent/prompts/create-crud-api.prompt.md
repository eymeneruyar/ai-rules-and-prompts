---
description: Oracle tablosundan template uyumlu CRUD API üret.
agent: api-creator
argument-hint: "Tablo adları, hedef proje yolu ve template proje yolu"
---

İstenen tablolar için CRUD API dosyalarını doğrudan oluştur veya mevcut dosyaları geliştir.

Görev bilgileri: ${input:crudRequest:Tablo adları, hedef proje yolu ve template proje yolunu yazın}

- DDL dizini: hedef depo kökünde `references/sql/parameter`.
- Template proje yolu: `<TEMPLATE_PROJECT_PATH>`; görev bilgilerinde verilen gerçek yolu kullan. Yer tutucu çözümlenmemişse gerçek yolu sor.
- [API standartları](../instructions/api-standards.instructions.md) ve [CRUD kuralları](../instructions/api-crud.instructions.md) dosyalarını oku ve uygula.
- Java 17, Spring Boot 3.5.x ve Onion Architecture kullan; template düzenini koru.
- Her tablo için controller/service/repository/entity/manuel mapper ve create/update/response DTO'larını üret.
- Basit CRUD JPA; JDBC yalnızca karmaşık sorgular. Ortak ApiResponse, validation ve merkezi exception handling uygula.
- STATUS=1 aktif; DELETE STATUS=0. LASTUPDATED ve doğrulanmış audit alanlarını mevcut olduklarında otomatik yönet.
- Uygun tüm iş alanlarını filtrele; GET listelerini sayfalı ve sıralı döndür.
- Açıkça istenmedikçe cache ekleme. Birim testi üretme.
- DDL/template'i değiştirme, şema ayrıntısı uydurma. Sadece engelleyici belirsizlikleri sor; ayrıca plan onayı isteme.
- Test çalıştırmadan derlemeyi kontrol et. Sonuçta yalnızca değişen dosyalar ve kısa doğrulama/engel bilgisi ver.
