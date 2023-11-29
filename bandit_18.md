# Bandit Over The Wire **18**
### Bu Leveldeki Amacımız 
> SSH kullanarak bandit18 bağlanıp `Home Directory` altında `readme` dosyası olduğunu ve bunun içindeki şifreyi elde etmek

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd` : Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar.  Daha fazlası için `man cd` komutunu kullanabilirsiniz.


## Bilinmesi Gerekenler
- Shell kullanmadan SHH ile komut çalıştırma ? 
    > SSH bağlantısı sırasında, parametreler sonrasında yazdığımız komutlar, bir shell ortamına ihtiyaç duymadan çalıştırılır.
   > 
   > Örnek `ssh kullanıcı_adı@adress -p port "ls -la"`
## Şifre Bulma
İlk olarak SSH bağlantısı yaparsak
```bash
kali@kali:~$ ssh bandit18@bandit.labs.overthewire.org -p 2220
...
Byebye !
Connection to bandit.labs.overthewire.org closed.
kali@kali:~$
```
Bağlandığımız zaman bize `Byebye !` yazısı ile karşılaşıyoruz ve bağlantı kapanıyor. Bu durumda bizim yapmamız gereken `readme` dosyasını okumak.
```bash
kali@kali:~$ ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
bandit18@bandit.labs.overthewire.org's
password:                                                                awhqfNnAbc1naukrpqDYcF95h7HoMTrC
```
Burada `cat readme` komutunu SSH bağlantısı sırasında yazdığımız için, bu komut çalıştırıldıktan sonra bağlantı kapanıyor. Bu sayede `readme` dosyasının içeriğini okuyabiliyoruz ve şifreyi elde ediyoruz. Bu şifre ilede bir sonraki levele geçebiliriz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*