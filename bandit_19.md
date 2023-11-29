# Bandit Over The Wire **19**
### Bu Leveldeki Amacımız 
> SSH kullanarak bandit19 bağlanmak ve `Home Directory` atlında bulunan `setuid` ile çalışan `bandit20-do` dosyasını çalıştırmak. Bu dosya `bandit20` kullanıcısının şifresini bulmamızı sağlayacak.
>

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd` : Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar.  Daha fazlası için `man cd` komutunu kullanabilirsiniz.
4. `file`: Dosya türünü belirlememizi sağlar. Daha fazlası için `man file` komutunu kullanabilirsiniz.

## Bilinmesi Gerekenler
- Dosya izinleri nelerdir ?
    > Bir dosya veya dizin üzerindeki erişim denetimini kontrol eder.
    >
    > Dosya izinleri, Linux sistemini daha güvenli hale getirmek için de kullanılır. Örneğin, bir dosyanın sahipliğiyle aynı gruba ait olmayan bir kullanıcı, dosyayı çalıştırma iznine sahip olmayabilir. Bu, kötü amaçlı bir uygulamanın yürütülmesini önlemeye yardımcı olur.
    >
    > Dosya izinleri, üç ayrı kategoriye ayrılır: kullanıcı, grup ve diğerleri. Kullanıcı, dosyanın sahibidir. Grup, dosyanın sahibinin ait olduğu gruptur. Diğerleri, dosyanın sahibi veya grubuyla aynı grupta olmayan tüm kullanıcılardır.
    > Bunlardan her birisine okuma (r), yazma(w) ve çalıştırma (x) olmak üzere üç tipte yetki verilebilir veya yetki kısıtlaması yapılabilir. Yetkiler sembolik (rw-) ve nümerik (110) olmak üzere iki şekilde ifade edilebilir.
    > Bu yetkiler ile ilgili daha fazla bilgiyi [buradan](http://www.baskent.edu.tr/~tkaracay/etudio/agora/nnn/chmod.htm "Türkçe") bulabilirsiniz.
- Setuid nedir ?
    > Setuid, bir dosyanın çalıştırılabilir dosya olarak işaretlenmesini sağlayan bir Linux dosya izni türüdür. Setuid, bir dosyanın sahibi tarafından belirlenen kullanıcı kimliğini kullanarak dosyayı çalıştırmak için izin verir. Bu, dosyanın sahibi olmayan bir kullanıcının dosyayı çalıştırmasına izin verir.
- Setgid nedir ?
    > Setgid, bir dosyanın çalıştırılabilir dosya olarak işaretlenmesini sağlayan bir Linux dosya izni türüdür. Setgid, bir dosyanın sahibi tarafından belirlenen grup kimliğini kullanarak dosyayı çalıştırmak için izin verir. Bu, dosyanın sahibi olmayan bir kullanıcının dosyayı çalıştırmasına izin verir.
- Sticky bit nedir ?
    > Sticky, bir dizin altında bulunan dosyalarda sadece dizin sahibinin silme ve değiştirme yetkisi bulunur, diğer kullanıcıların ise sadece dosya oluşturma ve okuma yetkisi bulunur. 
## Şifre Bulma
İlk olarak `ls -la` komutunu kullanarak bulunduğumuz dizindeki dosyaları listeliyoruz.
```bash
bandit19@bandit:~$ ls -la
total 36
drwxr-xr-x  2 root     root      4096 Oct  5 06:19 .
drwxr-xr-x 70 root     root      4096 Oct  5 06:20 ..
-rwsr-x---  1 bandit20 bandit19 14876 Oct  5 06:19 bandit20-do
-rw-r--r--  1 root     root       220 Jan  6  2022 .bash_logout
-rw-r--r--  1 root     root      3771 Jan  6  2022 .bashrc
-rw-r--r--  1 root     root       807 Jan  6  2022 .profile
```

burada `bandit20-do` dosyasının `setuid` ile çalıştığını görüyoruz.
`file` ile `bandit20-do` dosyasının türünü bakalım.
```bash
bandit19@bandit:~$ file bandit20-do
bandit20-do: setuid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, BuildID[sha1]=037b97b430734c79085a8720c90070e346ca378e, for GNU/Linux 3.2.0, not stripped
```
burada `setuid` olduğunu görüyoruz. Şimdi bu dosyayı çalıştıralım.
```bash
bandit19@bandit:~$ ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do id
```
burada `bandit20-do` dosyasının nasıl çalıştırılacağını gösteriyor. Şimdi `bandit20` kullanıcısının şifresini bulmak için `cat` komutunu kullanalım.
```bash
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
VxCazJaVykI6W36BkBU0mJTCM8rR95XT
```
burada `bandit20` kullanıcısının şifresini bulduk. Bir sonraki levele bu şifre ile geçebiliriz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*