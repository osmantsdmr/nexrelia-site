# NexRelia Web Testleri — Standart ve Playbook

Bu doküman, nexrelia.com/testler/ altındaki kişilik testlerinin (kaçıngan,
red-flag ve sonrakiler) nasıl tasarlandığını, hangi kalite çıtasında
tutulduğunu ve hangi teknik kurallara uyduğunu tanımlar. Yeni bir test
eklerken — yeni bir sohbette veya doğrudan Claude Code ile — buradan
başlanır.

---

## Canlı Testler

**5 canlı test** — vitrindeki hedefe ulaşıldı, "Yakında" yer tutucusu
kalmadı.

| Test | Çerçeve | Model / görselleştirme | Soru | Sonuç | URL |
|---|---|---|---|---|---|
| Ne Kadar Kaçıngansın? | Bağlanma teorisi (kaygı × kaçınma) | 2 sürekli eksen, kadran + eksen haritası | 14 | 8 | `/testler/kacingan` |
| Ne Kadar Red Flag'sin? | Gottman'ın Dört Atlısı | Baskın kategori, 4 köşeli radar | 16 | 9 | `/testler/red-flag` |
| Aşk Dilin Ne? | Chapman'ın Beş Aşk Dili | Birincil + ikincil, pentagon radar | 20 | 5 | `/testler/ask-dili` |
| Çatışma Tarzın Ne? | Thomas-Kilmann | 2 eksen + merkez dairesi, harita | 12 | 5 | `/testler/catisma-tarzi` |
| Ne Tür Bir Aşıksın? | Lee'nin Aşkın Renkleri (Colours of Love) | Dominant-kazanan; eksen/kadran yok, altıgen radar | 18 | 6 | `/testler/ask-stili` |

Bu tablo yeni test eklendiğinde güncellenir. Bölüm numarası bilinçli
olarak verilmedi — §1-§10 referansları (ör. §3.3, §9.6) sabit kalsın diye.

---

## 1. Felsefe / Kalite Çıtası

