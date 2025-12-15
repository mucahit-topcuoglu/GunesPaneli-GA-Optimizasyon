# ☀️ Güneş Paneli Optimizasyonu: Genetik Algoritma (GA)

Bu proje, bir belediyenin kurmayı planladığı güneş enerjisi sistemi için **maksimum enerji verimi** sağlayacak şekilde panel parametrelerini Genetik Algoritma (GA) kullanarak optimize etmektedir.

## 1. 📝 Problem Tanımı ve Matematiksel Model

Amaç, güneş paneli eğim açısı ($x_1$) ve güney yönüne göre sapma açısı ($x_2$) değişkenlerini kullanarak toplam enerji verimini ($y$) maksimize etmektir.

### Amaç Fonksiyonu (Maksimizasyon)
Maksimum enerji verimini hesaplamak için kullanılan fonksiyon:
$$y = 6x_1 + 4x_2 - 0.1(x_1)^2$$

* $x_1$: Panel eğim açısı (derece)
* $x_2$: Güney yönüne göre sapma açısı (derece)

### Kısıtlamalar

Değişkenler, hem fiziksel aralıklar hem de problem özgü kısıtlamalar ile sınırlandırılmıştır:

| Kısıt Tipi | Değişken | Aralık / Kural |
| :--- | :--- | :--- |
| **Fiziksel Aralık** | $x_1$ (Eğim Açısı) | $10 \leq x_1 \leq 45$ |
| **Fiziksel Aralık** | $x_2$ (Sapma Açısı) | $0 \leq x_2 \leq 90$ |
| **Problem Kısıtı** | $x_1, x_2$ | $x_1 + 0.5x_2 \leq 60$ |
| **Problem Kısıtı** | $x_2$ | $x_2 \geq 15$ |

## 2. ⚙️ Genetik Algoritma (GA) Yapısı

Bu optimizasyon problemini çözmek için kullanılan Genetik Algoritma'nın temel parametreleri ve mekanizmaları aşağıda listelenmiştir.

### GA Parametreleri

| Parametre | Değer | Açıklama |
| :--- | :--- | :--- |
| Popülasyon Büyüklüğü (`populasyon_buyuk`) | 50 | Her nesildeki birey sayısı. |
| Nesil Sayısı (`nesil_sayisi`) | 150 | Algoritmanın çalışacağı toplam döngü sayısı. |
| Mutasyon Oranı (`mut_orani`) | 0.1 ( %10 ) | Mutasyonun gerçekleşme olasılığı. |
| Mutasyon Büyüklüğü (`mutasyon_buyuk`) | 5.0 | Mutasyon uygulandığında gene eklenecek maksimum rastgele değişim (derece). |

### GA Operatörleri ve Stratejileri

* **Başlangıç Popülasyonu:** Popülasyon, başlangıçta rastgele oluşturulur ve yalnızca tanımlanan tüm **kısıtları sağlayan** bireylerden oluşur.
* **Seçilim (Selection):** Bir sonraki nesli oluşturacak ebeveynleri seçmek için **Sıralama Tabanlı Seçim (Rank Selection)** yöntemi kullanılmıştır.
* **Çaprazlama (Crossover):** **Tek Noktalı Çaprazlama** yöntemi uygulanmıştır. Çocuklar, bir ebeveynin $x_1$ genini ve diğer ebeveynin $x_2$ genini birleştirerek oluşturulur.
* **Mutasyon (Mutation):** Mutasyon, genetik çeşitliliği korumak amacıyla `mut_orani` olasılıkla uygulanır. Mutasyon sonrasında, genlerin **fiziksel aralıklar** içinde kalması için sınır kontrolü yapılır.
* **Kısıt Yönetimi (Ceza Fonksiyonu):** GA döngüsü sırasında **problem kısıtlarını** sağlamayan bireylere (`kısıt_kontrol` fonksiyonu ile denetlenir) çok düşük bir fitness değeri (`1e-6`) atanarak yeni nesil seçiminde elenmeleri sağlanır (dış ceza yöntemi).
* **Elitizm:** Her nesildeki en yüksek fitness değerine sahip birey, doğrudan bir sonraki nesle aktarılır (korunur).

## 3. 🚀 Çalıştırma ve Kurulum

Bu proje tek bir Jupyter Notebook dosyası (`Untitled6.ipynb`) içerir ve Python ortamında çalıştırılmalıdır.

### Gerekli Kütüphaneler

Projeyi çalıştırmak için aşağıdaki temel kütüphanelerin yüklü olması gerekmektedir:

```bash
pip install numpy matplotlib
