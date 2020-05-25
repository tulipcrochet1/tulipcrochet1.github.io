---
title: #3 Foursquare Api- Kullanıcı Keşfetme 📍
image: /assets/img/blog/FAPİ3.png

description: >

---

### **3. Foursquare'de Kullanıcı Arama 🗺️**

> https://api.foursquare.com/v2/users/**USER_ID**?client_id=**CLIENT_ID**&client_secret=**CLIENT_SECRET**&v=**VERSION**

Bir kullanıcıya ait ilgli özellikleri görüntüleyebilmek için yukardaki api url kullanılır . 
Url bilgileri tanımlanır, Get isteği gönderilir.
Kullanıcıya ait hangi tip özellikler görüntüleneceği bilgisi keys parametresi ile getirilir.

    user_id = '******' #user id 'li kullanıcı kimliği tanımlanır
    
    url = 'https://api.foursquare.com/v2/users/{}?client_id={}&client_secret={}&v={}'.format(user_id, CLIENT_ID, CLIENT_SECRET, VERSION) # define URL  
    
    #get isteği gönderme
    results = requests.get(url).json()
    user_data = results['response']['user']
    
    #kullanıcıyla ilgili görüntüleme özellikleri
    user_data.keys()

Bir önceki yazımda mekana ait yapılan yorum ve o yorumu yapan kullanıcıya dair id bilgisi almıştım.
**id değeri=97863500** olan kullanıcıya ait parametre değerlerine bakalım :

~~~python
import requests
import pandas as pd
from pandas.io.json import json_normalize

CLIENT_ID ='***************'
CLIENT_SECRET ='***********'
VERSION ='2019120'


user_id = '97863500'  #user id 'li kullanıcı kimliği değişkende tanımlanır

url = 'https://api.foursquare.com/v2/users/{}?client_id={}&client_secret={}&v={}'.format(user_id, CLIENT_ID, CLIENT_SECRET, VERSION) # define U$

#get isteği gönderme
results = requests.get(url).json()
user_data = results['response']['user']

#kullanıcıyla ilgili görüntüleme özellikleri
print(user_data.keys())
~~~~

output:
~~~bash
sum@sumaray:~/Desktop/api$ python api24.py

dict_keys(['id', 'gender', 'homeCity', 'lists', 'friends', 'type', 'lenses', 'tips', 'lastName', 'photos', 'mayorships', 'photo', 'contact', 'firstName', 'canonicalUrl', 'bio', 'checkins'])
~~~

Şimdi bu kullanıcıya ait bilgleri yazdıralım :

~~~python
import requests
import pandas as pd
from pandas.io.json import json_normalize
CLIENT_ID ='***********************'
CLIENT_SECRET ='**************************'
VERSION ='20180604'

user_id = '97863500' #user id 'li kullanıcı kimliği değişkende tanımlanır

url = 'https://api.foursquare.com/v2/users/{}?client_id={}&client_secret={}&v={}'.format(user_id, CLIENT_ID, CLIENT_SECRET, VERSION) # define U$

#get isteği gönderme
results = requests.get(url).json()
user_data = results['response']['user']

#kullanıcıyla ilgili görüntüleme özellikleri
#print(user_data.keys())

print('Ad: ' + user_data['firstName'])
print('soyad: ' + user_data['lastName'])
print('ev adresi: ' + user_data['homeCity'])
#kullanıcı kaç tavsiye gönderdi
print(user_data['tips'])
~~~

output:
~~~bash
sum@sumaray:~/Desktop/api$ python api25.py

Ad: Mevlüde
soyad: Selvi
ev adresi: Istanbul, Istanbul
{'count': 1}
~~~

En başta kullanıyı dair aldığım parametre değerlerinden friends ile 
Kullanıcının arkadaş listesini getirmek istersek : 

~~~python
import requests
import pandas as pd
from pandas.io.json import json_normalize

CLIENT_ID ='*******************'
CLIENT_SECRET ='****************'
VERSION ='2019120'

user_id = '97863500' #user id 'li kullanıcı kimliği değişkende tanımlanır

url = 'https://api.foursquare.com/v2/users/{}?client_id={}&client_secret={}&v={}'.format(user_id, CLIENT_ID, CLIENT_SECRET, VERSION) # define URL
 
#get isteği gönderme
results = requests.get(url).json()
user_data = results['response']['user']

