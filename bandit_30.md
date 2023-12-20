# Bandit Over The Wire **30**
### Bu Leveldeki Amacımız
> SSH ile bandit30 bağlanıp `ssh://bandit30-git@localhost/home/bandit30-git/repo` adresinde bulanan dosyaları git ile çekip mevcut şifreyi bulmak.


## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cd`: Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar. Daha fazlası için `man cd` komutunu kullanabilirsiniz.
3. `cat`: Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
4. `git`: Git'in bir çok parametresi bulunuyor. Bu parametreler sayesinde farklı işlemler yapmamızı sağlıyor. Daha fazlası için `man git` komutunu kullanabilirsiniz.


## Şifre Bulma
Daha öncekiler gibi yine `/tmp` klasörünün altına gidip `git` ile bize verilen adresten dosyaları alıp içine bakalım.

```bash
bandit30@bandit:~$ cd /tmp
bandit30@bandit:/tmp$  git clone ssh://bandit30-git@localhost:2220/home/bandit30-git/repo bandit30kolaydi
bandit30@bandit:/tmp$ cd bandit30kolaydi/
```

```bash
bandit30@bandit:/tmp/bandit30kolaydi$ ls -a
.  ..  .git  README.md
```

Buradaki  `README.md` dosyasına bir bakalım
```bash
bandit30@bandit:/tmp/bandit30kolaydi$ cat README.md
just an epmty file... muahaha
```
İçinde kayda değer bir şey olmadığını görüyoruz. 

Birde `git log` ile log kayıtlarına bakalım.

```bash
bandit30@bandit:/tmp/bandit30kolaydi$ git log
commit d39631d73f786269b895ae9a7b14760cbf40a99f (HEAD -> master, origin/master, origin/HEAD)
Author: Ben Dover <noone@overthewire.org>
Date:   Thu Oct 5 06:19:45 2023 +0000

    initial commit of README.md

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..029ba42
--- /dev/null
+++ b/README.md
@@ -0,0 +1 @@
+just an epmty file... muahaha
```

Burada da kayda değer bir şey bulamadık.Bir de `Branchlere` bakalım.

```bash
bandit30@bandit:/tmp/bandit30kolaydi$ git branch -r
  origin/HEAD -> origin/master
  origin/master
```
Burada da bir şey olmadığını gördük. Son olarak bakacağımız yer `git tag`

```bash
bandit30@bandit:/tmp/bandit30kolaydi/.git$ git tag
secret
bandit30@bandit:/tmp/bandit30kolaydi/.git$ git show secret
OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt
```

Şifremizi bulduk bununla birlikte bir sonraki levele geçebiliriz.


<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*
