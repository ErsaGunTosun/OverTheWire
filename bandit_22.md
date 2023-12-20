# Bandit Over The Wire **22**
### Bu Leveldeki Amacımız
> SSH kullanarak bandit22 bağlanıp bir önceki level gibi `cron` ile tekrarlanan bir işlemi inceleyerek şifrenin yerini bulmak ve bir sonraki level için şifreyi bulmak.

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat`: Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd`: Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar. Daha fazlası için `man cd` komutunu kullanabilirsiniz.


## Şifre Bulma
İlk olarak bize cron dosyalarının sakladığı yeri vermiştir. Bu yeri bulup içindeki dosyaları listelememiz gerekiyor. Bunun için `ls` komutunu kullanabiliriz.

```bash
bandit22@bandit:~$ ls -al /etc/cron.d/
total 56
drwxr-xr-x   2 root root  4096 Oct  5 06:20 .
drwxr-xr-x 106 root root 12288 Oct  5 06:20 ..
-rw-r--r--   1 root root    62 Oct  5 06:19 cronjob_bandit15_root
-rw-r--r--   1 root root    62 Oct  5 06:19 cronjob_bandit17_root
-rw-r--r--   1 root root   120 Oct  5 06:19 cronjob_bandit22
-rw-r--r--   1 root root   122 Oct  5 06:19 cronjob_bandit23
-rw-r--r--   1 root root   120 Oct  5 06:19 cronjob_bandit24
-rw-r--r--   1 root root    62 Oct  5 06:19 cronjob_bandit25_root
-rw-r--r--   1 root root   201 Jan  8  2022 e2scrub_all
-rwx------   1 root root    52 Oct  5 06:20 otw-tmp-dir
-rw-r--r--   1 root root   102 Mar 23  2022 .placeholder
-rw-r--r--   1 root root   396 Feb  2  2021 sysstat
```
Burada bir sonraki level yani bandit23 için bir `cronjob` dosyası olduğunu görebiliriz. Bu dosyayı `cat` komutu ile açıp içindeki kodu inceleyelim.

```bash
bandit22@bandit:~$ cat /etc/cron.d/cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
```
Burada `cronjob_bandit23.sh` dosyasının her dakika çalıştığını görebiliriz. Bu dosyayı da `cat` komutu ile açıp içindeki kodu inceleyelim.

```bash
bandit22@bandit:~$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget

```
Burada bir bash komudu görüyoruz. `myname` ve `mytarget` isminde iki değişken tanımlanmış ve bu değişkenlerin içine `whoami` ve `echo I am user $myname | md5sum | cut -d ' ' -f 1` komutları ile değerler atanmış. Daha sonra `echo` komutu ile `/etc/bandit_pass/$myname` dosyasının içeriği `/tmp/$mytarget` dosyasına yazdırılmış. Hedef dosyası tekrar tekrar bulmak yerine bu komut dosyasının içindeki komutları çalıştırarak hedef dosyayı bulabiliriz.

```bash
bandit22@bandit:~ echo I am user $myname | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
```
Şifrenin nereye kaydedildiğini bulduk. Şimdi bu dosyayı açıp içindeki şifreyi bulalım.

```bash
bandit22@bandit:~$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G
```

Bu şifre ile bir sonraki levele geçebiliriz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*

