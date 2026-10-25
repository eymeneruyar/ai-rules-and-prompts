---
applyTo: "**/*.java"
---

# Tablo bazlı CRUD

## Şema ve dosyalar

- Yalnızca istenen tabloların `references/sql/parameter` içindeki Oracle DDL'lerini esas al. Kolon, PK, FK, default, sequence/identity ve constraint uydurma; DDL'yi değiştirme.
- Her tablo için bir controller, service, repository, entity, manuel mapper ve create/update/response DTO'su üret. Gerektiğinde filtre DTO'su ve bileşik PK için JPA anahtar tipi ekle; ilişkili tablolar için istenmeyen CRUD üretme.
- Anahtar üretimini yalnızca doğrulanmış DDL/template bilgisiyle kur. PK yoksa veya üretim stratejisi belirsizse engeli sor.

## İşlemler

Template'in route ve DTO adlandırmasını kullan. Eşdeğer yoksa aşağıdaki HTTP sözleşmesini uygula:

| İşlem | Endpoint | Sonuç |
| --- | --- | --- |
| Oluştur | POST /<resource> | 201, ApiResponse<Response> |
| Tekil getir | GET /<resource>/{id} | 200, aktif kayıt |
| Listele | GET /<resource> | 200, ApiResponse içinde sayfa verisi ve metadata |
| Güncelle | PUT /<resource>/{id} | 200, ApiResponse<Response> |
| Sil | DELETE /<resource>/{id} | 200, ApiResponse ile silme sonucu |

- Bileşik anahtarda template'in gösterimini izle; yoksa tüm PK parçalarını açıkça taşıyan kararlı bir route kullan.
- Service yazma transaction'larını yönetsin. Update mevcut aktif entity'yi yüklesin ve yalnızca izinli iş alanlarını değiştirsin. PUT alan doğrulamalarını create ile tutarlı uygula; kısmi güncelleme istenmedikçe PATCH davranışı türetme.
- Create/update request'lerinden PK üretim alanlarını, STATUS ve otomatik audit alanlarını çıkar. Kullanıcının kontrol ettiği anahtar varsa yalnızca create için doğrulanmış sözleşmeyi izle; update path anahtarını değiştirme.

## Soft delete ve audit

- STATUS kolonu mevcut ve uyumluysa create sırasında STATUS=1 ata; tüm tekil/liste/update/delete sorgularını STATUS=1 ile sınırla. Fiziksel silme çağrısı yapma.
- DELETE, aktif kaydın STATUS değerini 0 yapar. Pasif veya bulunamayan kayıt için 404 döndür. Pasif kaydı otomatik yeniden etkinleştirme; silmeyi ilişkili tablolara kendiliğinden yayma.
- STATUS yoksa veya tip/anlamı 0/1 kuralıyla çelişiyorsa kolon ekleme ya da hard delete'e dönme; ilgili tablo için engeli sor.
- LASTUPDATED mevcutsa create, update ve soft delete sırasında uygun zaman değeriyle yönet. DDL/template bir trigger veya database default ile yönetiyorsa bu sahipliği koru; çift yazma yapma. Kolonun tarih/saat tipi ve doğrulanmış timezone yaklaşımını izle.
- Diğer audit alanlarını yalnızca DDL/template anlamını doğruluyorsa otomatik yönet. Kullanıcı kimliği gibi bağlamı uydurma; eksik kolon ekleme. STATUS filtresinin kullanıcı parametresiyle aşılmasına izin verme.
- Soft delete sonrası unique constraint'in pasif satırlar için de geçerli olabileceğini koru; constraint'i değiştirme veya pasif satırı otomatik tekrar kullanma.

## Filtreleme, sayfalama, sıralama

- Uygun tüm iş alanlarını isteğe bağlı, tip güvenli filtre yap. LOB/binary, hassas veya teknik audit alanlarını otomatik genel filtre olarak açma; iş alanı kapsamını DDL/template'ten belirle.
- Metinlerde template'in eşitlik/contains yaklaşımını, sayısal alanlarda eşitlik ve gerekli aralıkları, tarih alanlarında başlangıç/bitiş, doğrulanmış kod/FK alanlarında eşitlik kullan. DDL constraint'i olmadan enum veya izinli değer listesi uydurma.
- Null filtreyi uygulama; boş metin davranışını template'e göre normalize et. Contains aramasında wildcard karakterlerini escape et. Ters aralık ve geçersiz tipleri 400 ile reddet.
- GET listesi daima sayfalı ve sıralı olsun. Template standardı yoksa page=0, size=20, max size=100 kullan; geçersiz değerleri 400 ile reddet.
- İzinli sıralama alanlarını açıkça belirle; kullanıcıdan SQL/JPQL parçası kabul etme. Varsayılan sıralama PK artan; başka sıralamada PK alanlarını kararlı eşitlik bozucu olarak ekle.
- Response'ta content, page, size, totalElements ve totalPages bilgisini ortak ApiResponse içinde sun; template'in eşdeğer sayfa sözleşmesini koru.
- Basit liste/filtre işlemleri JPA Specification ve Pageable kullanır; yalnızca karmaşık sorgular JDBC'ye gider. JDBC sorgularında da aktif kayıt filtresi, count, sayfalama ve izinli sıralama kuralları aynıdır.
