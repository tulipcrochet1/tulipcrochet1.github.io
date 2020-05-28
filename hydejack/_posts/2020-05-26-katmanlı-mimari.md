---
title: Katmanlı Mimari 
image: /assets/img/blog/katmanlimimari.png

description: >

---
# **Katmanlı Mimari** 

Katmanlı mimari, yazılım geliştirme tekniği olarak bilinmektedir.. Nesne tabanlı büyük projeler veya kurumsal projeler günümüzde katmanlı mimari (n katmanlı) ile yazılmaktadır.

Birden çok proje oluşturup, her birini birbirine referans göstererek kullanma mantığına dayalıdır. Uygulamamızı farklı katmanlara ayırdığımızda her katmanın sabit bir sorumluluğu üstlenerek ekipler arası da iş bölümü oluşacaktır. sonuç olarak katmanlı mimaride her proje kendi amacına uygun şekilde hareket ediyor olacaktır. Aynı şekilde her katman da kendi amacına uygun işleri yapmaktadır.

## **Katmanlı Mimari Neden Ortaya Çıktı ?**

-   İlk neden tekrar takrar kullanılabilirlik (reusability) ’dir..
-   Yani yazılan bir kodun değiştirilebilir olmasını sağlamak. Gerektiğinde çok zahmetsiz bir şekilde tek bir yerde değişiklik ile bütünlüğü sağlamak.
-   başka projelerde kullanılabilir olmasını sağlamayarak, projenin tak çıkar özelliği ile çalışabilmek. Mesela projede sadece arayüzü değiştirerek farklı bir proje ortaya çıkarılabilir olması için veri erişim katmanında ve iş katmanında yazdıklarınızı tekrar kullanabilir olmasıdır.
-   bir projede yazılan işler aynı proje içinde bir başkası tarafından veya farklı bir ekranda tekrara düşmesinin önüne geçmek. Geliştirmede kod tekrarına düşmemek
-   aynı projenin mobil, web tarafında hepsinin aynı anda çalışıyor ve ortak çalışma alanlarını bütün halinde yönetmek.

Örnek verecek olursam ; büyük kurumsal firmaların projelerini, hayata geçirilmesini düşünürseniz epey büyük bir ekip ve iş bölümü gerektiren projeler oluyor. Bireysel yaptığımız projeler gibi ufak çaplı olmuyor. Mesela kurumsal projelerde ; veritabanları tasarlanıyor, web, mobil uygulamaları ayrı ayrı tasarlanıyor, geliştiriliyor. Bu projelerden elde edilen veri ve analizler başka kişilerle paylaşılarak birde raporlama projeleri geliştiriliyor… Daha okurken yorulduğunuzu duyar gibiyim :) Bunların hepsi bir uygulamanın bir sürü entagrasyonu için yapılıyor. Dolayısıyla bu kadar işlemleri yapabilmek için bir çalışma disiplini oluşturup projenin her bir görevini birbirinden ayırmak hedefleniyor. Ama bunu yaparken veri bütünlüğünün sağlanması gerekmektedir.

## 💎 Amaç :

-   Yapılan işleri birbirinden ayırmak.
-   Güvenlik oluşturmak. Yani projeye herhangi bir saldırı olduğunda tüm her şey tek bir proje içinde olsa saldırıya daha açık hale gelir. mesela verilerim ile son kullanıcıya gösterdiğim arayüz veya web sayfalarım aynı projede olduğunda o web sayfasından gelen bir saldırı verilere erişimi sağlayacağından benim için daha büyük bir tehdit haline geliyor.
-   fazla sayıda ekibin ve bu ekipte içerisinde eş zamanlı iş bölümü yapması da daha kolay sağlanabiliyor.

Daha derin örnekleme yapmadan önce katmanlı mimarinin n katmandan oluşabileceğini bilin. Fakat bir standartlaşma ile en az 3 katman kullanılmaktadır

## 🧱 Katmanlı mimari temelde 3 standart katmanı şunlardır;

-   _Veri Erişim Katmanı ( Data Layer )_
-   _İş Katmanı ( Business Layer )_
-   _Sunum- arayüz Katmanı ( Presentation Layer )_

# 1. Veri Erişim Katmanı (Data Access Layer)

Veri erişim katmanında sadece veritabanına erişilmektedir. Bu katmanda veritabanına erişim için update, delete, insert, select, injection, truncate gibi gerekli olan kodlar yazılır.

