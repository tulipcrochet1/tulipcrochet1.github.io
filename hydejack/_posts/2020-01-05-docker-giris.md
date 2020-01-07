---
title: #DOCKER 101 - Workshop Klavuzum 🐳
image: /assets/img/blog/docker.jpg
description: >
---

## #DOCKER 101 - Workshop Klavuzum 🛳️

Bu docker serisi, gelişitiricilerin konteynırlarla çalışmaya başlamasına yardımcı olmak amacıyla başladım. Öğretici olması için hem kendim çalışıp hemde çıkarttığım ve uyguladığım notları bir örnek olması açısından faydalı olmasını umarım. Çok fazla derinlemesine ilerlemese de, aşağıdaki konuları kapsayacaktır.
 - İlk konteynırımı run etme
 - konteynırları build etme
 - hangi konteynırların çalıştığını öğrenme ve bunları kaldırma
 - Verileri devam ettirmek için Volume kullanma
 - Geliştirmeyi desteklemek için bind  mount kullanmak
 - Birden çok konteyner uygulamalarını desteklemek için multi-container ağ oluşturmak
 - Uygulamaların tanımını ve paylaşımını basitleştirmek için Docker Compose'u kullanma
 - Build(derlemeyi) hızlandırma ve push/pull boyutunu azaltmak için image layer önbelleğini kullanma
 - build-time ve runtime bağımlılıklarını ayırmak için multi-stage(çok aşamalı) derlemeler kullanma

