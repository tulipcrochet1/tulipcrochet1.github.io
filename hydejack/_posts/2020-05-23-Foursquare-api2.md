---
title: #2 Foursaure Api- Mekanı Keşfetme 
image: /assets/img/blog/fapi2.png

description: >

---
**##  2. Belirli Bir Mekanı Keşfetme 📍**

**### 2.A  En Yakın Mekanı Tanıma**

> `https://api.foursquare.com/v2/venues/`**VENUE_ID**`?client_id=`**CLIENT_ID**`&client_secret=`**CLIENT_SECRET**`&v=`**VERSION**

Bir önceki Foursquare Api yazı serimde istenilen bir konuma , istenilen türde en yakın mekanların isimleri ve id'lerini panda ile listelemiştik.
Şimdi ise o mekanlardan istediğimiz üzerinden o mekanı tanımak için çeşitli parametreler üzerinde çalışmalar yapmaya başlayabilriz.
 
**venue_id=" keşfedilmek istenen en yakın mekanın id'si "**

Url ile mekanı arama standart çıktısı aşağıdaki gibi yerleştirilerek, en yakın mekanın venue_id değeri söylenerek aranabilir
~~~python
url = 'https://api.foursquare.com/v2/venues/{}?client_id={}&client_secret={}&v={}'.format(**venue_id**, CLIENT_ID, CLIENT_SECRET, VERSION)
print(url)
~~~
output:

> 'https://api.foursquare.com/v2/venues/*******?client_id=*********&client_secret=*************&v=20191201'

Sonuçlar için GET isteği gönderilir:  

#girilen id değeri için tüm sonuçları getirmek için get request şu şekilde kullanılr
  

    result=requests.get(url).json()
    
    print(result['response']['venue'].keys())
    
    result['response']['venue']

Bir önceki yazımda ki örnekte dataframe ile filtrelediğim mekan ve id listesinden
**`0                Öznur Cafe Ev Yemekleri  ...  5061bb4ee4b0acb17101a45b**
` 'nin hangi keys parametrelere sahip olduğunun hiyerarşisini ve keşfetmek için mekanın bilgilerini json türünde getirelim:

~~~python
import requests

import pandas as pd

from pandas.io.json import json_normalize

CLIENT_ID ='***************************'
CLIENT_SECRET ='*****************************'

VERSION ='20191201'

venue_id = '5061bb4ee4b0acb17101a45b' #öznur ev yemeklerinin id'si
limit = 150 #set limitinin toplam ipucu sayısından büyük veya ona eşit olması

url = 'https://api.foursquare.com/v2/venues/{}?client_id={}&client_secret={}&v={}'.format(venue_id, CLIENT_ID, CLIENT_SECRET, VERSION)

#sonuçları getirmek içn get isteği
result = requests.get(url).json()

print(result['response']['venue'].keys())
print(result['response']['venue'])
~~~

output:
~~~bash
sum@sumaray:~/Desktop/api$ python api19.py

  

dict_keys(['id', 'dislike', 'likes', 'ok', 'ratingSignals', 'reasons', 'createdAt', 'photos', 'inbox', 'allowMenuUrlEdit', 'ratingColor', 'popular', 'shortUrl', 'stats', 'listed', 'tips', 'hereNow', 'colors', 'specials', 'categories', 'attributes', 'canonicalUrl', 'verified', 'location', 'name', 'pageUpdates', 'rating', 'bestPhoto', 'contact', 'beenHere', 'timeZone'])

  

