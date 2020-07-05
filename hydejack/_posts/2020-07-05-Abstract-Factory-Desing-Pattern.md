---
title: #CREATİONAL PATTERN: 3.ABSTRACT FACTORY DESİNG PATTERN
image: /assets/img/blog/AbstractFactoryDesingPattern.png

description: >

---
## 3. ABSTRACT FACTORY DESİNG PATTERN ? 

**“Abstract Factory Desing Pattern”,** somut sınıflarını belirtmeden birbiriyle ilişkili tüm ürünleri oluşturma sorununu çözen bir **creational desing pattern** türüdür**.**

-   Yani nesnenin üretimiyle ilgilenen tasarımlardan biride diyebiliriz.

-   Temel olarak istemcinin ihtiyacı olan , ve aralarında ilişkiler bulunan nesnelerin üretiminden sorumlu soyut fabrikaların tasarlanması öne çıkmaktadır. İstemciler, ihtiyaç duydukları ürünlerin tipine göre farklı fabrikaları seçip kullanabilirler. Bu durumda istemcinin ihtiyaç duyduğu ürünler ve bu ürünler arasındaki ilişkilerin tanımlandığı fonksiyonellikler abstract düzeyde gerçekleştirilerek , istemciden soyutlanmış olacaktır.

-   Çok sık kullanılan mimari desenlerden birisidir.

**> _Abstract Factory_, tüm farklı ürünleri oluşturmak için bir interface veya abstract sınıf tanımlar. Gerçek ürün oluşturma işlemini concrete factory classına bırakır.**  

**> Her fabrika tipi belirli bir ürün çeşidine karşılık gelir._**

**Görevi : Toplu nesne kullanım ihtiyaçlarında nesnenin kullanımını kolaylaştırmaktır.**

-   İstemci tarafında kod, bir constructor çağrısı (new operatörü) ile doğrudan ürünler oluşturmak yerine fabrika nesnesinin oluşturma yöntemlerini çağırır. Bir fabrika tek bir ürün çeşidine karşılık geldiğinden, tüm ürünleri uyumlu olacaktır.

-   İstemci kodu fabrikalarla ve ürünlerle yalnızca abstract interface’leri aracılığıyla çalışır. Bu, istemci kodunun fabrika nesnesi tarafından oluşturulan tüm ürün değişkenleriyle çalışmasını sağlar. Biz burada sadece yeni bir concrete factory sınıfı oluşturup bunu istemci koduna iletimini sağlayacağız.

**> _📊 Çizdiğim U_ML diyagramı şu şekilde :**

![singletonDesingPattern](/assets/img/blog/AbstractFactoryDesingPattern2.png)

Yukarı da Abstruct Factory örneğim için çizdiğim uml diyagramında;

-   Türetmeler yardımıyla asıl ürünlerin(concrete product) tanımlaması yapıldı. Mesela **BisikletUret()** product(base) classımda **_FabrikaAUret , FabrikaBUret_**  şeklinde 2 ürün tasarladım.

-   Aynı şekilde bu ürünler **BisikletSiparis()** base classı içinde tanımlandı.

-   Asıl ürünler **FabrikaAUret, FabrikaBUret, FabrikaASiparis, FabrikaBSiparis** tiplerimizdir. Base class’ lardan, implamente olmuş oldular.

-   Çoklu senaryo olacak şekilde 2 fabrikamın olması lazımdı. Bu fabrikalar yine ortak bir **concrete factory** sınıfından türeyecektir. Buna da **BisikletFactory** adını verdim. Her bir tip için ayrı bir fabrika tasarlmam gerekti: “**FabrikaAFactory”** ve **“FabrikaBFactory”** isminde 2 fabrika türettim.

-   **FacrikaAFactory**’nın kullanacağı ürünler **FabrikaAUret** ve **FabrikaASiparis** ‘dir.Uml diyagramında gördüğnüz gibi bu ilişkisini mavi ok işaretleriyle göstermekteyim.

-   Aynı şekilde **FabrikaBFactory**’nin de gösterimi kırmızı çizgilerle gösterdiğim gibidir.

-   **Factory** : bir istemcimiz var. Bunun kullanacağı bir uygulama sınıfı olarak tasarlandı.

-   Factory ‘de asıl ürünlerle ilişkilidir. Uml’ de gördüğünüz gibi, diğer ürünlere ait tipleri kendi bünyesine taşımaktadır.

-   Senaryoda istemcimiz kendi veya **Factory** yardımıyla üretmek istediği ürünün üreticisi olan fabrikanın tipini seçiyor. Mesela o anda **FabrikaA**’ya yönelik ürünler gerekiyorsa **FabrikaASipris** veya **FabrikaAUret** gibi ürünlerin aralarındaki ilişkilerin sağlayıcısı fabrika tipi neyse onu seçerek üretimi gerçekleştirmiş oluyor.

Bir önceki [örneğimi](https://medium.com/@sumeyyekilic/factory-desi̇ng-pattern-ff4490aef46b) düşünürsek Dağ bisikletinin bir markada bile birçok modeli olabileceği ve bunların her biri için switch case yazıldığını düşünürsek oldukça karmaşık hale gelir. **Bunu çözmek için Abstruct factoru desing kalıbı çıkmıştır.**

**> Yazdığım Kod üzerinden bakarsak :**

<script src="https://gist.github.com/sumeyyekilic/bb0c13ee241044599ab0ffedbba2907d.js"></script>

**> SONUÇ : Yukarıda ki gördüğünüz kod bloğunu çalıştırdığımda ise şu çıktıyı alarak sizlerle paylaşıyorum :**

![singletonDesingPattern](/assets/img/blog/AbstractFactoryDesingPattern3.png)

**> _Avantaj :_**

-   Birbiriyle ilişkili olan nesnelerin üretimini , fabrika olarak üstlenen tipler içerisinde istemciden soyutlamış oluyoruz.

-   **SOLİD** prensiplerinden ;

**  * Single Responsibility Principle**’ı destekler. Örneğin ürün oluşturma kodunu tek bir yere çıkararak kodun daha kolay desteklenmesini sağlayabilirsiniz.  

** * Open/Closed Principle**’ ı destekler. Mevcut müşterinin istemci kodunu bozmadan yeni ürün çeşitlerini tanıtabilirsiniz.

**> _Dezavantaj :_**

-   Yeni ürünler eklenmek istediği zaman kodda müdahale etmemiz gerekiyor. mesela fabrika içine yeni bir connetion tip eklemek kolay çünkü türetmeyi yapıp kullanıyoruz. ama yeni bir durum ekleyip bu fabrikalar içinde ele almak istediğimizde sıkıntılar olabilir.

_Bu yazım, [https://medium.com/@sumeyyekilic/](https://medium.com/@sumeyyekilic/abstract-factory-desi%CC%87ng-pattern-afb88f0ab80e) ' da 5 Temmuz 2020 tarihinde medium sayfamda yayınlanmıştır._



