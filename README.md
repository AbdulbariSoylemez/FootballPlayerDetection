# Footbolo Player Detection

Bu proje, futbol maçlarında oyuncuları tespit etmek için YOLOv8 modelinin kullanılmasını içerir. Proje kapsamında Liverpool ve Rangers arasındaki bir maçın veri seti kullanılarak model eğitilmiş ve test edilmiştir.

## Veri Seti

Veri seti, Liverpool ve Rangers maçından alınan görüntülerden oluşmaktadır. Görüntüler, oyuncuları içeren farklı sahneleri temsil etmektedir. Veri seti, labelImg ortamında etiketlenmiş ve görselleştirilmiştir.

## Kurulum

1. **Google Drive'e Bağlanma:** Google Drive'daki veri setine erişmek için aşağıdaki kodu çalıştırın:

    ```python
    from google.colab import drive
    drive.mount("/content/drive")
    ```

2. **Veri Setini Zipten Çıkartma:**
   Veri setini Google Drive'dan çıkartmak için aşağıdaki adımları izleyin:

   ```bash
   !cd /content
   !unzip -q /content/drive/MyDrive/FootboloPlayerDetections/footbol.zip
   ```

### Model Eğitimi:

YOLOv8 modelini eğitmek için aşağıdaki kodları çalıştırın:

```bash
!yolo task=detect mode=train model=yolov8x.pt data=/content/footbol/data.yaml epochs=50 imgsz=640 batch=16 optimizer=Adamax lr0=0.001618 device=0
```

### Model Testleri

- **Örnek Resim Üzerinde Test:** Modeli örnek bir resim üzerinde test etmek için aşağıdaki kodu çalıştırın:

  ```bash
  !yolo task=detect mode=predict model=/content/ultralytics/runs/detect/train/weights/best.pt conf=0.40 source=/content/drive/MyDrive/FootboloPlayerDetections/Ekran2.png
  ```

- **Video Üzerinde Test:** Modeli bir video üzerinde test etmek için aşağıdaki kodu çalıştırın:

  ```bash
  !yolo task=detect mode=predict model=/content/ultralytics/runs/detect/train/weights/last.pt conf=0.40 source=/content/drive/MyDrive/FootboloPlayerDetections/Liv-Ran-Match.mov
  ```