{'id': '5061bb4ee4b0acb17101a45b', 'dislike': False, 'likes': {'groups': [{'type': 'others', 'items': [{'id': '513094291', 'photo': {'suffix': '/513094291_r8-0B1Xx_TgFObKWEY0aNMga6z6jttrdQYQY9UxeuIkTmTr4S31O5ZaIstD_LoxFyPJ-n2WyA.jpg', 'prefix': 'https://fastly.4sqi.net/img/user/'}, 'lastName': 'Albayrak', 'firstName': 'İbrahim', 'gender': 'none'}, {'id': '88422156', 'photo': {'suffix': '/88422156-OQ4TQKVLBHPEFK5I.jpg', 'prefix': 'https://fastly.4sqi.net/img/user/'}, 'lastName': 'Kaya', 'firstName': 'Mustafa', 'gender': 'male'}, {'id': '64400929', 'photo': {'suffix': '/64400929_kCzrFE4n_Bvve9GiSFYjCGupNHGO5nx3MnUauILmWE2GW7Q7BQnsgrbGavC98IxJELPibuVLt.jpg', 'prefix': 'https://fastly.4sqi.net/img/user/'}, 'lastName': 'K&k', 'firstName': 'Şakir Kır', 'gender': 'male'}], 'count': 6}], 'count': 6, 'summary': '6 Likes'}, 'ok': False, 'ratingSignals': 12, 'reasons': {'items': [], 'count': 0}, 'createdAt': 1348582222, 'photos': {'groups': [{'type': 'venue', 'items': [{'id': '59b8f76a6f706a62fe1d6476', 'source': {'url': 'https://www.swarmapp.com', 'name': 'Swarm for iOS'}, 'user': {'id': '88422156', 'photo': {'suffix': '/88422156-OQ4TQKVLBHPEFK5I.jpg', 'prefix': 'https://fastly.4sqi.net/img/user/'}, 'lastName': 'Kaya', 'firstName': 'Mustafa', 'gender': 'male'}, 'createdAt': 1505294186, 'height': 1440, 'suffix': '/88422156_JvWco68kjMMs6-5BWd6bULkgKQsxoNR96iHhT-wcf3I.jpg', 'visibility': 'public', 'prefix': 'https://fastly.4sqi.net/img/general/', 'width': 1920}], 'name': 'Venue photos', 'count': 108}], 'count': 108}, 'inbox': {'items': [], 'count': 0}, 'allowMenuUrlEdit': True, 'ratingColor': 'FFC800', 'popular': {'richStatus': {'text': 'Likely open', 'entities': []}, 'status': 'Likely open', 'isLocalHoliday': False, 'timeframes': [{'days': 'Today', 'segments': [], 'includesToday': True, 'open': [{'renderedTime': '7:00 AM–2:00 PM'}, {'renderedTime': '4:00 PM–8:00 PM'}]}, {'days': 'Sat', 'segments': [], 'open': [{'renderedTime': '10:00 AM–8:00 PM'}]}, {'days': 'Sun', 'segments': [], 'open': [{'renderedTime': '6:00 AM–2:00 PM'}]}, {'days': 'Mon', 'segments': [], 'open': [{'renderedTime': '7:00 AM–10:00 AM'}, {'renderedTime': 'Noon–8:00 PM'}]}, {'days': 'Tue–Wed', 'segments': [], 'open': [{'renderedTime': '8:00 AM–8:00 PM'}]}, {'days': 'Thu', 'segments': [], 'open': [{'renderedTime': '9:00 AM–8:00 PM'}]}], 'isOpen': True}, 'shortUrl': 'http://4sq.com/Q5S5ds', 'stats': {'tipCount': 6}, 'listed': {'groups': [{'type': 'others', 'items': [{'id': '4f03dc9f9adf4efb1363ea35', 'description': '', 'user': {'id': '19183938', 'photo': {'suffix': '/2NPSHBUS4XTOZGRG.jpg', 'prefix': 'https://fastly.4sqi.net/img/user/'}, 'lastName': 'Şahin', 'firstName': 'Tuncay', 'gender': 'male'}, 'canonicalUrl': 'https://foursquare.com/user/19183938/list/tt', 'url': '/user/19183938/list/tt', 'photo': {'id': '50d43f4be4b025347e4cdff9', 'suffix': '/7340221_b0NWKsVk43ZOkaO5tEPziwUv05z4rxbBEWh62EgSmmw.jpg', 'user': {'id': '7340221', 'photo': {'suffix': '/7340221-QOU013M2DS5XUVS3.jpg', 'prefix': 'https://fastly.4sqi.net/img/user/'}, 'lastName': 'Haytural', 'firstName': 'Özden', 'gender': 'female'}, 'width': 720, 'height': 519, 'createdAt': 1356087115, 'visibility': 'public', 'prefix': 'https://fastly.4sqi.net/img/general/'}, 'createdAt': 1325653151, 'updatedAt': 1403640306, 'editable': False, 'type': 'others', 'collaborative': False, 'public': True, 'followers': {'count': 5}, 'name': 'tt', 'listItems': {'items': [{'id': 'v5061bb4ee4b0acb17101a45b', 'createdAt': 1354207928}], 'count': 81}}], 'name': 'Lists from other people', 'count': 1}], 'count': 1}, 'tips': {'groups': [{'type': 'others', 'items': [{'id': '517e98e3e4b08822f4591389', 'likes': {'groups': [{'type': 'others', 'items': [{'id': '51044660', 'photo': {'suffix': '/YTDASVMFUUMSMTAB.jpg', 'prefix': 'https://fastly.4sqi.net/img/user/'}, 'lastName': 'Kaya', 'firstName': 'Mehmet', 'gender': 'male'}], 'count': 1}], 'count': 1, 'summary': '1 like'}, 'user': {'id': '47528821', 'photo': {'suffix': '/1FDXNKNI4QVDGI2X.jpg', 'prefix': 'https://fastly.4sqi.net/img/user/'}, 'lastName': 'Kaya', 'firstName': 'Mustafa', 'gender': 'male'}, 'text': 'Sıcak bi karşılama ve muhtesem yemek yemek ısteyenler hiç kaçırmasın burayı anne yemeği gibi :)', 'createdAt': 1367251171, 'type': 'user', 'canonicalUrl': 'https://foursquare.com/item/517e98e3e4b08822f4591389', 'todo': {'count': 0}, 'agreeCount': 1, 'authorInteractionType': 'liked', 'logView': True, 'lang': 'tr', 'disagreeCount': 0}], 'name': 'All tips', 'count': 6}], 'count': 6}, 'hereNow': {'groups': [], 'count': 0, 'summary': 'Nobody here'}, 'colors': {'highlightColor': {'photoId': '59b8f76a6f706a62fe1d6476', 'value': -6250336}, 'highlightTextColor': {'photoId': '59b8f76a6f706a62fe1d6476', 'value': -16777216}, 'algoVersion': 3}, 'specials': {'items': [], 'count': 0}, 'categories': [{'id': '5283c7b4e4b094cb91ec88d4', 'primary': True, 'name': 'Turkish Home Cooking Restaurant', 'shortName': 'Turkish Home Cooking', 'pluralName': 'Turkish Home Cooking Restaurants', 'icon': {'suffix': '.png', 'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/turkish_'}}, {'id': '4bf58dd8d48988d16d941735', 'pluralName': 'Cafés', 'icon': {'suffix': '.png', 'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_'}, 'name': 'Café', 'shortName': 'Café'}, {'id': '52e81612bcbc57f1066b7a0a', 'pluralName': 'Pie Shops', 'icon': {'suffix': '.png', 'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/pieshop_'}, 'name': 'Pie Shop', 'shortName': 'Pie Shop'}], 'attributes': {'groups': []}, 'canonicalUrl': 'https://foursquare.com/v/%C3%B6znur-cafe-ev-yemekleri/5061bb4ee4b0acb17101a45b', 'verified': False, 'location': {'city': 'İstanbul', 'labeledLatLngs': [{'lat': 40.98233458770847, 'label': 'display', 'lng': 29.059884316778895}], 'country': 'Türkiye', 'lat': 40.98233458770847, 'state': 'İstanbul', 'formattedAddress': ['İstanbul', 'Türkiye'], 'cc': 'TR', 'lng': 29.059884316778895}, 'name': 'Öznur Cafe Ev Yemekleri', 'pageUpdates': {'items': [], 'count': 0}, 'rating': 6.5, 'bestPhoto': {'id': '59b8f76a6f706a62fe1d6476', 'source': {'url': 'https://www.swarmapp.com', 'name': 'Swarm for iOS'}, 'createdAt': 1505294186, 'height': 1440, 'suffix': '/88422156_JvWco68kjMMs6-5BWd6bULkgKQsxoNR96iHhT-wcf3I.jpg', 'visibility': 'public', 'prefix': 'https://fastly.4sqi.net/img/general/', 'width': 1920}, 'contact': {}, 'beenHere': {'marked': False, 'unconfirmedCount': 0, 'lastCheckinExpiredAt': 0, 'count': 0}, 'timeZone': 'Europe/Istanbul'}
~~~

