---
title: Git ve Github Kurmak
image: /assets/img/blog/git.jpg
description: >
---

## Git ve Github'ı kurma
Git bir sürüm kontrol sistemidir. Projedeki herhangi veya tüm değişikleri takip etmeyi sağlar. Yapacağımız projenin adım adım  versiyon , kopyalarını alır. ihtiyaç duymamız halinde bu versiyonlara, kopyalara kolayca geri dönmemizi sağlar. kodu herkesle paylaşmanın çok kolay bir yoludur.  Github depomuzda yaptığımız gibi.

Git'i kullanarak kodlarımızı Heroku, AWS ve diğerleri gibi hizmetlerde canlı bir bulut uygulama hizmetleriyle dağıtmak için de kullanabilirsiniz.

Django projemi kullanarak bu kılavuzu uyguladım:


1 git'in yüklenmesi, şu yöntemlerden biriyle yüklenebilir :

    *[git-scm](https://git-scm.com/) 'in kendisinden (tercih edilen) 
    
    *[Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)
    
    *[Homebrew](https://brew.sh/)
   

2  Terminal'i açın ve kurulumu doğrulayın

`sum@sumaray:~$ git --version
`

`git version 2.7.4`

3  Değişiklikleri "izlemek" istediğiniz bir dizinde (klasör) git'i başlatın.

`sum@sumaray:~/Desktop/blogSite$ git init
`

`Reinitialized existing Git repository in /home/sum/Desktop/blogSite/.git/
`

4   " .gitignore " oluşturun

Bunun amacı, git ile izlenen dosyaların "yoksayılması" dır. Bu, yerden tasarruf sağlar ve gereksiz dosyaları kaldırır. Önceden oluşturulmuş her türlü yazılım gitignore dosyalarını burada bulabilirsiniz

```(venv) sum@sumaray:~/Desktop/blogSite$ echo "*.py[cod]
> .DS_Store
> __pycache__/
> *.py[cod]
> *$py.class
> " > .gitignore
```

5  Dosya durumunu kontrol etme:

`(venv) sum@sumaray:~/Desktop/blogSite$ git status
`

```On branch master
Your branch is up-to-date with 'blogRepo/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   .gitignore

no changes added to commit (use "git add" and/or "git commit -a")
```

6  Tüm dosyaları ekleyin ve commit etme

`````
(venv) sum@sumaray:~/Desktop/blogSite$ git add --all

(venv) sum@sumaray:~/Desktop/blogSite$ git commit -m "gerekli eklemeler yapıldı"[master b24700e] gerekli eklemeler yapıldı
 1 file changed, 5 insertions(+), 5 deletions(-)
`````


7  Uzak bir repo hazır olduğunda (oluşturma adımları aşağıda ki gibi), değişiklikleri push etmek yeterlidir. 

```
(venv) sum@sumaray:~/Desktop/blogSite$ git push blogRepo master
```
`Username for 'https://github.com': .... //github kullanıcı adı ve şifre bilgileri girilerel push edilir.
`

**Github Deposu Oluşturma (uzak git reposu ile )**

- https://github.com adresinden Hesap Oluştur ve Giriş Yap
     
 - Add New Repository ile Yeni Depo Ekle
  
- Bir ad ve açıklama verin. Ne yaptığınızı bilmiyorsanız .gitignore veya readme eklemeyin.

- "adding to existiing respository" talimatlarını uygulayın veya şu talimatları izleyebilirsiniz:


**Github'a gönderme**

A.  repo'nun adresini kopyala

B.  git remote add  repoAdı http://......

C. git remote    //bağlantı başarılımı

D.  git push -u repoAdı master

**Projeye Ekleme Yapıldığında** 

terminalden proje dizinine gelinmelidir. 

```
git status 
git add .
git commit -m "değişiklikler mesajı"
git status
git log 
git remote
git push -u repoAdı master
```

Yerel Dosyayı Push Etme!
