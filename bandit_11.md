# Bandit Over The Wire **11**

### Bu Leveldeki Amacımız
> SSH Kullanarak bandit11 bağlanıp `Home directory` içindeki `data.txt`
içerisindeki metini alfabetik olarak 13 harf kaydırarak şifreyi bulmak ve bir sonraki levele geçmek
>
>İhtiyaçımız olabilecek komutlar: `ssh`, `ls`, `cat`, `file`, `du`, `find`, `grep`, `sort`, `uniq`

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd` : Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar.  Daha fazlası için `man cd` komutunu kullanabilirsiniz.
4. `tr` : Karakterler üzerinde işlem yapmamızı sağlayan bir komuttur.Verdiğimiz parametrelere göre karakterleri çevirir veya siler.. Daha fazlası için `man tr` komutunu kullanabilirsiniz.

## Şifre Bulma
ilk başta `cat` komutu ile dosyanın içeriğine bakalım. 
```bash
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf WIAOOSFzMjXXBC0KoSKBbJ8puQm5lIEi
```
Gördüğümüz gibi dosya içinde bir şifre var. Ama bu şifre biraz garip. Burada her harf 13 harf kaydırarak orjinal metine erişeceğiz. Bu şifreleme yöntemini `tr` komutu ile çözeceğiz. Burada `'[A-Za-z]' '[N-ZA-Mn-za-m]'` parametresini kullanacağız.

`'[A-Za-z]'` parametresi ile bütün harfleri seçiyoruz. `'[N-ZA-Mn-za-m]'` parametresi ile ise seçtiğimiz harfleri 13 harf kaydırıyoruz. Bu şekilde şifreyi çözmüş oluyoruz.

```bash
bandit11@bandit:~$ cat data.txt | tr '[A-Za-z]' '[N-ZA-Mn-za-m]'
The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
```

Bu şekilde şifreyi bulmuş olduk. Şimdi bu şifre ile bir sonraki levele geçebiliriz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*