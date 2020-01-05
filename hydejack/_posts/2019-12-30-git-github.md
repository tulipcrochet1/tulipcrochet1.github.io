---
title: Git ve Github Kurmak
image: /assets/img/blog/git.jpg
description: >
---

## Git Kurulumu & Github Repo Oluşturma

**Git** bir sürüm kontrol sistemidir. Projedeki herhangi veya tüm değişikleri takip etmeyi sağlar. Yapacağımız projenin adım adım  versiyon , kopyalarını alır. ihtiyaç duymamız halinde bu versiyonlara, kopyalara kolayca geri dönmemizi sağlar. kodu herkesle paylaşmanın çok kolay bir yoludur.  Github depomuzda yaptığımız gibi.

Git'i kullanarak kodlarımızı Heroku, AWS ve diğerleri gibi hizmetlerde canlı bir bulut uygulama hizmetleriyle dağıtmak için de kullanabilirsiniz.

Django projemi kullanarak aşağıdaki adımları uyguladım:


1. Git'in yüklenmesi
şu yöntemlerden biriyle yüklenebilir :

 [git-scm](https://git-scm.com/) 'in kendisinden (tercih edilen) 
   
 [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)
    
 [Homebrew](https://brew.sh/)
   
2. Terminal'i açın ve kurulumu doğrulayın

~~~bash
sum@sumaray:~$ git --version

git version 2.7.4
~~~

Bu şekilde yüklenen/kullanılan sürümün bilgisini alırız.

3. Değişiklikleri "izlemek" istediğiniz bir dizinde (klasör) git'i başlatın.

~~~bash
sum@sumaray:~/Desktop/blogSite$ git init

Reinitialized existing Git repository in /home/sum/Desktop/blogSite/.git/
~~~

4. " .gitignore " oluşturun

Bunun amacı, git ile izlenen dosyaların "yoksayılması" dır. Bu, yerden tasarruf sağlar ve gereksiz dosyaları kaldırır. Önceden oluşturulmuş her türlü yazılım gitignore dosyalarını burada bulabilirsiniz.

~~~bash
(venv) sum@sumaray:~/Desktop/blogSite$ echo "*.py[cod]
> .DS_Store
> __pycache__/
> *.py[cod]
> *$py.class
> " > .gitignore
~~~
yukarıda .gitignore dosyasını oluştururken dahil etmek istediğim doyalarıda ekleyerek oluşturdum:


5. Dosya durumunu kontrol etme:

~~~bash
(venv) sum@sumaray:~/Desktop/blogSite$ git status

On branch master
Your branch is up-to-date with 'blogRepo/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   .gitignore

no changes added to commit (use "git add" and/or "git commit -a")
~~~

6. Tüm dosyaları ekleyip commit etme

~~~bash
(venv) sum@sumaray:~/Desktop/blogSite$ git add --all*

(venv) sum@sumaray:~/Desktop/blogSite$ git commit -m "gerekli eklemeler yapıldı"
[master b24700e] gerekli eklemeler yapıldı
 1 file changed, 5 insertions(+), 5 deletions(-)
~~~


7. **Uzak bir Repo** (oluşturma adımları aşağıda ki gibi) hazır olduğunda, yerel dosyayı Push et!


**Github Deposu Oluşturma (Uzak Git Reposu ile )**

- https://github.com adresinden Hesap Oluştur ve Giriş Yap
     
- Add New Repository ile Yeni Depo Ekle
  
- Bir ad ve açıklama verin. (Ne yaptığınızı bilmiyorsanız .gitignore veya readme eklemeyin.)

- "adding to existiing respository" talimatlarını uygulayın veya benim uyguladığım şu talimatları izleyebilirsiniz:


**Github'a gönderme**

- Repo'nun adresini kopyala

- git remote add http://githubKullaniciAdı/repoAdı.github.io.git

- git remote    //bağlantı başarılımı

- git push -u repoAdı master


**Projeye Ekleme Yapıldığında** 

terminalden proje dizinine gelinmelidir. 

~~~bash
$ git status 
$ git add .
$ git commit -m "değişiklikler mesajı"
$ git status
$ git log 
$ git remote
$ git push -u repoAdı master
~~~

7. Yerel Dosyayı Push Etme!
Github repo'su eklendikten sonra 7.adımdaki push etme adımı şu şekilde sonlanır:

~~~bash
(venv) sum@sumaray:~/Desktop/blogSite$ git push blogRepo master

    Username for 'https://github.com': .... 
~~~

yukarıda  kullanıcı adı,şifre bilgileri girilerek push edilir. Github repo'nuzu yenileyerek eklenen dosyaları görebilirsiniz.
!
