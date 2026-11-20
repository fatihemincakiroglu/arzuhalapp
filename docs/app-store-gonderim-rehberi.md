# App Store gönderim rehberi — Arzuhal

Bu belge App Store Connect'te "Add for Review" öncesi doldurulacak alanları ve önerilen cevapları listeler.
Ekran adları Apple tarafından zaman zaman değişir; birebir aynı görmezsen en yakın başlığı kullan.

## 0. Siteyi yayınla (URL'ler için)

`site/` klasörü 4 sayfalık statik bir sitedir (ana sayfa, gizlilik, destek, koşullar).

**Seçenek A — GitHub Pages:** Pages yalnızca kökten (`/`) ya da `/docs` klasöründen yayınlayabilir; `site/` seçilemez. Bu yüzden `site/` içindekileri yeni bir **public** repoya (örn. `arzuhal-site`) kopyala, sonra Settings → Pages → Branch `main` / `(root)` → Save. Özel repoda Pages ücretli plan ister.

**Seçenek B — Vercel (özel repoda da ücretsiz):** vercel.com → Add New → Project → bu repo → **Root Directory: `site`** → Deploy. Çıkan adres (örn. `https://arzuhal.vercel.app`) alttaki URL'lerin tabanı olur.

Yayından sonra dört adresi tarayıcıda aç ve çalıştığını doğrula.

| App Store Connect alanı | Değer |
|---|---|
| Marketing URL (isteğe bağlı) | `https://SİTEN/` |
| **Support URL (zorunlu)** | `https://SİTEN/destek/` |
| **Privacy Policy URL (zorunlu)** | `https://SİTEN/gizlilik/` |
| Terms of Use (isteğe bağlı) | `https://SİTEN/kosullar/` |

Not: Gizlilik ve koşul metinleri uygulama içindeki metinle uyumludur. Metni değiştirirsen ikisini birlikte güncelle.

## 1. App Privacy (Admin / hesap sahibi doldurur)

- App Privacy → **Get Started**
- "Do you or your third-party partners collect data from this app?" → **No, we do not collect data from this app**
- Save → **Publish**

Bu cevap, uygulamanın hiçbir sunucuya veri göndermemesine dayanır. `eas.json` içinde `EXPO_PUBLIC_API_URL` tanımlı **değilse** doğrudur. İleride `server/` yazım asistanını açarsan bu anketi ve gizlilik sayfasını güncellemen gerekir.

## 2. Age Rating (Yaş derecelendirmesi)

Soruların hepsini **None / Hayır** olarak işaretle (şiddet, cinsel içerik, kumar, küfür, tıbbi içerik, korku vb.). Ek sorularda da: kullanıcı üretimi içerik yok, mesajlaşma yok, sınırsız web erişimi yok, uygulama içi satın alma yok.
Beklenen sonuç: **4+** (docs/app-store.md ile uyumlu).

## 3. App Compliance (yeni bölüm)

- **Şifreleme (Export Compliance):** `app.json` içinde `ITSAppUsesNonExemptEncryption: false` var; build gönderirken tekrar sorulmaz. Sorulursa: yalnızca standart iOS şifrelemesi, muaf.
- **AB Dijital Hizmetler Yasası (DSA) "trader" durumu:** AB'de dağıtım yapacaksan Apple, kendini **trader** (ticari faaliyet yürüten) ya da **non-trader** olarak beyan etmeni ister. Bu, senin kişisel durumuna bağlıdır; hukuki bir tercih olduğu için kendin karar vermelisin. "Trader" seçersen ad, adres, telefon ve e-postan AB App Store sayfasında herkese görünür. Emin değilsen AB'yi dağıtım ülkelerinden çıkarabilir ya da bir uzmana danışabilirsin.
- Başka bir uyum sorusu çıkarsa (örn. Çin için güvenlik değerlendirmesi uyarısı): Çin anakarasında dağıtım yapmayacaksan **Pricing and Availability** bölümünden o ülkeyi kapat; mavi bilgi kutusu engel değildir.

## 4. App Accessibility (yeni, isteğe bağlı)

Erişilebilirlik etiketleri gönderim için zorunlu değil. Uygulamada birçok düğmede `accessibilityLabel` var; ama VoiceOver, büyük yazı ve karşıtlık özelliklerini gerçek cihazda **denemeden** "destekler" işaretleme. Boş bırakabilirsin.

## 5. Sürüm bilgileri (Distribution → iOS App Version 1.0)

| Alan | Değer |
|---|---|
| Promotional Text | docs/app-store.md → "Tanıtım metni" |
| Description | docs/app-store.md → "Açıklama" |
| Keywords | docs/app-store.md → "Anahtar kelimeler" |
| What's New (1.0'da yok / ilk sürüm) | "İlk sürüm: 20 dilekçe türü, toplu dilekçe, takip ve hatırlatma, kanıt ekleme ve PDF." |
| Copyright | `2026 Fatih Emin Çakıroğlu` |
| Screenshots | iPhone 6.1"/6.3" için 1179×2556 veya 1206×2622 (JPG/PNG, şeffaflıksız), en fazla 10 |
| Build | TestFlight'ta işlenmiş **çalışan** build (çökmeyen sürüm) seç |

## 6. App Information

| Alan | Değer |
|---|---|
| Name | Arzuhal: Dilekçe Yaz |
| Subtitle | Cebindeki arzuhalci |
| Category | Primary: Productivity · Secondary: Utilities |
| Content Rights | "Uygulama üçüncü taraf içeriği içermiyor" |
| Age Rating | 4+ (bölüm 2) |

## 7. Pricing and Availability

- Price: **Free** (0 TL)
- Availability: Türkiye (istersen tümü). Dilekçeler Türkiye mevzuatına göre yazıldığı için yalnızca Türkiye de mantıklıdır.

## 8. App Review Information

- Sign-in required: **No** (hesap yok)
- Contact: ad, soyad, **telefon** ve e-posta (Apple, inceleme sırasında ulaşabilmek için telefonu ister)
- Notes: docs/app-store.md → "App Review notu"

## 9. Gönder

Tüm kırmızı uyarılar bitince **Add for Review** → **Submit for Review**. Sürüm yayın şeklini (manuel / otomatik) "Version Release" bölümünden seç.

## Sık reddedilme nedenleri (kontrol listesi)

- [ ] Support URL ve Privacy Policy URL açılıyor
- [ ] Ekran görüntüleri uygulamayı gerçekten gösteriyor
- [ ] İncelemede kullanılan build açılıyor (çökme yok)
- [ ] Hukuki tavsiye vermediği açıkça yazılı (uygulamada ve açıklamada var)
- [ ] App Privacy cevabı gerçek davranışla uyumlu (veri toplanmıyor)
