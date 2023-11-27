# Bandit Over The Wire **10**

### Bu Leveldeki Amacımız
> SSH kullanarak bandit10 bağlanıp `Home directory` içindeki base64 ile encode edilmiş `data.txt` dosyasını decode hale getirip içerisinde bulunan şifre ile bir sonraki levele geçmek
> 
>İhtiyaçımız olabilecek komutlar: `ssh`, `ls`, `cat`, `file`, `du`, `find`, `grep`, `sort`, `uniq`

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd` : Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar.  Daha fazlası için `man cd` komutunu kullanabilirsiniz.
4. `base64`: 8 bitlik verileri 64 bitlik bloklara dönüştüren bir kodlama şemasıdır. Bu kodlama şeması, verileri metin formatında iletmeye veya depolamaya olanak tanır. Daha fazlası için `man base64` komutunu kullanabilirsiniz.

## Şifre Bulma
ilk başta `cat` komutu ile dosyanın içeriğine bakalım. 
```bash
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIDZ6UGV6aUxkUjJSS05kTllGTmI2blZDS3pwaGxYSEJNCg==
```
Gördüğümüz gibi dosya içinde bir şifre var. Ama bu şifre base64 ile encode edilmiş. Bunun için `base64` komutunu kullanacağız.
Burada `-d` parametresi ile decode edeceğiz.

```bash
bandit10@bandit:~$ base64 -d data.txt
The password is 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
```

Burada şifre ile bir sonraki seviyeye geçebiliriz.
<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*
