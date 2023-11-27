# Bandit Over The Wire **6**


### Bu Leveldeki Amacımız
>SSH kullanarak bandit6 bağlanıp `Home directory` içindeki `inhere` dizini içindeki dosyalardan `owned user bandit7 / owned group bandit6 / size 33byte` dosyayı bulmak ve içersinde bulunan şifre ile bir sonraki seviyeye ulaşmak.
>
>İhtiyaçımız olabilecek komutlar: `ssh`, `ls`, `cat`, `file`, `du`, `find`

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd` : Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar.  Daha fazlası için `man cd` komutunu kullanabilirsiniz.
4. `find`: Verdiğimiz parametreler ile dosya sistemlerinde arama yapmamızı sağlar. Daha fazlası için `man find` komutunu kullanabilirsiniz.

## Bilmemiz gerekenler 
- User Nedir ?
    >Bir sistemde çalışan gerçek veya sanal bir kişiyi temsil eden bir kimliktir. User, bir sisteme giriş yapmak, dosya ve dizinleri kullanmak ve sistem kaynaklarını kullanmak için kullanılır.
- Group Nedir ?
    > Bir sistemde çalışan kullanıcıları mantıksal olarak gruplayan bir kimliktir. Group, kullanıcılara dosya ve dizinlere erişim izinleri vermek için kullanılır

## Şifreyi Bulma
Burada yine find komudunu kullanacağız. Ama bu sefer biraz daha farklı olacak. Çünkü bizden istediği dosya sahibi ve grup bilgileri de var. Bunun için `find` komutunun `-user` ve `-group` parametrelerini kullanacağız.

Burada bizden istediği 3 şey var.
1. `owned user bandit7`
    > Bunu yapabilmek için `-user bandit7` parametresini kullanacağız. `-user` ile dosya sahibini belirtiyoruz. `bandit7` ilede dosya sahibinin `bandit7` olduğunu belirtiyoruz.
2. `owned group bandit6`
    > Bunu yapabilmek için `-group bandit6` parametresini kullanacağız. `-group` ile dosya grubunu belirtiyoruz. `bandit6` ilede dosya grubunun `bandit6` olduğunu belirtiyoruz.
3. `size 33byte`
    > Bunu yapabilmek için `-size 33c` parametresini kullanacağız. `-size` ile dosya boyutunu belirtiyoruz. `33c` ile 33 byte olduğunu belirtiyoruz.

Bir önceki seviyede arama yaparken `./` dizini içinde yapmıştık ama bu sefer bizim bulunduğumuz dizi boş. Burada arama yapmamız bize bir sonuç çıkarmayacak. Bunun için bu sefer aramamızı `/` dizini yani kök dizini içinde yapacağız.

```bash
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c
find: ‘/etc/ssl/private’: Permission denied
find: ‘/etc/polkit-1/localauthority’: Permission denied
find: ‘/etc/sudoers.d’: Permission denied
find: ‘/etc/multipath’: Permission denied
find: ‘/root’: Permission denied
find: ‘/boot/efi’: Permission denied
...
/var/lib/dpkg/info/bandit7.password
....
```
Burada bize bir çok hata verdi ve istediğimiz cevap bu hatalar arasında kayboldu.Yine dikkatlice bakarsan bulabiliriz ama biz bunu kolaylaştırmak için `2>/dev/null` parametresini kullanacağız. 

`2>` Nedir ? Bu linuxta hata çıktılarını yönlendirmek için kullanılan bir komuttur. Linux çıktı yönlendirme hakkında daha fazla bilgiye [buradan](https://www.yusufsezer.com.tr/linux-cikti-yonlendirme/ "Türkçe") ulabilirsiniz.

`/dev/null` Nedir ? Bu linuxta çıktıları yok etmek için kullanılan bir komuttur. Bir kara deliğe benzetebiliriz. 

Şimdi bu parametre ile bir defa daha deneyip istediğimiz dosyayı bulup içeriğini `cat` ile okuyacağız.

```bash
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password

bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
```

Bu dosyanın içeriğinde şifremiz bulunuyor. Bu şifre ile bir sonraki seviyeye geçebiliriz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*
