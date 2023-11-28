# Bandit Over The Wire **14**

### Bu Leveldeki Amacımız
> SSH kullanarak bandit14 bağlanıp localhost(127.0.0.1) üzerindeki 30000 portuna mevcut şifreyi göndermek ve bir sonraki levele için gerekli olan şifreyi elde etmek. 
>
> İhtiyaçımız olabilecek komutlar: `ssh`, `telnet`, `nc`, `openssl`, `s_client`,

## Kullanacağımız Komutlar
1.`nc`: Netcat, TCP veya UDP protokolü kullanarak ağ bağlantıları üzerinden veri okuyan ve yazan basit bir Unix yardımcı programıdır.. Daha fazlası için `man nc` komutunu kullanabilirsiniz.

## Bilinmesi Gerekenler
- Netcat Nedir ?
    > TCP/IP protokolünü kullanarak ağ bağlantıları üzerinden veri okuyan ve yazan çok yönlü bir ağ oluşturma yardımcı aracıdır. Aynı zamanda, ihtiyaç duyacağınız hemen hemen her türlü bağlantıyı oluşturabilen ve birçok ilginç yerleşik yeteneğe sahip, zengin özelliklere sahip bir ağ hata ayıklama ve araştırma aracıdır. Daha fazla ayrıntı için [buraya](https://hackernoon.com/tr/nmap-ve-netcat'ta-uzmanla%C5%9Fmak-i%C3%A7in-nihai-rehber "Türkçe") bakabilirsiniz.
- Localhost Nedir ?
    > localhost, 127.0.0.1 adresini temsil eden bir terimdir. Bu terim, bir bilgisayarın kendi üzerinde çalışan uygulamaları belirtmek için kullanılır.
- Port Nedir ?
    > Bir bilgisayarın veya sunucunun belirli bir uygulama veya hizmet için kullandığı bir bağlantı noktasıdır. Portlar, bir bilgisayarın ağ üzerinden veri aktarımını yönetmesine yardımcı olur.
    >
    > Bir bilgisayarın IP adresi, bir bilgisayarın fiziksel konumunu belirler. Port numarası, bir bilgisayarın hangi uygulama veya hizmete erişileceğini belirler.
    >
    > Portlar, 0 ile 65535 arasındaki sayılardan oluşur. Her port, belirli bir uygulama veya hizmetle ilişkilendirilir. Örneğin, 80 portu, web sunucuları için kullanılır. 25 portu, e-posta sunucuları için kullanılır.

## Şifre Bulma
Burada netcat ile `localhost(127.0.0.1)` adresinin `30000` portuna bağlanıp mevcut şifreyi göndermemiz gerekiyor. Bunun için `nc -vv localhost 30000` komutunu kullanıyoruz.
Buradaki `-vv` parametresi bize daha fazla bilgi vermesini sağlıyor. `-v` parametreside kullanılabilir. 

```bash
bandit14@bandit:~$ nc -vv 127.0.0.1 30000
Connection to 127.0.0.1 30000 port [tcp/*] succeeded!                                                                   fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
Correct!                                                                                  jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt 
```
Burada `Correct!` yazısından sonraki bizim şifremiz ve bununla birlikte sonraki levele geçbiliriz. 

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*