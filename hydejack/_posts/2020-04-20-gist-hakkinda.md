---

title: Gist Hakkında 🐳

description: >

---
##Gist Hakkında

Gist nedir?  Nerede, Nasıl kullanılır? Github'da Gists ile Neler Yapabilirsiniz?
Bu yazımda github gist hakkında yazacağım. 

Bir github hesabınız varsa mutlaka profil seçeneklerinden **"Your Gists"** seçeneğini görmüş olmalısınız.  Bende Github Gist 'in ne amaçla kullanacağımı biraz araştırdım ve hemen öğrendiklerimi ve uyguladıklarımı anlatmaya geçeyim !

Gits ; istenilen türde kod parçacıklarının ve ya metin dosyalarının çok kolay şekilde oluşturulup Github tarafında barındırıldığı bir servistir. Github reposunda olduğu gibi  Gist'de de forks, clone , star gibi birçok özelliğe sahip olmakla birlikte, bunları bize daha basite indirgenmiş şekilde sağlayamaktadır.

- Her Gist, bir Github reposudur. 
- Bir Gits, tek bir dosyayı, kod parçacığını veya içerisinde bir klasör yapısı gerektirmeyen herhangi bir dosya koleksiyonunu paylaşmak için kullanılabilir.
- Gits'de oluşturacağımız dosya herkese açık veya gizli olarak oluşturma seçeneği sunmaktadır.
- Oluştururulacak gits sayfasında sol alt tarafta "add file" butonu var.  Bu bize Birden fazla kod parçacığımızı veya dosya parçalarını bir gits ile birbirine bağlayarak seri oluşturma imkanı sunuyor.
- Eğlenceli yanı web sitelerinde örnek kod içeren ve bunları siteye gömen embed kodlar oluşturmamızı sağlıyor.

Biraz kurcaladığımda gits oluştururken eklediğim kodun isim alanına yazdığım uzantıya göre o dil için renklendirme yapması dikkatimi çekti.  

Gits Oluşturma


- ilk olarak Github adresinizden oturum açın .
- Gits ana sayfanıza gidin.(veya gist.github.com adresine)
- Oluşturmak istediğiniz gits dosya adını yazın. ( Açıklama kısmı isteğe bağlı) 
- İstediğiniz kodu girin
- Create Public Gist'e tıklayın
- İhtiyaç halinde kod parçalarınızı farklı dosyalara bölmeniz gerekirse, sayfanın alt sol köşesinde yer alan Add File'e tıklayabilirsiniz.

![gistdeneme](/assets/img/gistdeneme.png)

- Gits bizlere kendi web sayfalarımızda renkli kodları otomatik olarak göstermeyi sunuyor.  Bunun için gits kodunuzun web url adresini alıp ;
- https: //gist.github.com/sumeyyekilic/4b6162399a6c73e2a9fec7b84541b083 yazdığınızda kod bloğunu, bize embed kod olarak veriyor ve aşağıdaki gibi bize sunuyor 🙂 


- Yukarda gördüğğünüz gibi github gist'e eklediğim kodu bir url ile embed kod verdi. Sadece bunu sağlamış olması bile çok büyük bir kolaylık. birçok farklı yerde kodumuzu bu şekilde kolayca başlarına aktarabiliriz ve kodun anlaşılabilirliği için bize kolaylık sağlar.

Gist Klonlama ve Erişim


- Konlama
~~~bash
sum@sumaray:~/Desktop$ git clone https://gist.github.com/sumeyyekilic/4b6162399a6c73e2a9fec7b84541b083
Cloning into '4b6162399a6c73e2a9fec7b84541b083'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
Checking connectivity... done.
~~~

" git clone gistAdresi " komutuyla lokalde git reposu oluşur. BUnun üzerinden istenilen değişiklik ve düzenleme yapılabiliriz. OLuşturduğunuz gist'i güncelleyebiliriz.


- Gist'e Commit Etme
~~~bash
sum@sumaray:~/Desktop/4b6162399a6c73e2a9fec7b84541b083$ git commit -m "değişiklik yapıldı"
[master b5444e6] değişiklik yapıldı
 1 file changed, 1 insertion(+), 1 deletion(-)
sum@sumaray:~/Desktop/4b6162399a6c73e2a9fec7b84541b083$ git push origin master -f
Username for 'https://gist.github.com': sumeyyekilic
Password for 'https://sumeyyekilic@gist.github.com': 
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 318 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://gist.github.com/sumeyyekilic/4b6162399a6c73e2a9fec7b84541b083
   12a55cf..b5444e6  master -> master
~~~

#### Gits Hizmetinin Kullanılan Alanları
1. Anonim metin yazma
2. Revisions ile değişiklikleri izleme
Paylaştığımız bir kodun gist içeriğini düzenlediğimizde, gist'in önceki sürümleri de saklanır. Zamanla yaptığımız bu düzenlemelere ve iki versiyon arasındaki değişikliğe görsel olarak erişebileceğimiz revizyonlar sekmesi sunulmuştur.
3. Markdown içerikleriyle gists yayınlama
4. Gists yalnızca düz metni kabul ederken, metninizi zengin HTML biçiminde yayınlamak için Markdown biçimini kullanabilirsiniz.
5. Yazılan metinleri yayınlama platformu olarak kullanılabilir
Blogger, Medium gibi çok sayıda yazma motoru olsa da, yazılarınızı hızlı bir şekilde yayınlamak için Github’un Gist hizmetini de kullanabilirsiniz. Düz metin biçiminde bir Gist oluşturun ve bu Gist'i bağımsız bir web sayfası olarak yayınlamak için roughdraft.io kullanın. Okunabilirliği Gistlerinizle entegre etmek gibidir.
6. yapılacaklar listesi tutabilirsiniz 
`
- [x] görev 1
- [] görev 2
- [x] görev 3 `
Gist'iniz puclic ise herkes yapılacaklar listelerinizi görebilir ama görevlerin durumunu işaretleyip değiştirmeyi sadece siz yapabilirsiniz.

7.Web ayfalarınızda gits kod satırlarını gömebilirsiniz.

8.Gits ile embed kod görüntülediğinizde hem paylaştığınız kod satırı ve dosya sözdizimini anlaşılır yapar. Hemde web sitenizi ziyaret edenler Gist linki ile Github hesaplarına kolayca klonlayabilirler..
`<script src = "https://gist.github.com/username/gist-id.js"> </script>
`

9.Trafiği Ölçme
Oluşturduğunuz gist'lere giden trafiği görüntülemek için Google Analytics kullanılabilir.
`! [Analytics] (https://ga-beacon.appspot.com/UA-XXXXX-X/gist-id?pixel)`