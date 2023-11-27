# Bandit Over The Wire **0**

### Bu Leveldeki Amacımız
> SSH kullanarak bandit0 bağlanıp `Home directory` içindeki `readme` dosyasını okumak ve burada bulunan şifre ile Bandit1'e geçmek.
>
> İhtiyaçımız olabilecek komutlar: `ssh`, `ls`, `cat`, `file`, `du`, `find`

## SSH ile bağlanma 
Windows üzerinde çözmeye çalışıyorsak `PowerShell` kullanacağız. Linux üzerinde ise `Terminal` kullanacağız.

Terminali açtıktan sonra `ssh` komutunu kullanarak bağlanacağız. Buradaki yapı `ssh kullanıcı_adı@ip_adresi -p port_numarası` şekilde olacak.

Banditlere bağlanmamız için Over the Wire ip adresi olarak `bandit.labs.overthewire.org` kullanacağız. Port numarası ise `2220` olacak. Kullanıcı adımızda her seviyenin kendi adı olacak. Bu seviye için kullanıcı adımız `bandit0` olacak.

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```
Bu komudumuzla ssh ile bandit0 bağlandık bundan sonraki amacımız şifreyi bulmak.

## Kullancağımız Komutlar
 1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.

## Şifreyi Bulma
Bağlantığımızı yapmıştık. Şimdi bulunduğumuz dizindeki dosyaları listelemek için `ls` komutunu kullanacağız.

```bash
bandit0@bandit:~$ ls
readme
```
Burada `readme` dosyası bulunuyor. Bu dosyanın içeriğini okumak için `cat` komutunu kullanacağız.

```bash
bandit0@bandit:~$ cat readme 
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
```
Bu dosyanın içeriğinde şifremiz bulunuyor. Bu şifre ile bir sonraki seviyeye geçebiliriz.


<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*


