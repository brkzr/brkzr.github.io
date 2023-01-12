---
layout: post
title: "Raspbian'a Visual Studio Code Kurulumu"
date: 2019-04-11T12:00:00+00:00
#image: /assets/images/profile.jpg
#headerImage: false
tags: ["tools","VScode"]
#star: true
#category: blog
author: brkzr
description: Installing VS Code on Raspbian
---


[Visual Studio Code](https://code.visualstudio.com/) günümüzde kullanılan en popüler yazılım geliştirme araçlarından birisi.  Microsoft destekli olarak, open source geliştirilen yazılımcı dostu bu IDE; Linux, Mac OS ve Windows işletim sistemlerini desteklenmektedir. Buna rağmen, Chromecast, Raspbian, Fedora,Linux Mint vb. gibi işletim sistemlerinde VS Code'u kullanmak için  biraz çaba sarf etmek gerekiyor.

Yukarıda bahsettiğim işletim sistemleri için Jay (aka [Headmelted](https://github.com/headmelted)), süper bir [çalışma](https://github.com/headmelted/codebuilds) yapmış. Bu sayede; VS Code, bu sistemlere hızlı bir şekilde yüklenip kullanabiliyor.

Öncelikle, sisteme doğru ve gerekli __GPG key__'i eklemek gerekiyor.
```sh
wget https://packagecloud.io/headmelted/codebuilds/gpgkey -O - | sudo apt-key add -
```
Sonrasında, VS Code'un şu komut ile yüklenmesi gerekmekte:
```sh
curl -L https://code.headmelted.com/installers/apt.sh | sudo bash
```
Bu adımlar tamamlandıktan sonra, Raspbian işletim sisteminde __Accessories__ altında __Code-OSS (Headmelted)__ adıyla VS Code'un gözüktüğünden emin olunmalı.

#### DipNot: 
Şu an için yüklemeden sonra VS Code siyah ekranda takılı kalıyor. Birden fazla kullanıcı bu konuda [github issue](https://github.com/headmelted/codebuilds/issues/64) açmış. VS Code tarafında yapılan son güncelleme buna sebep olmuş görünüyor. Şimdilik eski versiyona geri dönülerek ilerlenebilir. 

Eski versiyona dönmek için:
```sh
sudo apt-get install code-oss=1.29.0-1539702286
```

VS Code "__hold__" olarak işaretlenerek, güncelleme alınması ve tekrar sorun yaşanması engellenebilir. İşlemi geri almak için "__unhold__" komutunu çalıştırılmalıdır.
```sh
sudo apt-mark hold code-oss
sudo apt-mark unhold code-oss
```