- **Her testin içeriği gerçek, tanınmış bir psikoloji/ilişki araştırmasına
  dayanmalı** (bağlanma teorisi, Gottman'ın Dört Atlısı gibi). TikTok
  içeriğinden ilham alınabilir ama asla referans/kaynak olarak
  kullanılmaz — TikTok serileri bilerek düşük derinlikli (5 soru, tek
  eksen) tutulmuştu, web testleri bunun kalite sıçraması yaptığı yer.
- Klinik tanı aracı değil — ama "meme kalitesinde" de değil. Arada,
  bilinçli bir yer: gerçek çerçeve + sıcak/eğlenceli sunum.
- **Her test kendi karakteristik tasarımına sahip olmalı.** Paylaşılan
  mimari (soru akışı, kart iskeleti, hikaye export'u) ortak; görsel kimlik
  (renk ailesi, veri görselleştirmesi, ikonlar, hub kartı motifi) her
  testte özgün.
- Anonim kalmalı — giriş/email/kayıt yok, client-side skor.

---

## 2. İçerik Geliştirme Süreci

1. Gerçek, araştırılmış bir çerçeve seç. `web_search` ile doğrula, hafızadan
   uydurma — özellikle sayısal iddialar (ör. "%90 doğrulukla öngörüyor")
   mutlaka kaynaklı olmalı.
2. Puanlama mekaniğini çerçevenin doğasına göre seç:
   - **2 bağımsız sürekli eksen** varsa (ör. bağlanma teorisi: kaygı ×
     kaçınma) → kadran modeli, eksen haritası (axis-map) görselleştirmesi.
   - **N bağımsız kategori** varsa (ör. Gottman'ın 4 atlısı) → baskın
     kategori modeli, radar grafik görselleştirmesi.
   - Yeni bir çerçeve bu ikisine de uymuyorsa, planlama sohbetinde
     mekaniği sıfırdan tartış — şablonu zorla uydurma.
3. Soru sayısı: eksen/kategori başına ~4-7 soru. Toplamda TikTok'un 5
   sorusundan kesinlikle daha derin (kaçıngan: 14, red-flag: 16).
4. Sonuç sayısı hedefi: ~8-9 (kategori × yoğunluk + varsa nötr/pozitif bir
   sonuç). Amaç: "hep aynı sonuç çıkıyor" hissini önlemek.
5. Her sonuç için: isim (Türkçe, akılda kalıcı, DİĞER testlerdeki
   isimlerle/motiflerle çakışmasın) + kısa caption (kart için) + uzun
   reflection metni (klinik olmayan, sıcak, yargılamayan ton) + 3 kısa
   etiket + kendine özgü ikon.
   - **Bu beşlinin en çok atlanan alanı `caption`.** Uzun reflection
     metni, etiketler ve ikon yönü yazılıp kısa caption unutulunca
     Claude Code'a gönderilen brief eksik kalıyor — kart şablonu o satırı
     zorunlu istediği için Claude Code onu kendisi uydurmak zorunda
     kalıyor ve arketip sesi senin onayından geçmemiş oluyor
     (ask-stili'nde altı caption'ın altısı da böyle üretildi). Caption
     brief'te AYRI bir alan olarak, birinci tekil şahısla yazılmalı.
6. Kapanış metni her testte aynı formülü izler: "Bu test eğlence ve
   öz-farkındalık amaçlıdır, klinik bir değerlendirme değildir" uyarısı +
   NexRelia uygulamasına yumuşak bir köprü cümlesi.
7. İçerik bir markdown taslağı olarak yazılır (bilimsel çerçeve + puanlama
   mekaniği + tam sorular + tam arketipler + kapanış + "AÇIK KARARLAR"
   bölümü) ve Osman'ın onayına sunulur — kodlamaya bundan ÖNCE
   başlanmaz.

---

## 3. Tasarım Süreci

1. İçerik onaylandıktan sonra **tek sayfalık, tam çalışan bir interaktif
   HTML prototip** kurulur (gerçek soru akışı + gerçek puanlama + sonuç
   kartı). Bu prototip planlama sohbetinde paylaşılır, Claude Code'a
   GÖNDERİLMEDEN önce.
2. Prototip sitenin GERÇEK renk token'larıyla kurulur — rastgele/uydurma
   renk yok: `--burgundy #1A0612 --mauve #D4A0C8 --mauve-light #E8C8E0
   --mauve-dark #B07CA6 --cream #FFF8F5 --text #2D1B28 --text-light
   #6B5566`.
3. Her testin kendi "aksan ailesi" olur ama bu palet AİLESİNİN içinde
   kalır. Testler hub sayfasında yan yana durunca görsel olarak
   ayrışmalı, ama markaya yabancı bir renk (parlak yeşil, neon mavi vb.)
   asla kullanılmaz.
4. Fontlar sabit: **Fraunces** (serif, başlıklar/arketip isimleri),
   **Manrope** (gövde metni), **IBM Plex Mono** (meta bilgiler, veri
   etiketleri, ilerleme göstergesi). Bu üçlü markanın "test sesi".
5. Kart mimarisi sabit iskelet: eyebrow → isim → caption → ikon → 3 etiket
   → veri görselleştirmesi (teste özel: axis-map / radar / vb.) →
   watermark URL. Veri görselleştirmesi DIŞINDA hiçbir eleman teste göre
   değişmez.
6. Renk/kart doluluğu/geçiş gibi kararlar ÖNCE bu sohbette görsel olarak
   iterasyona sokulur, geri bildirim alınır, SONRA Claude Code'a
   implementasyon promptu yazılır. Görülmeden Claude Code'a "böyle bir
   kart tasarla" denmez.

---

## 4. Teknik Mimari (nexrelia-site)

- Site **%100 statik, build adımı yok**, ortak layout/partial mekanizması
  yok. Her sayfa kendi `<head>`/nav/footer/cookie-banner'ını taşır
  (`soru.html`'den kopyalanır — bu, sitedeki "interaktif sayfa" için en
  yakın emsal).
- Her test şu yapıyı izler:
  - `testler/{test-slug}.html` — quiz akışı (tek sayfa, sonuç ekranı YOK).
  - `testler/{test-slug}-{sonuç-slug}.html` — her sonuç için AYRI, statik
    bir sayfa (N adet).
  - **Neden statik sonuç sayfaları:** WhatsApp/Twitter/Instagram paylaşımında
    doğru OG görseli SADECE statik meta etiketiyle garanti edilir; JS ile
    sonradan enjekte edilen meta etiketlerini sosyal medya botları
    genellikle okumaz.
- Skor(lar), quiz sayfasından sonuç sayfasına **URL query param'larıyla**
  taşınır (ör. kaçıngan: `?k=&a=`, red-flag: `?ce=&ku=&sa=&du=`). Sonuç
  sayfasının JS'i bu param'ları okuyup kartı kişiselleştirir. Param
  yoksa (çıplak URL, ikinci elden paylaşılan link) sayfa HATA VERMEDEN
  genel/statik arketip içeriğini gösterir — sayı/harita/radar gizlenir.
- **CSS tek dosyada toplanır: `testler.css`.** Sayfa içi `<style>` bloğu
  kullanılmaz. Yeni bir test eklerken ÖNCE bu dosyayı oku — özellikle
  jenerik isimli class'lar (`.card`, `.card-icon`, `.card-name` gibi)
  muhtemelen zaten dolu. Çakışma varsa yeni bir önek (`.tcard-*`,
  `.rf-*` gibi) kullan, mevcut kuralları asla üzerine yazma.

---

## 5. Sonuç Kartı ve Paylaşım Formatı

- **Görünen kart** (sayfa içi önizleme): 4:5 oranında.
- **İndirilen/paylaşılan kart HER ZAMAN 9:16'dır.** 4:5 asla indirilip
  paylaşılmaz — Instagram/TikTok Hikaye'de küçük bir dikdörtgen olarak
  kalır, ekranı doldurmaz, estetiği bozar. (Bu, kaçıngan testinde sonradan
  düzeltilen bir hataydı — red-flag'de baştan doğru yapıldı.)
- 9:16 export mimarisi:
  - Gizli bir export elementi: `position:absolute; left:-9999px` —
    **`display:none` KULLANILMAZ**, html2canvas görünmeyen elementleri
    render edemez.
  - Element boyutu 540×960 CSS px, `html2canvas` `scale:2` → gerçek çıktı
    1080×1920.
  - Arketibin küçük ikonu `cloneNode(true)` ile büyütülüp (~13-14×),
    çok soluk (opacity `.07`) bir arka plan motifi olarak yeniden
    kullanılır — yeniden çizilmez. Bu, uzun dikey alanı anlamlı doldurur
    (boş dolgu değil).
  - Veri görselleştirmesi (axis-map/radar) hem görünen kartta hem hikaye
    kartında **AYNI fonksiyonla**, ikinci bir hedef parametresiyle
    çizilir — kopyalanmaz.
  - Dosya adı deseni: `nexrelia-{test-slug}-{sonuç-slug}.png`.

---

## 6. Renk ve İkon Kuralları

- Her testin kendi aksan ailesi olur, site paletinin (burgundy/mauve
  ailesi) İÇİNDE kalarak. Örnek: kaçıngan → mor-pembe/mauve tonları;
  red-flag → mercan-kiremit (bilinçli olarak saf kırmızı DEĞİL, çünkü
  krem/bordo paletinde alarm gibi durur).
- Testler hub sayfasında yan yana durunca görsel olarak ayrışmalı — aynı
  aksan ailesini iki testte kullanma.
- **Renk kontrolü İKİ AŞAMALI.** §3.3'teki "marka paletinin içinde kal"
  kuralını geçmek yeterli DEĞİL; bu yalnızca birinci süzgeç. İkinci
  süzgeç: yeni renkler **mevcut testlerin arketip renkleriyle tek tek
  karşılaştırılmalı**. Bunlar birbirinden bağımsız iki risk —
  marka dışı renk riski (parlak yeşil vb.) ile repo içi çakışma riski
  (yeni testin altını, aşk dilinin altınıyla aynı aileye düşmesi gibi)
  aynı kontrolle yakalanmaz. Arketip renkleri tek bir yerde tanımlı
  değil, her sonuç sayfasının `#stage` elementinde inline duruyor:
  `grep -ho 'id="stage" style="[^"]*"' testler/*.html | sort -u`
  komutu mevcut tüm aksan çiftlerini listeler, karşılaştırma bunun
  üzerinden yapılır.
- Her arketibin **kendine özgü, anlamına gönderme yapan** bir ikonu olur
  (jenerik/tekrar eden ikon yok). Testler ARASI motif çakışmasına da
  dikkat — ör. "tuğla duvar" ikonu kaçıngan'ın "Duvar Ustası"nda
  kullanıldığı için, red-flag'in "Duvar Örme" kategorisinde FARKLI bir
  motif (kapalı kapı) seçildi.

---

## 7. Vitrin (Hub) Entegrasyonu — `testler/index.html`

- Yeni test eklendiğinde, varsa "Yakında" yer tutucu kartı gerçek kartla
  değiştirilir; yoksa yeni kart eklenir.
- Her kartın kendi **karakteristik motifi** olur — testin mekaniğine
  gönderme yapan, büyük ve soluk bir arka plan deseni (kaçıngan: 2×2
  ızgara; red-flag: radar ana hatları). Jenerik ikon + düz beyaz kart
  yeterli değildir.
- "+X sonuç daha" önizleme şeridi: birkaç arketibin aksan renginden küçük
  noktalar — HANGİ rengin HANGİ sonuca ait olduğu söylenmez (spoiler yok,
  merak uyandırır, tıklama isteği yaratır).
- Kart zemini canlı/doygun olmalı (düz beyaz DEĞİL) — vitrindeki en canlı
  öğe test kartları olmalı, sayfanın geri kalanı (hero) daha sakin
  kalabilir.
- **`conic-gradient` kullanılan kartta çarkın MERKEZİ kritik.** Merkez
  kartın içinde/ortasında kalırsa altı hue metnin altında birleşip
  bulanık bir yakınsama lekesi yapıyor; sert dilimler (`0deg 60deg`
  biçiminde stop'lar) ise metni kesip plaj topuna benziyor. Doğru kurgu:
  **merkezi tam köşeye al** (`at 100% 0%`) — kartın gördüğü dilim böylece
  tam 90° olur — ve renkleri açık stop'larla o dar açıya dağıt
  (`0deg, 18deg, 36deg …`). Tüm renkler görünür kalır, dikiş oluşmaz.
- **Çok renkli kartta değer rampasını ayrı bir katman vermeli.** Kardeş
  kartların hepsi `linear-gradient(150deg, açık → koyu)`: sol üst açık,
  sağ alt koyu. Saf `conic` bu rampayı taşımadığı için kart vitrinde
  yassı duruyor; üstüne ince bir linear katman bindirilerek ritim geri
  kazanılır. İkisi birlikte: `testler.css:929-953` (ask-stili, G varyantı).

---

## 8. GA4 / UTM / Ölçüm

- Standart event'ler: `quiz_start`, `quiz_complete` (parametre:
  `result_type: "{sonuç-slug}"`), `store_click`, `quiz_card_click`
  (yalnızca hub'da).
- Consent-aware GA yükleme deseni (`localStorage.cookie_consent`
  kontrolü) her sayfada birebir aynı — `soru.html`'deki kaynak desen.
- Mağaza linklerine UTM: `utm_source=web_quiz_{test-slug}&utm_medium=web
  &utm_campaign=testler`.
  - **DİKKAT:** `utm_campaign` değeri her zaman **`testler`** (çoğul,
    doğru yazım) — bir kez `tesler` yazım hatası yapılmıştı, tekrar
    kontrol edilmeli.
- **Play Store linki düz `&utm_source=...` parametresiyle ÇALIŞMAZ.**
  Google Play kampanya atfı yalnızca tek, encoded `&referrer=` parametresini
  okur:
  `&referrer=utm_source%3Dweb_quiz_{slug}%26utm_medium%3Dweb%26utm_campaign%3Dtestler`
- App Store linkindeki mevcut `?l=tr` korunarak UTM eklenir (App Store
  bunu kampanya atfı için kullanmaz ama zararı da yoktur).
- Bu UTM'ler SADECE test sayfalarında — `index.html`/`soru.html`'deki
  mevcut mağaza linklerine dokunulmaz.

---

## 9. Süreç / İş Akışı (Claude Code ile)

1. **Planlama sohbetinde:** araştırma (`web_search`) + içerik taslağı
   (`.md` dosyası, bölüm 2'deki formatla) → Osman'ın onayı.
2. **Planlama sohbetinde:** tam çalışan interaktif prototip (`.html`) →
   görsel/UX geri bildirim turu (renk, kart doluluğu, geçişler, veri
   görselleştirmesi) → onay. Gerekirse birden fazla iterasyon.
3. **Tek, kapsamlı FAZ A+B promptu:** pre-flight (mevcut CSS/mimari
   durumunu DOĞRULA, önceki testten bu yana değişmiş olabilir, tahmin
   etme) + implementasyon (onaylı prototipteki her veri/mantık birebir
   korunarak) + gerçek tarayıcı testi.
4. **Tamamlama raporunda gerçek görseller/PNG'ler bu sohbete
   YÜKLENMELİDİR.** Claude Code'un kendi dosya sistemindeki yollar
   ("yukarıda paylaştım", `C:\Users\...\scratchpad\...`) plan sohbetine
   ULAŞMAZ — görsel onay için dosya gerçekten bu sohbete eklenmeli.
5. Commit ayrı onay, push ayrı onay — proje genelindeki disiplin burada da
   geçerli. `git add -A` yok, hedefli staging.
6. Yeni test eklerken **mevcut testlerin sayfalarına ASLA dokunulmaz** —
   sadece yeni dosyalar + `testler.css`'e ekleme + `_redirects`/
   `sitemap.xml`'e ekleme + hub kartı güncellemesi.

---

## 10. Bilinen Tuzaklar (tekrar düşülmesin)

- **Radar/harita etiketleri viewBox sınırının dışına taşabilir** —
  köşe etiketleri (ör. "KÜÇÜMSEME", "DUVAR ÖRME") kırpılabilir; SVG
  viewBox'ını gerektiği kadar genişletip merkezleri koru, koordinat
  mantığına dokunma.
- **N köşeli radar bileşenleri tek bir açı sabitine bağlı, ama köşe
  sayısı değişince tuval taşar.** Fonksiyonun geometrisi `CATS` dizisi +
  `-90 + i * (360/N)` üzerinden sürülüyor; N'i değiştirmek için tek
  dokunulacak yer o sabit (pentagon 72° → altıgen 60°). Buna karşılık
  köşelerin nereye düştüğü değiştiği için etiketler eski viewBox'tan
  taşabiliyor — altıgende yatay köşeler pentagondan daha dışarı çıktığı
  için tuval 164 → 168 birime genişletildi (`-14 -14 168 168`).
  Koordinat mantığına yine dokunulmadı, yalnızca pay büyütüldü.
- **Class adı çakışması:** yeni test class'ları jenerik isim kullanırsa
  (`.card`, `.card-icon` vb.) mevcut sonuç kartı stilleriyle çakışır —
  namespace/önek şart.
- **4:5 kart paylaşılırsa Hikaye'de küçük kalır** — export HER ZAMAN
  9:16.
- **`display:none` ile gizlenen export elementleri html2canvas'ta hiç
  render olmaz** — `position:absolute; left:-9999px` kullan.
- **Play Store UTM'i düz parametreyle sessizce yok sayılır** — encoded
  `referrer` şart, aksi halde ölçüm hiç çalışmadan "çalışıyormuş gibi"
  görünür (hata vermez, sadece veri gelmez).
- **html2canvas, `text-transform: uppercase`'i Türkçe yerel ayarla (İ/ı
  noktalama kuralları) doğru uygulamıyor** — export'ta harfler bozuk
  çıkabilir (ör. `İŞBİRLİĞİ` → `İŞBIRLIĞI`). Büyük harfle görünmesi
  gereken ve html2canvas'ın yakalayacağı herhangi bir metin (eksen/harita
  etiketleri gibi), CSS `text-transform`'a GÜVENMEDEN, HTML'de doğrudan
  büyük harfle yazılmalı.
  - Tarayıcı doğru render ettiği için sayfada fark edilmez; sorun
    yalnızca indirilen/paylaşılan PNG'de görünür — bu yüzden her yeni
    testte export PNG'si yakınlaştırılarak kontrol edilmeli.
  - SVG `<text>` içeriklerinde `text-transform` zaten uygulanmaz; oradaki
    etiketler düz büyük harf yazıldığı sürece güvenlidir.
- **Watermark/URL metinlerine `text-transform: uppercase` uygulanmaz** —
  hem Türkçe/ASCII büyük harf uyuşmazlığı yaratır (tarayıcıda `NEXRELİA.COM`,
  export'ta `NEXRELIA.COM`) hem de bir alan adı için anlamsızdır. Watermark
  metni HTML'de zaten istenen (küçük harf) biçimde yazılmalı; ilgili
  class'lar `.card-bottom` ve `.story-watermark`.

---

## AÇIK İŞLER

Aktif olarak üzerinde çalışılmayan, ama unutulmaması gereken maddeler.

- **Nav'daki "Testler" linki her sayfada yok.** `/testler/` linki yalnızca
  `index.html` ve `testler/index.html` nav'ında bulunuyor; `soru.html`,
  `delete-account.html` ve beş `yasal/*.html` sayfasında eksik (toplam 7
  sayfa). Site ortak bir nav partial'ı taşımadığı için (§4) her sayfaya
  elle eklenmesi gerekir. **Karar Osman'da** — testlere her sayfadan
  erişim isteniyor mu, yoksa nav bilinçli olarak mı sade tutuluyor.
- **Hikaye kartındaki arka plan ikonu büyütülünce bozulabiliyor.**
  §5'teki desen gereği arketip ikonu `cloneNode` ile ~13-14× büyütülüp
  soluk bir motif olarak kullanılıyor. 40×40 tuvale çizilmiş, ince
  detaylı veya dikeyde tuvali dolduran ikonlar bu ölçekte soyut/garip
  bir şekle dönüşebiliyor (ask-stili "Dost Aşık": el ele iki figürün
  bacakları kartın altına doğru uzuyor). **Tek teste özel bir hata
  değil** — `.story-bgicon` konumlandırması tüm testlerde ortak, yani
  aynı davranış hepsinde geçerli. Düzeltmek ayrı bir görsel polish turu
  ister: ya ikonlar büyütmeye uygun sadelikte seçilir, ya `.story-bgicon`
  ölçek/konumu ikon başına ayarlanabilir hale getirilir. **Düşük
  öncelik** — çıktı bozuk değil, yalnızca motif okunaklılığı meselesi.

---

## AÇIK KARAR

Bu doküman `CLAUDE.md` olarak nexrelia-site reposunun köküne mi
yerleşsin (NexRelia ana app reposundaki gibi, gelecekte otomatik referans
alınabilecek bir konum), yoksa ayrı bir dosya adıyla (ör.
`TESTLER_STANDARDI.md`) mı dursun? Öneri: `CLAUDE.md` — bu repo şu ana
kadar hiç böyle bir dosyaya sahip değildi, bu iyi bir başlangıç noktası
ve gelecekte site mimarisine dair başka gerçekler de (statik yapı,
_redirects deseni, GA kurulumu) buraya eklenebilir.
