---

title: #DOCKER 101 - Uygulamaya Kaynak Kod Eklenmesi ve Container'ı Değiştirme 🐳

image: /assets/img/blog/docker3.jpg

description: >

---
Uygulamaya Kaynak Kod Eklenmesi ve Container'ı Değiştirme 🐳

Bir önceki [seri](https://sumeyyekilic.github.io/hydejack/2020-01-07-docker-uygulama/) de bir imaj oluşturup, konteyner başlatıp ve bunun üzerinden çalışan uygulamayı görmüştük.

Bu çalışan container üzerinden devam edeceğim. Çalışan konteynerları görüntülemek için pwd terminalinden:

  

~~~bash

(venv) [node1] (local) root@192.168.0.48 ~/dfAPIs/dfAPI

$ docker container ls

CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES

a5f68b6e32be dockersamples/101-tutorial "nginx -g 'daemon of…" 2 hours ago Up 2 hours 0.0.0.0:80->80/tcp ecstatic_hamilton

~~~

  

Uygulama içerisinde Değişiklik Yapma

  

    self.fields['venue'].widget.attrs['placeholder'] = 'bir mekan türü gir..'
    
      

yerine ;

  

    self.fields['venue'].widget.attrs['placeholder'] = 'önceki mekan türü için boş bırak..'
    
      

Sadece text değişikliğini yapıp save ettim.

  

## Kaynak Kodumuzu Güncelleme

1.Yukardaki kod satırını güncelledim

2.Daha önce kullandığımız komutu kullanarak görüntünün güncellenmiş sürümünü oluşturalım.

  

> docker build -t < container-name > .



~~~bash


venv) [node1] (local) root@192.168.0.48 ~/dfAPIs/dfAPI

$ docker build -t dj-foursquare .

Sending build context to Docker daemon 3.612MB

Step 1/7 : FROM python:3

--------

Successfully built 902eac983028

Successfully tagged dj-foursquare:latest

~~~

  

3.Güncellenmiş kodu kullanarak yeni bir container başlatalım.

  

~~~bash

(venv) [node1] (local) root@192.168.0.48 ~/dfAPIs/dfAPI

$ docker run -dp 3000:3000 dj-foursquare

1c5c773cef8fb48b5b5c30e906aeb34fdb21bf519f618ef0bff29e3c7e25140d

~~~

Buraya kadar, kaynak kod değişikliği ile birlikte yeni bir konteyner'ı başarıyla başlatabildim.📝
 
❗ Ancak ;

> docker: Error response from daemon: driver failed programming external
> connectivity on endpoint laughing_burnell

Yukadaki kod bloğundaki gibi hata alıyorsanız, eski konteynerın remove edilmesi gerekiyor.
Bu hatanın nedeni eğer bir container'ımız hala çalışıyosa yeni container başlatamıyoruz.
Benim çalıştırıdğım django uygulamam 8000 portunu kullanıyordu. Uygulamayı run ettikten sonra durdurdum ve değişiklikleri yapıp tekrar build ettim ve hata almadım. Fakat  başka dilde yazdığınızda portu kapatamayabilirsiniz ve arka planda sürekli açık kalabilir. 

💡Sonuç olarak şöyle ki, container'ın ana bilgisayarın bağlantı noktası 8000'i kullanması ve yalnızca bir işlemin (kaplar dahil) belirli bir bağlantı noktasını dinleyebilmesidir. Bunu düzeltmek için eski container'ı kaldırmamız gerekiyor. 

## 📝Eski Container'ımızın Değiştirilmesi

Bir containerı kaldırmak için, öncelikle o containerın durdurulması gerekir. Sonra çıkarılabilir.
  
1. `docker ps` komutu, container ıd'si ve diğer kimlik bilgilerini bize liste olarak getirir.

~~~bash

[node1] (local) root@192.168.0.8 ~
$ docker ps
CONTAINER ID        IMAGE                        COMMAND                  CREATED             STATUS              PORTS                NAMES
74fab2442359        dockersamples/101-tutorial   "nginx -g 'daemon of…"   45 minutes ago      Up 45 minutes       0.0.0.0:80->80/tcp   charming_hopper
~~~


2.Container'ı durdurmak için `docker stop < container-id >` komutunu kullanın.

~~~bash
[node1] (local) root@192.168.0.8 ~
$ docker stop 74fab2442359
74fab2442359

~~~

3.Container'ı durduktan sonra `docker rm < container-id >` komutunu kullanarak kaldırabilirsiniz.

~~~bash

docker rm < container-id >

~~~

4.Güncellenmiş uygulamayı başlatın.
Uygulamayı başlatmadan önce login olmanızı isteyecektir. `docker login` yazarak giriş bilgilerinizi doğrulayın ve aşağıdaki gibi uygulamanızı başlatabilirsiniz.

~~~bash

docker run -dp 3000:3000 docker-name

~~~
  

Açılan port ile uygulamanızı açtığınızda güncellenmiş halini göreceksiniz.
 

***

Sonraki yapılacak adımlarda kalıcılıktan bahsetmeden önce, bu imajları başkalarıyla nasıl paylaşacağımızı göreceğiz.