#kullanıcıyla ilişkili özellikleri görüntüleme.
user_data.keys()

#kullanıcının arkadaşlarını alma, görüntüleeme
user_friends = json_normalize(user_data['friends']['groups'][0]['items'])
print(user_friends)
~~~
  

output:
~~~python
sum@sumaray:~/Desktop/api$ python api28.py

bio firstName gender ... photo.prefix photo.suffix tips.count
0 Deniz female ... https://fastly.4sqi.net/img/user/ /15327016_Ye88wP5J_eJ1xS1vHgaYGTSJ1zcwUByFDTGX... 0
1 Ferhan female ... https://fastly.4sqi.net/img/user/ /69419648-W3VIOZ5DDT3BEOAS.jpg 0
2 Mukaddes female ... https://fastly.4sqi.net/img/user/ /102914099-CPKRNUS104SME3X2.jpg 15
3 Tuba none ... https://fastly.4sqi.net/img/user/ /163616936-THDBPNDJDEH0VPP1.jpg 0
4 Şeyma female ... https://fastly.4sqi.net/img/user/ /84222130-X4M4JZNXSVSJMJW3.jpg 0
5 Mehmet male ... https://fastly.4sqi.net/img/user/ /130479951-II1W21HTIABEKOPQ.jpg 0
6 Ekrem male ... https://fastly.4sqi.net/img/user/ /28606380-3FHPENBTMY4IIO1T.jpg 0
7 Belgin female ... https://fastly.4sqi.net/img/user/ /129102549-3SV24JJJ3XIWHXXH.jpg 0
8 Banu none ... https://fastly.4sqi.net/img/user/ /46169363_VJwabvW6_lEf5GqLWodZM2TIcWYhxI6_f_EG... 0
9 Ferdun male ... https://fastly.4sqi.net/img/user/ /ME0L2CFMB10J10QR.jpg 0

[10 rows x 10 columns]
~~~

panda.io.json ile kullanıcının arkadaşlarına dair bilgi alabildik.

Kullanıcının profil resmi almak için:

~~~python
from IPython.display import Image

import requests

import pandas as pd
from pandas.io.json import json_normalize
CLIENT_ID ='**************************'
CLIENT_SECRET ='*************************'
VERSION ='2019120'

user_id = '97863500' #user id 'li kullanıcı kimliği değişkende tanımlanır

url = 'https://api.foursquare.com/v2/users/{}?client_id={}&client_secret={}&v={}'.format(user_id, CLIENT_ID, CLIENT_SECRET, VERSION) 	# define URL

 

#get isteği gönderme
results = requests.get(url).json()
user_data = results['response']['user']
 
#kullanıcıyla ilişkili özellikleri görüntüleme.
user_data.keys()

#kullanıcının arkadaşlarını alma, görüntüleeme
#user_friends = json_normalize(user_data['friends']['groups'][0]['items'])
#print(user_data)

  

#1 fotoğrafın prefix'ini al
#2 fotoğrafın suffix 'ini al
print(user_data['photo'])

#3.bunları resim boyutunu kullanarak birleştir
print(Image(url='https://igx.4sqi.net/img/user/300x300/97863500-EXMSPQSVITTSEUJV.jpg'))
~~~


output:

~~~bash
sum@sumaray:~/Desktop/api$ python api30.py
{'suffix': '/97863500-EXMSPQSVITTSEUJV.jpg', 'prefix': 'https://fastly.4sqi.net/img/user/'}

<IPython.core.display.Image object>
~~~


**#kullanıcı kaç tavsiye gönderdiği :**

print(user_data['tips'])


**kulllanıcının (user_friends) arkadaş listesini getirme ????**

user_friends = json_normalize(user_data['friends']['groups'][0]['items'])
print(user_friends)


🏹İstenilen türde mekanı istenilen konuma indeksleyerek, başka mekanlara erişim  tavsiye raitng , kullanıcı harita vs ile ilgli sınırsız erişim ve kullanımı bize foursquare api sunuyor. sınırsız erişim var ancak sınırlı sayıda günlük sorgu kotas aşımı bulunmaktadır.

🌏Gördüğnüz gibi Foursquare Api'nin geliştiricilere açtığı bu api ile bir çok bilgiyi alıp projelerimize dahil ederek
farklı analiz ve görsellikler katabiliriz.