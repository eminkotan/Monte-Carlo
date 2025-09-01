# Montecarlo
# Kodun Açıklaması: Monte Carlo ile DCF Simülasyonu

Bu kod, bir şirketin değerini **Monte Carlo simülasyonu** kullanarak **DCF (Discounted Cash Flow)** yöntemiyle tahmin etmektedir. Aşağıda adım adım detaylı açıklaması verilmiştir:  

---

## 1. Parametreler
- **`n_sim`**: Simülasyon tekrar sayısını belirtir.  
- **`cash_flow0`**: Başlangıçtaki nakit akışı değeridir.  
- **`years`**: Projeksiyon süresini ifade eder (ör. 5–10 yıl).  

---

## 2. Rastgele Sayı Üretici
- **`numpy`** kütüphanesinin `default_rng` fonksiyonu kullanılarak rastgele sayı üreteci oluşturulur.  
- Bu üreteç, simülasyon sırasında kullanılacak olan rastgele değerlerin güvenilir şekilde üretilmesini sağlar.  

---

## 3. Dağılımlar
Simülasyon için gerekli belirsizlikler normal dağılımlardan alınır:  
- **Nakit akış büyüme oranları (growth rates)**  
- **İskonto oranları (WACC)**  
- **Terminal büyüme oranları**  

Bu dağılımlar sayesinde her simülasyon farklı değerlerle çalışır ve olasılık tabanlı bir analiz yapılır.  

---

## 4. DCF Hesaplaması
Her simülasyonda:  
1. Projeksiyon yılları için nakit akışları hesaplanır.  
2. Her yılın nakit akışı bugünkü değere (PV) iskonto edilir.  
3. **Terminal Değer (TV)**:  
   - Eğer iskonto oranı (WACC), terminal büyüme oranından büyükse hesaplanır.  
   - Formül:  
     \[
     TV = \frac{CF_{t+1}}{WACC - g}
     \]  

Toplam şirket değeri, **tüm iskonto edilmiş nakit akışlarının toplamı + terminal değer** olarak bulunur.  

---

## 5. Uç Değerlerin Kırpılması
- Hesaplanan DCF sonuçları arasında aşırı uçta kalan değerler (örneğin 1. ve 99. persentil dışındaki değerler) çıkarılır.  
- Bu sayede **uç değerlerin etkisi azaltılarak** daha anlamlı ve güvenilir bir değerleme analizi elde edilir.  
