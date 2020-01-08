---
title: #DOCKER 101 - Django Uygulaması ile Container Image Oluşturma ve Çalıştırma 🐳
image: /assets/img/blog/docker2.jpg
description: >
---


# #docker101- Django Uygulaması ile Container Image Oluşturma ve Çalıştırma 🐳️

Önceki yazım Docker 101-workshop Klavuzumun devamı için, kendi Django uygulamam ile çalışacağım.

**Başlayalım!**

#[pwd](https://labs.play-with-docker.com) İçerisinde Kendi Uygulamanızı Başlatma

Öncelikle:

~~~sh 
[node1] (local) root@192.168.0.48 ~
$ pwd
/root
~~~

Yazdığım pwd komutu bize hangi dizinde (klasörde) olduğunuzu söyledi !

Burada python ile yazdığım bir web uygulamamı kullanacağım. (dilerseniz başka dilde yazılış bir uygulama/uygulamanız üzerinden uygulayabiirsiniz. Django uygulamamı çalıştırmadan önce, kaynak kodunu Play with Docker ortamına almamız gerekmektedir. 

Gerçek proje için uygulamamı indirip onun üzerinden benimle birlikte takip etmek için ;
- github hesabımdaki [Foursquare api ile django uygulamamı](https://github.com/sumeyyekilic/FoursquareAPI_DjangoApp) kullanmak istersneiz Clone butonundan **zip download** deyip  indirin.
- Veya django repomu terminalden ` git clone https://github.com/sumeyyekilic/FoursquareAPI_DjangoApp` komutu ile bilgisayarınıza indirebilirsiniz (Ancak, bu durumda indirdiğin klasörü ZIP'e çevirmen gerekecektir. Çünkü pwd 'de oluşturduğumuz ortama proje zip ile yüklenebiliyor.)

Bir Uygulama Üzerinden sizinde uygulamanız için şu adımları takip ediniz:

1. https://github.com/sumeyyekilic/FoursquareAPI_DjangoApp []  Docker ile Play'e yüklenmesi: 
*önerildiği şekilde, uygulama dosyasını (veya başka bir dosyayı) PWD'deki terminale sürükleyip bırakabilirsiniz.*

2. pwd'den zip dosyasını çıkartın:
~~~bash 
[node1] (local) root@192.168.0.18 ~
$ unzip app1.zip
...
~~~
3. Çalışma dizininizden, zipten çıkarttığınız uygulama klasörüne gidin.
`(ben dfAPIs isimli uygulama klasörüme geçtim)`
~~~bash
[node1] (local) root@192.168.0.18 ~
$ ls
app1.zip  dfAPIs 

[node1] (local) root@192.168.0.18 ~
$ cd dfAPIs
[node1] (local) root@192.168.0.18 ~/dfAPIs
~~~
4. Bu dizinde [node1] tabanlı uygulamanızı ls komutu ile görüntüleyin.
~~~sh
[node1] (local) root@192.168.0.18 ~/dfAPIs
$ ls
dfAPI  venv
~~~
~~~bash
//django uygulamamda sanal ortamı aktif edip bu aşamada şu şekilde ilerledim:
[node1] (local) root@192.168.0.18 ~/dfAPIs
$ source venv/bin/activate
(venv) [node1] (local) root@192.168.0.18 ~/dfAPIs
$ cd dfAPI/
~~~
- Proje dizinimi görüntülersem şu şekilde :
~~~bash
(venv) [node1] (local) root@192.168.0.18 ~/dfAPIs/dfAPI
$ ls
Android           db.sqlite3        manage.py         static
Images            dfAPI             requirements.txt  staticfiles
Procfile          dfas              runtime.txt       templates
~~~

# Uygulamanın Container Image'ını Build etme

Uygulamayı oluşturmak için bir **Dockerfile** kullanmamız gerekiyor. 
_**Dockerfile, bir container image oluşturmak için kullanılan metin tabanlı bir komut dosyasıdır.**_

Eğer dockerfiles daha önceden oluşturduysanız, aşağıdaki Dockerfile içinde birkaç hata görebilirsiniz. Bu seride bunun üzerine gideceğiz.

1. Öncelikle aşağıdaki içeriği ekleyerek Dockerfile adlı bir dosya oluşturun.
Termianlde: $ touch dockerfile komutuyla dosyayı oluşturdum. bu PWD içerisindeki terminalin üzerinde gelişitirciye tanınmış bir Editor seçeneği düşünülmüş.BUradan dockerfile dosyamın içerisine django projem için şu eklemeleri yazdım:
~~~bash
FROM python:3.7.4-alpine3.10

ADD djAPIs/requirements.txt /app/requirements.txt
#uygulamalarımızın bağımlılıklarının görüntünün dosya sisteminde kullanılabilmesi için requirements.txt dosyasını /app/requirements.txt dosyasına kopyalayacaktır.

RUN set -ex \
    #Alpine’nin apk paket yöneticisini kullanarak PostgreSQL geliştirme dosyalarını ve temel derleme bağımlılıklarını yükleyin
    && apk add --no-cache --virtual .build-deps postgresql-dev build-base \
    #Sanal ortam oluşturma
    && python -m venv /env \
    #Pip ile needs.txt dosyasında listelenen Python bağımlılıklarını yükleyi
    && /env/bin/pip install --upgrade pip \
    #Kurulu Python paketlerinin gereksinimlerini analiz ederek çalışma zamanında ihtiyaç duyulan paketlerin bir listesini derleyin
    && /env/bin/pip install --no-cache-dir -r /app/requirements.txt \
    #Gereksiz derleme bağımlılıklarını kaldırın, her bir adımı run etmek yerine birbirine bağladıkk
    && runDeps="$(scanelf --needed --nobanner --recursive /env \
        | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
        | sort -u \
        | xargs -r apk info --installed \
        | sort -u)" \
    #Her ADD, COPY ve RUN komutu için Docker, mevcut dosya sisteminin üstünde yeni bir görüntü katmanı oluşturur, 
    # talimatı yürütür ve ardından ortaya çıkan katmanı kaydeder. 
    && apk add --virtual rundeps $runDeps \
    && apk del .build-deps
#run komutunun ardından
#uygulama kodunu kopyalamak için ADD ve 
ADD djAPIs /app
# görüntünün çalışma dizinini kod dizinimize ayarlamak için WORKDIR kullanırız.
WORKDIR /app
#ENV komutunu, imajımızdan ortaya çıkan container'larda mevcut olacak iki ortam değişkeni ayarlamak için kullanırız
# bu iki satır, bir sanal ortamı etkinleştirmenin geleneksel yöntemi olan /env/bin/activate komut dosyasını hazırlayıp sonuçlarını bize sunar..
ENV VIRTUAL_ENV /env
ENV PATH /env/bin:$PATH
#Docker'ı konteynerin çalışma zamanında 8000 bağlantı noktasında dinleyeceğini bildirmek için EXPOSE kullanırız.
EXPOSE 800
~~~ 
bu yazdığım django için docker image kullandığım referansa [şu](https://www.digitalocean.com/community/tutorials/how-to-build-a-django-and-gunicorn-application-with-docker) linkten ulaşabilirsin.

2. Docker build komutunu kullanarak container image oluşturun.

`docker build -t dj-foursquare .  
` //burada dj-foursquare kendi belirlediğimiz imaj ismi
~~~bash
(venv) [node1] (local) root@192.168.0.13 ~/dfAPIs/dfAPI
$ docker build -t dj-foursquare .
.
.
Successfully built cb58c2f896fd
Successfully tagged dj-foursquare:latest
~~~
Buraya kadar başarıyla imaj oluşturmuş oldum !

Bu komut, yeni bir container image'i oluşturmak için Dockerfile'ı kullandı. 
Bir çok katmanın indirildiğini fark ettim. 


# Uygulama Container'ımızı Başlatalım

Artık bir image'ım var ve uygulamayı çalıştırabilirim! 
Bunu yapmak için, docker run komutunu kullanacağız.

1. Docker run komutunu kullanarak container'ı başlatma:
` docker run -dp 3000:3000 foursquare 
` 
~~~bash
(venv) [node1] (local) root@192.168.0.13 ~/dfAPIs/dfAPI
$ docker run -dp 3000:3000 dj-foursquare
73e1d614a4ae26b9cef5e0c7868f0e26775265343b821b83f13c1d6ea40af497
~~~
PYthon projesi javascript veya başka diller gibi çalışmadığından oluşturduğum container image'ına ek olarak docker-compose eklemek gerekliymiş. Bunun için proje içerisine docker-compose.yml isimli dosya oluşturdum :
~~~bash
(venv) [node1] (local) root@192.168.0.13 ~/dfAPIs/dfAPI
$ touch docker-compose.yml
~~~
**docker-compose.yml** içerisine [araştırmam sonucu](https://docs.docker.com/compose/django/) editörden şu eklemeyi yaptım:

~~~bash
version: '3'

services:
  db:
    image: postgres
  web:
    build: .
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/code
    ports:
      - "8000:8000"
    depends_on:
      - db
~~~
Projemizde bulunan requirements.txt dosyası oluşturduğum Dockerfile tarafından kullanılıyor. Bu yüzden tüm eklemeleri şu komutla içerisinde olması gerektiği teyit edilerek olmayan eklemeler de yapılmalıdır.
~~~bash
(venv) [node1] (local) root@192.168.0.13 ~/dfAPIs/dfAPI
$ pip install -r requirements.txt
~~~
2. Django projesini Oluşturma:

Bu adımda, image'ı önceki adımda tanımlanan komut devamında bir Django başlangıç projesi oluştururmuş olacağız.
- Proje dizininizin kök dizininde olduğunuzdan emin olun.

~~~bash
 $ sudo docker-compose run web django-admin startproject composeexample .
 Successfully built 5141e1e2715b
Successfully tagged dfapi_web:latest
~~~
bu aşamada önceki oluşturudğumuz imaj üzerine docker-compose oluşturduğumuz için  bize otomatik olarak djapi_web isminde yeniden imaj dosyasını yeniden build etti.

~~~bash
(venv) [node1] (local) root@192.168.0.13 ~/dfAPIs/dfAPI
$ docker run -dp 3000:3000 dfapi_web
f47bd3f243c2ea5ea215175ae1a92ea3e43109acbf50d53da4addc7cdc1b3927
~~~
Komutta kullanılan -d ve -p bayrakları, Yeni container için "ayrılmış" modda (arka planda) çalıştırıyor. Ana ilgisayarın 3000 numaralı bağlantı noktası ile container'ın 3000 numaralı bağlantı noktası arasında bir eşleme oluşturuyoruz.


3. Docker-compose run komutunu aşağıdaki gibi çalıştırarak Django projesini çalıştırın.

`docker-compose up
`

~~~bash
(venv) [node1] (local) root@192.168.0.13 ~/dfAPIs/dfAPI
$ docker-compose up
dfapi_db_1 is up-to-date
Creating dfapi_web_1 ... done
~~~

Uygulama çalıştırıldığı anda bir ekran görüntüsü aldım ve şu şekilde:

![foto](/assets/img/blog/docker.jpg)

[PWD](https://labs.play-with-docker.com) arayüzünün üst kısmındaki ilk uygulammda oluşan 80 port bağlantısının yanına "3000" linkli bağlantı daha eklendi.

Buna tıklayarak uygulamayı açtım ve sizde görmek isterseniz ekran görüntüsü:

![foto2](/assets/img/blog/docker.jpg)

❗Bu kısa bölümde, bir kapsayıcı görüntüsü oluşturmanın temellerini öğrendik ve bunu yapmak için bir Dockerfile oluşturduk. Bir görüntü oluşturduktan sonra, konteyneri başlattık ve çalışan uygulamayı gördük!


💎Bir sonraki blog yazımda , uygulamamın bazı yerlerinde kod değişikliği yapacağım ve çalışan uygulamamın yeni bir image ile nasıl güncelleyeceğimi öğreneceğim ve bu linkte anlatacağım 