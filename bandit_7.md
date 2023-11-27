# Bandit Over The Wire **7**

### Bu Leveldeki Amacımız
>SSH kullanarak bandit7 bağlanıp `Home directory` içindeki `data.txt` dosyasının içindeki veriler arasında bulunan `millionth` satırı bulmak ve içersinde bulunan şifre ile bir sonraki seviyeye ulaşmak.

>İhtiyaçımız olabilecek komutlar: `ssh`, `ls`, `cat`, `file`, `du`, `find`, `grep`, `sort`


## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd` : Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar.  Daha fazlası için `man cd` komutunu kullanabilirsiniz.
4. `grep` : Bir dosya içinde arama yapmamızı sağlar. Daha fazlası için `man grep` komutunu kullanabilirsiniz.

## Şifre Bulma 
Burada bize verilen dosya içindeki veriler arasında bulunan `millionth` satırı bulmamız isteniyor. Bunun için `grep` komutunu kullanacağız.

ilk başta `cat` komutu ile dosyanın içeriğine bakalım. 
```bash
bandit6@bandit:~$ cat data.txt
...
Barth's VF433DBGVHONz1feBPEs4yL1nYkht1vq
inchoating      tYCSpQu0l8frbFrsqkK2ra77KkCmaIN2
checkpoint      WmhYI1bs6amBFUPZUJPbmdmOxRri9Rmm
Wycherley's     r0E9d7I3ItaXOxKshARe6Bu4swD42Et0
beware  wGQ4AapDykc3WoGQeGKSpe2g4kSFUSaI
kennelled       GWmE134nyfnan9SwUkb7lsRXTqkBUyHa
...
```
Gördüğümüz gibi dosya içinde bir çok satır var. Bunların arasında `millionth` satırı bulmamız gerekiyor. Bunun için `grep` komutunu kullanacağız.

`grep` komutu ile dosya içinde arama yapabiliyoruz. Bunun için `grep` komutunun `-n` parametresini kullanacağız. `-n` parametresi ile arama sonucunda bulunan satırın numarasınıda görebileceğiz. 

```bash
bandit6@bandit:~$ grep -n "millionth" ./data.txt
10032:millionth TESKZC0XvTetK0S9xNwm25STk5iWrBvP
```
Gördüğümüz gibi `millionth` satırı `10032` numaralı satırda bulunuyor. Bu şifre ile bir sonraki seviyeye geçebiliriz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*


