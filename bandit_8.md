# Bandit Over The Wire **8**

### Bu Leveldeki Amacımız
>SSH kullanarak bandit8 bağlanıp `Home directory` içindeki `data.txt` dosyasının içindeki veriler arasında tekrar etmeyen satırı bulmak ve bu satırın içersinde bulunan şifre ile bir sonraki seviyeye ulaşmak.
>
>İhtiyaçımız olabilecek komutlar: `ssh`, `ls`, `cat`, `file`, `du`, `find`, `grep`, `sort`, `uniq`

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd` : Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar.  Daha fazlası için `man cd` komutunu kullanabilirsiniz.
4. `sort`: Bir dosyanın içindeki verileri sıralamamızı sağlar. Daha fazlası için `man sort` komutunu kullanabilirsiniz.
5. `uniq`: Bir dosyanın içindeki verileri tekrar etmeyen şekilde sıralamamızı sağlar. Daha fazlası için `man uniq` komutunu kullanabilirsiniz.


## Şifre Bulma
Burada bize verilen dosya içindeki veriler arasında tekrar etmeyen satırı bulmamız isteniyor. Bunun için `sort` ve `uniq` komutlarını kullanacağız.

Uniq komudunu tek başına kullanada bilirizim ama bu tekrarlanan satırları yanlış tespit etmesine sebeb olabilir. Bundan dolayı önce `sort` komutunu kullanıp verileri sıralayacağız. Daha sonra `uniq` komutunu kullanarak tekrar etmeyen satırı bulacağız. `uniq` kullanırken `-u` parametresini kullanacağız. Bu parametre ile tekrar etmeyen satırları bulacağız.

`sort` ile sıraladığımız veriyi `uniq` komuduna aktarmak için `|` kullanacağız. Bu işleme `pipe` işlemi deniyor. Bu işlem ile bir komudan çıkan veriyi başka bir komuta aktarabiliyoruz.

```bash
bandit7@bandit:~$ sort data.txt | uniq -u
EN632PlfYiZbn3PhVK3XOGSlNInNE00t
```
Gördüğümüz gibi `uniq` komutu ile tekrar etmeyen satırı bulduk. Bu şifre ile bir sonraki seviyeye geçebiliriz.
<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*

