---
title: #1 Foursquare API 📍
image: /assets/img/blog/fApi.png

description: >

---

###  Foursquare APİ 

Çeşitli türlerde bir mekanı arama, o mekanı keşfetme,  veya bir Foursquare kullanıcısını keşfetme, coğrafi bir yeri keşfetme ve bir konum etrafında ki trend mekanı bulma isteği için bir URL(internette karşılığı olan standart karakter dizisi) oluşturmalıdır.

Gelişitiricilere projelerinde güncel konum verilerini dahil ederek farklı projeler geliştirmeleri için Foursquare api araçlar sunmaktadır. 

Verileri kullanabilmemiz için bazı gerekli kütüphaleri projemize dahil etmemiz lazım:

 - request			(istekleri iletmek için gerekli kütüphane)  
 - geopy.geocoders       (bir adresi enlem ve boylam değerlerine dönüştürmek için)
 - pandas.io.json            (json verilerini panda veri çerçevesi kütüphanesi ile görselleştirme)
 
**📍 Foursquare Kimlik Bilgilerini ve Sürümünü Tanımla**

Öncelikle [şu linkten](https://developer.foursquare.com/)

Foursquare geliştirici hesabı oluşturmanız için sizi yönlendirecektir. 
Kayıt olduktan sonra sizin uygulamanıza özel kimlik bilgilerinizi elinizde bulunduracağınız uygulama oluşturmanızı sağlayacaktır.
 

👉CLIENT_ID =  'Foursquare ID Değeri'

👉CLIENT_SECRET =  'Foursquare Secret Değeri'

👉VERSION =  '20191201'     #foursquare sürümü


Olduğunuz konumda etrafınızda ki belirli kategori, belirli bir alan içindeki veya aratmak istenilen kelimelerin bulunduğu mekanları listeleyebilmektedir.

Foursquare Mekan Kategori listesi belli bir hiyerarşide geliştiricilere sunulmuştur. Sizlerde dökümantasyonunda [şu linkte](https://developer.foursquare.com/docs/build-with-foursquare/categories/)  görüntüleyebilir ve projelerinize belirtilen kurallar çerçevesinde dahil edebilirsinizz.

[Apı nedir](https://sumeyyekilic.github.io/hydejack/2020-05-01-api-nedir/) yazımda anlattığım gibi Foursquare Api'ıda  bizlere biçimlendirilmiş bir JSON tipinde veri döndürür.

Bunun için sorgulama türlerine ve kullanabileceğimiz parametrelerinin yordamlarına [şu linkten](https://developer.foursquare.com/docs/api-reference/venues/search/) ulaşabilirsiniz.
belirtilen url formatına uygul tanımladığımız url değişkenimizin sonuna istediğimiz türden parametre ekleyebiliriz.

bu şekilde sorgumuzu http client sayesinde iletiriz. Foursquare api den bize dönen yanıtı istediğimiz parametreler ile özelleştirip sunabiliriz.

📍Bir örnek üzerinden yelpazeyi açmaya çalışacağm..

Bir hastanenin enlem ve boylam koordinatlarına dönüştürme ile başladım: 

Geocoder ile bir örnek tanımlamak için, bir user_agent tanımlamamız gerekir. Bunu foursquare_agent ile gösterdim:
adres parametresine ise Göstepe araştırma hastanesinin adresini yazarak enlem ve boylam bilgilerini şu şekilde aldım :
 
~~~python
from geopy.geocoders import Nominatim

CLIENT_ID ='******************'
CLIENT_SECRET ='************************'

VERSION ='20191201'
adres = 'Eğitim Mahallesi Dr. Erkin Caddesi, Kadıköy, tr'
  

geolocator = Nominatim(user_agent="foursquare_agent")
location = geolocator.geocode(adres)

enlem = location.latitude
boylam = location.longitude
print(enlem, boylam)
 ~~~
 **output**:

     40.9844887 29.0586383
     
  istediğim şekilde enlem ve boylam parametrelerini bana getirdi.


### 1. Belirli Bir Mekan Kategorisi için Arama:

`https://api.foursquare.com/v2/venues/)**search**?client_id=**CLIENT_ID**&client_secret=**CLIENT_SECRET**&ll=**LATITUDE**,**LONGITUDE**&v=**VERSION**&query=**QUERY**&radius=**RADIUS**&limit=**LIMIT**
`


 📝🌟 **Hastaneye 500 metre mesafedeki türk yemek yerlerini aramak için bir sorgu tanımlayalım.**

**#belirli bir mekan kategorisi arama**

search_query='ev yemekleri'

**#radius istenen yeri 10.000km ye kadar sınırlar**

radius=500

İlgili Url'i tanınlama: Aşağıdaki inputta önceden tanımlanan yada hesaplanan lokasyon verilerine göre format metodu ile URL standardına atanır..

~~~bash 
url = 'https://api.foursquare.com/v2/venues/search?client_id={}&client_secret={}&ll={},{}&v={}&query={}&radius={}&limit={}'
.format(CLIENT_ID, CLIENT_SECRET, latitude, longitude, VERSION, search_query, radius,LIMIT)
print(url)
~~~
output:
~~~bash
sum@sumaray:~/Desktop/api$ python api12.py

https://api.foursquare.com/v2/venues/search?client_id=PGBQWU3LLONODVNJ3DAOCU0WCO1UVCENQJ0M0W1FUYKJZQHB&client_secret=13WART3RQMCHJF3IUGKQXMP4DVW5ALUPVEFKNDX1J0NG0GXB&ll=40.9844887,29.0586383&v=20180604&query=Turkish&radius=500&limit=30
~~~

Buradan aldığım url'yi sonuçları json türünden listelemek için kullanacağım.
 
 ### **📝 Get isteği ile ilgili sonuçları getirme:**
 
results = requests.get(url).json()
print(result)

Göstepe hastanesi mekanına radius değerine atadığım uzaklıkta ki ve limit parametresine verdiğim değer ile yukarda bir url tanımlamıştım.
Bu parametre ile bana ev yemekleri mekanlarını parametreler aracılığıyla getirmesini istediğim sonuçları json formatında görüntüleyelim:

~~~python
import requests
from geopy.geocoders import Nominatim
CLIENT_ID ='*************************'
CLIENT_SECRET ='**************************'
VERSION ='20191201'
LIMIT= 3
adres = 'Eğitim Mahallesi Dr. Erkin Caddesi, Kadıköy, tr'

#adresin enlem ve boylam bilgilerini
geolocator = Nominatim(user_agent="foursquare_agent")
location = geolocator.geocode(adres)
latitude = location.latitude
longitude =location.longitude
search_query='ev yemekleri'
radius=500

#gerekli parametreler ile birliktee url'yi tanımlama 
url = 'https://api.foursquare.com/v2/venues/search?client_id={}&client_secret={}&ll={},{}&v={}&query={}&radius={}&limit={}'.format(CLIENT_ID, CLIENT_SECRET, latitude, longitude, VERSION, search_query, radius, LIMIT)

#get isteği ile url sonuçlarını inceleme(json formatında)
results = requests.get(url).json()
print(results)
~~~

output:

~~~bash
sum@sumaray:~/Desktop/desktop/api$ python api13.py
{'meta': {'code': 200, 'requestId': '5ec93a04c94979001b216663'}, 'response': {'venues': 
[{'referralId':'v-1590245923', 'location': {'country': 'Türkiye', 'cc': 'TR', 'city': 'İstanbul', 'lng': 29.059884316778895, 'lat': 40.98233458770847, 'distance': 261, 'labeledLatLngs': [{'lng': 29.059884316778895, 'lat': 40.98233458770847, 'label': 'display'}], 'formattedAddress': ['İstanbul', 'Türkiye'], 'state': 'İstanbul'}, 'hasPerk': False, 'id': '5061bb4ee4b0acb17101a45b', 'name': 'Öznur Cafe Ev Yemekleri', 'categories': [{'shortName': 'Turkish Home Cooking', 'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/turkish_', 'suffix': '.png'}, 'primary': True, 'id': '5283c7b4e4b094cb91ec88d4', 'pluralName': 'Turkish Home Cooking Restaurants', 'name': 'Turkish Home Cooking Restaurant'}]}, {'referralId': 'v-1590245923', 'location': {'country': 'Türkiye', 'cc': 'TR', 'address': 'Mustafa Mazharbey Cd.', 'city': 'İstanbul', 'lng': 29.060172397394417, 'lat': 40.98385667598501, 'distance': 146, 'labeledLatLngs': [{'lng': 29.060172397394417, 'lat': 40.98385667598501, 'label': 'display'}], 'formattedAddress': ['Mustafa Mazharbey Cd.', 'İstanbul', 'Türkiye'], 'state': 'İstanbul'}, 'hasPerk': False, 'id': '4f4cb5d4e4b0b0a21387c252', 'name': 'Lezzet Durağı Ev Yemekleri', 'categories': [{'shortName': 'Mexican', 'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/mexican_', 'suffix': '.png'}, 'primary': True, 'id': '4bf58dd8d48988d1c1941735', 'pluralName': 'Mexican Restaurants', 'name': 'Mexican Restaurant'}]}, {'referralId': 'v-1590245923', 'location': {'country': 'Türkiye', 'cc': 'TR', 'lng': 29.059738, 'lat': 40.982221, 'distance': 268, 'labeledLatLngs': [{'lng': 29.059738, 'lat': 40.982221, 'label': 'display'}], 'formattedAddress': ['Türkiye']}, 'hasPerk': False, 'id': '534bbb07498eafa1e7017090', 'name': 'Tevatir Cafe & Ev Yemekleri', 'categories': [{'shortName': 'Turkish', 'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/turkish_', 'suffix': '.png'}, 'primary': True, 'id': '4f04af1f2fb6e1c99f3db0bb', 'pluralName': 'Turkish Restaurants', 'name': 'Turkish Restaurant'}]}]}}
~~~

Yukarda ki örnekte json formatında anahtar değer ilişkisiyle bize gelen veriler pek anlamlı değil ve açıkcası anlaması biraz zahmetli.
Bunu daha anlaşılır kılmak için panda numpy gibi çeşitli veri ktüüphaneleri vardır. 

**📝 JSON'un ilgili bölümünü alarak onu bir panda veri çerçevesine dönüştürelim**
**#JSON'un ilgili bölümünü alanlara atamak**
venues = results['response']['venues'] 

 **#değerleri veri çerçevesine dönüştürme**
dataframe = json_normalize(venues)
dataframe.head()


Bize daha anlamlı veri çerçevesi vermesi adına Panda kütüphanesi ile  json meta formatındaki verileri alıp daha anlamlı hale dönüştürelim. 

~~~python
from pandas.io.json import json_normalize
import requests
from geopy.geocoders import Nominatim
CLIENT_ID ='******************'
CLIENT_SECRET ='********************'
VERSION ='20191201'
LIMIT= 30
adres = 'Eğitim Mahallesi Dr. Erkin Caddesi, Kadıköy, tr'

#adresin enlem ve boylam bilgilerini
geolocator = Nominatim(user_agent="foursquare_agent")
location = geolocator.geocode(adres)
latitude = location.latitude
longitude = location.longitude
search_query='ev yemekleri'
radius=500

#gerekli parametreler ile birliktee url'yi tanımlama
url = 'https://api.foursquare.com/v2/venues/search?client_id={}&client_secret={}&ll={},{}&v={}&query={}&radius={}&limit={}'.format(CLIENT_ID, CLIENT_SECRET, latitude, longitude, VERSION, search_query, radius, LIMIT)

#get isteği ile url sonuçlarını inceleme
results = requests.get(url).json()

#JSON'un ilgili bölümünü edinip
#pandas veri çerçevesine dönüştürme
venues=results['response']['venues']

dataframe=json_normalize(venues)

#json bölümünü getirip bunları
#pandas veri çerçevesi(dataframe) ile gösterne 
print(dataframe.head())
~~~

output:

                                              categories  hasPerk  ...                         name    referralId
    0  [{'id': '5283c7b4e4b094cb91ec88d4', 'pluralNam...    False  ...      Öznur Cafe Ev Yemekleri  v-1590245562
    1  [{'id': '4bf58dd8d48988d1c1941735', 'pluralNam...    False  ...   Lezzet Durağı Ev Yemekleri  v-1590245562
    2  [{'id': '4f04af1f2fb6e1c99f3db0bb', 'pluralNam...    False  ...  Tevatir Cafe & Ev Yemekleri  v-1590245562
    3  [{'id': '52e81612bcbc57f1066b7a00', 'pluralNam...    False  ...    Palmiye Cafe Ev Yemekleri  v-1590245562
    4  [{'id': '52e81612bcbc57f1066b7a00', 'pluralNam...    False  ...           Derin Ev Yemekleri  v-1590245562
    
    [5 rows x 17 columns]


📝 Daha sade bir gösterim ile sadeleştirme yapalım. 
Siz ilgilendiğiniz bilgileri tanımlabiyalirsiniz. 
Son olarak dataframe ile en yakın 5 mekanı name ve id parametreleri ile filtrelmele yapacağımm :

~~~python
from pandas.io.json import json_normalize
import requests
from geopy.geocoders import Nominatim
CLIENT_ID ='******************'
CLIENT_SECRET ='**************'
VERSION ='20191201'
LIMIT= 5
adres = 'Eğitim Mahallesi Dr. Erkin Caddesi, Kadıköy, tr'

#adresin enlem ve boylam bilgilerini
geolocator = Nominatim(user_agent="foursquare_agent")
location= geolocator.geocode(adres)
latitude = location.latitude
longitude = location.longitude
search_query='ev yemekleri'
radius=500
#gerekli parametreler ile birliktee
#url'yi tanımlama ve ekrana bastırma
url = 'https://api.foursquare.com/v2/venues/search?client_id={}&client_secret={}&ll={},{}&v={}&query={}&radius={}&limit={}'.format(CLIENT_ID, CLIENT_SECRET, latitude, longitude, VERSION, search_query, radius, LIMIT)

#get isteği ile url sonuçlarını inceleme
results = requests.get(url).json()

#JSON'un ilgili bölümünü edinip
#pandas veri çerçevesine dönüştürme

venues=results['response']['venues']

dataframe=json_normalize(venues)

#istenen bilgileri tanımlayıp
#dataframe'de gösterme

filtered_columns = ['name', 'categories'] + [col for col in dataframe.columns if col.startswith('location.')] + ['id']
dataframe_filtered = dataframe.loc[:, filtered_columns]

#mekan kategorisini getiren fonk
def get_category_type(row):
    try:
        categories_list = row['categories']
    except:
        categories_list = row['venue.categories']
        
    if len(categories_list) == 0:
        return None
    else:
        return categories_list[0]['name']

#her satır için kategoriyi filtrelet
dataframe_filtered['categories'] = dataframe_filtered.apply(get_category_type, axis=1)

# Yalnızca son terimi koruyarak sütun adlarını temizle
dataframe_filtered.columns = [column.split('.')[-1] for column in dataframe_filtered.columns]
print(dataframe_filtered)
~~~

output:
~~~bash
sum@sumaray:~/Desktop/desktop/api$ python api15.py
                                    name  ...                        id
0                Öznur Cafe Ev Yemekleri  ...  5061bb4ee4b0acb17101a45b
1             Lezzet Durağı Ev Yemekleri  ...  4f4cb5d4e4b0b0a21387c252
2            Tevatir Cafe & Ev Yemekleri  ...  534bbb07498eafa1e7017090
3              Palmiye Cafe Ev Yemekleri  ...  544b806f498e693acaf9cc90
4                     Derin Ev Yemekleri  ...  58d261ff3731817f30d3559f
[5 rows x 14 columns]
~~~

🏹Buradan aldığım mekanın ismi ve id'si ile o mekana dair yapılan yorumlar verilen değerlendirme puanları, 
anlık olarak mekanda kimlerin bulunduğu ve yapılmış yorumlar gibi daha spesifik bilgilere ulaşabileceğim. 
Bunu bir sonraki yazımda örnek üzerinden devam edeceğim.