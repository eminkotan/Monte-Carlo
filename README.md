# Montecarlo
# Kodun Açıklaması: Monte Carlo ile DCF Simülasyonu

Bu kod, bir şirketin değerini **Monte Carlo simülasyonu** kullanarak **DCF (Discounted Cash Flow)** yöntemiyle tahmin etmektedir. Aşağıda adım adım detaylı açıklaması verilmiştir:  

---
## Nasıl Çalışır?

1. **Parametrelerin Belirlenmesi**  
   - Simülasyon sayısı (`n_sim`), başlangıç serbest nakit akımı (`cash_flow0`) ve projeksiyon süresi (`years`) tanımlanır.  
   - Rastgele sayı üreteci (`rng`) ile tekrarlanabilirlik sağlanır.

2. **Dağılımların Oluşturulması**  
   Simülasyonun belirsizlikleri üç temel dağılımla modellenir:  

   - **Nakit akış büyüme oranları (`growth_rates`)**  
     - Normal dağılım: Ortalama **%5**, standart sapma **%2**.  
     - Her yıl için ayrı değer çekilir.  
     - Böylece her senaryoda, yıllar boyunca farklı büyüme patikaları oluşur.  

   - **İskonto oranı (`discount_rates`, WACC)**  
     - Normal dağılım: Ortalama **%10**, standart sapma **%1**.  
     - Her senaryo için tek değer çekilir, senaryodan senaryoya değişir.  
     - Şirketin sermaye maliyetindeki belirsizliği yansıtır.  

   - **Terminal büyüme oranı (`terminal_growth`)**  
     - Normal dağılım: Ortalama **%3**, standart sapma **%0.5**.  
     - Terminal dönemde şirketin uzun vadeli büyüme beklentisini temsil eder.  
     - Her senaryo için tek değer çekilir.  

3. **DCF Hesaplaması (Her Senaryo için)**  
   - Her yıl serbest nakit akımı (FCF) bileşik şekilde büyütülür.  
   - Nakit akışları iskonto edilerek bugünkü değeri (PV) hesaplanır.  
   - Terminal değer, yalnızca \( WACC > terminal büyüme oranı\) koşulu sağlanıyorsa eklenir.  

4. **Sonuçların Düzenlenmesi**  
   - Tüm senaryolardan elde edilen DCF değerleri bir listeye eklenir.  
   - Daha sonra uç değerler kırpılır (1. ve 99. persentil dışındakiler çıkarılır).  

5. **İstatistiklerin Hesaplanması**  
   - %5, %50 (medyan), %95 persentil değerleri bulunur.  
   - Ortalama değer (`mean_val`) hesaplanır.  

6. **Histogram ile Görselleştirme**  
   - Elde edilen değer dağılımı histogram olarak çizilir.  
   - İlgili istatistikler dikey çizgiler ile işaretlenir.  
   - Grafik kaydedilir: `dcf_monte_carlo_histogram_clean.png`.  
