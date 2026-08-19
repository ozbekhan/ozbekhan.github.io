---
title: "DORA Metrikleri ile Pipeline Sağlığının Ölçülmesi: DevOps Süreçlerinde Hız ve Güvenliği Dengelemek"
date: 2026-06-09
categories: 
  - "devops"
  - "proje-yonetimi"
coverImage: "Modern_Software_Delivery_-_Slide_11.png"
---

Günümüz yazılım dünyasında, ürünleri kullanıcıya hızlı bir şekilde ulaştırmak tek başına yeterli değildir; bu hızın sürdürülebilir, kaliteli ve güvenli olması da kritik bir öneme sahiptir. Yazılım geliştirme ve dağıtım süreçlerinin kalbi olarak nitelendirilen CI/CD (Sürekli Entegrasyon / Sürekli Dağıtım) ardışık düzenlerinin (pipeline) ne kadar verimli çalıştığını ölçmek, mühendislik ekiplerinin en büyük zorluklarından biridir.

İşte bu noktada, DevOps Araştırma ve Değerlendirme (DevOps Research and Assessment) grubu tarafından geliştirilen ve sektör standardı haline gelen **DORA Metrikleri** devreye girer. Bu makalede, DORA metriklerinin ne olduğunu, pipeline sağlığını ölçmede nasıl kullanılacağını ve yüksek performanslı mühendislik kültürüne nasıl katkı sağladığını ele alacağız.

### DORA Metrikleri Nedir?

DORA, yıllar süren araştırmalar sonucunda yazılım teslimat performansını belirleyen dört temel metrik ortaya koymuştur. Bu dört metrik, temelde iki ana denge üzerine kuruludur: **Hız (Hız ve Akış)** ve **Kararlılık (Kalite ve Güvenilirlik)**.

#### 1\. Dağıtım Sıklığı (Deployment Frequency - DF)

- **Nedir?** Ekiplerin başarılı bir şekilde canlı ortama (production) ne kadar sıklıkla kod gönderdiğini ölçer.

- **Pipeline Sağlığı İçin Önemi:** Kodların küçük parçalar halinde, sürekli olarak canlıya alınması pipeline'ın tıkalı olmadığını gösterir. Yüksek dağıtım sıklığı, CI/CD süreçlerinin otomatize edildiğinin ve süreçteki sürtünmelerin minimumda olduğunun bir kanıtıdır.

#### 2\. Değişiklik Teslim Süresi (Lead Time for Changes - LTC)

- **Nedir?** Bir kod taahhüdünün (commit) yazıldığı andan itibaren canlı ortamda başarıyla çalışmaya başlamasına kadar geçen süredir.

- **Pipeline Sağlığı İçin Önemi:** Bu süre; kod inceleme (code review), otomatik testler, derleme (build) ve dağıtım aşamalarını kapsar. Eğer teslim süresi çok uzunsa, testlerin yavaş olmasından, manuel onay süreçlerinden veya pipeline'daki performans darboğazlarından şüphelenilmelidir.

#### 3\. Hizmeti Geri Döndürme Süresi (Time to Restore Service - TRRS / MTTR)

- **Nedir?** Canlı ortamda meydana gelen bir hizmet kesintisi veya hatanın (örneğin bir çökme veya performans düşüşü) giderilip sistemin normal haline dönmesi için geçen süredir.

- **Pipeline Sağlığı İçin Önemi:** Pipeline yalnızca kod dağıtmakla kalmamalı, kriz anında hızlı aksiyon alabilmelidir. Hızlı bir geri alma (rollback) mekanizması veya otomatik yamalama süreçleri, pipeline'ın esnekliğini ve sağlığını gösterir.

#### 4\. Değişiklik Başarısızlık Oranı (Change Failure Rate - CFR)

- **Nedir?** Canlı ortama yapılan dağıtımların yüzde kaçının bir hataya yol açtığını ve sonrasında müdahale (hotfix, rollback vb.) gerektirdiğini ölçer.

- **Pipeline Sağlığı İçin Önemi:** Sadece hızlı olmak yetmez. Eğer dağıtımlarınız sürekli hata veriyorsa, pipeline içerisindeki otomatik test kalitesi (unit, entegrasyon vb.) veya kod kalitesi kontrol mekanizmaları yetersiz demektir.

### DORA Metrikleri ile Pipeline Sağlığı Nasıl Analiz Edilir?

Pipeline sağlığını tek bir göstergeye bakarak anlamak imkansızdır. DORA metrikleri, bir madalyonun iki yüzü gibi birbirini dengeleyerek bütünsel bir bakış açısı sunar.

- **Hız ve Kararlılık Dengesi:** Eğer Dağıtım Sıklığınız çok yüksek fakat Değişiklik Başarısızlık Oranınız da yüksekse, pipeline'ınız hızlı ama güvensiz çalışıyor demektir. Ekipler muhtemelen testleri atlıyor veya yeterince kontrol yapmıyor olabilir. Tersine, Değişiklik Başarısızlık Oranınız sıfıra yakın ancak Değişiklik Teslim Süreniz haftalar sürüyorsa, aşırı bürokratik, hantal ve manuel onaylara bağımlı bir pipeline sağlığı söz konusudur. Sağlıklı bir pipeline'da hedef, **hızı artırırken başarısızlık oranını düşük tutabilmektir**.

- **Geri Bildirim Döngülerinin Kısaltılması:** Pipeline sağlığının en büyük göstergelerinden biri de "geliştirici deneyimi" (Developer Experience - DevEx) ve geri bildirim süresidir. Kısa bir Değişiklik Teslim Süresi (LTC), geliştiricinin yazdığı kodun kalitesini çok hızlı görmesini sağlar. Pipeline üzerinde yapılan optimizasyonlar (örneğin testlerin paralelleştirilmesi veya akıllı önbellekleme), doğrudan bu metriği iyileştirir.

### Veriye Dayalı İyileştirme Süreci

DORA metriklerini kullanarak pipeline sağlığını iyileştirmek için şu adımlar izlenebilir:

1. **Görünürlük Sağlayın:** İlk adım, bu verileri otomatik olarak toplamaktır. GitHub Actions, GitLab CI/CD, Jenkins gibi araçların loglarından ve Jira gibi proje yönetim araçlarından beslenen gösterge panelleri (dashboard) oluşturulmalıdır.

3. **Darboğazları (Bottleneck) Tespit Edin:** Teslim süresinin en çok hangi aşamada (örn. manuel QA testleri veya uzun süren derleme aşamaları) takıldığını analiz edin.

5. **Otomasyonu Artırın ve Güvenliği Sola Çekin (Shift-Left):** Güvenlik taramalarını (SAST/DAST) ve test senaryolarını pipeline'ın olabildiğince erken aşamalarına yerleştirin. Böylece hatalar canlıya yaklaşmadan yakalanır ve Değişiklik Başarısızlık Oranı düşer.

### Sonuç

Pipeline sağlığı, soyut hislerle değil, somut verilerle ölçülmelidir. DORA metrikleri, mühendislik organizasyonlarına süreçlerindeki kör noktaları görme fırsatı sunar. Pipeline verimliliğini bu dört metriğe dayandırarak sürekli optimize eden şirketler, sadece daha hızlı kod üretmekle kalmaz; aynı zamanda daha mutlu geliştiricilere, daha kararlı sistemlere ve dolayısıyla daha memnun son kullanıcılara sahip olurlar. Modern DevOps dünyasında yüksek performanslı bir ekip olmanın anahtarı, pipeline sağlığını DORA pusulasıyla takip etmekten geçer.
