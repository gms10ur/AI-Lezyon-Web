
## Skin-Lesion-Analyzer

Live Web App: http://myrista.tplinkdns.com

<br>

<img src="http://myrista.tplinkdns.com/assets/app_pic.png" width="350"></img>

<br>

Bu, doktorlara ve laboratuvar teknisyenlerine belirli bir cilt lezyonu için en yüksek olasılıklı üç tanıyı söyleyebilen, ücretsiz olarak erişilebilen bir çevrimiçi aracın prototipidir. Yüksek riskli hastaları hızla belirlemelerine ve iş akışlarını hızlandırmalarına yardımcı olabilir. Uygulama, 3 saniyeden daha kısa sürede bir sonuç üretecektir. Gizliliği sağlamak için, kullanıcı tarafından gönderilen görüntüler önceden işlenir ve yerel olarak analiz edilir ve asla harici bir sunucuya yüklenmez.

Bu uygulama, Yapay Zeka tarafından desteklenmektedir. Bu projedeki amacım, model oluşturmayla başlayıp canlı bir web uygulamasıyla biten uçtan uca bir çözüm oluşturmaktı. Kullanıcılar bir cilt lezyonunun resmini gönderebilir ve anında bir tahmin alabilir.

Uygulama, bu yazıda açıklandığı gibi 7 tip cilt lezyonunu sınıflandırabilir:

HAM10000 Veri Kümesi: Yaygın Pigmentli Deri Lezyonlarının Çok Kaynaklı Dermatoskopik Görüntülerinin Geniş Bir Koleksiyonu<br>
https://arxiv.org/abs/1803.10417


Tüm model oluşturma ve eğitim süreci bu Kaggle çekirdeğinde açıklanmıştır:<br>
https://www.kaggle.com/vbookshelf/skin-lesion-analyzer-tensorflow-js-web-app

Modeli oluşturmak ve eğitmek için kullanılan python kodu, Jupyter not defterine dahil edilmiştir. Tüm javascript, css ve html dosyaları da burada ücretsiz olarak mevcuttur. Eğitilmiş model de mevcuttur.


<hr>


<b>Bu Proje Nasıl Çalıştırılır</b>

Bu projeyi çalıştırmak için bir web adresi oluşturmanız ve ardından bir web sitesi oluştururken yaptığınız gibi dosyaları ona yüklemeniz gerekecektir.

Bu adımlar:

1. Bir web sunucusu kurun.

2. Web sunucunuza aşşağıda listelenen dosyaları ve klasörleri yükleyin.

- index.html<br>
- faq.html<br>
- assets (klasör)<br>
- jscript (klasör)<br>
- final_model_kaggle_version1 (klasör)<br>
- favicon.png<br>

2. app_startup_code.js dosyasında, kodun parçası olan web adresleri vardır. Modeli yüklemek için bu adresleri, kullandığınız alan adresiyle eşleşecek şekilde değiştirmeniz gerekecektir.

```
model = await tf.loadModel('http://myrista.tplinkdns.com/model_kaggle_version12/model.json');
$("#selected-image").attr("src", "http://myrista.tplinkdns.com/assets/ISIC_0024334.jpg")
```

3. Dosyaları ve klasörleri yüklemeyi bitirdikten sonra web sitenizin adresini tarayıcınıza yazın ve sitenize gidin. Tıpkı benimki gibi görünmeli ve çalışmalı. Dürüst olmalıyım, ilk kez bir web sitesi kurduğunuzda bazen sinir bozucu bir süreç olabilir. Ancak sabırlı olun çünkü sonunda her zaman işe yarar - biraz saç çektikten ve birkaç gözyaşından sonra.


Lütfen, web sitenize https sitesi yapmak için bir güvenlik sertifikası eklerseniz, bu güvenlik özelliğinin, bir kullanıcı web sitenizi ziyaret ettiğinde modelin otomatik olarak indirilmesini engelleyebileceğini unutmayın.