# 🔺Docker Hub'a Kaydol
[https://hub.docker.com/](https://hub.docker.com/) adresine tıklayın ve [Get Started](https://hub.docker.com/signup) deyip bir hesap oluşturarak başlayın. Eğer kayıtlıysan kendi tanımladığın docker id ve şfren ile [Giriş Yapın](https://id.docker.com/login/?next=%2Fid%2Foauth%2Fauthorize%2F%3Fclient_id%3D43f17c5f-9ba4-4f13-853d-9d0074e349a7%26next%3D%252F%253Foverlay%253Donboarding%26nonce%3DeyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiI0M2YxN2M1Zi05YmE0LTRmMTMtODUzZC05ZDAwNzRlMzQ5YTciLCJleHAiOjE1NzgzMTMzMTUsImlhdCI6MTU3ODMxMzAxNSwicmZwIjoiQ29lc2ZVS1gxNzl6bkYwdS1fN2Frdz09IiwidGFyZ2V0X2xpbmtfdXJpIjoiLz9vdmVybGF5PW9uYm9hcmRpbmcifQ.Hgpm9BBWFsoxsEGXN-NWX_RtwK-LhXJOFPooNscdlGw%26redirect_uri%3Dhttps%253A%252F%252Fhub.docker.com%252Fsso%252Fcallback%26ref%3Dlogin%26response_type%3Dcode%26scope%3Dopenid%26state%3DeyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiI0M2YxN2M1Zi05YmE0LTRmMTMtODUzZC05ZDAwNzRlMzQ5YTciLCJleHAiOjE1NzgzMTMzMTUsImlhdCI6MTU3ODMxMzAxNSwicmZwIjoiQ29lc2ZVS1gxNzl6bkYwdS1fN2Frdz09IiwidGFyZ2V0X2xpbmtfdXJpIjoiLz9vdmVybGF5PW9uYm9hcmRpbmcifQ.Hgpm9BBWFsoxsEGXN-NWX_RtwK-LhXJOFPooNscdlGw).

Docker Workshop'una katıldığım ve uygulamada bize verilen klavuz yönergesi şu şekildeydi:
1. https://labs.play-with-docker.com/ adresine giderek yapacağımız örneğin ilk adımıdır. bu adreste canlı bir sürüm bizi karşılıyor.
2. add new instance seçneği oluşturulan ortam ile gelen terminalde şunu çalıştır:
~~~bash 
docker run -dp 80:80 dockersamples/101-tutorial
~~~ 
3. Kontenerı başlamasını bekleyin ve bitince en üstte sağda açılan 80 port bağlantısına tıklayarak tutoriala ulaşabilirsiniz. 
4. Have fun! 🐳

İkinci adımda gelişitirici ve öğrenmek için deneyen kişilere verilen çalışma alanı bulunmaktadır. BUrada ki alanda biz örnek oluşturduğumuzda, oturum 4 saat sonra siliniyor. Tekrar tekrar alanlar oluşturma imkanınız olduğu için verilen sürelerde istediiniz gibi kurcalayıp silip yeniden örnekler oluşturabilirsiniz. İyi eğlenceler.


Yukarda çalıştırdığım komut ile bana verdiği 80 port bağlantısıyla tutorialı başlattığım komut şuydu:
~~~bash 
docker run -dp 80:80 dockersamples/101-tutorial
~~~   
bu komuttaki ki flag'lerin açıklaması:
  - **-d** : containerı bağımsız modda, arkaplanda çalıştırır.
  - **-p 80:80** : dünyaya açmak istediğm portu (sunucu) uygulamanın dinledği port ile eşleştir.
  - **dockersamples/101-tutorial** : çalıştırılan imaj.


## **Container nedir?**

Yukarda ki komut ile artık bir konteyner çalıştırdım.

**Peki konteyner nedir?**  
Container, ana makinedeki diğer tüm proseslerden izole edilmiş olan sadece senin makinende çalışan prosese verilen isimdir. Bu izolasyon, Linux'ta uzun zamandır var olan kernel ad ve gruplarını kullanıyor. Docker, bu özellikleri ulaşılabilir ve kullanımı kolay hale getirmek için çalışmıştır.

##  🔺 Docker Nedir ? Neden herkes bunu hakkında konuşuyor...

dockerı en sade biçimde anlatırsam, öncelikle gökten bir bilgisayar iniyor...  

Bilgisayarımızın içerisinde farklı servisler çalıştırmak istiyoruz diyelim ki. Farklı servislerin çalıştırabileceği en küçük birimde prosesdir. 
 - İstiyoruz ki ; bunlar çalıştırığında birbiriyle etkileşime girmesin,
 - sadece belirli yüzey aralıklarında yada belirli bir port üzerinden çalışsın,
 - biri bozulduğunda diğeri bundan etkilenmesin.
 bu istekleri önceden yapmanın en kolay yolu fiziksel ayrı makinelerle oluyordu.(pahalı + fiziksel makinaların çoğu kullanılmaz hale geldi.)

İçine sanal makine (VM) kurulduğunda : 
 - izolasyon güzel ama o sanal makineyi çalıştıracak VM'in ağırlığı oluşmuştur. 
 - üzerine onun içerisinde çalışan işletim sisteminin üzerine bir işletim sistemi daha kuruluyor. bir işletim sistemi varken birde uygulamalarin her birine ayrı işletim sistemi kuruluyor.

Docker, VM'in yaptığını kernel seviyesinde yapma amaçlı çıkıyor. Linux kernel seviyesinde(çekşrdek seviyesi), izolasyon yapıyor. İşletim sistemi seviyesinde 
bunlar birbirini görmesinler yani işletim sistemi seviyesinde dünyaya baktıklarında sadece kendilerini görsünler düşüncesi üzerine kurulmuştur.
Docker, yazılım geliştirme döngüsünün geliştirme aşaması ile dağıtım aşamasına gelene kadar geçen süre zarfını azaltan bir araçtır.

Docker ve VM aynı gibi görünmektedir. Disk ve ram koyulsa bir fark yok gibi görünüyor. Aslında büyük farklılıkları var: 
- sanallaştırma , izolasyon , kaynak tasarrufu , güvenlik gibi

Docker kendi uygulamamızı yanında olan bir diğerine karıştırmadan çalıştırmayı  **daha iyi, daha temiz, daha verimli** yapıyor. Maliyeti uygun ve yapmak daha kolay. Tekrar tekrar kullanılabilir ve en önemli olan; sadece bir şey yap ve onu en iyi yap (Unix felsefesi) tüm felsefe ; herkes tek işi yapsın ve aradaki koordinasyonu iyi belirlesin.

**Docker Mantığı** ; uygulama geliştiricilere uygulamayı iyi paketlemesini söylerken, birde:
 "ben bunu her yerde çalıştırdığımda bana teslim ettiğin gibi çalışır halde bulacaksın"ın garantisini veriyor.

*happy cycling* 🙂 (*"Mutlu son olmasın, mutlu sonsuz olsun" mottomu savunur nitelikte 💪 )*

Docker'ında temel mottosu anladığım kadarıyla : "sen uygulamayı build et, paketle, ben bunu her yerde çalıştırıcam".

Docker;
    ✔ ️ Diğer işlemleri kesintiye uğratmadan çalışan birbirinden izole çalışan hava geçirmezkonteynerdır. Bu da aynı anda istediğiniz kadar konteyner çalıştırabilmenizi sağlar. 
    ✔ ️ Docker konteynerları paylaşılabilir'dir. 
    ✔ Birkaç docker komutu çalıştırmanız gerekiyor ve uygulama çalışmaya hazır. Ortam kurulumları için zaman harcamanıza gerek yok. 
    ✔ Docker ile çalışmak, Docker konteynerlerini oluşturabileceğiniz ve çalıştırabileceğiniz ve hatta Swarm modu gibi Docker özellikleriyle kümeler oluşturabileceğiniz bulutta ücretsiz bir Linux sanal makinesine sahip olma deneyimini sunar.

##  🔺Container Image Nedir?

Bir konteyner çalıştırırken, yalıtılmış bir dosya sistemi kullanır. Bu özel dosya sistemi bir konteyner image tarafından sağlanır.

Image container  dosya sistemini içerdiğinden, bir uygulamayı çalıştırmak için gereken her şeyi (tüm bağımlılıklar, yapılandırma dosyaları, komut dosyaları, ikili dosyalar gibi) içermelidir 

image ayrıca konteyner için ortam değişkenleri, çalıştırılacak varsayılan komut ve diğer meta veriler gibi başka yapılandırmalar da içerir.


Docker Uygulama ve anlatımım sonraki yazımda bu linkten ulaşabilirsin !

***
