# BAOBAB — İki Dilli Yayıncılık Platformu

> Bu depo; iki dilli yayıncılık sitesi ve editoryal yönetim platformunun kod
> içermeyen vaka çalışmasıdır. Özel kaynak kodu, erişim bilgileri ve
> yayımlanmamış müşteri içerikleri paylaşılmamıştır.

[English version](README.md) · [Mimari](docs/ARCHITECTURE.md) · [Özellik haritası](docs/FEATURE-MAP.md)

## Genel Bakış

BAOBAB; halka açık kitap ve içerik sitesini özel bir yönetim paneliyle
birleştiren Türkçe–İngilizce bir yayıncılık platformudur. Kitaplar, yazarlar,
önizlemeler, etkinlikler, yazılar, satış noktaları, medya, aboneler, anasayfa
bölümleri ve site ayarları tek sistemden yönetilir.

| Alan | Bilgi |
|---|---|
| Durum | İleri geliştirme aşamasında; canlıya hazırlık işleri sürüyor |
| Rolüm | Ürün, mimari ve geliştirme sürecinin uçtan uca sahipliği |
| Ürün türü | İki dilli halka açık site ve özel içerik paneli |
| İçerik modeli | Ayrı TR/EN alanlarına sahip bağlantılı 14 veri modeli |
| Açık kapsam | Yalnızca vaka çalışması; uygulama kodu özel depoda |

## İhtiyaç

Bir yayıncılık sitesi yalnızca statik kitap sayfalarından oluşmuyor. Editörlerin
kitapları yazarlarla ilişkilendirmesi, önizlemeleri düzenlemesi, yazı ve
etkinlik yayımlaması, medyayı yönetmesi, satış noktalarını güncellemesi ve iki
dili kod değiştirmeden sürdürebilmesi gerekiyor.

Sistem bu editoryal ilişkiler etrafında tasarlandı.

## Rolüm

- Ürün ve geliştirme akışının tamamını üstlendim.
- Yayıncılık ihtiyaçlarını veri modellerine ve panel akışlarına dönüştürdüm.
- İki dilli rota ve içerik stratejisini tasarladım.
- Halka açık sayfaları, sunucu işlemlerini ve panel modüllerini geliştirdim ve kontrol ettim.
- Linux, Nginx ve PM2 tabanlı test ortamını hazırladım.
- Paydaş geri bildirimlerine göre revizyonlar yaptım.

## Kullanıcı Tarafı

- `/tr` ve `/en` altında Türkçe–İngilizce içerik
- Yönetilebilir hero ve anasayfa bölümleri
- Kitap listesi, kitap detayı ve etkileşimli sayfa önizlemesi
- Yazar listesi ve detayları
- Yazılar, etkinlikler, atölye ve satış noktaları
- Site içi arama ve bülten kaydı
- KVKK, gizlilik ve kullanım koşulları
- Sitemap, robots, JSON-LD ve SEO altyapısı

## Yönetim Paneli

- Dashboard ve hero slider yönetimi
- Kitap, kategori, önizleme ve kitap–yazar ilişkileri
- Yazar, etkinlik, yazı ve satış noktası yönetimi
- Arama ve çöp kutusu akışına sahip merkezi medya kütüphanesi
- CSV dışa aktarımlı bülten aboneleri
- Aynı panelde Türkçe ve İngilizce içerik alanları
- Site ayarları, hesap, tema ve bölüm sıralama işlemleri

## En Zor Mühendislik Problemi

Çoklu dili yalnızca arayüz metinlerinin çevirisi olarak değil, içerik modelinin
temel parçası olarak kurmak önemliydi.

Kitaplar, yazarlar, etkinlikler, yazılar, hero alanları ve site bölümleri ayrı
Türkçe ve İngilizce içeriğe sahip. Halka açık rotalar dile duyarlı çalışırken
editörler iki sürümü aynı panel akışı içinde yönetebiliyor.

## Teknolojiler

Next.js 16, React 19, TypeScript, Tailwind CSS 4, shadcn/ui, Motion, Tiptap,
react-pageflip, Auth.js v5, Zod, sanitize-html, Prisma 7, SQLite, next-intl,
Sharp, Linux, Nginx ve PM2.

## Kapsam Sınırları

- Ürün şu anda katalog ve editoryal platformdur; çevrim içi ödeme sistemi değildir.
- Satın alma işlemleri dış mağaza bağlantıları ve satış noktalarına yönlendirilir.
- Sepet ve ödeme henüz tamamlanmış özellik olarak sunulmamaktadır.
- Canlı yayın; analitik kimlikleri, alan adı/altyapı erişimi ve yasal metin incelemesine bağlıdır.


## Arayüz

### Editoryal yönetim paneli

![Yönetim paneli genel bakış](docs/screenshots/admin-overview.png)

Yönetim girişi tablolar yerine işler etrafında kurgulanmıştır: kitap ekle, yazı
yayınla, etkinlik duyur, satış noktalarını yönet. Alttaki sayaçlar canlı
kataloğu raporlar — ekran alındığında 51 kitap, 44 yazar ve çizer, 24 satış
noktası, 490 medya varlığı.

### Kitap düzenleyici

![Kitap düzenleyici](docs/screenshots/book-editor.png)

Tek bir kayıt; katalog verisini (ISBN, sayfa sayısı, ebat, kapak özelliği, fiyat,
yayın tarihi), zengin metin tanıtımını, rolleriyle birlikte katkı verenleri,
kategorileri, künyeyi ve koleksiyon üyeliğini bir arada tutar. Kapak yükleyici
beklenen ölçüyü söyler ve listelerde kullanılacak kırpma alanını editöre seçtirir.

### Sayfa bazlı SEO

![Sayfa bazlı SEO](docs/screenshots/per-page-seo.png)

SEO sonradan eklenen bir şey değil, birinci sınıf bir düzenleme yüzeyidir. Her
sabit sayfanın kendi başlığı, odak anahtar kelimesi ve açıklaması vardır; arama
motorlarının gerçekten uyguladığı sınırlara karşı canlı karakter sayacı ve
oluşacak arama sonucunun önizlemesi gösterilir. Boş bırakılan alanlar boş etiket
yayınlamak yerine site varsayılanına düşer.

## Sonuç

Planlanan site ve panel özelliklerinin büyük kısmı tamamlandı. Kalan işler
ağırlıklı olarak ölçümleme, üretim altyapısı, canlıya alma ve son paydaş/yasal
onaylar etrafında bulunuyor.

Bu depo, özel uygulama kodunu yayımlamadan yapılan mühendislik çalışmasını
güvenli ve profesyonel biçimde sunar.
