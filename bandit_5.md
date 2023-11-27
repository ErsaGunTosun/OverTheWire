# Bandit Over The Wire **5**

### Bu Leveldeki Amacımız
> SSH kullanarak bandit5 bağlanıp `Home directory` içindeki `inhere` dizini içindeki dosyalardan `human readable / 1033 byte boyuta sahip olan / çalıştırılamayan` dosyayı bulmak ve içersinde bulunan şifre ile bir sonraki seviyeye ulaşmak. 
>
> İhtiyaçımız olabilecek komutlar: `ssh`, `ls`, `cat`, `file`, `du`, 

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd` : Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar.  Daha fazlası için `man cd` komutunu kullanabilirsiniz.
4. `find`: Verdiğimiz parametreler ile dosya sistemlerinde arama yapmamızı sağlar. Daha fazlası için `man find` komutunu kullanabilirsiniz.

## Şifreyi Bulma
Burada istediği dosyayı dizinleri gezerek bulabiliriz ama bu yöntem çok uzun sürecektir. Bunun yerine `find` komutunu kullanarak istediğimiz dosyayı bulabiliriz.

Burada bizden istediği 3 şey var.
1. `human readable`
    > Bunu yapabilmek için `-type f -readable` parametrelerini kullanacağız. `-type f` ile dosya olduğunu belirtiyoruz. `-readable` ile okunabilir olduğunu belirtiyoruz.
2. `1033 byte boyutunda`
    > Bunu yapabilmek için `-size 1033c` parametresini kullanacağız. `-size` ile dosya boyutunu belirtiyoruz. `1033c` ile 1033 byte olduğunu belirtiyoruz.
3. `çalıştırılamayan`
    > Bunu yapabilmek için `-not -executable` parametresini kullanacağız. `-executable` ile çalıştırılabilen `-not` ilede bunun tam tersi olacağınu belirtiyoruz.

ilk önce `inhere` dizinine gireceğiz.

```bash
bandit5@bandit:~$ cd inhere/
```
Burada `find` komutunu kullanarak istediğimiz dosyayı bulacağız.
```bash
bandit5@bandit:~/inhere$ find ./ -type f -readable -size 1033c -not -executable
./maybehere07/.file2
```

Bize söylediği 3 özelliğe sahip dosyamız `./maybehere07/.file2` dosyası. Bu dosyanın içeriğini okumak için `cat` komutunu kullanacağız.

```bash
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
```

Bu dosyanın içeriğinde şifremiz bulunuyor. Bu şifre ile bir sonraki seviyeye geçebiliriz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*
