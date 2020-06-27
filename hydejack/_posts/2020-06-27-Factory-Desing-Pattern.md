---
title: #CREATİONAL PATTERN: 2.FACTORY DESİNG PATTERN🏭
image: /assets/img/blog/FactoryDesingPattern.png

description: >

---
## #CREATİONAL PATTERN: 2.FACTORY DESİNG PATTERN🏭 ?

**“Factory Desing Pattern”** günümüz desing pattern’ları arasında en çok kullanılan Creational Desing Pattern methodlarından birisidir.

**> _Kalıtımsal ilişkileri olan nesnelerin, ürünlerin üretilmesi amaçlı kullanılan desing pattern’dır.._**

-   **Factory** kelime anlamı **fabrika** demektir.
-   Farbrika deyince akla üretim gelir. İhtiyacımız olan her nesneyi üretebilen fabrikalar vardır.
-   Nesneyi oluşturma görevini müşteriden fabrikaya bırakabiliriz. Mesela kullandığımız bilgisayarı bayiler değil fabrikalar üretir.
-   Pattern ‘in kalıbının esasını teşkil eden kavramımız bir **method**tur. bu method ise üreticinin asıl istediği ürünlerin üretilmesini sağlarlar.
-   İstemcinin ihtiyacı olan nesne üretiminin sorumluluğu , bir metoda devrediliyor. Bu metot ise **“Factory Method”** olarak adlandırılmaktadır.

**> **_Factory Method; bir nesne oluşturmak için abstract veya interface sınıfları tanımlayan ancak alt sınıfların, somutlaştırılacak nesnelerin türüne karar vermesine izin veren bir Creational Desing Pattern türüdür._****

-   Amaç “yazılımda değişimi kontrol altında tutmaktır.”
-   Factory Desing Pattern’ ında en temel olay bizim bir class fabrikamızın olmasıdır.

> **Uyguladığım örnek koda bakalım;**


<script src="https://gist.github.com/sumeyyekilic/0be860b57a86cc2405b401b8c15a5fa3.js"></script>

-   ilk olarak “**IBisiklet**” adında bisikletler üreten bir product class’ı oluşturdum. Bunu interface olarak ürettim, baş harfinden de anlaşılacağı üzere :) Bu sınıf asıl ürünler için(concrete product’lar için) base class görevindedir. Factory metodun da geriye döndüreceği metot olacak. İçerisine de basit bir **Uret()** adında metot yazdım.

-   Daha sonra IBisiklet sınıfımdan , 3 tane **concrete product** türettim. Bunlar **“DagBisikleti, YarisBisikleti, GeziBisikleti”** dir. IBisiklet interface’ini miras aldıkları için Uret metodunu bunlar içerisinde istediğimiz şekillerde tasarlayıp yeni özellikler katabiliriz. Ben örnek olması için sadece output verdim.

-   Ardından yeni bir “CreatorFactory” adında creator classı oluşturdum. Bu class Factory metodunu içinde taşıyacak bir class ’dır.

-   CreatorFactory sınıfı içine BisikletFactory adında bir metot yazdım. Yazdığım metot öncelikli olarak geriye IBisiklet tipinden bir referans döndürüyor.. Bu metodun implemantasyonu bisiklet modellerini tutan “BisikletModel” adında bir enum tanımladım. Yani hangi türde bisiklet istediğini istemciden veya fabrikadan talep edebilmemiz için içerisine değer attım.

-   Daha sonra "BisikletFactory" metodumun BisikletModel tipinden değerler alması için bisikletModel tipi tanımlamasını yaptım. BisikletFactory içerisinde bunun referansını başta **“ IBisiklet bisiklet= null; ”** olarak tanımladım.

-   BisikletModel’i parametre alan bir switch blogu tanımladıım.Burada dağ , yarış bisiklet türlerine göre uygun ürünün üretimi gerçekleştirmiş oluyorum. BisikletFactory içerisinde null olarak tanımladığım bisiklet referansımı son olarak switch den sonra döndürdüm.

-   Son olarak main metodu içerisine ilk olarak CreatorFactory sınfından örnek türettim. daha sonra bu örneği kullanarak,

-   IBisiklet bisikletDag = creator.BisikletFactory(BisikletModel.Dag); tanımlaması; BisikletFactory’ ler geriye IBisiklet türünden değerler döndürdükleri için bu tanımlama, bisikletDag, bisikletGezi, bisikletYaris diye tüm sınıfların ataması yapıldı.

-   Daha sonra : **bisikletDag.Uret();**

şeklinde her bir bisiklet türünün Uret(); metodu çağırılarak, üretim gerçekleştirmiş oldu.

**> **Sonuç :****

Yukarıda ki gördüğünüz kod bloğunu çalıştırdığımda ise şu çıktıyı alarak sizlerle paylaşıyorum :

![singletonDesingPattern](/assets/img/blog/fdp.png)

**> **📊 Oluşturduğum kodun uml sınıf diyagramı ise şu şekildedir:****

![singletonDesingPattern](/assets/img/blog/FactoryDesingPattern2.jpg)


**📌Avantajları:**

-   Factory Desing Pattern, alt sınıfların oluşturulacak nesne türünü seçmesine olanak tanır.
-   SOLID’in Single Responsibility Principle ve Open/Closed Principle destekler.

**📌Dezavantajları:**

-   Deseni uygulamak için birçok yeni alt sınıf eklemeniz gerektiğinden kod daha karmaşık hale gelebilir..

_Bu yazım, [https://medium.com/@sumeyyekilic/](https://medium.com/@sumeyyekilic/factory-desi%CC%87ng-pattern-ff4490aef46b) ' da 27 Haziran 2020 tarihinde medium sayfamda yayınlanmıştır._

❤ Yazımı buraya kadar okuduğunuz için sevgiler ❤