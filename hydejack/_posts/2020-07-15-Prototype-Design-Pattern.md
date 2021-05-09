---
title: #CREATİONAL PATTERN: 5.PROTOTYPE DESİGN PATTERN
image: /assets/img/blog/PrototypeDesingPattern1.png

description: >

---
## 5.PROTOTYPE DESİGN PATTERN ?

**“Prototype”**, kodumuzu sınıflarına bağımlı hale getirmeden mevcut nesnelerini kopyalamamızı sağlayan **creational design pattern**’ idir.

Prototype elimizde olan nesneyi klonlayarak yeni bir nesne üretmiş oluruz. Bunu klonlanan meşhur koyun Dolly gibi düşünsek bence sakıncası olmaz :)

-   Temeli Clone() metoduna dayanır. Bir nesneyi klonlayarak yeni bir nesne oluşturuyoruz. Bunu yaparken meşhur “**new”** operatorümüzü kullanmıyoruz.Doğal olarak bir nesneyi en baştan yaratarak projeye maliyet oluşturmamış oluyoruz.
-   Kısacası, mevcut bir nesnenin bir kopyasını oluşturmanıza ve onu sıfırdan bir nesne oluşturma ve kurma zahmetlerini almak yerine, ihtiyaçlarınıza göre değiştirmenize izin vermenizi sağlayan bir design patterndir.

**> AMAÇ:** Nesne maliyetlerini en aza çekmektir._

-   İçerisinde bulundurduğu yardımcı ögeleri , fonksiyonellikleri ile işlemlerimizi kolaylaştırmayı sağlar.
-   Kullanışlı ve kolaydır.
-   Ancak her zaman kullanılmaz, ihtiyaç dahilinde kullanılmaktadır.

Mesela elimizde bir temel sınıftan mevcutsa, onun prototype’ ını oluşturup, onun üzerinden yeni nesne klonlama sürecini sürdürebiliriz.

Şu açıdan bakarsanız, başka tipte nesneler de söz konusu olabilir. Birden fazla Concrete Prototype olabilir.

**> 📊 Çizdiğim UML diyagramı şu şekilde :**
![prototypeDesignPattern](/assets/img/blog/PrototypeDesingPattern2.png)

Yukarıda gördüğünüz üzere;

-   **Concrete Prototype:** oluşturma maliyeti yüksek nesneler için kullanılır oluşturulur. çalışma zamanında ki nesne örneğini ilk seferde oluşturmak mecburidir. daha sonra ihtiyaç duyulan anlarda en aza indirilir. Birden fazla başka tipte nesnelerde Concrete Prototype olabilir.

-   UML de gördüğünüz üzere Concrete Prototype olarak 2 tür var, bunlar: **ConcretePrototypeCicek1** ve **ConcretePrototypeCicek2** ‘dir

-   **Prototype** : maliyeti yüksek olan nesnelerin üretimi için kullanılan bir üst sınıftır. Örneğimde ise **CicekPrototype** ‘dır

-   **clone ()**: clone fonksiyonu tanımlanmış olduğu tipe ait nesneyi geriye döndürür.

-   Asıl prototype (**Concrete Prototype**) tiplerinde bu clone fonksiyonunu kendi içlerinde kullanması gerekir.

-   Concrete prototype içerisinde ki her **Clone()** fonksiyonu o tipine ait nesne tipinden bir nesne örneği geriye döndürür.

-   **Client**: prototype tipini kullanacak istemcidir. İçeride herhangi bir operasyonda , concrete prototype tiplerini kullanarak oluşturma maliyeti yüksek olan nesnelerin yükünü azaltır.

-   Prototype tipini ben **abstract** olarak tasarladım. Fakat interface olarak da tasarlanabilir.

**> Yazdığım Kod üzerinden bakarsak :**

<script src="https://gist.github.com/sumeyyekilic/c3df9efce4122e2362ccc8364e351272.js"></script>

📌Yukarı da gördüğünüz üzere yazdığım örnek kodda :

-   **CicekProtoype** adında bir abstract türünde Prototype oluşturdum.

-   **CicekProtoype’ım** ile oluşturduğum temel nesnelerim var. Çiceği adını, yaşayabildiği sıcaklık değerini tutan ve birde hangi familyaya ait olduğunu tutan nesneleri tanımladım.

-   Birde CicekPrototype’ıma Clone() metodu özelliğini atadım. Bu sayede CicekPrototype’ını miras alan diğer Concrete Prototype’lar bu nesneleri Clone() metoduyla istedikleri şekilde kopyalayıp klonlayabilecekler. Kendilerine özel nesneler oluşturabilecekler.

-   ConcretePrototypeCicek1 ve ConcretePrototypeCicek2 adında 2 sındım , CicekPrototype’ımı miras almakta.

-   Main classı içerisinde de Concrete product ‘lardan oluşturduğum X ve Y adında 2 örneğim ile de klonlama işlemini yapıyorum.

-   Ardından klonladığım nesne türlerine istediğim değerleri atayıp görüntülüyorum. Çicek1 türü için iki klon oluşturdum **BEYAZ GÜL** ve **KIRMIZI GÜL** adında çiçekler için nesne örneğinden klonlama yaptım. Klonlanan kopya değerlere bu çiçeklere ait özellikleri tanımladım.

-   Birde Cicek2 türüne ait tanımladığım örnek üzerinden KARANFİL değerine ait özellikleri atadım.

-   Görüntüleme işlemi için de **GorumunTanımları** adında bir standart yazdım. Neticede hepsi aynı nesnenin klonu olduğu için o class içerisine giderek ekrana bastırma işlemini tamamlıyorum.

**> SONUÇ :** Yukarıda ki yazdığım kod bloğumu çalıştırdığımda ise şu çıktıyı alarak sizlerle paylaşıyorum :

![BUİLDERDesignPattern](/assets/img/blog/PrototypeDesingPattern3.png)

**> 📌Avantajları :**

-   Var olan değerleri değiştirerek yeni nesneler belirtme: Şöyle ki , yeni sınıflar tanımlamak yerine bir nesnenin değişkenleri için değerler belirterek nesne kompozisyonu aracılığıyla yeni davranışlar tanımlamanızı sağlar.

-   Yapıyı değiştirerek yeni nesneler belirleme : Birçok uygulama parçalardan ve alt parçalardan nesne oluşturur. Kolaylık sağlamak için, bu tür uygulamalar genellikle belirli bir alt devreyi tekrar tekrar kullanmak için karmaşık, kullanıcı tanımlı yapıları başlatmanızı sağlar.

**> 📌Dezavantajları :**

-   Bazı projeler için prototype design pattern kullanmak aşırıya kaçmak olabilmektedir. Neden derseniz ; mesela projede az nesne kullanılıyorsa veya prototip dizisinin genişlemesine ihtiyaç yoksa buda projenin aşırıya kaçması olmaktadır.

-   Concrete product sınıflarını client’dan gizler.

_Bu yazım, [https://medium.com/@sumeyyekilic/](https://medium.com/@sumeyyekilic/5-prototype-desi%CC%87ng-pattern-6a29af78998) ' da 15 Temmuz 2020 tarihinde medium sayfamda yayınlanmıştır._

❤ Yazımı buraya kadar okuduğunuz için sevgiler❤