Şöyle ki ; bağlantı kodlarını kullandığımız sınıf , özel bir sınıf olan Sql connection sınıfıdır. Sql connection ile veritabanıyla bağlantıyı açmamızı, veri listesini çekeceğimiz zaman alma , silme, güncelleme için bu işlemlere erişimimizi sağlar. Önce bağlantı açılır. Ondan sonra delete update dediğimiz sorgu işlemlerini saql command ile çalıştır hale getiririz. Ardından yazılan kodları çalıştırıp verileri listeleyip silip kaydedebileceğiz, güncelleyebileceğiz. Veri erişim katmanında bu metotları tanımlayabilir ve sınıf oluşturup gerekli yerlerde kullanabiliriz.

Veri erişim katmanına bir görev kodu , loglama veya validasyon yapılmaz. Sadece veritabanına erişilmektedir.

# 2. İş Katmanı (Business Layer)

İş katmanında sadece iş kodları yazılır. İş kodları yazılırken veri erişim katmanı ile iletişim kurulur. Çünkü yapılacak kaydın veritabanına uygunluğundan emin olunmalıdır. Olası mimari hatada bir kaydın daha önceden veritabanına kayıt edilmesi yaşanabilir.

İstediğimiz verilerin listesini çekebileceğimiz; insert, delete, update işlemlerini yapacağımız kodlar burada yazılır. Veri listesinin alınması gerektiğinde bunu bir sınıf ile nasıl almamız gerektiğini bilmeliyiz.

Örneğin; veri erişim ile ilgili bir müşteriyi kayıt ekleyeceksiniz. Müşteri isimli bir metot tanımlayınca müşteri tablosuna veri eklemeye çalışacak. Adı soyadı gibi verileri eklerken her veriyi bir sınıfa atadığını düşünün. Bu sınıf içinde yine adı soyadı gibi alanlar olacak. Yine aynı şekilde kayıt almak istedik ve elimize 15 liste geldiyse bu listeyi müşteri sınıfına aktaracağız.

Bu şekilde liste halinde bir sınıfı sonraki katman olan sunum katmanında kullanabileceğiz.

# 3. Sunum Katmanı (Presentation Layer)

Sadece kullanıcı ile etkileşim kodlarının yazıldığı yerdir. Sunum katmanında kullanıcıya bir arayüz verilir ve o kullanıcıdan veri alınır.

Örneğin; mail hesabınıza giriş yaparken formu doldurup girişi yapmak için bir butona basıyorsunuz. Bir kurumsal projenin form tasarımında da biz bunları yaparak kullanıcıdan değer alıyoruz. Kullanıcıdan istediğimiz inputları bu arayüzden, yani sunum katmanı ile oluşturmuş oluruz.

## 💎 Katmanlı Mimarinin Özellikleri:

-   Katmanlı mimaride her katmanının uygulama içinde belirli bir rolü ve sorumluluğu vardır. Örneğin, bir sunum katmanı tüm kullanıcı ara birimini ve tarayıcı iletişim mantığını işlemekten sorumlu olurken, bir iş katmanı da istekle ilişkili belirli iş kurallarını yürütmekten sorumlu olacaktır.
-   Arayüz katmanı bir kullanıcının verilerinin veritabanından nasıl alınacağıyla veya nasıl gönderileceği konusuyla ilgilenmez. Sadece kullanıcıya ait formsa eğer o ilgilerin belirli bir formatta ekranda görüntülenmesini ve kullanıcıya sunulmasını sağlar.
-   Aynı şekilde, iş katmanının müşteri verilerinin bir ekranda görüntülemek için nasıl sunulacağını bilmez. Hatta kullanıcı verilerinin nereden geldiğini bilmesine gerek olmadığı gibi bu işleri yapması da mimari için doğru olmaz. Yalnızca veri erişim katmanından istenen veriyi alması, verilere karşı iş mantığı gerçekleştirmesi (ör. hesaplama işlemi) ve bu bilgileri arayüz katmanına aktarması gerekir.
-   Bir veritabanı uygulaması yaptığınızda bir katmanı, veritabanına bağlantı kodlarını yazdığınız katman olarak kullanıyorsunuz. Bir diğer katmanı da verileri kaydettiğiniz verileri çekeceğiniz, sileceğiniz, güncelleyeceğiniz kodları yazmış olduğunuz katman oluyor. Bir katmanda ise insert, delete, update yani veri erişim ve iş katmanı, sunum katmanında kullanılmaktadır. Sunumda ise bir kişinin kaydını aldığınız ekrandır. Bir input veri girişi sağlayarak buton ile kayıt yaptırılan ekranlar sunum katmanı oluyor. Böylelikle bir katmanlı mimarinin standart yapısını uygulamış oluyoruz.