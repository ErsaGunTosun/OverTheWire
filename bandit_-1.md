# Bandit Over The Wire **-1**

### Oyunun Amacı 
Temel linux komut satırı becereliremizi geliştirmek, temel güvenlik sistemini ve ctf yaklaşımına anlamak.

### Peki Bu Nasıl Olacak
Basit bir sistemi bulunyor, oyunda 34 level bulunmak ve her levelde içinde öğreneceğimiz veya kullancağımız şeyler için ipucular bulunuyor. Bu ipuclarını kullanarak bir sonraki seviyenin parolosı elde etmek. 

### Başlamadan Önce Bilinmesi gerekenler
- MAN nedir ?
    > Linux işletim sisteminde bulunan çevrimiçi bir yazılım belgeleme sistemidir. Komutlar, kütüphaneler, sistem çağrıları, dosya formatları ve diğer Linux bileşenleri hakknda bilgi sağlar.
    > Bu komudu her levelde yeni bir komut öğrenirken çokça kullanacağız.
    >
    > Terminalde `man man` komudunu kullanarak veya [kendi websitesinden](https://man7.org/linux/man-pages/man1/man.1.html) ayrıntı bilgiye ulaşabilirsiniz.
- SSH Nedir ?
    > SSH, Secure Shell kısaltılmiş halidir. Uzaktan güvenli bir şekilde erişim yapmamızı sağlayan protokoldür. Kullanıcının bir sunucuya güvenli bir şekilde bağlanmasına ve aynı zamanda işlem yapmasına izin verir.
    > Over the wire'nın sunucularına bağlanırkende kullanıcağımız protokoldür.
    >
    > Daha fazla ayrıntı için 
        > 1. [Türkçe Kaynak](https://www.tolgabagci.com/ssh-nedir/ "Türkçe")
        > 2. [Man](https://man7.org/linux/man-pages/man1/ssh.1.html "İngilizce")
        > 3. [Wikipedia](https://en.wikipedia.org/wiki/Secure_Shell "İngilizce")
        > 4. [Video](https://www.youtube.com/watch?v=zlv9dI-9g1U "İngilizce")

Over the wire temel mantığını ve başlamadan önce bilmememiz gereken bazı şeyleri öğrendik. Şimdi ana seviye olan Bandit0'a başlayabiliriz. 

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*