<hr>

<b>Hatalar ve Alınan Dersler</b>

1. Model web sitenize yüklenmiyorsa:<br>
Modeli FileZilla kullanarak yüklediyseniz varsayılan aktarım ayarının değiştirilmesi gerekebilir.<br>
Ayarlar->Aktarımlar->File_Types'a gidin ve varsayılan aktarım türünü İkili olarak ayarlayın.<br>
Ardından modeli tekrar sunucuya yükleyin.

2. Web sitenizde sorun giderirken tarayıcınızın "Gizli" modda olduğundan emin olun. Aksi takdirde, önbellekte depolanan modeli (ve siteyi) yükler ve modelin en son sürümüne bakmazsınız.

3. Modeli Keras'ta oluşturun ve kaydetmeden Tensorflow.js'ye dönüştürün. Kaydederseniz, kaydedilmiş bir modeli yükleyin ve dönüştürün - model sitenize yüklendiğinde çalışmayabilir.

4. Dönüştürülmüş bir tf.keras modeli, uygulamaya yüklendiğinde çalışmıyor. Yerel bir Keras modeli kullanılmalıdır. 'Çalışmıyor' dediğimde, model ya uygulamaya yüklenmeyecek ya da yüklenirse bir tahmin çıkmayacak demek istiyorum.

5. Başka bir komplikasyon - tf.keras kullanmazsanız, karışıklık matrisinden hesaplanan doğruluk, eğitim ve değerlendirme sırasında elde edilen doğrulukla eşleşmeyecektir. Yerel Keras'ta tahmin_generator() ile ilgili bir sorun olduğunu düşünüyorum - ya da belki yanlış kullanıyorum.

6. Uygulama, OSX Safari'de çalışmıyor. Chrome'un en son sürümünü kullanmak en iyisidir. Tensorflowjs tabanlı uygulamalar geliştirirken tarayıcı desteğinin akılda tutulması gerekir.

7. Bazı görüntü veri kümeleri, TIF formatında görüntüler içerir. Web tarayıcıları TIF biçimini desteklemez. Bu nedenle, kullanıcıların görüntüleri jpg veya png formatında göndermeleri gerekecektir. Bu nedenle, modeli eğitirken eğitim görüntülerini eğitim için kullanmadan önce jpg veya png'ye dönüştürmek önemlidir. Bunu yapmazsanız, uygulamadan gelen tahminlerin modelden gelen tahminlerle eşleşmeyeceğini göreceksiniz - uygulama tahminleri kötü olacaktır.

8. Görüntüler bilgisayar ve cep telefonu aracılığıyla gönderildiğinde, tahmin edilen olasılıklarda küçük farklılıklar vardır. Bu, mobil tarayıcının görüntüyü tahmin için modele gönderilmeden önce bir şekilde değiştiriyor olabileceğini gösteriyor gibi görünüyor.

9. Tensorflow.js sürüm 1.0.0 ve sonrasında onProgress kullanarak bir ilerleme çubuğu eklemek mümkündür. İlerleme çubuğu, model indirme sırasında kullanıcıya güzel bir görsel ipucu verir. Ayrıca, bir kullanıcı daha sonra uygulamaya döndüğünde, tam bir ilerleme çubuğu kullanıcıya önbelleğe alınmış bir modelin anında kullanılabilir olduğunu söyler, böylece indirmeyi beklemesine gerek kalmaz. Dezavantajı ise, bir ilerleme çubuğu eklendiğinde, internet bağlantısı yavaşsa model indirme işleminin güvenilmez hale gelmesidir. Aslında model indirme düzenli olarak başarısız olur. İlerleme çubuğu işlevini kötü bir şekilde uygulamış olabilirim. İlerleme çubuğu olmadığında, bağlantı yavaş olduğunda bile modelin yavaş ama başarılı bir şekilde indirildiğini buldum.
