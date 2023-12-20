# Bandit Over The Wire **27**
### Bu Leveldeki Amacımız
> SSH ile bandit27 bağlanıp `ssh://bandit27-git@localhost/home/bandit27-git/repo` adresinde bulanan dosyaları git ile çekip mevcut şifreyi bulmak.
>

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cd`: Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar. Daha fazlası için `man cd` komutunu kullanabilirsiniz.
3. `git`: Git'in bir çok parametresi bulunuyor. Bu parametreler sayesinde farklı işlemler yapmamızı sağlıyor. Daha fazlası için `man git` komutunu kullanabilirsiniz.
4. `cat`: Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.

## Bilinmesi Gerekenler
- Git nedir ?
> Git, dağıtık çalışan bir sürüm kontrol ve kaynak kod yönetim sistemidir.Bir projenin kaynak kodunun farklı sürümlerini saklamak ve yönetmek için kullanılır. Bu sayede, bir proje üzerinde birden fazla kişi çalışabilir ve projenin geçmişine kolayca geri dönülüp eski sürümler alınabilir.
- GitHub nedir ?
> GitHub, 2005 yılında duyurulan ve günümüzde yazılımcılar arasında oldukça popüler hale gelen git için bir depolama alanıdır. Bulut tabanlı bir istemci olan GitHub, pek çok açık kaynaklı projeye ev sahipliği yapıyor. Yazılımcılar arasında sıklıkla kullanılan GitHub, organize olmayı sağlayan büyük bir platformdur.

## Şifre Bulma
İlk olarak dosya işlemi yapabilmemiz için `/tmp` klasörünün altına gitmeliyiz.

```bash
bandit27@bandit:~$ cd /tmp
```
Bundan sonra `git'in` `clone` komudunu kullanarak bize verdiği adreste dosyaları çekip içinde bulunan `README.md` dosyasını okuyalım.

```bash
bandit27@bandit:/tmp$ git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo bandit27kolaydi
Cloning into 'bandit27kolaydi'...
...
bandit27@bandit:/tmp$ cd bandit27kolaydi/
```
```bash
bandit27@bandit:/tmp/bandit27kolaydi$ ls -a
. ..  .git  README
bandit27@bandit:/tmp/bandit27kolaydi$ cat README
The password to the next level is: AVanL161y9rsbcJIsFHuw35rjaOM19nR
```
Böylece mevcut şifreyi bulmuş olduk.


<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*