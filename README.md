# AI Content Automation Pipeline (n8n)

n8n kullanarak Notion, TikTok ve LinkedIn için otonom yapay zeka içerik üreticisi.

Bu proje, "İçerik Üretim ve Dağıtım Otomasyonu" vaka çalışmasının (case study) **Faz-1 (Minimum Uygulanabilir Ürün - MVP)** aşamasıdır. Sistem, yapay zeka kullanarak sosyal medya içeriklerini otomatik olarak üretir, veriyi işler ve Notion veritabanına yapılandırılmış veri blokları formatında kaydeder.

## 🚀 Proje Mimarisinin Kapsamı
Nihai hedef 5 aşamalı uçtan uca bir sistem (Araştırma, Üretim, Onay, Yayınlama, Analiz) olmakla birlikte, bu repoda projenin en temel ve teknik yükü barındıran **Veri İşleme ve API Entegrasyonu** kısmı modellenmiştir:

* **Tetikleyici:** Geliştirme ve test süreçleri için şimdilik manuel tetikleyici kurgulanmıştır.
* **AI Entegrasyonu:** Groq API üzerinden LLM'e (Large Language Model) HTTP POST isteği atılarak LinkedIn ve TikTok için hedef kitleye uygun içerik üretimi sağlanır.
* **Veri İşleme (JavaScript):** AI modelinden dönen ham string verisi, özel bir JavaScript kodu (Node) ile ayrıştırılarak (parse) JSON formatına çevrilir.
* **Notion Veritabanı Kaydı:** İşlenen veriler, Notion API üzerinden dinamik değişkenler (Expression) kullanılarak sayfaya aktarılır. Veriler düz metin yerine doğru hiyerarşideki blok nesneleri (`heading_2` ve `paragraph`) olarak işlenir.

## 🛠️ Kullanılan Teknolojiler
* **n8n:** İş akışı (workflow) yönetimi ve sistemler arası veri yönlendirme.
* **JavaScript:** Veri manipülasyonu ve JSON ayrıştırma.
* **Groq API / LLM:** Yüksek hızlı yapay zeka metin üretimi.
* **Notion API:** Veritabanı ve döküman içi yapılandırılmış blok (block objects) yönetimi.
* **REST API:** Servisler arası HTTP Request haberleşmesi.

## 🔮 Gelecek Vizyonu (Geliştirme Yol Haritası)
Çekirdek mimari modüler olarak tasarlandığı için sisteme aşağıdaki düğümler kolayca entegre edilebilir:
* **Perplexity API:** Sürecin en başına sektör trendlerini tarayacak bir araştırma modülü eklenmesi.
* **Slack Katmanı:** Üretilen içeriklerin yayınlanmadan önce insan onayından (Human-in-the-loop) geçmesi için tek tıkla onay mekanizması kurulması.
* **Buffer/Hootsuite API:** Onaylanan içeriklerin doğrudan platformlarda zamanlanması.
* **n8n Scheduler:** Sistemin her Pazartesi saat 09:00'da Cron Job ile otonom olarak başlatılması.

## ⚙️ Nasıl Çalıştırılır?
1. Bu repodaki `workflow.json` dosyasını bilgisayarınıza indirin.
2. Kendi n8n çalışma alanınızda sağ üstteki menüden `Import from File` seçeneği ile akışı içe aktarın.
3. Groq (HTTP Request) ve Notion (HTTP Request 1) düğümlerinin Header kısımlarına kendi `Bearer Token` (API) anahtarlarınızı girin.
4. Notion düğümündeki Body (JSON) kısmına içeriği yazdırmak istediğiniz kendi sayfanızın `page_id` bilgisini ekleyin.
5. `Execute Workflow` butonuna basarak otomasyonu test edin!