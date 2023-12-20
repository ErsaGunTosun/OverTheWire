# Bandit Over The Wire **29**
### Bu Leveldeki Amacımız
> SSH ile bandit29 bağlanıp `ssh://bandit29-git@localhost/home/bandit29-git/repo` adresinde bulanan dosyaları git ile çekip mevcut şifreyi bulmak.


## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cd`: Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar. Daha fazlası için `man cd` komutunu kullanabilirsiniz.
3. `cat`: Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
4. `git`: Git'in bir çok parametresi bulunuyor. Bu parametreler sayesinde farklı işlemler yapmamızı sağlıyor. Daha fazlası için `man git` komutunu kullanabilirsiniz.

## Şifre Bulma
`/tmp` klösörüne altına gidip orada `git` ile bize verilen adresten dosyaları kopyalıyoruz. 

```bash
bandit29@bandit:~$ cd /tmp
bandit29@bandit:/tmp$ git clone ssh://bandit29-git@localhost:2220/home/bandit29-git/repo bandit29kolaydi
bandit29@bandit:/tmp$ cd bandit29kolaydi/
```

`git` ile klonladığımız dosya içinde `README.md` dosyanın içeriğini okuyalım.

```bash
bandit29@bandit:/tmp/bandit29kolaydi$ cat README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>
```

Burada yapacağımız ilk şey başka bir `branch` varmı diye kontrol etmek. Bunuda `git branch -r` veya `git branch --all -vv` ile yapabiliriz. 

```bash
bandit29@bandit:/tmp/bandit29kolaydi$ git branch -r
 origin/HEAD -> origin/master
  origin/dev
  origin/master
  origin/sploits-dev
```
Biz `HEAD` yani `master` üzerinde çalıştığımız görüyoruz. Bunu `dev` olarak değiştirip tekrar `README.md` dosyasını okuyalım.

```bash
bandit29@bandit:/tmp/bandit29kolaydi$ git checkout dev 
Switched to branch 'dev'
bandit29@bandit /tmp/bandit29kolaydi$ cat README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: xbhV3HpNGlTIdnjUrdAlPzc2L6y9EOnS
```

Şifremizi bulduk bununla birlikte bir sonraki level geçebiliriz.


<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com](mailto:ersagun@ersaguntosun.com)*   