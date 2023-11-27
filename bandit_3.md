# Bandit Over The Wire **3**

### Bu Leveldeki Amacımız
> SSH kullanarak bandit3 bağlanıp `Home directory` içindeki `inhere` dizini içindeki `hidden` dosyasını okumak ve burada bulunan şifre ile Bandit4'e geçmek.
>
> İhtiyaçımız olabilecek komutlar: `ssh`, `ls`, `cat`, `file`, `du`, `find`



## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd` : Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar.  Daha fazlası için `man cd` komutunu kullanabilirsiniz.


## Şifreyi Bulma

Bağlantığımızı yapmıştık. Şimdi bulunduğumuz dizindeki dosyaları listelemek için `ls` komutunu kullanacağız.

```bash
bandit3@bandit:~$ ls
inhere
```
Burada görüdüğümüz bir `directory` bizim şifremiz burada olabilir. Bu dizine girmek için `cd` komutunu kullanacağız.

```bash
bandit3@bandit:~$ cd inhere/
```
Burada `ls` komutunu kullanarak dizindeki dosyaları listeliyoruz.

```bash
bandit3@bandit:~/inhere$ ls
```

`ls` komudunu çalıştrdığımız zaman bir şey göremedik çünkü  `ls` komuduna gizli dosyaları göster parametresini girmediğimiz için gizli dosyaları göremiyoruz. Bu parametre `-a` olacak.

```bash
bandit3@bandit:~/inhere$ ls -a
.  ..  .hidden
```
Burada `.hidden` dosyası bulunuyor. Bu dosyanın içeriğini okumak için `cat` komutunu kullanacağız.

```bash
bandit3@bandit:~/inhere$ cat .hidden
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
```
Bu dosyanın içeriğinde şifremiz bulunuyor. Bu şifre ile bir sonraki seviyeye geçebiliriz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*