**### 2.B Mekanın Genel Puanı (Rating)  Alma**

Yukarda gördüğünüz gibi bir mekana ait hangi parametreleri alacağımıza dair o mekana air anahtar değerleri gelmiştti.
Sonuçlardan rating parametresi ile mekanın puanına erişilmektedir.
Listelediğimiz ilk 5 ev yemekleri listesini birinci sırada ki ;

0                Öznur Cafe Ev Yemekleri  ...  5061bb4ee4b0acb17101a45b

id değerli en yakın ev yemekleri mekanının puanını alalım:

~~~python
import requests

import pandas as pd

from pandas.io.json import json_normalize

CLIENT_ID ='PGBQWU3LLONODVNJ3DAOCU0WCO1UVCENQJ0M0W1FUYKJZQHB'

CLIENT_SECRET ='13WART3RQMCHJF3IUGKQXMP4DVW5ALUPVEFKNDX1J0NG0GXB'

VERSION ='20191201'

venue_id = '5061bb4ee4b0acb17101a45b' #öznur ev yemeklerinin id'si

limit = 150 #set limitinin toplam ipucu sayısından büyük veya ona eşit olması

url = 'https://api.foursquare.com/v2/venues/{}?client_id={}&client_secret={}&v={}'.format(venue_id, CLIENT_ID, CLIENT_SECRET, VERSION)

