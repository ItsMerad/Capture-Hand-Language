# Capture Hand Language

Kamera uzerinden el isareti verisi toplama ve siniflandirma icin basit bir proje.

## Ozellikler
- Web kameradan el algilama (CVZone + OpenCV)
- Kareleri sabit boyuta getirip kaydetme
- Egitilmis model ile siniflandirma

## Gereksinimler
- Python 3.8+
- Web kamera
- Kutuphaneler:
  - opencv-python
  - cvzone
  - numpy

Kurulum:
```bash
pip install opencv-python cvzone numpy
```

## Kurulum Sonrası
Bu repoyu klonladiktan sonra eksiksiz calisma icin asagidaki klasorleri olusturmaniz gerekir:

1. **Veri Klasoru:** Egitim verisi icin
   ```bash
   mkdir -p data/class_a data/class_b data/class_c
   ```

2. **Model Klasoru:** Egitilmis modeli icin
   ```bash
   mkdir -p model
   ```
   - `keras_model.h5` dosyasini ekleyin (eger egitilmis modele sahipseniz)
   - `model/labels.txt` dosyasini olusturun (etiket isimleri, her satira bir)

## Klasor Yapisi
```
Capture Hand Language/
  capture_hand_dataset.py
  classify_hand_sign.py
  README.md
  data/                    # Yerel - GitHub'a eklenmez
    class_a/
    class_b/
    class_c/
  model/                   # Yerel - GitHub'a eklenmez
    keras_model.h5
    labels.txt
```

**Not:** `data/` ve `model/` klasörleri `.gitignore` tarafından hariç tutuluyor. Bunlar yerel gelistirme icin gereklidir.

## Veri Toplama
1. [capture_hand_dataset.py](capture_hand_dataset.py) dosyasinda `folder` degiskenini hedef sinif klasorune ayarlayin (ornegin `data/class_b`).
2. Calistirin:
   ```bash
   python capture_hand_dataset.py
   ```
3. Kamera acildiginda `s` tusuna bastikca, olusturulan kareler klasore kaydedilir.

Not: Kodda `offset` ve `imgSize` degerleri el kirpma ve olcekleme icin kullanilir. Ihtiyac halinde degistirebilirsiniz.

## Siniflandirma
1. [classify_hand_sign.py](classify_hand_sign.py) dosyasinda `labels` listesi ve `model/labels.txt` dosyasi uyumlu olmalidir.
2. Calistirin:
   ```bash
   python classify_hand_sign.py
   ```
3. Ekranda tahmin edilen etiket goruntulenir.

## Model
- Model dosyasi: `model/keras_model.h5` (Yerel olarak bulunmasi gerekir)
- Etiketler: `model/labels.txt` (Yerel olarak bulunmasi gerekir)

Model dosyalarini birisi kolay yontemiyle TensorFlow/Keras kullanarak egitebilir. Modelin input boyutu ve sinif sayisi `classify_hand_sign.py` ile uyumlu olmalidir.

## Ipuclari
- Daha iyi sonuclar icin aydinlatma ve arka planin sabit olmasi faydali olur.
- Yeni siniflar ekleyecekseniz `data/` altinda klasor acip `labels` listesini guncelleyin.

## Lisans
Bu depo icin lisans belirtilmedi.
