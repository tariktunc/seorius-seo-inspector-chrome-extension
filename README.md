<div align="center">

<img src="src/icons/logo.svg" alt="Seorius logosu" width="96" height="96">

# Seorius — Sayfa İçi SEO Analizi

**Açık sekmedeki sayfanın sayfa içi SEO'sunu tarayıcınızın içinde inceleyen, açık kaynaklı Chrome eklentisi.**

![Manifest V3](https://img.shields.io/badge/Manifest-V3-4285F4?logo=googlechrome&logoColor=white)
![Sürüm](https://img.shields.io/badge/s%C3%BCr%C3%BCm-1.0.0-2ea44f)
![Lisans](https://img.shields.io/badge/lisans-MIT-blue)
![Testler](https://img.shields.io/badge/birim%20testi-50%20ge%C3%A7ti-brightgreen)
![Gizlilik](https://img.shields.io/badge/veri-yaln%C4%B1zca%20yerel-informational)
![Durum](https://img.shields.io/badge/durum-geli%C5%9Ftirme%20a%C5%9Famas%C4%B1nda-yellow)

**[Tanıtım sayfası](https://tariktunc.github.io/seorius-seo-inspector-chrome-extension/)** · **[Dökümanlar](https://tariktunc.github.io/seorius-seo-inspector-chrome-extension/docs.html)** · [GitHub](https://github.com/tariktunc/seorius-seo-inspector-chrome-extension)

[Neler yapar](#neler-yapar) · [Kurulum](#kurulum-paketlenmemiş) · [İlkeler](#ilkeler) · [İzinler](#izinler) · [Geliştirme](#geliştirme) · [English](#english)

</div>

> **Durum:** geliştirme aşamasında. Henüz Chrome Web Mağazası'nda yok, paketlenmemiş olarak yüklenir.

---

## Neler yapar

Simgeye tıklayın, o sayfanın SEO durumunu anında görün. Tek bir sayfada bile başlık yapısından yönlendirme zincirine, Open Graph'tan yapılandırılmış veriye kadar bakılacak şeylerin hepsi tek yerde.

### Açılır pencere (popup)

URL, HTTP durumu, hata / uyarı / not sayıları ve altı sekme:

| Sekme | İçerik |
|---|---|
| Özet | Temel alanlar, schema türleri, dikkat gereken ilk 5 bulgu |
| Başlıklar | H1–H6 yapısı |
| Görseller | alt metni, boyut |
| Bağlantılar | iç / dış, nofollow |
| Sosyal | Open Graph, Twitter |
| Araçlar | Dış araç bağlantıları + tam rapor |

Her sekmenin sonunda raporun ilgili bölümünü açan "Rapordaki ayrıntılar" bağlantısı bulunur.

### Google arama sonuçları katmanı (SERP)

Google'da arama yaparken sonuç sayfasının üstüne bilgi ekler:

- Organik sonuçlara **sıra numarası** (2. sayfa 11'den başlar, aynı adres bir kez sayılır).
- Reklamlara ayrı renk, çerçeve ve "Reklam #n · üst/alt" etiketi. Organik sıraya karışmaz.
- **SERP özellik etiketleri:** öne çıkan snippet, "diğer kullanıcılar şunu sordu", yerel paket, video karuseli, görsel paketi, öne çıkan haberler, site bağlantıları, AI Overview.
- Sağ altta açılıp kapanan panel: organik / reklam sayıları, açma-kapama düğmeleri, **CSV indirme**, AI Overview kaynak listesi + CSV, ülke / dil ile yeniden arama.
- Ayarlardan kendi alan adınızı girerseniz o sonuçlar ayrıca çerçevelenir.

### Tam rapor (ayrı sekme)

- **Denetim:** Teknik / İçerik / Mobil / Sosyal.
- Sayfa bilgisi, head öğeleri, başlık ağacı, görsel tablosu, bağlantı tablosu ve **bağlantı kontrolü**.
- Anahtar kelime yoğunluğu (1–4 kelime, Türkçe büyük/küçük harf duyarlı).
- Open Graph / Twitter ve paylaşım kartı önizlemesi.
- JSON-LD / microdata / RDFa.
- Teknik bilgiler: durum, adım adım **yönlendirme zinciri**, başlıklar, HSTS, karışık içerik, HTML boyutu, robots.txt kararı, site haritası.
- Ham ve işlenmiş HTML karşılaştırması, çerçeve ve izleme etiketi tespiti.
- **2–5 URL karşılaştırması**, dış araç bağlantıları.
- Dışa aktarma: JSON / CSV / yazdır-PDF.

### Sayfada işaretleme

Başlıkları, bağlantıları (nofollow, boş metin) ve alt metni olmayan görselleri sayfanın üstünde işaretler. İstek üzerine eklenir, kapatınca kaldırılır.

### Ayarlar

Dil (Türkçe / İngilizce), SERP katmanı (aç/kapat, numaralar, reklam işaretleme, özellik etiketleri, alan adım), işaretleme renkleri, ek etkisiz kelimeler ve beyaz liste, gösterilen denetim grupları, tablo sütunları, ayarları içe / dışa aktarma.

Tüm bulgular ve düzeltme önerileri seçtiğiniz dilde gösterilir. Durum modeli: **hata / uyarı / not / geçti / çalışmadı**. "Çalışmadı" hiçbir zaman "geçti" sayılmaz. Uzunluk aralıkları öneridir, Google kuralı değildir.

## Kurulum (paketlenmemiş)

Gereken: Node.js 20 veya üstü (geliştirme Node 24 ile yapıldı).

```bash
git clone https://github.com/tariktunc/seorius-seo-inspector-chrome-extension.git
cd seorius-seo-inspector-chrome-extension
npm install
npm run build
```

1. Chrome'da `chrome://extensions` sayfasını açın.
2. Sağ üstten **Geliştirici modu**nu açın.
3. **Paketlenmemiş öğe yükle**ye basın ve `dist/` klasörünü seçin.
4. Bir sayfa açın ve araç çubuğundaki Seorius simgesine tıklayın.

## İlkeler

- **Yalnızca yerel.** Sayfa tarayıcınızda analiz edilir. Hiçbir sayfa verisi, URL veya geçmiş Blakfy sunucularına ya da üçüncü taraflara gönderilmez.
- **En az izin.** Kurulumda yalnızca `activeTab`, `scripting`, `storage`. `host_permissions` ve `<all_urls>` yoktur.
- **Analiz tıklayınca çalışır.** Sayfa analizi yalnızca simgeye tıkladığınızda, yalnızca o sekmede çalışır.
- **SERP katmanı ağ isteği yapmaz.** Yalnızca açık olan sonuç sayfasını okur. Semrush, Whois veya başka bir üçüncü taraf verisi kullanılmaz.
- **Açık kaynak.** MIT lisansı.

## İzinler

| İzin | Ne zaman | Ne için |
|---|---|---|
| `activeTab`, `scripting` | Simgeye tıklayınca | Açık sekmedeki sayfayı analiz etmek |
| `storage` | Her zaman | Ayarlarınızı saklamak |
| İçerik betiği (43 Google alan adı) | Yalnızca `google.<ülke>/search*` sayfaları | SERP katmanı. Başka hiçbir sitede çalışmaz |
| `webRequest` + `http://*/*`, `https://*/*` | **İsteğe bağlı**, kurulumda istenmez | Aşağıya bakın |

**İsteğe bağlı izin.** Tam raporda "Yönlendirme zincirini göster", "Diğer sitelere erişime izin ver" veya "Başka sunuculardaki site haritalarını kontrol et" düğmesine bastığınızda Chrome bir kez izin ister. Tek izin üçünü de kapsar. Bununla rapor, yönlendirme zincirini adım adım (her URL ve durum kodu) gösterir ve başka sitelerdeki bağlantıları, görselleri ve site haritalarını o sitelerin CORS başlıklarına bağlı kalmadan kontrol eder.

- `webRequest` dinleyicisi yalnızca eklentinin kendi isteği sürerken açıktır, gezinmenizi görmez ve kaydetmez.
- İzni vermezseniz eski davranış sürer ve ilgili satırda "çalışmadı" notu görünür.
- İzni `chrome://extensions` sayfasından geri alabilirsiniz.

**Ağ istekleri.** Tarama sırasında yalnızca incelenen siteye gider: sayfanın kendisi (ham HTML + yanıt başlıkları), `robots.txt`, aynı sitedeki site haritası. Bağlantı kontrolü, görsel boyutu ölçümü, yönlendirme zinciri ve başka sunuculardaki site haritaları yalnızca siz başlatınca çalışır. Tüm istekler çerezsiz gönderilir, Blakfy'ye veya üçüncü taraflara hiçbir şey gönderilmez.

## Geliştirme

```bash
npm run build      # dist/ klasörünü üretir (esbuild, simgeler derleme sırasında çizilir)
npm test           # 50 birim testi (node --test)
npm run test:e2e   # gerçek Chromium'da uçtan uca test (önce npm run build)
npm run check      # dist/manifest.json izinlerini ve URL'leri denetler
```

`npm run check` şunları doğrular: kurulum izinleri, isteğe bağlı izinlerin tam listesi, tek içerik betiğinin yalnızca Google arama yollarında olduğu, SERP betiğinde ağ isteği API'si olmadığı. Derlenmiş dosyalardaki tüm URL'leri de listeler.

`test:e2e` yönlendirme zincirini, döngüyü ve CORS başlığı olmayan sitede bağlantı / görsel / site haritası kontrolünü sınar. İsteğe bağlı izinler test kopyasında baştan verilir, izin penceresinin kendisi otomatik tıklanamaz.

### Klasörler

```
src/engine/     analiz motoru (kopya) + eşik dosyaları
src/lib/        saf modüller: denetim, anahtar kelime, bağlantı, robots.txt, site haritası, schema
src/inspector/  sayfaya enjekte edilen betik ve işaretleme katmanı
src/serp/       Google arama sonuçları katmanı (içerik betiği + stil)
src/ui/         popup, rapor ve ayarlar sayfaları
src/_locales/   tr ve en metinleri
test/           birim testleri
docs/           tasarım notları
```

Analiz motoru WebForge `site-builder/seo-uzman/health/page-inspect-core.mjs` dosyasından `src/engine/` içine kopyalanmıştır (kaynak yolu dosya başlığında yazar). Kopyada tek bir yerel değişiklik vardır: her bulgu, İngilizce metninin yanında bir mesaj kodu ve parametreler taşır (arayüz çevirisi için). Motor yeniden kopyalanırsa bu değişiklik yeniden uygulanmalıdır. `test/engine-i18n.test.mjs` metni eksik bir kod olursa başarısız olur.

## Gizlilik

Gizlilik politikası blakfy.com üzerinde yayımlanacak: <https://blakfy.com/>

<!-- TODO: gizlilik politikasının kesin adresi belli olunca bu bağlantıyı ve src/ui/options.html içindeki bağlantıyı güncelle. -->

## Lisans

[MIT](./LICENSE) © 2026 Blakfy Studio

---

## English

**Seorius** is an open-source Chrome extension (Manifest V3) that audits the on-page SEO of the current tab entirely inside your browser.

- **Popup:** URL, HTTP status, error / warning / note counts, six tabs (Overview, Headings, Images, Links, Social, Tools).
- **Google SERP overlay:** organic rank numbers, ad labelling, SERP feature tags (featured snippet, People Also Ask, local pack, AI Overview and more), CSV export.
- **Full report:** technical / content / mobile / social audit, redirect chain, keyword density, Open Graph and Twitter cards, JSON-LD / microdata / RDFa, robots.txt and sitemap checks, 2–5 URL comparison, JSON / CSV / print export.
- **Private by design:** analysis runs locally, nothing is sent to Blakfy or third parties. Install-time permissions are only `activeTab`, `scripting` and `storage`; the broader network access is optional and asked for only when you use the features that need it.
- **Languages:** Turkish and English.

**Install (unpacked, status: in development):** `npm install && npm run build`, then load the `dist/` folder from `chrome://extensions` with *Developer mode* on.

Website and docs: <https://tariktunc.github.io/seorius-seo-inspector-chrome-extension/>

Made by [Blakfy Studio](https://blakfy.com). Licensed under MIT.
