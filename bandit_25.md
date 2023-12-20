# Bandit Over The Wire **25**
### Bu Leveldeki Amacımız
> SSH ile bandit25 bağlanıp `Home Directory` atlında bulunan `bandit26.sshkey` ile bandit26 bağlanıp bir sonraki level için şifreyi bulmak. 

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cd`: Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar. Daha fazlası için `man cd` komutunu kullanabilirsiniz.
3. `ssh`: SSH ile uzak bir makineye bağlanmamızı sağlar. Daha fazlası için `man ssh` komutunu kullanabilirsiniz.
4. `cat`: Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
5. `more`: Bir dosyanın içeriğini sayfa sayfa gösterir. Daha fazlası için `man more` komutunu kullanabilirsiniz.


## Şifre Bulma
Direk `bandit26.sshkey` ile bandit26 bağlanmaya çalıştığımız, giriş işlemi oluyor ama hemen sonlanıyor. Bunun nedeni ipucunda verilen bandit26 kullanıcı için shell’in bash olmaması olabilir.
Kontrol etmek için parola dosyası olarak türkçeleştirilen /etc/passwd dosyasına bakılabilir.
```bash
bandit25@bandit:~$ cat /etc/passwd | grep 'bandit26'
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
```
Burada `/usr/bin/showtext` ile `bash` olmadığını onun yerine bir script olduğunu görebiliriz. Bu scriptin içeriğine bakalım.
(passwd ile ilgili daha fazla bilgiyi [buradan](https://en.wikipedia.org/wiki/Passwd) bulabilirsiniz.)

```bash
bandit25@bandit:~$ cat /usr/bin/showtext
#!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0
```
`TERM=linux` ile terminal tipini linux olduğunu ve `more ~/text.txt` ilede bir txt dosyasını okuduğunu görebiliriz.
Burada `more ` kodunu o txt dosyasını sayfa sayfa gösteriyor ve bittiği an terminal kapanıyor. Bunu önlemek için kullandığımız terminalin boyutunu küçültüp işlem yapmamız gerekiyor. 

```bash
bandit25@bandit:~$ ssh bandit26@bandit.labs.overthewire.org -p 2220 -i bandit26.sshkey
```
Eğer doğru oranda terminalin boyutunu küçültüyseniz `v` komudu ile editör moda geçebilirsiniz.
Editör moda geçtikten sonra `:` tuşan basıp `:set shell=/bin/bash` yapıyoruz bu şekilde terminali bash olarak değiştirmiş oluyoruz. Daha sonra `:` tuşuna tekrar basıp bu sefer `:sh` yazarak terminale giriş yapıyor. 

Terminale giriş yaptıktan sonra `/etc/bandit_pass/bandit26` dosyasını okuyarak bir sonraki levelin şifresini bulabiliriz.

```bash
bandit26@bandit:~$ cat /etc/bandit_pass/bandit26
c7GvcKlw9mC7aUQaPx7nwFstuAIBw1o1
```

Bu şifre ile bir sonraki levele geçiş yapabiliriz. 


<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*