# Bandit Over The Wire **28**
### Bu Leveldeki Amacımız
> SSH ile bandit28 bağlanıp `ssh://bandit28-git@localhost/home/bandit28-git/repo ` adresinde bulanan dosyaları git ile çekip mevcut şifreyi bulmak.


## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cd`: Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar. Daha fazlası için `man cd` komutunu kullanabilirsiniz.
3. `cat`: Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
4. `git`: Git'in bir çok parametresi bulunuyor. Bu parametreler sayesinde farklı işlemler yapmamızı sağlıyor. Daha fazlası için `man git` komutunu kullanabilirsiniz.

## Şifre Bulma
Bir öncekinde yaptığımız gibi bundanda `/tmp` klasörün altında işlem yapacağız. Öncelikle `/tmp` klasörüne gidelim.
```bash
bandit28@bandit:~$ cd /tmp
    ```

Şimdi de `git` ile bizi verilen adresten dosyaları kopyalayım.
```bash	
bandit28@bandit:/tmp$ git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo bandit28kolaydi
bandit28@bandit:/tmp$ cd bandit28kolaydi/
```

Şimdi de `cat` ile `README.md` dosyasının içeriğini okuyalım.
```bash
bandit28@bandit:/tmp/bandit28kolaydi$ cat README.md
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
```

Burada bir kullanıcı ismi ve şifre var ama şifreyi göremiyoruz. Burada yapacağımız daha önce bu şifre varmıydı diye log kayıtlarına bakacağız.
```bash
bandit28@bandit:/tmp/bandit28kolaydi$ git log
commit 14f754b3ba6531a2b89df6ccae6446e8969a41f3 (HEAD -> master, origin/master, origin/HEAD)
Author: Morla Porla <morla@overthewire.org>
Date:   Thu Oct 5 06:19:41 2023 +0000

    fix info leak

commit f08b9cc63fa1a4602fb065257633c2dae6e5651b
Author: Morla Porla <morla@overthewire.org>
Date:   Thu Oct 5 06:19:41 2023 +0000

    add missing data

commit a645bcc508c63f081234911d2f631f87cf469258
Author: Ben Dover <noone@overthewire.org>
Date:   Thu Oct 5 06:19:41 2023 +0000

    initial commit of README.md
```

Son yüklemenin commitinde kaçak bir verinin kapatıldığın söylemiş. Bu veriyi görmek için bir önceki commite gidersek şifreyi görebiliriz.
```bash
bandit28@bandit:/tmp/bandit28kolaydi$ git checkout f08b9cc63fa1a4602fb065257633c2dae6e5651b
Note: checking out 'f08b9cc63fa1a4602fb065257633c2dae6e5651b'.
...
```
Bir önceki versiyona döndük şimdi tekrar `README.md` dosyasını okuyalım.
```bash
bandit28@bandit:/tmp/bandit28kolaydi$ cat README.md
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S
```
Gördüğünüz gibi şifremizi bulduk. Şimdi de bir sonraki levele geçebiliriz.


<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com](mailto:ersagun@ersaguntosun.com)*   