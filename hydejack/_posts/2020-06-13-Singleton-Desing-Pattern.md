---
title: #CREATİONAL PATTERN: 1.SİNGLETON DESİNG PATTERN
image: /assets/img/blog/SingletonDesingPattern.png

description: >

---

## #CREATİONAL PATTERN: 1.SİNGLETON DESİNG PATTERN ?

#### Singleton Desing Pattern Nedir?

_**Singleton Desing Pattern bir nesne örneğinden sadece bir defa üretilip , bu nesne örneğinin her zaman kullanılmasını söyleyen bir patterndir.**_

-   Pattern bir önceki [**yazımda**](https://medium.com/@sumeyyekilic/desi%CC%87ng-pattern-e85c89fd5075?source=---------2------------------) açıkladığım gibi bir sorun, ve bu sorunun da çözümü demekti.

-   Singleton Pattern, Desing Pattern’ların 3 kategoriden ilki olan Creational Pattern ‘ın çözümlerinden en çok kullanılan pattern’idir.

-   Singleton “tekil” demektir. Yani ilgili nesneden bir tane olsun istiyorsak singleton kullanabiliriz.

👩🚀 Desing patternler ile uzayı keşfe gerek yok..

📌 **Peki biz geliştiricilerin gezegenlerinde ki uygulamalarında nerelerde ve nasıl kullanırız ?**

-   **En büyük amaç : “**Bir nesnenin örneğinin ve o örnek değerinin bir çok kullanıcı tarafından değiştiği zaman bile aynı şekilde kullanılmasını**”** amaçlar.

> _Örneğin sizin bir uygulamanız var. Bu uygulamanızda günlük kaç kişinin kullandığı saysını tutmak istiyorsunuz diyelim. Anlık ziyaret sayısı tüm kullanıcılar için aynı nesnede tutulur. Herkes için aynı değer okunur ve sisteme giren olunca bu değer bir artar._

-   **En büyük 2.amaç : “**Bir nesnenin durumunun kontrol edilmesi**”** amaçlanır.

Mesela benim gezegenim de bir nesne örneğim var. Katmanlar arasında geçerken **bu nesne sadece işlem yapıyorsa**, yani **bir değeri tutmak gibi görevi yoksa** o zaman yine Singleton Pattern’ dan yararlanmakta fayda vardır.

> _Örneğin ; iş katmanındaki bir nesneyi düşünün : bu nesne ekleme, silme, güncelleme, arama yapsın ve bunları bir metot şeklinde yapsın. Diyelim ki 5 bin tane kullanıcınız var. Bu 5 bin kullanıcı iş katmanına her istekte bulunduğunda yeniden new’lenir.. **buda bize daha pahalı bir işlem sunar.**_

⭐Burada olduğu gibi madem biz işlem yapacak bir nesne üretiyoruz. Herkesin bunu kullanmasını istiyoruz. Öyleyse bizim **bu nesneyi bir defa üretip herkesin kullanımına açmamız** gerekir.

#### 📌 Peki Singelton Desing Pattern'ı ne zaman **kullanmamalıyız** **?**

-   Singelton Desing Pattern ile bir nesne ürettiğinizde bu bellekte her zaman sabit kalır. Diyelim ki MVC uygulamasında bir signelton manager nesnesi ürettiğinizde, IIS’i restart etmeyene kadar bu nesne ortadan kalkmaz.

⭐Burada dikkat etmemiz gereken şey ; bir nesneyi singleton olarak ürettiğimiz zaman herkes bunu kullanmak durumunda mı ? Yada aynı şeyi kullanacak mı ?

-   Bir nesneyi ürettik ve diyelim ki o nesneyi kullanıcı uygulama boyunca sadece bir yerde bir kere istiyor. Belki de günlerce kimse o nesneye kimse istekte bulunmuyor. **Burada olduğu gibi “nadir kullanılan bir ürün singleton olarak üretilmemelidir.”** Nesnenin ömrü işlem bitince bitmelidir. Eğer ihtiyaç olursa yeniden üretilebilir. Çünkü diğer türlü bellekte hep yer kaplayacaktır.

Bir nesneden sadece bir tane oluşturmak istiyoruz. Gelin bunun için kafa yoralım.. 🤯

Elimde bir class var.Bundan sadece bir tane oluşturmak istediğimi düşünün.

-   Singaleton adında bir class oluşturdum:

<script src="https://gist.github.com/sumeyyekilic/ebf063197acb2c3c9382796f219dcfeb.js"></script>

-   Yukarıda ki kodu incelerseniz ilk olarak Singleton adında bir class oluşturdum. Bu class normalde update, insert vs işlemleri yaptığı için bunu singleton desing pattern kullanır hale getirmek istedim.

-   Öncelikle bu nesnenin private bir constructor ‘ını oluşturdum. Dışardan erişimi engelledim.

-   Singleton örneğini oluşturacak metodu yine bu classın içine yazdım. Oda static olarak yazılmalıdır. CreateSingleton nesnesi Singleton’ın kendisini döndürür.

-   CreateSingleton() metodu ile singleton nesnesinden daha önce oluşturulmuş mu bunu kontrol edicez. Daha önce oluşturulmuş varsa onu vereceğiz. Eğer yoksa bir tane oluşturup onu döndüreceğiz.

-   Bunun için bir tane yöneteceğimiz nesne ihtiyacımız vardı. Onu da static olarak **“_singleton”** adında bir örnek tanımladım.Daha sonra da if bloğu içerisinde bu nesne null durumu ile kontrol edildi. _singleton nesnesi private olduğu için buna erişim için new’ledim. Burada singleton oluşturulmuş mu diye kontrol edip ona göre aksiyon üretip , return ile geri dönüş yaptırdım.

-   Bu format ile temiz bir implementasyon yapılmış oldu.

-   Şimdi asıl önemli olan bu nesneye ihtiyaç duyduğumda kullanmam.  
    
    Void main in içinde bu nesne new’lenemez. Kodda gördüğünüz şekilde ürettim.

-   Artık yapacağım işlemleri, main class’ında oluşturduğum nesne ile çağırıp kullanabileceğim.

-   Delete adında bir operasyon yazdım. Ve bu metodu main class’ı içerisinde oluşturduğum nesne ile erişebilip kullabilmesini sağladım.

-   Burada amacım temiz kod ile singleton desing pattern yazmayı göstermekti.

📊 Oluşturduğum kodun uml sınıf diyagramı ise şu şekildedir.


![singletonDesingPattern](/assets/img/blog/singletonDesingPattern2.png)

Burada olayın işleyiş ve mantığını anlamamız önemlidir. Çünkü önemli olan singleton kullanıp, kullanmayacağınızı bilip doğru karar vermemizdir. Tabi buda tecrübe gerektirir.

Sizinde bildiğiniz gibi artık bir şeyi yapmak kolay. Önemli olan neyi, nerede kullanacağını kestirip ,doğru zamanda nerede ne yapacağını bilmek gereklidir.. Singleton desing’ı bu şekildedir.

❤ Yazımı buraya kadar okuduğunuz için teşekkürler ❤ 
Bir sonraki yazımda desing patternın kategorilerinden Creational Patterns 'ın diğer alt pattern'ları için bu serinin devamı olacaktır.

_Bu yazım, [https://medium.com/@sumeyyekilic/](https://medium.com/@sumeyyekilic/si%CC%87ngleton-desi%CC%87ng-pattern-d26dae7acb3f) ' da 13 Haziran 2020 tarihinde medium sayfamda yayınlanmıştır._
