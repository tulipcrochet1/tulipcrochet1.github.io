---

title: #DOCKER 101 - APP Paylaşımı 🐳

description: >

---

App'imizin Paylaşımı


Önceki serilerde image yani görüntü oluşturmuştuk. Şimdi bunu paylaşalım! 
Bu uygulamada uygulamamızı kalıcı olarak paylaşmayı ve başka ortamlarda çalıştırmayı göreceğiz..

Docker images'larını paylaşmak için **Docker registery** kullanmanız gerekir. Varsayılan register Docker Hub'tır. 
Nedir bu Docker Hub? Kullandığımız tüm images'ların geldiği yerdir.   Çalışma sonucu ürettiğimiz Image’larda Docker Registry de tutulur.

Docker bütün açık kaynak sistemler gibi paylaşıma özendirmesi onu daha işlevsel ve kıymetli hale getirmiştir. DockerHub ile takımların geliştirip oluşturduğu görüntüler(image) herhangi bir ücret talep edilmeksizin sınırsız indirilebilmektedir. Oluşşturulan image'ı yüklemek ve indirmek herkese açık olarak ücretsiz yükleme yapılabilirken , kişiye özel kapalı kaynaklı image'ler 5 taneden sonra ücretlendirilmektedir.
  

### Repo oluşturma

1.Bir imagess'ı push etmek için önce Docker Hub'da bir repo oluşturmamız gerekir.
2.[Docker hub](https://hub.docker.com/)'a (giriş yapın).

- Repo Oluştur (Create Repository ) butonuna tıklayın.
[foto1](/assets/img/create-repo.jpg)
- Kendi Repo adınızı yazın, ben `django-app` kullandım. Visibilty alanının Public seçili olduğunu teyit edin.
- Oluştur düğmesini tıklayın!
[foto1](/assets/img/repo-name-and-create(1).png)

 Sayfanın sağ tarafına bakarsanız Docker komutları adlı bir bölüm görürsünüz. Burada , repoya push etmek için çalıştırmanız gereken bir örnek komut verir.
[foto1](/assets/img/docker-run.png)


## Image'ımızı Push Edelim

1.PWD örneğime geri dönüp, komutu çalıştırmayı deneyelim.
KOmutu çalıştırdığımızda şu hatayı alıyoruz:

~~~bash
[node1] (local) root@192.168.0.23 ~
$ docker push sumk/django-app:tagname
The push refers to repository [docker.io/sumk/django-app]
An image does not exist locally with the tag: sumk/django-app
~~~
Docker bana sumk/django-app:  tagi ile yerel olarak bir image mevcut olmadığını söylüyor. Peki Neden? 
`docker push sumk/django-app:tagname` burada push komutu docker sumk/django-app:tagname adlı bir görüntü aradı ve bulamadı. 
bundan emin olmak için image'ları listeleyelim. Sizde`docker ımage ls`komutunu pwd terminalinde çalıştırarak teyit edebilirsniz


Bunu düzeltmek için, image'ımızı "tag" vermemiz gerekir, Temel olarak başka bir isim vermeyi deneyelim.

2.`docker login -u kullanıcıAdı` komutunu kullanarak Docker hub'a giriş yapın.  

3.Uygulama image'ına yeni bir ad vermek için `docker tag` komutunu girin. Burda kullanıcı adı kısmına, tanımlı olan Docker id'nizi gireceksiniz
~~~bash
[node1] (local) root@192.168.0.23 ~
$ docker tag dockersamples/101-tutorial sumk/django-app:tagname
~~~
  
Şimdi push komutunuzu tekrar deneyin. Eğer docker Hub'dan değeri kopyalıyorsanız, image adına bir etiket eklemediğimiz için tag adı bölümünü boş bırakabilirsiniz.

docker push sumk/django-app


### Image'imizi Yeni Bir Instance Üzerinde Çalıştırma¶

Artık bu aşamaya kadar imajımız oluşturuldu ve bir docker hub'a aktardık.

Image'ı yeni bir instance üzerinde çalıştırmak demek; bizim kontainerımızı daha önce hiç görmemiş bir alan üzerinde çalıştırmak demek!
Bunun için izleyeceğimiz adım çok basit:

1.PWD terminal sayfamızda yeni bir instance oluşturmak için add new instance 'a  tıklayın.
[foto1](/assets/img/new-instance.png)

2.Yeni alanda, push edilen uygulamayı başlatmak için: 

~~~bash
 docker run-DP 3000: 3000 sumk/django-app
~~~

3.Üstte port alanına 3000 linki gelektir. Buna tıklayarak değişiklikler ile uygulamanızı görmüş olacaksınız.

