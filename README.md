# 🎬 AptozaQ2 Ekaran Kayıt ve Video Edit Pro

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![FFmpeg](https://img.shields.io/badge/FFmpeg-Required-orange?style=for-the-badge&logo=ffmpeg)

**Gelişmiş, çok özellikli bir Python ekran kaydedici.**  
Gerçek zamanlı çizim, webcam PiP, ses kaydı, timeline editörü ve çok daha fazlası — tek bir uygulamada.

</div>


https://github.com/user-attachments/assets/aefcdbb3-8ee0-430f-9484-a46560762a28


---

## 📋 İçindekiler

- [Özellikler](#-özellikler)
- [Ekran Görüntüleri](#-ekran-görüntüleri)
- [Gereksinimler](#-gereksinimler)
- [Kurulum](#-kurulum)
- [Kullanım](#-kullanım)
- [Modüller & Mimari](#-modüller--mimari)
- [Kısayol Tuşları](#-kısayol-tuşları)
- [Ayarlar & Yapılandırma](#-ayarlar--yapılandırma)
- [Sıkça Sorulan Sorular](#-sıkça-sorulan-sorular)
- [Bilinen Sınırlamalar](#-bilinen-sınırlamalar)

---

## ✨ Özellikler
<img width="1919" height="1079" alt="ses8" src="https://github.com/user-attachments/assets/3255a3b3-3305-4d24-8447-7748fa8c737f" />

---

<img width="1919" height="1079" alt="AnaEkran1" src="https://github.com/user-attachments/assets/aae79bd8-4e52-4d22-95dc-772a5cc274dc" />

### 🖥️ Ekran Kaydı
- **Tam ekran veya bölge seçimi** — sürükleyip bırakarak piksel hassasiyetinde alan seçin
- **Ayarlanabilir FPS** — 10, 15, 20, 24, 30 veya 60 FPS seçeneği
- **Kalite kontrolü** — CRF tabanlı (0–51) sıkıştırma; `ultrafast` önayarı ile sıfır gecikme
- **Duraklatma / Devam** — kayıt sırasında duraklat, zaman çizelgesi doğru tutulur (tekrarlanan kareler ile boşluk dolumu)
- **ffmpeg entegrasyonu** — H.264 / libx264 codec ile üst düzey MP4 çıktısı; ffmpeg yoksa OpenCV fallback

### 🎙️ Ses Kaydı
- **Sistem mikrofonu** — PyAudio ile 44100 Hz, stereo, 16-bit PCM
- **Senkronizasyon** — Ses ve video ayrı thread'lerde kaydedilir, `ffmpeg -aresample async=1` ile birleştirilir
- **Duraklatma desteği** — Duraklama sırasında ses de otomatik olarak durdurulur
<img width="1919" height="1079" alt="ses9" src="https://github.com/user-attachments/assets/2c23b6be-34f6-40fd-a82c-95d563e16528" />

---

<img width="1919" height="1079" alt="ses8" src="https://github.com/user-attachments/assets/36964433-313a-4bc9-9dac-4aa38d7c8511" />

### 📷 Webcam (Picture-in-Picture)

<img width="1919" height="1079" alt="kameraönizleme13" src="https://github.com/user-attachments/assets/cf305d9e-a0ea-4e3b-a47c-335f811a3c31" />

- **Canlı PiP katmanı** — Webcam görüntüsü videonun üzerine gömülür
- **4 köşe konumu** — Sol üst, sağ üst, sol alt, sağ alt
- **Ayarlanabilir PiP boyutu** — Küçük / Orta / Büyük / Özel
- **Beyaz çerçeve + gölge efekti** — Profesyonel görünüm için otomatik border ve drop shadow
- **Canlı önizleme penceresi** — Kayıt sırasında ayrı bir pencerede webcam akışı gösterilir
- **Ayrı thread** — `WebcamVideoStream` sınıfı, ana kayıt döngüsünü bloklamaz

### 🎨 Gerçek Zamanlı Çizim Katmanı
<img width="1919" height="1079" alt="araçlarzoom11" src="https://github.com/user-attachments/assets/2c361216-c556-4dd7-9f40-dfea3c4fea08" />

Kayıt sırasında ekranın üzerine şeffaf bir katmanda çizim yapın:

| Araç | Açıklama |
|------|----------|
| 🖱️ Fare | Çizim modunu devre dışı bırakır, normal kullanım |
| ▭ Dikdörtgen | Bölge vurgulama kutusu |
| ○ Çember / Elips | Dairesel vurgu |
| ➜ Ok | Yön gösterme oku (PIL alpha-blended) |
| ╱ Çizgi | Düz çizgi |
| ✏️ Serbest Çizim | Kalemle serbest çizgi (smooth) |
| T Metin | Çift tıkla, yazı gir, boyut seç |
| ⌫ Silgi | Çizilen alanı temizler |

- **Renk seçici** — Tüm araçlar için özel renk
- **Kalınlık kaydırıcısı** — 1–15 px
- **Ekranı temizle** butonu
- **Çizim kaydedilir** — Tüm çizimler videonun içine gömülür (PIL alpha composite)
- **Platform uyumlu şeffaflık** — Windows `transparentcolor`, macOS `systemTransparent`, Linux `alpha=0.3`

### 🔍 Yakınlaştırma (Zoom)
- Kayıt sırasında **1×'ten 4×'e** kadar dinamik zoom
- **Fare imlecini takip eder** — Zoom merkezi otomatik güncellenir
- Kayan araç panelinden kaydırıcı ile anlık kontrol

### 💧 Filigran (Watermark)
- **Metin filigranı** — Özel yazı, arka plan arkaplan kutusu, yarı saydam
- **Görsel filigran** — PNG/JPG logo, alfa kanalı destekli
- **5 konum** — Sol üst, sağ üst, sol alt, sağ alt, merkez
- **Opaklık kaydırıcısı** — %0–%100

### 🖱️ İmleç Vurgulama
- Kaydedilen videoda imleç konumuna **renkli halka** çizilir
- Renk seçici ve boyut kaydırıcısı ile özelleştirilebilir

### 📸 Ekran Görüntüsü
<img width="1919" height="1079" alt="görselkayıt12" src="https://github.com/user-attachments/assets/0400baa1-6f05-4f4e-a2c7-94a2defb158d" />

- Kayıt sırasında veya bağımsız olarak PNG ekran görüntüsü al
- Otomatik zaman damgalı dosya adı

### ⏰ Zamanlanmış Kayıt
<img width="1919" height="1079" alt="timeline6" src="https://github.com/user-attachments/assets/3dc4454c-cf56-4296-9c84-32988399b35a" />

---

<img width="1919" height="1079" alt="ayarlar10" src="https://github.com/user-attachments/assets/894e5265-4635-4a0e-b9b0-fff675fdbbbf" />

- **Başlangıç ve bitiş saati** ayarla (SS:DD formatı)
- Arka planda bekleyen thread, belirlenen saatte kaydı otomatik başlatır/durdurur
- Durum çubuğunda geri sayım göstergesi

---

## 🛠️ Video & Ses Editörü
<img width="1919" height="1079" alt="timeline6" src="https://github.com/user-attachments/assets/dec7947f-8d04-464f-b86c-525d83085e37" />

---

<img width="1919" height="1079" alt="timeline7" src="https://github.com/user-attachments/assets/d83a9606-2f77-4366-b064-008a268af76a" />

### ✂️ Video Editörü
- **Kırpma (Trim)** — Başlangıç ve bitiş saniyesi girerek video kırpma
- **Birleştirme (Merge)** — Birden fazla videoyu sırayla tek dosyaya birleştir
- **Format Dönüştürme** — MP4, AVI, MKV, MOV, GIF, WebM, MP3, WAV
- Tüm işlemler arka planda thread ile yürütülür, arayüz donmaz

### 🎵 Ses Editörü

<img width="1919" height="1079" alt="ses8" src="https://github.com/user-attachments/assets/841c87bb-90cc-47f9-a3f2-c5c1b09f4aeb" />

---

<img width="1919" height="1079" alt="ses9" src="https://github.com/user-attachments/assets/d7e9aaa7-2532-4449-b7ca-e231cbdfe129" />

- **Kırpma** — Saniye bazlı ses kırpma (8 format destekli)
- **Bölme (Split)** — Ses dosyasını belirli bir noktadan ikiye böl
- **Dönüştürme** — MP3, WAV, OGG, AAC, FLAC, M4A, Opus, WMA
- **Birleştirme** — Birden fazla ses dosyasını sırayla birleştir
- **Önizleme** — pygame ile ses dosyası oynatma

### 🎞️ Timeline Editörü
Tam özellikli çok parçalı video editörü:

<img width="1919" height="1079" alt="timeline7" src="https://github.com/user-attachments/assets/17e1f7a7-bdcd-4c7b-8467-5142911a9758" />

---

<img width="1919" height="1079" alt="timeline6" src="https://github.com/user-attachments/assets/a76c08b6-4826-4a28-8606-94a84f5564f1" />

- **Sürükle & Bırak** — Klipleri timeline'da serbestçe konumlandır
- **Kenar Kırpma** — Sol/sağ kenarları sürükleyerek trim et
- **Hız Kontrolü** — Her klip için 0.25× – 4× hız ayarı
- **Klip Susturma** — Seçilen klibin sesini kapat
- **Yeniden Ölçekleme** — Klip için özel çözünürlük
- **Geçiş Efektleri** — Klipler arası geçiş; Fade, Dissolve, Wipe (Sağ/Sol/Yukarı/Aşağı), Zoom, Slide
- **Metin Katmanları (TextOverlay)** — Belirli zaman aralığında ekrana metin ekle
- **Ses Parçaları** — Bağımsız ses dosyaları (MP3/WAV/AAC vb.) timeline'a ekle, trim et, ses seviyesi ayarla
- **Thumbnail önizleme** — Her klibin zaman çizelgesindeki küçük resmi
- **Timeline Zoom** — Saniye/piksel oranını artır/azalt
- **Export** — Tüm timeline'ı ffmpeg concat + filter_complex ile tek dosyaya aktar

### 🖼️ Görselden Video (ImageToVideoModule)
<img width="1919" height="1079" alt="görselkayıt12" src="https://github.com/user-attachments/assets/e54f2fd8-85b8-4ca2-9694-10f1c681d4fd" />

- PNG / JPG / BMP / WebP görsellerden video oluştur
- Her görsel için ayrı süre ayarı
- **Efektler (her görsel için bağımsız)**:
  - Renk: Parlaklık, Kontrast, Doygunluk, Gama, Ton (Hue)
  - Filtreler: Siyah-Beyaz, Sepya, Kırmızı/Mavi Filtre, Vignette, Keskinleştir, Renk Tersine Çevir, Bulanıklık
  - Transform: Ayna (yatay), Dikey Çevir, 90° Döndür
  - Geçişler: Fade In / Fade Out (saniye bazlı)
- **Canlı önizleme** — Her efekt değiştiğinde otomatik güncellenen önizleme
- Çözünürlük: 1920×1080, 1280×720, 854×480 veya özel
- Arka planda ffmpeg ile işleme

---

## 📦 Gereksinimler

### Python Sürümü
- **Python 3.8 veya üzeri** (Python 3.10+ önerilir)

### Sistem Bağımlılıkları

#### FFmpeg (Zorunlu)
FFmpeg olmadan video kaydedilemez. Yüklemek için:

**Windows:**
```
https://ffmpeg.org/download.html
winget install ffmpeg
# veya
choco install ffmpeg
```

**macOS:**
```bash
brew install ffmpeg
```

**Linux (Debian/Ubuntu):**
```bash
sudo apt install ffmpeg
```

#### PyAudio Sistem Bağımlılığı
**Linux:**
```bash
sudo apt install portaudio19-dev python3-pyaudio
```

**macOS:**
```bash
brew install portaudio
```

**Windows:** `pip install pyaudio` genellikle yeterlidir.

---

## 🚀 Kurulum

### 1. Depoyu Klonlayın
```bash
git clone https://github.com/kullanici/ekrankayit-pro.git
cd ekrankayit-pro
```

### 2. Sanal Ortam Oluşturun (Önerilir)
```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

### 3. Bağımlılıkları Yükleyin
```bash
pip install -r requirements.txt
```

### 4. Uygulamayı Başlatın
```bash
python AQ2son.py
```

---

## 🎮 Kullanım

### Temel Kayıt Akışı

1. **Bölge Seç** (opsiyonel) — "Bölge Seç" butonuna basıp sürükleyerek alan belirleyin, ya da tam ekran bırakın.
2. **FPS & Kalite** — Yan panelden ayarlayın.
3. **Webcam / Ses** — Gerekirse toggle switch ile etkinleştirin.
4. **▶ Başlat** — Kaydı başlatın. Zamanlayıcı canlı olarak güncellenir.
5. **⏸ Duraklat / ▶ Devam** — İstediğiniz zaman duraklatın.
6. **⏹ Durdur** — Kayıt bitirilir, ses ve video otomatik birleştirilir.
7. Çıktı dosyası, seçili klasöre zaman damgalı isimle (örn. `kayit_20240815_143022.mp4`) kaydedilir.

### Çizim Modu
1. Kayıt başladıktan sonra **"Çizim Modu"** switch'ini açın.
2. **Araç Paneli** otomatik açılır — araç, renk ve kalınlık seçin.
3. Ekranın üzerinde çizin; çizimler videonun içine gömülür.
4. **"Ekranı Temizle"** ile tüm çizimleri silin.
<img width="1919" height="1079" alt="araçlarzoom11" src="https://github.com/user-attachments/assets/91152a59-7406-411b-98f8-193aca631a9c" />

### Timeline Editörü
1. **"Timeline Editörü"** sekmesine geçin.
2. **"Video Ekle"** ile klip(ler) içe aktarın.
3. Klipleri sürükleyerek konumlandırın; kenarlarından çekerek trim edin.
4. Klipler arası **çift tıklayın** veya "Geçiş Ekle" butonunu kullanarak geçiş efekti seçin.
5. **"Ses Parçası Ekle"** ile arka plan müziği ekleyin.
6. **"Metin Ekle"** ile zaman damgalı altyazı/başlık ekleyin.
7. **"Dışa Aktar"** ile son videoyu oluşturun.

---

## 🗂️ Modüller & Mimari

```
ekrankayit-pro/
├── AQ2son.py               # Ana uygulama (UI + Engine)
├── ImageToVideoModule.py   # Görselden video oluşturma modülü
├── AQ2.ico                 # Uygulama ikonu (opsiyonel)
├── requirements.txt
└── README.md
```

### Temel Sınıflar

| Sınıf | Dosya | Açıklama |
|-------|-------|----------|
| `App` | AptozaQ2main.py | Ana pencere, sekme yönetimi, ayarlar |
| `RecordingEngine` | AptozaQ2main.py | Kayıt motoru; ekran, webcam, ses thread'leri |
| `WebcamVideoStream` | AptozaQ2main.py | Webcam'i ayrı thread'de okur |
| `WebcamPreviewWindow` | AptozaQ2main.py | Canlı webcam önizleme penceresi |
| `DrawingOverlay` | AptozaQ2main.py | Şeffaf çizim katmanı (2 Toplevel pencere) |
| `FloatingToolWindow` | AptozaQ2main.py | Yüzer araç paneli (always-on-top) |
| `RegionSelector` | AptozaQ2main.py | Ekran bölgesi seçim arayüzü |
| `VideoEditor` | AptozaQ2main.py | ffmpeg tabanlı video işlemleri |
| `AudioEditor` | AptozaQ2main.py | ffmpeg tabanlı ses işlemleri |
| `TimelineEditor` | AptozaQ2main.py | Çok parçalı timeline editörü |
| `ClipData` | AptozaQ2main.py | Timeline klip verisi |
| `AudioTrack` | AptozaQ2main.py | Timeline ses parçası verisi |
| `TextOverlay` | AptozaQ2main.py | Timeline metin katmanı |
| `TransitionData` | AptozaQ2main.py | Klip geçiş efekti verisi |
| `ImageToVideoEditor` | ImageToVideoModule.py | Görselden video oluşturma modülü |

### Kayıt Pipeline'ı

```
mss.grab()  ──►  numpy array  ──►  ffmpeg (pipe / OpenCV fallback)
                      │
              Zoom (crop+resize)
              PiP (webcam çerçeveleme)
              DrawingLayer (PIL alpha composite)
              CursorHighlight (OpenCV circle)
              Watermark (PIL RGBA overlay)
                      │
               ffmpeg stdin pipe  ──►  video.mp4 (libx264)

pyaudio stream  ──►  WAV buffer  ──►  ses.wav

ffmpeg -i video.mp4 -i ses.wav -c copy  ──►  FINAL.mp4
```

---

## ⌨️ Kısayol Tuşları

Varsayılan kısayollar aşağıdaki gibidir; **Ayarlar → Kısayollar** sekmesinden tamamen özelleştirilebilir.

| İşlem | Varsayılan Kısayol |
|-------|--------------------|
| Kaydı Başlat | `F9` |
| Duraklat / Devam | `F10` |
| Durdur | `F11` |
| Ekran Görüntüsü | `F12` |
| Çizim Modunu Aç/Kapat | `ctrl+d` |

> **Not:** `pynput` kütüphanesi yüklüyse kısayollar **global** (uygulama arka plandayken de) çalışır. Yoksa yalnızca uygulama odaktayken aktif olur.

Yeni kısayol atamak için:
1. **Ayarlar → Kısayollar** sekmesini açın.
2. İstediğiniz işlemin karşısındaki **"Ata"** butonuna tıklayın.
3. Klavyede istediğiniz tuşa basın.
4. **"✓ Uygula"** ile kaydedin.

---

## ⚙️ Ayarlar & Yapılandırma

Ayarlar, uygulama kapatıldığında otomatik olarak kaydedilir ve bir sonraki açılışta yüklenir.

**Yapılandırma dosyası konumu:**
- Windows: `C:\Users\<kullanici>\.ekran_kayit_pro.json`
- macOS / Linux: `~/.ekran_kayit_pro.json`

**Kaydedilen ayarlar:**

```json
{
  "output_dir": "/home/kullanici/Videos",
  "fps": 30,
  "quality": 23,
  "cursor_hl": false,
  "cursor_sz": 22,
  "wm_text": "© Benim Şirketim",
  "wm_pos": "bottom-right",
  "wm_opacity": 0.6,
  "shortcuts": {
    "start": "F9",
    "pause": "F10",
    "stop": "F11",
    "screenshot": "F12",
    "draw": "ctrl+d"
  }
}
```

---

## ❓ Sıkça Sorulan Sorular

**S: Kayıt çok sık atlıyor (frame drop), ne yapmalıyım?**  
C: FPS değerini düşürün (30→15) ve kalite CRF değerini artırın (daha yüksek CRF = daha az kalite ama daha az işlem yükü). Aynı zamanda kayıt bölgesini küçültün.

**S: Ses kaydedilmiyor.**  
C: `PyAudio` kurulu mu kontrol edin. Linux'ta `portaudio19-dev` paketinin yüklü olması gerekir. Ses sekmesinin toggle'ı açık mı kontrol edin.

**S: Webcam görüntüsü siyah geliyor.**  
C: Kamera dizinini kontrol edin. Varsayılan `0`'dır; birden fazla kamera varsa `1` veya `2` deneyin. Webcam başka bir uygulama tarafından kullanılıyor olabilir.

**S: Timeline dışa aktarma çok uzun sürüyor.**  
C: Bu normaldir; timeline editörü her klip için ayrı bir ffmpeg işlemi çalıştırır. Uzun ve yüksek çözünürlüklü videolarda bu süre uzayabilir.

**S: macOS'ta çizim katmanı görünmüyor.**  
C: macOS'ta `systemTransparent` pencere desteği bazı sürümlerde kısıtlı olabilir. Tk/Tcl sürümünüzü güncelleyin.

---

## ⚠️ Bilinen Sınırlamalar

- **Linux'ta tam şeffaflık** yalnızca kompozit (compositing) pencere yöneticisi bulunan masaüstü ortamlarında (GNOME, KDE, XFCE+Compton vb.) düzgün çalışır.
- **Ekran görüntüsü / kayıt kalitesi**, kullanılan ekranın DPI ölçekleme ayarından etkilenebilir. Windows'ta `%125` veya `%150` ölçekleme varsa bölge koordinatları kayabilir.
- **macOS M1/M2 (Apple Silicon)** üzerinde `PyAudio` kurulumu ek adımlar gerektirebilir (`brew install portaudio` ardından `pip install pyaudio`).
- Timeline editörü, **50'den fazla klip** için ağır olabilir; büyük projeler için `ffmpeg` komut satırı araçları önerilir.
- Görsel filigranlar `.PNG` formatında (alfa kanalı ile) en iyi sonucu verir; JPEG filigranlar şeffaflık içermez.

---

## 📄 Lisans

Bu proje **MIT Lisansı** ile lisanslanmıştır. Ayrıntılar için `LICENSE` dosyasına bakın.

---

<div align="center">
  <sub>EkranKayıt Pro — Python ile üretilmiş, <strong>CustomTkinter</strong> ile stilize edilmiş.</sub>
</div>
