# 60W GaN-Based Synchronous Buck Converter for Avionics Systems

![Altium 3D Render]([BURAYA ALTIUM 3D RENDER GÖRSELİNİN LİNKİNİ EKLE])

## 📌 Proje Özeti (Project Overview)
[cite_start]Bu proje, aviyonik sistemlerin görev bilgisayarları ve telemetri modülleri gibi kritik yükleri için tasarlanmış yüksek frekanslı, GaN (Galyum Nitrür) tabanlı bir senkron düşürücü (Buck) dönüştürücü donanımıdır[cite: 233, 234, 886]. [cite_start]Geleneksel Si-MOSFET tasarımlarının aksine, EPC2218 GaN FET'ler ve LTC7891 kontrolcüsü kullanılarak anahtarlama kayıpları minimize edilmiş ve fansız soğutma hedeflenmiştir[cite: 235, 238, 242, 595].

### ⚙️ Temel Sistem İsterleri (System Specifications)
* [cite_start]**Giriş Gerilimi (Vin):** 18V - 36V DC (Aviyonik Batarya Standardı) [cite: 187, 502, 576]
* [cite_start]**Çıkış Gerilimi (Vout):** 12V DC (Sabit) [cite: 187, 502]
* [cite_start]**Maksimum Çıkış Akımı (Iout):** 5A [cite: 502]
* [cite_start]**Maksimum Güç:** 60W [cite: 886, 890]
* [cite_start]**Anahtarlama Frekansı (Fsw):** 500 kHz [cite: 188, 506]
* [cite_start]**Tepe Verimlilik (Peak Efficiency):** %95.8 (Tam Yükte) [cite: 707, 890]
* [cite_start]**Kontrol Topolojisi:** Peak Current Mode Control (LTC7891) [cite: 189, 242]

---

## 🔬 Kritik Donanım Tasarım Çözümleri (Hardware Highlights)

### 1. Sinyal Bütünlüğü ve EMI Yönetimi (4-Layer Stack-Up)
[cite_start]GaN FET'lerin yüksek $dv/dt$ anahtarlama hızlarından (100V/ns) kaynaklı EMI yayılımını baskılamak için IPC standartlarında 4 katmanlı (4-Layer) PCB mimarisi kullanılmıştır[cite: 719, 720, 721]. 
* [cite_start]**Layer 2 (GND Plane):** Layer 1'deki yüksek $di/dt$ döngülerinin hemen altına kesintisiz bir Toprak düzlemi yerleştirilerek dönüş akımlarına (Return Path) en kısa yol sağlanmış ve elektromanyetik yayılım engellenmiştir[cite: 726, 727, 899].
* [cite_start]**Via Shielding:** Analog sinyal hatlarının etrafı GND dikişleriyle (Via Stitching) kapatılarak Faraday Kafesi etkisi yaratılmıştır[cite: 803].

### 2. Hassas Akım Okuma (Kelvin Sensing)
[cite_start]Sistemin kararlılığı için kritik olan $R_{SENSE}$ akım geri beslemesi, direnç pedlerinin iç kısmından alınan "Diferansiyel Kelvin Bağlantısı" ile sağlanmıştır[cite: 796, 797]. [cite_start]Sense yollarının Layer 3'teki güç düzleminden etkilenmemesi için "Polygon Cutout" yöntemi uygulanarak gürültü izolasyonu maksimize edilmiştir[cite: 799, 800].

### 3. Çok Katmanlı Aviyonik Koruma (Protection Stage)
* [cite_start]**Ters Polarite Koruması:** İletim kayıplarını sıfıra indirmek için geleneksel diyot yerine düşük $R_{DS(on)}$ değerli P-Kanal MOSFET (Vishay SQJ459EP) kullanılmıştır[cite: 651, 653, 656].
* [cite_start]**Geçici Gerilim (Surge) Koruması:** Giriş hattındaki ani voltaj sıçramalarını sönümlemek için 40V Stand-off gerilimine sahip SMAJ40A-HT TVS diyot kullanılmıştır[cite: 657, 658, 659].

---

## 📊 Simülasyon ve Doğrulama (LTSpice Results)

[cite_start]Sistem fiziksel üretim öncesi LTSpice ortamında dinamik stres testlerine tabi tutulmuştur[cite: 676]:

1. [cite_start]**Start-Up Tepkisi:** 100nF Soft-Start kapasitörü sayesinde sistem herhangi bir aşım (overshoot) yapmadan 7 ms içerisinde 12V kararlı duruma ulaşır[cite: 680, 681].
   *(Bkz: /Measurements/Startup_Graph.png)* ![Start-Up]([BURAYA START-UP GRAFİĞİNİ EKLE])

2. **Yük Değişim Tepkisi (Load Transient):** 0.5A'den 5A'e (%10 -> %100) ani yük çıkışlarında voltaj dalgalanması %2.2 (254mV) ile sınırlı kalmış ve kontrolcü 150 µs içerisinde regülasyonu yeniden sağlamıştır[cite: 694, 695, 696, 894, 895].
   *(Bkz: /Measurements/Transient_Graph.png)* ![Transient]([BURAYA TRANSIENT GRAFİĞİNİ EKLE])

3. [cite_start]**Çıkış Dalgacığı (Voltage Ripple):** 500 kHz anahtarlama ve düşük ESR'li seramik hibrit kapasitör dizilimi ile tam yükte (5A) çıkış ripple değeri **<10mV** seviyesine indirilmiştir[cite: 700, 701].

---

## 📁 Depo İçeriği (Repository Structure)

* `\Hardware_Source`: Altium Designer proje dosyaları (.PrjPcb, .SchDoc, .PcbDoc).
* `\Simulation`: LTSpice doğrulama dosyaları ve analiz grafikleri.
* `\Manufacturing`: Üretime hazır Gerber, NC Drill dosyaları ve Endüstriyel BOM listesi.
* `\Docs`: GaN FET ve LTC7891 detaylı veri sayfaları.
