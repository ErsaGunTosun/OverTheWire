# Bandit Over The Wire **16**
### Bu Leveldeki Amacımız 
> SSH Kullanarak bandit16 bağlanıp localhost(127.0.0.1) üzerinde 31000-32000 arasında çalışan portu bulmak ve bu porta bir önceki levelde olduğu gibi SSL protokölü ile iletişim kurup bir sonraki levelin şifresini elde etmek
>
> İhtiyaçımız olabilecek komutlar: `ssh`, `telnet`, `nc`, `openssl`, `s_client`,

## Kullanacağımız Komutlar
1. `openssl`: OpenSSL, açık kaynaklı bir SSL ve TLS uygulama programlama arayüzüdür. Daha fazlası için `man openssl` komutunu kullanabilirsiniz.
2. `nc`: Netcat, TCP ve UDP bağlantıları kurmak ve dinlemek için kullanılan bir ağ aracıdır. Daha fazlası için `man nc` komutunu kullanabilirsiniz.Daha fazla ayrıntı için [buraya](https://hackernoon.com/tr/nmap-ve-netcat'ta-uzmanla%C5%9Fmak-i%C3%A7in-nihai-rehber "Türkçe") bakabilirsiniz.
3. `nmap`: Nmap, ağ keşfi ve güvenlik denetimi için kullanılan bir güvenlik tarayıcısıdır. Daha fazlası için `man nmap` komutunu kullanabilirsiniz.Daha fazla ayrıntı için [buraya](https://hackernoon.com/tr/nmap-ve-netcat'ta-uzmanla%C5%9Fmak-i%C3%A7in-nihai-rehber "Türkçe") bakabilirsiniz.
4. `echo`: Echo, terminalde yazdığınız metni ekrana yazdırır. Daha fazlası için `man echo` komutunu kullanabilirsiniz.
5. `chmod`: chmod, dosya ve dizinlerin okuma, yazma ve çalıştırma izinlerini değiştirmek için kullanılır. Daha fazlası için `man chmod` komutunu kullanabilirsiniz.

## Bilinmesi Gerekenler
- Nmap Nedir?
    > Nmap, bir ağdaki ana bilgisayarları, bu ana bilgisayarlar tarafından sunulan hizmetleri, çalıştırdıkları işletim sistemlerini, kullandıkları paket filtrelerinin/güvenlik duvarlarının türünü ve düzinelerce başka özelliği keşfetmek için bize yardımcı olur.
    >[buraya](https://hackernoon.com/tr/nmap-ve-netcat'ta-uzmanla%C5%9Fmak-i%C3%A7in-nihai-rehber "Türkçe") bakabilirsiniz.
    
## Şifre Bulma
Bizden istediği ilk şey `31000` ile `32000` arasında SSL protokölü ile iletişim kurabileceğimiz portu bulmamız. Bunun için `nmap` komutunu kullanıyoruz. `nmap` kullanırken yanında `-sV` parametresini kullanırsak bize portun yanında çalışan servisin adınıda gösteriyor. `-sV` parametresi ile birlikte `-p` parametresi ile hangi portları tarayacağımızı belirtiyoruz. 
```bash
bandit16@bandit:~$ nmap -sV -p 31000-32000 localhost
Service scan Timing: About 80.00% done; ETC: 08:17 (0:00:16 remaining)
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00010s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
```

Burada `31518` ve `31790` portlarının SSL ile çalıştığını görebiliyoruz. Bu portlara `openssl` ile bağlanıp şifremizi gönderiyoruz. 
`31518` portuna bağlanıp şifremizi gönderdiğimiz zaman bir cevap alamayacağız ama `31790` portuna bağlanıp şifremizi gönderirsek bize bir `private key` geri dönderecektir.
```bash
bandit16@bandit:~$ openssl s_client -connect localhost:31790
read R BLOCK
JQttfApK4SeyHwDlI9SXGR50qclOAil1
Correct!
-----BEGIN RSA PRIVATE KEY-----
...
```
Buradaki `private key'i` `echo` ile bir dosya içine kaydedip `chmod` ile izinlerini değiştirip `ssh` ile bağlanıp bir sonraki levele geçebiliriz.
```bash
kali@kali:~$ echo "-----BEGIN RSA PRIVATE KEY-----
                        ..." > /bandit17.sshkey.private
kali@kali:~$ chmod 400 /bandit17.sshkey.private
kali@kali:~$ ssh -i /bandit17.sshkey.private bandit17@bandit.labs.overthewire.org -p 2220
bandit17@bandit:~$ cat /etc/bandit_pass/bandit17
VwOSWtCA7lRKkTfbr2IDh6awj9RNZM5e 
```

şifremiz bulduk ve bununla birlikte sonraki levele geçbiliriz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*