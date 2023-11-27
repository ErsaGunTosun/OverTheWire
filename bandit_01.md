# Bandit Over The Wire **1**

### Bu Leveldeki Amacımız
> SSH kullanarak bandit1 bağlanıp `Home directory` içindeki `-` dosyasını okumak ve burada bulunan şifre ile Bandit2'e geçmek.
>
> İhtiyaçımız olabilecek komutlar: `ssh`, `ls`, `cat`, `file`, `du`, `find`

## Kullanacağımız Komutla
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.

2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.

## Şifreyi Bulma
Bağlantığımızı yapmıştık. Şimdi bulunduğumuz dizindeki dosyaları listelemek için `ls` komutunu kullanacağız.

```bash
bandit1@bandit:~$ ls
-
```
Burada `-` dosyası bulunuyor. `-, --, ---` terminaller bulunan özel karakterlerdir. Bu özel karakterlere [Buradan](https://www.oreilly.com/library/view/learning-the-bash/1565923472/ch01s09.html) bakabilirsiniz.

Burada bir önceki levelde olduğıu gibi `cat` komutunu kullanarak dosyanın içeriğini okuyacağız ama burada biraz farklı olacak.

```bash
bandit1@bandit:~$ cat -
```
Bu şekilde yaptığımız zaman ekranımız donacaktır. Çünkü `-` karakteri terminalde bir komut olarak algılanıyor. Bu yüzden `CTRL + C` ile çıkış yapacağız.

Burada dosyayı okumak için dosyanın başına `./` ekleyeceğiz. Bu bize bu dizinin içindeki dosya okumak istediğimizi belirtiyor.

```bash
bandit1@bandit:~$ cat ./-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
```
Bu dosyanın içeriğinde şifremiz bulunuyor. Bu şifre ile bir sonraki seviyeye geçebiliriz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*

