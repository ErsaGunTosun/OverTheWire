# Bandit Over The Wire **15**

### Bu Leveldeki Amacımız 
> SSH kullanarak bandit15 bağlanıp localhost(127.0.0.1) üzerindeki 30001 portuna mevcut şifreyi göndermek ve bir sonraki levele için gerekli olan şifreyi elde etmek.
> 
> İhtiyaçımız olabilecek komutlar: `ssh`, `telnet`, `nc`, `openssl`, `s_client`,

## Kullanacağımız Komutlar
1.`openssl`: OpenSSL, açık kaynaklı bir SSL ve TLS uygulama programlama arayüzüdür. Daha fazlası için `man openssl` komutunu kullanabilirsiniz.

## Bilinmesi Gerekenler
- SSL nedir ? 
 >Server ile client arasındaki şifrelenmiş bağlantı denilebilir. SSL, iletilen mesajın doğru adreste deşifre edilerek okunabilmesi amacıyla tasarlanmış şifreleme protokolüdür.

## Şifre Bulma
Burada ssl üzerinde mevcut şifremizi gönderip bir sonraki levele geçmemiz gerekiyor. Bunun için `openssl s_client -connect localhost:30001` komutunu kullanıyoruz.
burada `-connect` parametresi ile bağlanacağımız adresi ve portu belirtiyoruz, `s_client` parametresi ilede ssl üzerinde bağlanacağımızı belirtiyoruz.

```bash
bandit15@bandit:~$ openssl s_client -connect localhost:30001
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN = localhost
verify error:num=18:self-signed certificate
....
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt
Correct!
JQttfApK4SeyHwDlI9SXGR50qclOAil1
```
Burada `Correct!` yazısından sonraki bizim şifremiz ve bununla birlikte sonraki levele geçbiliriz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*