result = requests.get(url).json()
~~~~
 
~~~bash
sum@sumaray:~/Desktop/api$ python api20.py

6.5
~~~
  
mekanın değerlendirmesi 6.5 çok iyi değerlendirme değil gibi.
en yakın 2.başka mekan denersek:

1	Lezzet Durağı Ev Yemekleri  ...  4f4cb5d4e4b0b0a21387c252

~~~bash
sum@sumaray:~/Desktop/api$ python api20.py

bu mekan değerlendirilmedi.
~~~

En yakın 3.mekana bakarsak

2             Palmiye Cafe Ev Yemekleri  ...  544b806f498e693acaf9cc90
~~~bash
sum@sumaray:~/Desktop/api$ python api20.py

7.7
~~~

7.7 Puanı daha iyi, bu mekan üzerinden mekan tavsiyelerine bakalım.

**### 2. C İpuçlarının-Tavsiye(tips) Değerin Bulma**

Bir mekanın tavsiye değerini sayısal olarak  ; 

> result['response']['venue']['tips']['count']
> 
> print(result)

şeklinde ulaşabiliyoruz.

7.7 ratinge sahip Palmiye ev yemeklerine kaç yorum yapıldığın bakalım.

~~~python
import requests

import pandas as pd

from pandas.io.json import json_normalize

CLIENT_ID ='***********'
CLIENT_SECRET ='**********'
VERSION ='20191201'

venue_id = '544b806f498e693acaf9cc90' #palmiye cafe ev yemeklerinin id'si

limit = 150 #set limitinin toplam ipucu sayısından büyük veya ona eşit olması

url = 'https://api.foursquare.com/v2/venues/{}?client_id={}&client_secret={}&v={}'.format(venue_id, CLIENT_ID, CLIENT_SECRET, VERSION)

result = requests.get(url).json()

try:
    print(result['response']['venue']['tips']['count'])

except:
    print('bu mekan değerlendirilmedi.') 
~~~

output:
~~~bash
sum@sumaray:~/Desktop/api$ python api20.py

4
~~~

Çıktı da gördüğünüz gibi bu mekan hakkında 4 yorum yapıldı bilgisine ulaştık.

### 2.D Mekanın tavsiyelerini alma (venue tips)
Bir mekanın tavsiye sayısını almıştık. Şİmdi ise bu yorumların iyi veya kötü olduğu yönünde bilgi edinelim..

> https://api.foursquare.com/v2/venues/**VENUE_ID**/tips?client_id=**CLIENT_ID**&client_secret=**CLIENT_SECRET**&v=**VERSION**&limit=**LIMIT**
  
BU şekilde url oluşturur ve get isteği gönderilir.

Tüm ipuçlarını almak için limit belirlenir

    ##mekan tavsiye
    limit = 10  
    #limitin toplam ipucu sayısına eşit veya ondan daha büyük olması gerekir
    
    url = 'https://api.foursquare.com/v2/venues/{}/tips?client_id={}&client_secret={}&v={}&limit={}'.format(venue_id, CLIENT_ID, CLIENT_SECRET, VERSION, limit)
    results = requests.get(url).json()
    results


Palmiye cafe ev yemeklerinin tavsiyelerini alalım:

~~~python

import requests

import pandas as pd

from pandas.io.json import json_normalize

CLIENT_ID ='*************************'

CLIENT_SECRET ='***************************'

VERSION ='20191201'

venue_id = '544b806f498e693acaf9cc90' #palmiye cafe ev yemeklerinin id'si

##palmiye cafe ev yemeklerinin tavsiyeleri

