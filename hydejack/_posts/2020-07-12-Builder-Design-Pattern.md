---
title: #CREATİONAL PATTERN: 4.BUİLDER DESİGN PATTERN
image: /assets/img/blog/builderDesingPattern.png

description: >

---
## 4.BUİLDER DESİGN PATTERN ?

**“Builder”**, adım adım bir yaklaşım kullanarak basit nesnelerden karmaşık bir nesne oluşturmak için kullanılan bir **creational design pattern**’idir.

-   Kelime anlamı “**oluşturucu**” demektir. İsminden de anlaşıldığı gibi ortaya bir nesne oluşturmayı hedefler.

-   Tanımda da söylediğim gibi yaklaşım olarak nesnenin adım adım oluşturup işlenmesiyle ortaya çıkar.

**> AMAÇ:** Karmaşık bir nesnenin yapımını temsilinden ayırmaktır. yani ard arda işlemler sonucu bir nesne çıkartmaktır.

-   **Neden kullanmalıyım?** Kısaca kod kalabalığından kurtarmak için kullandığımız bir tasarım desenidir. Çalışma zamanına ve performansa aman aman bir etkisi yoktur :)

Fakat geliştirme esnasında büyük projelerin geliştirilmesinde ve testinin yapılmasında kullandığınızı varsayarsanız , kod açısından geliştirdiğimiz 15bin satırı 12bine indirir.

-   Diğer creational desenlerden farkı: Builder , ürünlerin ortak bir arayüze sahip olmasını gerektirmez. Böyle bir kısıtlama içerisine bizi sokmuyor. Buda aynı yapım sürecini kullanarak birden fazla farklı ürünler üretmemizi sağlar.

-   Önceki creational tasarım kalıplarında anlattığım bisiklet üzerinden örnek verirsem: Bir bisikletimiz olsun istiyoruz ve bunun Dağ, yarış veya gezi bisikleti olduğunu seçebiliyorduk. Fakat bir dağ bisikleti sipariş verirken size özel özellikleri olan ve birde daha dayanıklı bir dağ bisikleti üretilmesini istiyorsanız gezi bisikleti size uygun olmaz. Bu durumda özel üretim yapan bir üretici bulmanız ve ona istediğiniz özellikleri belirtmeniz gerekir. Çünkü istenilen özelliklerde kadrosunun çelik olması rengi markası ayrıca ek özellikler ile daha spesifik bir üretim oluşacaktır. İşte burada devreye **builder design patternı** yardımımıza koşuyor diyebilirim. Builder oluşturduğumuz nesnelerin instancelarını özelleştirmek istediğimizde kullanabiliriz.

-   Karmaşık bir nesnenin yapımını basitleştirmek gerektiği durumlarda kullanılır.

-   Katmanlarda kodları belli döngülerle yazmak yerine, ilgili üreticiye tak çıkar özelliği ile enjekte edilmesi ve ona göre başka bir nesnenin ortaya çıkması olarakta kullanılır.

**> 📊 Çizdiğim UML diyagramı şu şekilde :**
![BUİLDERDesignPattern](/assets/img/blog/builderDesingPattern2.png)

**> Yazdığım Kod üzerinden bakarsak :**

<script src="https://gist.github.com/sumeyyekilic/715d7761bc559f18f554ab762c972ac0.js"></script>

Yukarıda yaptırdığım şey kullanıcının verdiği özellikler doğrultusunda istediği tipte bir bisiklet üretim siparişini almasını sağlamak ve bunu göstermektir.. Burada istemcinin bisiklet üretimini gerçekleştiren asıl **BisikletBuilder** nesne örneğini seçmesi gerekir.

Bu seçim işlemi **Bayi** sınıfı içerisindeki **Constructor** metoduna parametre olarak gönderilir.

Daha sonra istemcinin istediği **Kadro, Vites ve Marka** türüne göre bisiklet üretilerek elde edilmiş olur.

**> SONUÇ :** Yukarıda ki yazdığım kod bloğumu çalıştırdığımda ise şu çıktıyı alarak sizlerle paylaşıyorum :

![BUİLDERDesignPattern](/assets/img/blog/builderDesingPattern3.png)

**> 📌Avantaj :**

-   Bir nesnenin yapımı ve örneği arasında açık bir ayrım sağlar.

-   Yapım süreci üzerinde aldığımız sipariş ile iyi kontrol sağlar.

-   Nesnelerin iç yapısını değiştirmeyi destekler.

-   Single Responsibility prensibini destekler.

**> 📌Dezavantaj :**

-   Kod karmaşıklığı artabilir.

_Bu yazım, [https://medium.com/@sumeyyekilic/](https://medium.com/@sumeyyekilic/4-bui%CC%87lder-desi%CC%87ng-pattern-782b103dd429) ' da 12 Temmuz 2020 tarihinde medium sayfamda yayınlanmıştır._

❤ Yazımı buraya kadar okuduğunuz için sevgiler❤
