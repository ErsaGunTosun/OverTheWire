# Bandit Over The Wire **32**
### Bu Leveldeki Amacımız
> SSH ile bandit32 bağlanıp oradan kaçmak


## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cd`: Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar. Daha fazlası için `man cd` komutunu kullanabilirsiniz.
3. `cat`: Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
4. `file`: Bir dosyanın türünü belirler. Daha fazlası için `man file` komutunu kullanabilirsiniz.

## Bilimesi Gerekenler
- Positional Parameter nedir ?
> Positional Parameter'lar, komut satırına giren argümanları temsil eden özel değişkenlerdir. Bunlar, komutun çalıştırılması sırasında komut adından sonra gelen değerlerdir. Argümanların sırasına göre numaralandırılırlar, `$1`'den başlayarak devam ederler.
>
>`$0` özel bir parametredir ve çalıştırılan script'in adını içerir.İlk çalıştırılan komut `sh` komutu olduğundan $0 değişkenine `sh` parametresi atanır.


## Şifre Bulma
İlk olarak `Home Directory` altında bir şey olup olmadığına bakalım. 

```bash
>> ls
sh: 1: LS: Permission denied 
>> dir
sh: 1: DIR: Permission denied
>> ls ./
sh: 1: LS: Permission denied
```
Yazdığımız her şey büyük harf olarak gidiyor bundan dolayıda hata alıyoruz. Burada `Positional Parameter` ilk olan yani `$0` kullanarak terminali sıfırlayabiliriz.

```bash
>> $0
$
$ ls -a
.  ..  .bash_logout  .bashrc  .profile  uppershell
```

Bir sonraki levelin şifresi almak için `/etc/bandit_pass` klasörüne gidiyoruz.
    
```bash
$ cd /etc/bandit_pass
$ ls
bandit0   bandit11  bandit14  bandit17  bandit2   bandit22  bandit25  bandit28  bandit30  bandit33  bandit6  bandit9
bandit1   bandit12  bandit15  bandit18  bandit20  bandit23  bandit26  bandit29  bandit31  bandit4   bandit7
bandit10  bandit13  bandit16  bandit19  bandit21  bandit24  bandit27  bandit3   bandit32  bandit5   bandit8
```

Burada `file` ile dosyaların türlerine bakalım.
```bash
$ file ./*
...
./bandit31: regular file, no read permission
./bandit32: regular file, no read permission
./bandit33: ASCII text
./bandit4:  regular file, no read permission
./bandit5:  regular file, no read permission
./bandit6:  regular file, no read permission
...
```
Burada `bandit33` dosyasının içeriğini okuyabileceğimiz gördük bunu okuyalım.
```bash
$ cat ./bandit33
odHo63fHiFqcWWJG9rLiLDtPm45KzUKy
```

Bu şifre ile son basamağa gelebiliriz.
<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*