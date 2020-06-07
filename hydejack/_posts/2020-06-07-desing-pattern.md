---
title: DESİNG PATTERN 
image: /assets/img/blog/desingPattern1.png

description: >

---
# **Desing Pattern** 

“Desing Patter nedir” demeden önce, “pattern nedir”i anlayarak başlayalım.

⭐**“ Pattern”**; örüntü, şablon anlamına gelmektedir. Tekrar eden yapı olarak kullanılır. Bu yapılar bize aynı programlama mantığının tekrar ettiğini gösterir.

Nasıl yani ❓

Diyelim ki bir sorunumuz var, bu sorun için üretilmiş birde çözüm vardır. Bu sorun/problem birden fazla da olabilir. **Pattern** da burada devreye giriyor **O soruna getirilen çözümün tekrar tekrar kullanılabilmesini sağlayan yapı pattern'dır**.

⭐**“Design Pattern”** ise bir yazılım projesinde sürekli karşılaştığımız aynı veya benzer sorunlar üzerinden yola çıkarak kod optimizasyonunu en iyi şekilde yapabilmemizi sağlayan yapıdır.

Türkçeye çevrilmiş halinde ise **Tasarım Kalıpları** oarak geçmektedir.

_**Tam olarak nedir?**_

Ortak problem ve ortak çözümlerimiz var.

-   Ama kaç tane çözüm var ?

Bir problemin sonsuz çözümü olabilir. “Hangisini kullanmalıyım ve hangisi benim sorunumu en iyi çözer” mottosuyla olan kalıplardan yararlanırız. Ayrıca kendimiz de kalıp üretmeye çalışabiliriz. Ama öncelikle şunu bilin ki bu desing pattern’lar pek çok insanın ortak ihtiyacını çözebilecek yapıdadır. Ortak ihtiyacı çözebilecek yapı oluşturulurken her yeni projenin deneyiminden test edilip onaylanmış çözümler oluyor.

📌 **Desing Pattern Ortaya Çıkışı?**

Desing Pattern, OOP(nesne yönelimli programlama) ile öne çıkmıştır. Daha önceden de vardır ama esas hayatımıza girmesi OOP ve buna bağlı olarak uml(Unified Modelling Language) ile hayatımıza grimiştir.

Bir proje geliştirirken oop dünyasında ve uml çizimlerin gelmesiyle ortaya çıkmıştır.

Uml tasarımı bize şunu sağlıyor; kafamızda soyut olarak tasarladığımız nesne yönelimli modelleri görselleştirebilmeyi , modellemeyi sağlar. . Diyelim elimde iki class var. Bunlar arasında inheritance ilişkisi var. Class’lardan birisinde ise interface bağlantısı var vs.. Bunları biz görsel olarak gösterebiliyoruz. Bu gösterimi yaparken şu anlaşılıyor: Biz belli programlama yapılarını tekrar ediyoruz. Bu sebeple Desing Pattern’lar ortaya çıkmıştır.

Desing Pattern yapısına bir örnek verecek olursam ; MVC yapısı. MVC (Model-View-Controller) en çok tekrar eden web framework’ lerinde sıkça kullanılan desing pattern’dır.

📌 **Desing Pattern’lara Neden İhtiyacımız var ?**

Nesne yönelimli programlamanın; **kapsülleme, kalıtım, soyutlama, polimorfizm** gibi temel prensiplerini bilirseniz, bu sizi iyi bir OO tasarımcısı yapar. C#, java gibi bir programlama dilinde basit bir hesap makinesi uygulaması yapmaya çalışsanız bile, gerçekten nesne yönelimli ilkeleri kullandığınızı düşünün. Ancak kodunuzun sınıfları için büyük değişiklikler yapmak zorunda kalmadan değişiklikleri kolayca dahil edebileceğinin bir garantisi yoktur. Burada pattern devreye girer.

Desing Pattern’ların ana mantığında şu yatıyor: Bu kullanacağımız kalıp türleri implementation üzerine değil interface üzerine kurulu kalıplardır. Hepsinin kendine ait bir yapısı var ama ortak bakarsanız hepsini bir araba gibi düşünebilirsiniz. Markasının önemi yoktur.

Yazılım projelerine baktığınızda , yazılım ilerlediğinde aslında yazan kişiye karşı bir canavara dönüşüyor. Ve kendi oluşturduğunuz canavara yeniliyorsunuz :) Çünkü projeyi oluşturuken nerelerde değişikliği olacağını, ilersini düşünmediğinizde, sayfalarca yazdığınız proje canavara dönüşüp sizi ısırır. O yüzden yazılımın değişken noktalarının, ilerde bu yazılımı düzenlemeye çalıştığınızı düşünün. Bu yazılım büyüyüp bizim için projede düzenleme güncellemede sorun yaratıcaktır. Bu detayları bilerek , önceden bir plan oluşturursak o zaman rahat edicez. Şu şu kısımlar bizim için değişlik olmasına uygun yapı deyip bunları göz önünde ayrı bir yere tutarsak, sabit kısımları da ayrı tutarsak işimiz kolaylaşır. İşte **tasarım kalıpları** da bunu **çözüyor**.

