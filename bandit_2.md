# Bandit Over The Wire **2**

### Bu Leveldeki Amacımız
> SSH kullanarak bandit2 bağlanıp `Home directory` içindeki `spaces in this filename` dosyasını okumak ve burada bulunan şifre ile Bandit3'e geçmek.
>
> İhtiyaçımız olabilecek komutlar: `ssh`, `ls`, `cat`, `file`, `du`, `find`

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.


## Şifreyi Bulma
Bağlantığımızı yapmıştık. Şimdi bulunduğumuz dizindeki dosyaları listelemek için `ls` komutunu kullanacağız.

```bash
bandit2@bandit:~$ ls
spaces in this filename
```
Burada `spaces in this filename` dosyası bulunuyor. Bu dosyanın içeriğini okumak için `cat` komutunu kullanacağız.

```bash
bandit2@bandit:~$ cat spaces in this filename
cat: spaces: No such file or directory
cat: in: No such file or directory
cat: this: No such file or directory
cat: filename: No such file or directory
```
Burada bir hata aldık. Çünkü `cat` komutu dosya isimlerinde boşluk karakteri gördüğü zaman dosya ismini bitirdiğini düşünüyor. Bu yüzden dosya ismini tırnak içine alacağız

```bash
bandit2@bandit:~$ cat "spaces in this filename"
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
```
Bu dosyanın içeriğinde şifremiz bulunuyor.

Başka bir yöntem olarak dosya ismindeki boşluk karakterini `\` ile escape edebiliriz.

```bash
bandit2@bandit:~$ cat spaces\ in\ this\ filename
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
```

Bu şifre ile bir sonraki seviyeye geçebiliriz.


<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*