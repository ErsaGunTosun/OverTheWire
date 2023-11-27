# Bandit Over The Wire **9**

### Bu Leveldeki Amacımız
>SSH kullanarak bandit9 bağlanıp `Home directory` içindeki `data.txt` dosyasının içindeki `=` ile başlayan satırı bulmak ve bu satırın içersinde bulunan şifre ile bir sonraki seviyeye ulaşmak.
>
>İhtiyaçımız olabilecek komutlar: `ssh`, `ls`, `cat`, `file`, `du`, `find`, `grep`, `sort`, `uniq`

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd` : Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar.  Daha fazlası için `man cd` komutunu kullanabilirsiniz.
4. `strings`: Dosyalardaki metinleri ve karakter dizilerini bulmak için kullanılan bir komut satırı aracıdır. Daha fazlası için `man strings` komutunu kullanabilirsiniz.


## Şifre Bulma
Bağlantığımızı yapmıştık. Şimdi bulunduğumuz dizindeki dosyaları listelemek için `ls` komutunu kullanacağız.

```bash
bandit9@bandit:~$ ls
data.txt
```
Burada `data.txt` dosyası bulunuyor. Bu dosyanın içeriğini okumak için `cat` komutunu kullanacağız.

```bash
bandit9@bandit:~$ cat data.txt
4SA&l"
FR^+
3+2)`
^gjb
zVC&
=2""L(
Qu
...
```

```bash
bandit9@bandit:~$ grep "=" data.txt
grep: data.txt: binary file matches
```
Burada bize bir hata verdi. Çünkü `grep` komutu dosya içindeki metinleri ararken bazı dosyaları binary olarak algılıyor. Bunun için `strings` komutunu kullanacağız.

```bash
bandit9@bandit:~$ strings data.txt | grep "="
=2""L(
x]T========== theG)"
========== passwordk^
Y=xW
t%=q
========== is
4=}D3
{1\=
FC&=z
=Y!m
        $/2`)=Y
4_Q=\
MO=(
?=|J
WX=DA
{TbJ;=l
[=lI
========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
>8=6
=r=_
=uea
zl=4
```
Burada bize bir çok sonuç verdi. Bunların arasında `========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s` satırı bize şifremizi veriyor. Bu şifre ile bir sonraki seviyeye geçebiliriz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*