limit = 15 #limitin toplam ipucu sayısına eşit veya ondan daha büyük olması (ipucu=4)

url = 'https://api.foursquare.com/v2/venues/{}/tips?client_id={}&client_secret={}&v={}&limit={}'.format(venue_id, CLIENT_ID, CLIENT_SECRET, VERSION, limit)

results = requests.get(url).json()
print(results)
~~~
  

output:
~~~bash
sum@sumaray:~/Desktop/api$ python api21.py

{'response': {'tips': {'count': 4, 
'items': [{'text': 'Sıcak kanlı çalışanları nefis yöresel yemekleri ve uygun fiyatlarıyla mükemmel seçim 😊', 'lang': 'tr', 'canonicalUrl': 'https://foursquare.com/item/544bbe81498e470ddb013e1d', 'disagreeCount': 0, 'todo': {'count': 0}, 'authorInteractionType': 'liked', 'id': '544bbe81498e470ddb013e1d', 'likes': {'groups': [{'count': 1, 'items': [{'photo': {'suffix': '/22567773-YQA5HQ5XQV3N1B0T.jpg', 'prefix': 'https://fastly.4sqi.net/img/user/'}, 'gender': 'male', 'id': '22567773', 'firstName': 'Mesut'}], 'type': 'others'}], 'count': 1, 'summary': '1 like'}, 'type': 'user', 'user': {'lastName': 'Selvi', 'photo': {'suffix': '/97863500-EXMSPQSVITTSEUJV.jpg', 'prefix': 'https://fastly.4sqi.net/img/user/'}, 'gender': 'female', 'id': '97863500', 'firstName': 'Mevlüde'}, 'createdAt': 1414250113, 'logView': True, 'agreeCount': 1}]}}, 'meta': {'code': 200, 'requestId': '5dbc22dd6f0aa2002c217cb6'}}
~~~

#### İlişkili özelliklerin ipuçlarını parametre tip listesini şu şekilde ulaşılır:

tips = results['response']['tips']['items']
tip = results['response']['tips']['items'][0]
tip.keys()

> dict_keys(['id', 'createdAt', 'text', 'type', 'canonicalUrl', 'lang',
> 'likes', 'logView', 'agreeCount', 'disagreeCount', 'todo', 'user',
> 'authorInteractionType'])

Yukarda ki örnekte aldığımız tavsiye pek net değil. Çünkü yapılan yorumlar bize json türünde geldi.
Bunları sütun genişliğini biçimlendirerek, tüm tavsiyelerin(ipuçların) daha anlamlı veriler olarak görüntülenmesi sağlayabilirz.

~~~python
import requests
import pandas as pd
from pandas.io.json import json_normalize
CLIENT_ID ='***********'
CLIENT_SECRET ='***********'
VERSION ='2019120'
venue_id = '544b806f498e693acaf9cc90' #palmiye cafe ev yemeklerinin id'si

##palmiye cafe ev yemeklerinin tavsiyeleri
limit =15 #limitin toplam ipucu sayısına eşit veya ondan daha büyük olması (ipucu=4)

url='https://api.foursquare.com/v2/venues/{}/tips?client_id={}&client_secret={}&v={}&limit={}'.format(venue_id, CLIENT_ID, CLIENT_SECRET, VERSION, limit)
results = requests.get(url).json()
tips = results['response']['tips']['items']

pd.set_option('display.max_colwidth', 1000)

tips_df = json_normalize(tips) # json ipuçları standartlaştırmak

#tutulacak sütunlar
filtered_columns = ['agreeCount', 'text', 'disagreeCount','id', 'user.firstName', 'user.lastName', 'user.gender', 'user.id']
tips_filtered = tips_df.loc[:, filtered_columns]

#sonuçları görüntüleeme
print(tips_filtered)
~~~

output:
~~~bash

sum@sumaray:~/Desktop/api$ python api23.py

agreeCount text ... user.gender user.id

0 1 Sıcak kanlı çalışanları nefis yöresel yemekleri ve uygun fiyatlarıyla mükemmel seçim 😊 ... female 97863500

  

[1 rows x 8 columns]
~~~

🏹Buradan yapılan yorum ve yorumu yapan kullanıcının id bilgisi bide getirildi.
bir sonraki yazımda bu id değerli kullanıcı üzerinden Foursquare api'de kullanıcı arama ve özellikeri ile çalışacağım.