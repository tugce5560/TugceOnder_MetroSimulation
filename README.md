# Metro Simulation Projesi

## Proje Başlığı ve Kısa Açıklama

**Metro Simulation** projesi, bir şehirdeki metro hatları ve istasyonları arasında en hızlı ve en az aktarmalı yolları bulmaya yardımcı olan bir simülasyon sistemidir. Kullanıcılar, iki istasyon arasındaki rotaları en az aktarmayla ya da en hızlı şekilde bulabilirler. Bu proje, metro hatları arasında geçiş yaparken en verimli yolları keşfetmek için tasarlanmıştır.

---

## Kullanılan Teknolojiler ve Kütüphaneler

Bu projede kullanılan bazı Python kütüphaneleri şunlardır:

- **heapq**: 
  - A* algoritmasında, istasyonları **öncelikli sırayla** işlemek için kullanılır. Bu kütüphane, her öğeyi küçükten büyüğe sıralar ve A* algoritmasının doğru bir şekilde çalışmasına yardımcı olur.

- **collections**:
  - **deque**: BFS algoritmasında kullanılan **ilk giren ilk çıkar (FIFO)** kuyruk yapısını sağlar. Bu yapı, algoritmanın düzgün çalışabilmesi için gereklidir.
  - **defaultdict**: Anahtarlar için **varsayılan değerler** belirlemeye yarar ve metro istasyonları arasındaki bağlantıları düzenli tutmamıza yardımcı olur.

---

## Algoritmaların Çalışma Mantığı

### 1. BFS (Breadth-First Search) Algoritması

**BFS**, bir grafiği veya ağı keşfetmek için kullanılan basit ama etkili bir algoritmadır. BFS, her seferinde bir istasyonun **komşularını** keşfeder ve **en az aktarmalı yolu** bulmak için çalışır.

- **BFS'in Çalışma Mantığı**:
  - Başlangıç istasyonundan başlar ve her istasyonun komşularını sırayla keşfeder.
  - Her seferinde aktarma sayısını artırmadan, hedef istasyona ulaşmaya çalışır.

- **Neden BFS Kullanıyoruz?**
  - BFS, en kısa yolda **en az aktarma** yapılmasını garanti eder. Yani, hedefe en az aktarmayla ulaşmak için ideal bir yöntemdir.

### 2. A* (A-star) Algoritması

**A*** algoritması, daha hızlı bir şekilde **en kısa yolu** bulmak için kullanılan bir algoritmadır. Bu algoritma, her istasyonun **mesafesini** ve **hedefe olan tahmini uzaklığını** göz önünde bulundurarak daha hızlı bir çözüm bulur.

- **A* Algoritmasında Kullanılan Hesaplamalar**:
  - A* algoritmasında, her istasyonun **geçilen mesafesi** (g-cost) ve **hedef istasyona olan uzaklık tahmini** (h-cost) kullanılarak, toplam **en düşük maliyetli** yol bulunur.
  
- **Neden A* Kullanıyoruz?**
  - A*, özellikle çok sayıda istasyon ve bağlantı olduğunda **çok daha hızlı** yol bulur. Çünkü gereksiz yolları eleyip doğrudan hedefe yönelir.

---

## Örnek Kullanım ve Test Sonuçları

Aşağıdaki örnek, metro simülasyonunun nasıl çalıştığını gösteriyor. Bu örnekte, bazı istasyonlar ekleniyor, bağlantılar oluşturuluyor ve en az aktarmalı ve en hızlı yollar bulunuyor.

```python
# Örnek kullanım
metro = MetroAgi()

# İstasyonlar ekleyelim
metro.istasyon_ekle("K1", "Kızılay", "Kırmızı Hat")
metro.istasyon_ekle("K2", "Ulus", "Kırmızı Hat")
metro.istasyon_ekle("M1", "AŞTİ", "Mavi Hat")
metro.istasyon_ekle("T1", "Batıkent", "Turuncu Hat")

# Bağlantılar ekleyelim
metro.baglanti_ekle("K1", "K2", 4)
metro.baglanti_ekle("K2", "M1", 5)
metro.baglanti_ekle("T1", "K2", 6)

# En az aktarmalı rota
rota = metro.en_az_aktarma_bul("K1", "M1")
print("En az aktarmalı rota:", " -> ".join(i.ad for i in rota))

# En hızlı rota
rota, sure = metro.en_hizli_rota_bul("K1", "M1")
print(f"En hızlı rota ({sure} dakika):", " -> ".join(i.ad for i in rota))
