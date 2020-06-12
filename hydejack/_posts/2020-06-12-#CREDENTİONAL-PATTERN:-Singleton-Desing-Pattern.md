---
title: # CREDENTİONAL PATTERN: Singleton Desing Pattern
image: /assets/img/blog/singletonDesingPattern.png

description: >

---

## SİNGLETON DESİNG PATTERN ?

_> **Singleton Desing Pattern bir nesne örneğinden sadece bir defa üretilip , bu nesne örneğinin her zaman kullanılmasını söyleyen bir patterndir.**_

-   Pattern bir önceki [**yazımda**](https://medium.com/@sumeyyekilic/desi%CC%87ng-pattern-e85c89fd5075?source=---------2------------------) açıkladığım gibi bir sorun, ve bu sorunun da çözümü demekti.

-   Singleton Pattern, Desing Pattern’ların 3 kategoriden ilki olan Credentional Pattern ‘ın çözümlerinden en çok kullanılan pattern’idir.

-   Singleton “tekil” demektir. Yani ilgili nesneden bir tane olsun istiyorsak singleton kullanabiliriz.

👩🚀 Desing patternler ile uzayı keşfe gerek yok..

📌 **Peki biz geliştiricilerin gezegenlerinde ki uygulamalarında nerelerde ve nasıl kullanırız ?**

-   **En büyük amaç : “**bir nesnenin örneğinin ve o örnek değerinin bir çok kullanıcı tarafından değiştiği zaman bile aynı şekilde kullanılmasını**”** amaçlar.

> _Örneğin sizin bir uygulamanız var. bu uygulamanızı günlük kaç kişinin kullandığı ziyaretçi saysını tutmak istiyoruz. anlık ziyaret sayısı tüm kullanıcı için aynıdır. Herkes yanı değeri okur ve sisteme giren olunca bu değer bir artar._

-   **En büyük 2.amaç : “**Bir nesnenin durumunun kontrol edilmesi**”** amaçlanır.

Mesela benim gezegenim de bir nesne örneğim var. Katmanlar arasında geçerken **bu nesne sadece işlem yapıyorsa**, yani **bir değeri tutmak gibi görevi yoksa** o zaman yine Singleton Pattern’ dan yararlanmakta fayda vardır.

> _Örneğin ; iş katmanındaki yönetici nesneyi düşünün : ekleme, silme, güncelleme, arama yapar ve bunları bir metot şeklinde yapar. diyelim ki 5 bin tane kullanıcınız var. Bu 5 bin kullanıcı iş katmanına her istekte bulunduğunda yeniden new’lenir.. ** buda bize daha pahalı bir işlem sunar.**_

Madem biz işlem yapacak nesne üretiyoruz. Herkesin bunu kullanmasını istiyoruz. öyleyse bizim **bu nesneyi bir defa üretip herkesin kullanımına açmamız** gerekir.

#### 📌 Peki Singelton Desing Pattern ne zaman **kullanmamalıyız** **?**

-   Singelton Desing Pattern ile bir nesne ürettiğinizde bu bellekte her zaman sabir kalır. Diyelim ki mvc uygulamasında bir signelton manager nesnesi ürettiğinizde, IIS’i restart etmeyene kadar bu nesne ortadan kalkmaz.

⭐Burada dikkat etmemiz gereken şey ; bir nesneyi singleton olarak ürettiğimiz zaman herkes bunu kullanmak durumunda mı ? Yada aynı şeyi kullanacak mı ?

-   Bir nesneyi ürettik ve diyelim ki o nesneyi kullanıcı uygulama boyunca sadece bir yerde bir kere istiyor. Belki de günlerce kimse o nesneye kimse istekte bulunmuyor. **Burada olduğu gibi “nadir kullanılan bir ürün singleton olarak üretilmemelidir.”** Nesnenin ömrü işlem bitince bitmelidir. Eğer ihtiyaç olursa yeniden üretilebilir. Çünkü diğer türlü bellekte hep yer kaplayacaktır.

Bir nesneden sadece bir tane oluşturmak istiyoruz. Bunun için gelin kafa yoralım.. 🤯

Elimde bir class var bundan sadece bir tane oluşturmak istediğimi düşünün.

-   Singaleton adında bir class oluşturdum:

<script src=”https://gist.github.com/sumeyyekilic/ebf063197acb2c3c9382796f219dcfeb.js"></script>

-   Yukarıda ki kodu incelerseniz ilk olarak Singleton.cs adında bir class oluşturup, içeride bunu private yaptım. Bunu yapmamda ki amaç başka bir class’ta new’lenmesinin önüne geçmek .

-   Daha sonra CreateSingleton isminde oluşturduğum controller’e Singleton tipinde bir metot yazarak, sürekli aynı nesneyi döndürmeyi sağlıyorum.

-   _singleton adında yöneteceğim bir nesne oluşturdum. Oluşturduğum nesne ile bağlayarak null değerini denetleyerek customer nesnesinden daha önce oluşturulup olşturmadığına göre sonuç döndürüyor.

-   Birde Delete adında bir metot oluşturup bu metodu main class ‘ından çağırdım. bu çağırma işini yaparken de new’lenmeden singleton metodunu ürettim.

Oluşturduğum kodun uml sınıf diyagramı ise şu şekildedir:

![singletonDesingPattern](/assets/img/blog/singletonDesingPattern2.png)

Burada olayın işleyiş ve mantığını anlamamız önemlidir. Çünkü önemli olan singleton kullanıp, kullanmayacağınızı bilip doğru karar vermemizdir. Tabi buda tecrübe gerektirir.

Sizinde bildiğiniz gibi artık bir şeyi yapmak kolay. Önemli olan neyi, nerede kullanacağını kestirip ,doğru zamanda nerede ne yapacağını bilmek gereklidir.. Singleton desing’ı bu şekildedir.

❤ Yazımı buraya kadar okuduğunuz için teşekkürler ❤ 
Bir sonraki yazımda desing patternın kategorilerinden Creational Patterns 'ın diğer alt pattern'ları için bu serinin devamı olacaktır.

_Bu yazım, [https://medium.com/@sumeyyekilic/](https://medium.com/@sumeyyekilic/si%CC%87ngleton-desi%CC%87ng-pattern-d26dae7acb3f) ' da 13 Haziran 2020 tarihinde medium sayfamda yayınlanmıştır._


