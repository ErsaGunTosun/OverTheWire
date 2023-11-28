# Bandit Over The Wire **13**

### Bu Leveldeki Amacımız 
> SSH Kullanarak bandit13 bağlanıp `Home directory` içindeki `sshkey.private` dosyasını kullanarak bir sonraki levele bağlanmak ve oradaki `/etc/bandit_pass/bandit14` ile şifreyi bulmak ve bir sonraki levele geçmek
>
>İhtiyaçımız olabilecek komutlar: `ssh`, `telnet`, `nc`, `openssl`, `s_client`,

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd` : Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar.  Daha fazlası için `man cd` komutunu kullanabilirsiniz.
4. `ssh`: bandit-1 bahsettiğimiz ssh bağlantısını kurmamızı sağlayan komuttur. Daha fazlası için `man ssh` komutunu kullanabilirsiniz.

## Bilinmesi Gerekenler
- Private Key nedir ?
    > Yalnızca ilgili kullanıcı veya kuruluş tarafından bilinen gizli bir anahtardır. Bu anahtar, şifrelenmiş mesajları çözmek ve dijital imzalar oluşturmak için kullanılır.

- Public Key nedir ? 
    >Herkese açık bir anahtardır ve herkes tarafından kullanılabilir. Bu anahtar, şifreli mesajları şifrelemek ve dijital imzaları doğrulamak için kullanılır.

Private ve Public key, birbirine karşılıklı olarak bağlıdır. Private key kullanılarak şifrelenen bir mesaj, yalnızca ilgili public key kullanılarak çözülebilir. Bu, şifreleme şifre çözme işlemlerinin güvenli bir şekilde gerçekleştirilmesini sağlar.
Daha fazla ayrıntı için aşağıdaki linklere bakabilirsiniz.

1. [Asimetrik Şifreleme ](https://www.webopedia.com/definitions/asymmetric-encryption/ "İngilizce")
2. [Private Key ve Public Key Nedir ?](https://medium.com/@tobb_blockchain_kulubu/blockblog-private-key-ve-public-key-nedir-17faaed4aed4#:~:text=Public%20Key%2C%20dijital%20imza%20olu%C5%9Fturulmas%C4%B1,taraf%C4%B1ndan%20bilinen%20bir%20gizli%20anahtard%C4%B1r. "Türkçe")
3. [SSH Anahatarları](https://www.sectigo.com/resource-library/what-is-an-ssh-key#:~:text=An%20SSH%20key%20relies%20upon,be%20encrypted%20and%20stored%20safely. "İngilizce")


## Şifre Bulma
İlk başta bize verilen `sshkey.private` dosyasının içeriğine bakalım.

```bash
bandit13@bandit:~$ cat sshkey.private
-----BEGIN RSA PRIVATE KEY-----
...
```
Burada bir private key görüyoruz. Bu key'i kullanarak bir sonraki levele bağlanacağız. Bunun için `ssh` komutunu kullanacağız. `ssh` komutu ile bağlanırken `-i` parametresi ile private key'i belirtmemiz gerekiyor.

```bash
ssh bandit14@bandit.labs.overthewire.org -p 2220 -i sshkey.private
```
Bu şekilde bağlantıyı kurduktan bundan sonra `cat` komutu ile `/etc/bandit_pass/bandit14` dosyasının içeriğine bakarak şifreyi bulabiliriz.

```bash
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq  
```
Bu şekilde şifreyi bulmuş olduk. Şimdi bu şifre ile bir sonraki levele geçebiliriz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*