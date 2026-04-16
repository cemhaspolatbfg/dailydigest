# Output Format — Game Industry Daily Digest (Routine Edition)

> Bu dosya, Claude'un hazırladığı günlük özetin nasıl ve kime iletileceğini tanımlar.
> Routine olarak çalıştığı için mail **doğrudan gönderilir** (taslak değil).

---

## Teslimat Kanalı

- **Kanal:** Gmail connector
- **Gönderim modu:** Doğrudan gönderim (taslak oluşturma yok)
- **Alıcı 1 (birincil):** cemhaspolat@bugfix.games
- **Alıcı 2:** ibrahimakcal@bugfix.games
- **Alıcı 3:** enesgenc@bugfix.games
- **Konu satırı:** `🎮 Günlük Oyun Digest — DD/MM/YYYY`
- Sadece yukarıda belirtilen 3 adrese mail gönder, başka alıcı ekleme
- Üç alıcının da `to` alanında olduğunu doğrula (cc veya bcc kullanma)

---

## Format

- **Dil:** Türkçe
- **Uzunluk:** 500-800 kelime
- **Body type:** HTML (Markdown değil)

### Neden HTML?

Gmail connector'a Markdown body verirsen `**bold**` ve `[link](url)` sözdizimi düz metin olarak görünür ve mail bozulur. HTML body verdiğinde tıklanabilir linkler, başlıklar ve listeler düzgün render olur.

---

## HTML Mail Şablonu

Aşağıdaki şablonu kullan. Köşeli parantez içindeki yer tutucuları içerikle doldur. Yapıyı bozma — başlık seviyeleri (h2, h3) ve liste yapısı sabittir.

```html
<div style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; max-width: 680px; line-height: 1.6;">

  <h2 style="margin-bottom: 4px;">🎮 Günlük Oyun Endüstrisi Digest — [DD/MM/YYYY]</h2>
  <p>Günaydın! İşte bugünün özeti:</p>

  <hr style="border: none; border-top: 1px solid #ddd; margin: 20px 0;">

  <h3>📰 Günün Önemli Gelişmeleri</h3>

  <p><strong>Endüstri Haberleri:</strong></p>
  <ul>
    <li><strong>[Bold başlık]</strong> — [2-3 cümle özet] (<a href="[URL]">[Kaynak Adı]</a>)</li>
    <!-- Her madde için tekrarla, max 5 madde -->
  </ul>

  <p><strong>Topluluk Tartışmaları:</strong></p>
  <ul>
    <li><strong>[Bold başlık]</strong> — [2-3 cümle özet] (<a href="[URL]">[Kaynak Adı]</a>)</li>
  </ul>

  <h3>📈 Trend Radarı</h3>
  <ul>
    <li><strong>[Bold başlık]</strong> — [2-3 cümle açıklama] (<a href="[URL]">[Kaynak Adı]</a>)</li>
  </ul>

  <h3>💡 İlham Köşesi</h3>
  <ul>
    <li><strong>[Bold başlık]</strong> — [2-3 cümle, neden ilham verici] (<a href="[URL]">[Kaynak Adı]</a>)</li>
  </ul>

  <hr style="border: none; border-top: 1px solid #ddd; margin: 20px 0;">

  <p>☕ İyi çalışmalar!</p>

  <hr style="border: none; border-top: 1px solid #eee; margin: 24px 0 12px;">

  <p style="color: #888; font-size: 12px;">
    <strong>Execution Summary:</strong><br>
    Taranan kaynak: [N] RSS feed + [M] endüstri sitesi<br>
    Toplanan ham madde: [X] · Elenen: [Y] · Dahil edilen: [Z]<br>
    Erişilemeyen kaynaklar: [varsa liste, yoksa "yok"]<br>
    Çalışma süresi: [routine'in toplam süresi]
  </p>

</div>
```

### Link Kuralları

- Kaynak isimleri **tıklanabilir link** olmalı: `<a href="URL">Kaynak Adı</a>`
- Doğrudan ilgili post veya makaleye link ver, ana sayfaya değil
- Link bulunamıyorsa kaynak adını düz metin olarak yaz (`<a>` tag'i kullanma)
- Reddit linkleri için `https://www.reddit.com/r/...` formatını kullan (RSS'ten dönen `/r/.../comments/...` linki)

### Boş Bölüm Kuralı

Bir bölüm boş kalırsa `<li>` içinde italik olarak şunu yaz:

```html
<li><em>Bugün bu kategoride dikkat çeken bir şey yok.</em></li>
```

Asla uydurma içerik ekleme.

---

## Arşivleme

- Her gönderilen özeti repo'daki `archive/` klasörüne commit'le
- Dosya adı formatı: `archive/YYYY-MM-DD-digest.md`
- Örnek: `archive/2026-04-16-digest.md`
- Commit mesajı: `digest: YYYY-MM-DD`
- Arşivdeki dosya **Markdown** formatında olacak (mail HTML, arşiv Markdown — okuma kolaylığı için)

---

## Hata Durumları

- **Bir kaynağa erişilemezse:** Mail gövdesinde belirtme; execution summary'deki "Erişilemeyen kaynaklar" satırına ekle
- **Hiçbir kaynağa erişilemezse:** Aşağıdaki bilgilendirme mailini gönder, boş özet uydurma:

  ```html
  <p>⚠️ Bugün hiçbir kaynağa erişilemedi. Lütfen routine loglarını kontrol et.</p>
  <p>Tarih: [DD/MM/YYYY] · Saat: [HH:MM]</p>
  ```

- **Gmail gönderimi başarısız olursa:** Digest'i yine arşive commit'le. Commit mesajına `(MAIL FAILED: <hata mesajı>)` ekle. Routine bir sonraki manuel kontrolde durumu görsün.

---

*Son güncelleme: 2026-04-16 (Routine migration)*
