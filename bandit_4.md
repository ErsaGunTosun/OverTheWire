# Bandit Over The Wire **4**

### Bu Leveldeki Amacımız
> SSH kullanarak bandit4 bağlanıp `Home directory` içindeki `inhere` dizini içindeki `human-readable` dosyayı bulmak ve içersinde bulunan şifre ile bir sonraki seviyeye ulaşmak.
>
> İhtiyaçımız olabilecek komutlar: `ssh`, `ls`, `cat`, `file`, `du`, `find`

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd` : Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar.  Daha fazlası için `man cd` komutunu kullanabilirsiniz.
4. `file` : Dosyanın türünü belirlememizi sağlar. Daha fazlası için `man file` komutunu kullanabilirsiniz.


## Şifreyi Bulma
Burada `human-readable` olarak bahsettiğin dosya insan tarafından okunan bilen bir dosya buda `text` dosyası olması gerekiyor. Bizim amacımızda bu `text` dosyasını bulmak

Bağlantığımızı yapmıştık. Şimdi bulunduğumuz dizindeki dosyaları listelemek için `ls` komutunu kullanacağız.

```bash
bandit4@bandit:~$ ls
inhere
```
Burada görüdüğümüz bir `directory` bizim şifremiz burada olabilir. Bu dizine girmek için `cd` komutunu kullanacağız. ve içerisinde neler olduğunu görmek için yine  `ls -a` komutunu kullanacağız.

```bash
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ ls -al 
drwxr-xr-x 2 root    root    4096 Oct  5 06:19 .
drwxr-xr-x 3 root    root    4096 Oct  5 06:19 ..
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file00
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file01
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file02
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file03
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file04
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file05
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file06
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file07
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file08
-rw-r----- 1 bandit5 bandit4   33 Oct  5 06:19 -file09
```

Burada gördüğüüz gibi 10 tane normal br dosya 2 tane gizli dosyamız var. Bu 10 tane normal dosya içinden `human-readable` olan dosyayı bulmamız gerekiyor. Bunun için `file` komutunu kullanacağız.

`file` kullanırken `*` karakterini kullanarak tüm dosyaları seçebiliriz.

```bash
bandit4@bandit:~/inhere$ file *
file: Cannot open `ile00' (No such file or directory)
file: Cannot open `ile01' (No such file or directory)
file: Cannot open `ile02' (No such file or directory)
file: Cannot open `ile03' (No such file or directory)
file: Cannot open `ile04' (No such file or directory)
file: Cannot open `ile05' (No such file or directory)
file: Cannot open `ile06' (No such file or directory)
file: Cannot open `ile07' (No such file or directory)
file: Cannot open `ile08' (No such file or directory)
file: Cannot open `ile09' (No such file or directory)
```
Burada bir hata aldık. Çünkü `file` komutu dosya isimleri `-f` ile başladığında dosya ismini parametre olarak alıyor. Bu yüzden `*` karakterini  `./*` kullanarak bu hatayı çözeceğiz.

```bash
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```

Burada gördüğümüz gibi `./-file07` dosyamız `ASCII text` olarak görünüyor. Yani bu dosya `human-readable` bir dosya. Bundan sonra `cat` ile dosyanın içeriğini ekrana yazdıracağız. 

```bash
bandit4@bandit:~/inhere$ cat ./-file07
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
```

Bu dosyanın içeriğinde şifremiz bulunuyor. Bu şifre ile bir sonraki seviyeye geçebiliriz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*
