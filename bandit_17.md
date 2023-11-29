# Bandit Over The Wire **17**
### Bu Leveldeki Amacımız 
> SSH kullanarak bandit17 bağlanıp `Home Directory` altında iki tane şifre dosyası olduğu ve bunların arasındaki farklı satırı bulup bir sonraki level için şifreyi elde etmek.

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd` : Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar.  Daha fazlası için `man cd` komutunu kullanabilirsiniz.
4. `diff`: İki dosya arasındaki farkları gösterir. Daha fazlası için `man diff` komutunu kullanabilirsiniz.
## Şifre Bulma
İlk olarak `ls` komutu ile bulunduğumuz dizindeki dosyaları listeliyoruz.
```bash
bandit17@bandit:~$ ls
passwords.new  passwords.old
```
Burada iki tane dosya olduğunu görüyoruz. Bu dosyaların içeriğine bakalım.
```bash
bandit17@bandit:~$ cat passwords.new
fMOYjvUY5uCDCbweKVmOqsxGmiqCug2W
i9zj4BOYY9OATSdwqBnAAsPTyoOpdlVW
4ipWQKzhSdNXLNkn3ytQAXapg0sm21xj
vCSTATER0iHC3AcfoaaugfYPpe2KbxlY
zeRdb0bCAurzvgkBbrdn1Vd2k7EzEquQ
63a4svAasv5xD1SsKq7UejZkFMwQ8TrC
ESR2tsFvQVuPdheIrV1cQHRzWPqjEspR
hIZ7ehVTkQ0iU8z3HIQaUBH9at9yRvpP
ub3exqqKUBxwGYvP93GkoZdNgYMCg2ax
25LhvrMLb4x4qFsl7CDsTi2bxI5OImIr
UZFBY0MYMJp0fHlejKIUBDvuHFxgbWDu
...
```
```bash
bandit17@bandit:~$ cat passwords.old
fMOYjvUY5uCDCbweKVmOqsxGmiqCug2W
i9zj4BOYY9OATSdwqBnAAsPTyoOpdlVW
4ipWQKzhSdNXLNkn3ytQAXapg0sm21xj
vCSTATER0iHC3AcfoaaugfYPpe2KbxlY
zeRdb0bCAurzvgkBbrdn1Vd2k7EzEquQ
63a4svAasv5xD1SsKq7UejZkFMwQ8TrC
ESR2tsFvQVuPdheIrV1cQHRzWPqjEspR
hIZ7ehVTkQ0iU8z3HIQaUBH9at9yRvpP
ub3exqqKUBxwGYvP93GkoZdNgYMCg2ax
25LhvrMLb4x4qFsl7CDsTi2bxI5OImIr
UZFBY0MYMJp0fHlejKIUBDvuHFxgbWDu
b7YeGq53MuTvW2W9RenT8ETHfyFrHejK
...
```
Burada iki tane içinde uzun şifrelerin olduğu dosya olduğunu görüyoruz. Bu dosyaların içeriğini `diff` komutu ile karşılaştırıp farklı olan satırı bulacağız.
```bash
bandit17@bandit:~$ diff passwords.old passwords.new
42c42
< p6ggwdNHncnmCNxuAt0KtKVq185ZU7AW
---
> hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
```
Burada ilk satırda `42c42` olarak belirtiği 42. satırda değişiklik olduğunu gösteriyor. `<` işareti ilk dosya içindeki farklılığı `>` ikinci dosyadaki farklığı gösteriyor.

Bizim şifremiz passwords.new içinde olduğu için  `>` sonra gelen bizim şifremiz oluyor ve bununla birlikte bir sonraki levele geçebiliyoruz.


<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*