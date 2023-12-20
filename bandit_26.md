# Bandit Over The Wire **26**
### Bu Leveldeki Amacımız
> Bandit19 yaptığımız gibi `setuid` ile çalışan bir dosya var bununla bir sonraki levelin parolasını bulmak.
## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat`: Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.

## Şifre Bulma
İlk olarak  `Home directory` altında ls yapalım.

```Bash
bandit26@bandit:~$ ls
bandit27-do  text.txt
```
Şifrelerin `/etc/bandit_pass` altında saklandığını biliyoruz. `bandit27-do` kullanarak `/etc/bandit_pass/bandit27` dosyasını okumak işlemini gerçekleştirebiliriz.

```Bash
bandit26@bandit:~$ ./bandit27-do cat /etc/bandit_pass/bandit27
YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS
```
Bu şifre ile bir sonraki levele geçiş yapabiliriz.


<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*