Desing pattern’ lar dilden bağımsızdırlar.

✅ Yapılarına göre tasarım kalıpları 3 tür kategori altında tutulur :

## **1.Creational Patterns**

Bu kategoriye giren desing pattern tamamen nesne yaratmanın farklı yollarıyla ilgilidir. Yeni objelerin yaratılmasıyla ilgilenir.

## **2. Structural Patterns**

Structural (yapısal) nesneler arasındaki ilişkilerle ilgili desing pattern’lar.

Oluşturulan yeni objelerin bir araya gelerek birbirleri arasında kompleks bir yapı oluşturmaıyla ilgili desing patternlardır.

## **3. Behavioral Patters**

Behavioral nesneler arasındaki etkileşimleri veya iletişimi tanımlayan desing pattern’lardır..

Objelerin birbiriyle mesajlaşmasını, birbirinden haber almasını sağlayan yapılardır.

✅ Bu 3 kategori de kendi içinde şu pattern’lara ayrılır :

![desingPatternCizimim](/assets/img/blog/desingPattern.png)

Fotoğrafta gördüğünüz gibi Desing Pattern'lar 3 temel kalıptan oluşmaktadır. Bunlarda kendi içerisindeki bir sürü pattern bulundurmakta. Hepsi işlevi ve amacına göre projelerde kullanılıyor. Bir başka blog yazımda bunları seri yapıp tek tek uygulama ile anlatmaya çalışacağım :)

📌 **Desing Pattern’ler Bize Ne Sağlar :**

-   Tekrar kullanılabilir, bakım yapılabilir ve genişletilebilir yazılımlar oluşturabilmeyi sağlar.
-   Başka projelerle ilgili hız kazandırır. Proje yönetimini hızlandırır.
-   Hataları daha iyi algılamanızı sağlar.
-   Yeni framework ve kütüphaneleri hızlı bir şekilde öğrenmenize yardımcı olacaktır.
-   Test senaryosu üretmek için kullanılabilir. Neyin, nasıl ilişkisi olduğu hakkında yol gösterir. Test tekniği stratejisi geliştirp bunları uygulayıp daha başarılı testler yapmasnızı sağlar.
-   Yazılım mühendisliğinde, bağlam(coupling) terimi bulunur, yazılım modülleri arasındaki karşılıklı bağımlılık derecesini belirler.

🔦Örneğin ; Arabanızın lastiği patladı ve yolun ortasında mahsur kaldınız. Lastiği değiştirmeniz gerekiyor. Burada lastiği değiştirmek için motorunuzu ,direksiyonunuzu veya arabanızın herhangi bir parçasını çıkartmak zorunda değilsinizdir. Çünkü arabanızın tasarımı bu şekildedir. Sadece yedek bir lastik ile değiştirmek yeterlidir. Burada arabanız Gevşek Bağlılık Prensibi olan ( Loose Coupling) bir sistem örneğidir. Yani aracınızın bileşenleri birlikte çalışır ancak birbirine yüksek bağımlı değildir. Motoru çalıştırmak için lastiklerinizle bir şey yapmanıza gerek yoktur. Bir tasarım deseninin sadece yazılım için değil, hayatınızın herhangi bir yerinde ne kadar etkili olabileceğini buradan anlayabilirsiniz.

-   **Gerçek hayatta ne işimize yarar?** Ortak dilde konuşabilmemizi sağlar. Problemler aynı , kullanılan dil aynı olunca tüm dünyada yazılımcılar aslında ortak bir dilde aynı dilde konuşmuş oluyor.
-   Anlaşılabilir bir yapı sağlar. Desing patternlar ile işi bir prosedüre döküyoruz. Bir standarta döktüğümüzde daha anlaşılabilir oluyor(isimlendirme, yada ortak bir konuşma alanı)
-   Güncellenebilir bir yapı sağlar. Mesela, niyet ettim tasarım kalıbı kullanmaya dediğimde, aslında yaptığım şey işi prosedüre dökmektir. Projenin üzerine şunu yaparken, şu kalıbı takip ederek yap diyorum. Böyle olunca projeyi ortak bir iskelet üzerine oturtunca artık güncellemek daha kolay oluyor. Kendi canavarımızın ipini çekip biraz bağlamış oluyoruz ..
-   Aynı programlama mantığının tekrar ettiğini söylemiştim. Biz şayet bir problemi bir yerde çözdüysek bunu başka bir yerde de kullanabiliyoruz. bir yerde risk taşıyan yapılara başka yerde de dikkat edebiliyoruz.
-   Bir programı tasarlarken nerelere dikkate edilmesi gerektiğini, bir problem ile karşılaşıldığında hangi pattern ile çözebileceğini önceki aksiyonlara bakarak daha hızlı, daha güvenilir üzerinde çalışılmış modeller üzerinden ilerletebiliyorlar.

_Bu yazım, [https://medium.com/@sumeyyekilic/](https://medium.com/@sumeyyekilic/desi%CC%87ng-pattern-e85c89fd5075) ' da 7 Haziran 2020 tarihinde medium sayfamda yayınlanmıştır._
