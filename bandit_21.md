# Bandit Over The Wire **21**
### Bu Leveldeki Amacımız
> SHH Kullanarak bandit21 bağlanıp `cron` tarafından belli bir zamana dayalı olarak çalışan işi bulup onun yapılandırma dosyalarının içindeki bir sonraki levelin şifresini bulmak.
>

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat`: Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd`: Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar. Daha fazlası için `man cd` komutunu kullanabilirsiniz.

## Bilinmesi Gerekenler
- Cron nedir ?
    >  Bir Görevi ilerleyen bir zamanda tekrarlamak için kullanılan bir programdır.
    > `cron job` ise görevi bellirli bir zamanda tekrarlamak için verilen kod parçasıdır.
    >
    > `Cron` interaktif olmayan görevleri yürütmek için arkaplanda çalışır.

## Şifre Bulma
İlk olarak bize cron dosyalarının sakladığı yeri vermiştir. Bu yeri bulup içindeki dosyaları listelememiz gerekiyor. Bunun için `ls` komutunu kullanabiliriz.

```bash
bandit21@bandit:~$ ls /etc/cron.d/
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
Burada bir sonraki level yani bandit22 için bir `cronjob` dosyası olduğunu görebiliriz. Bu dosyayı `cat` komutu ile açıp içindeki kodu inceleyelim.

```bash
bandit21@bandit:~$ cat /etc/cron.d/cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```
Burada `cronjob_bandit22.sh` dosyasının her dakika çalıştığını görebiliriz. Bu dosyayı da `cat` komutu ile açıp içindeki kodu inceleyelim.

```bash
bandit21@bandit:~$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

Bu dosyanın içini incelediğimizde `/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv` dosyasının `chmod` ile izinlerinin değiştirildiğini ve `cat` ile `bandit22` şifresinin bu dosyaya yazıldığını görebiliriz. Bu dosyayı da `cat` komutu ile açıp içindeki şifreyi görebiliriz.

```bash
bandit21@bandit:~$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff
```

Bu şifre ile bir sonraki levele geçebiliriz.


<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*

