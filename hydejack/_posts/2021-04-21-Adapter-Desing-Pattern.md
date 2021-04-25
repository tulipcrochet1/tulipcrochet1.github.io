---
title: # STRUCTURAL PATTERN: ADAPTER DESİNG PATTERN
image: /assets/img/blog/AdapterPattern.jpg

description: >

---

-   Bildiğimiz üzere Desing pattern’lar 3 grup altında çeşitlendirilyor. [**Desing patterns**](https://medium.com/@sumeyyekilic/desi%CC%87ng-pattern-e85c89fd5075)  yazımı veya ilk grup creational pattern serimi okuyarak bir giriş yapabilirisiniz. .

Bu yazımda ise ikinci grup olan **Structural Patterns** serisine giriş yapmaktayım..

**Structural Desing Pattern** nedir ? 💫 **HATIRLAYALIM ..**

-   Structural = **Yapısal**. Yani nesneler arasındaki ilişkileri mimarileri yönetebilmek adına kullanılır.
-   **Structural patterns** ‘ lerden , **“ADATPER DESING PATTERN”** ‘a gelin birlikte bakalım :)

#### 📌Giriş:

**Adapter pattern** ; farklı uygulama parçalarının bizim uygulamamıza entegre edilmesi ile o uygulamanın bizim uygulamamızı bozmadan entegre olarak çalışmasını sağlayan bir **pattern**’dir.

💭 💭Adaptör denilince aklınıza ilk ne geliyor ?

> 🔌 Günlük hayatta kullandığım bir “Adapter” örneği vereyim. Bildiğimiz üzere ülkeden ülkeye voltaj farklılıkları vardır. Bu yüzden voltaj dönüştürücüler kullanılır. Bende bulunan telefon için aldığım Çin tipi bir güç fişi var. Türkiye’de yaşadığım için soket türü uyumsuz oluyor. Bu yüzden doğrudan kullanamıyorum. Ve şarj edebilmek için adaptör kullanıyorum.

#### 💡 Amaç :

Var olan bir class ‘ımın mevcut intreface’i olsun ve birde uygulamamı tanımayan başka bir interface olsun. Bu çalışma yöntemleri farklı olan ve birbirinin nasıl çalıştığını bilmeyen iki interface ’in birlikte çalışmasını sağlar.

-   Farklı sistemleri kendi sistemimize entegre ettiğinizi düşünün. Kendi sisteminizin bozulmadan başka sistemlerin, bize ait bir sistemmiş gibi davranmasını sağlar.

#### ⚡️ Özellikleri :

-   İnterface ‘leri uyumlu hale getirir.
-   Yabancı bir sistem parçasını var olan bir sisteme adapte edilebilmesini, kullanılabilmesini sağlar.
-   Farklı bir uygulama parçasını, var olan bir uygulamaya adapte edilip o uygulama içerisinde de kullanılmasını sağlar.

#### **Ne zaman kullanılır:**

-   Birbirine uyumsuz tiplerin kaynak kodu değiştitirilemediğinde “Adapter” kullanılır.

🔌**Gelin daha geliştirici bakış açısıyla bakalım..**

> Dışarıdaki yabancı bir servisi kendi projenize dahil etmek istiyoruz diyelim.. Bu yabancı servisi istediğimiz yere referans edebiliriz. Ama nasıl referans ettiğimiz burda devreye giriyor.Çünkü o yabancı servisi direkman bizim metodumuzun içinde kullanırsak o servise bağımlı oluruz. Burada adapter desing pattern’i , bağımlılığı ortadan kaldırmak için kullanabiliriz. Ve bu sayede nesnel programlama ve test edilebilirlik durumlarında sıkıntıya girmemiş oluruz.

💰 Mesela bir projede borçlandırma web servisini kullanıyor olalım. Onu direk metoda dahil etmek yerine ; bir adapter yazıp, bir interface’ den implemente edip metodun içinde onu kullanmak daha mantıklı olur.

#### ⚡️ Adapter Deseninde yer alan class ve objeler şunlardır :

-   **_ITarget_** : istemcinin kullandığı kesimlere özel bir interface tanımlar.
-   **_Client_**: Uyumsuz bir arayüz kullanması gereken sınıfı temsil eder. Bu uyumsuz arayüz Adaptee tarafından uygulanmaktadır. Target interface ‘ine uygun objelerle işbirliği yapar.
-   **_Adaptee_**  : Adapte edilmesi gereken mevcut bir interface i tanımlar.
-   **_Adapter_**** : Adaptörün somut uygulamasıdır. **Adaptee** interface’ini , **Target** interface ine adapte eder..

> **📊 Çizdiğim UML diyagramı şu şekilde :**


![adapterpDesingPattern](/assets/img/blog/AdapterUml2.jpg)


**Yazdığım Kod üzerinden bakarsak :**

<script src="https://gist.github.com/sumeyyekilic/2109a848844a9b9d30f5357a95fa8037.js"></script>


📌 Yukarı da gördüğünüz üzere yazdığım örnek kodda :

-   **_Client_** : “**Customer Repository”**; Kurduğum yapıyı kullanmak isteyen istemcidir.
-   **_ITArget_** : “I**CacheManager**” ;kurduğum veya dışardan kulanacağım cache’lemede olmasını istediğim ve bunun için tasarladığım interface’dir.adapter
-   **_Adaptee_** : “**CachingDecorator”** ; kurduğum yapının tanımadığı ve dışında olan uygulamama adapte edeceğim class’dır. CachingDecorator classıı içerisinde, kullanıcıya ayda sağlayacak türde cacheleme property’leri olabilir.class
-   **_Adapter_** : “**CacheDecoratorAdaptor”** adapteri ise ; CachingDecorator adaptee ‘i içerisinde ki yöntemleri (caching decorator ün kendisini) , mevcut yapıma adapte ederek kullanmamı sağlar. BUrada adapter class’ımıza, ICache manager’i implemente ediyoruz.
-   **_SKCache_** : Kendi projeme özgü bir cache ihtiyacı içi oluşturduğum cacheleme yöntemidir. ITArget(ICacheMAnager) ın tanımadığı özellikleri bu sınıfta implemente etmek zorundayız.
-   Burada ki kod, birlikte çalışabilmeleri için bir sınıfın arayüzünü diğerine map’leyen Adapter pattern’ı gösterir. Bu birbirini tanımayan class’lar farklı kütüphane veya frameworklerden oluşabilir..

> **Avantajları :**

-   open/closed principle : Var olan sınıfımı değiştirmeme gerek olmuyor. Mesela gelen taleplere göre geliştirici olarak yeni bir özelllik eklememiz gerekecektir. Bu open clodesed prensibine göre yeni bir özellik eklediğimde mevut sistemin hiç bir şekilde değişikliğe uğramaması gerekir.
-   (Single responsibility principle) : kodu iyi ayırabilmeliyiz.

> **Dezavantajları :**

-   Bir takım interface ve class oluşturmamız gerektiğinden, kodun genel karmaşıklığı artar. Bu yüzden, kodunuzun geri kalanıyla match ederek servis sınıfını değiştirmek daha kolaydır.

❤ Yazımı buraya kadar okuduğunuz için sevgiler❤


Bu yazım, https://medium.com/@sumeyyekilic/ medium sayfamda yayınlanmıştır..
