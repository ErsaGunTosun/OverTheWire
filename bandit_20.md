# Bandit Over The Wire **20**

### Bu Leveldeki Amacımız

> SSH kullanarak bandit20 bağlanıp `Home Directory` atlında bulunan `suconnect` dosyasını ile bir port üzerinde locahost bağlanma ve `netcat` ile o portu dinleyip mevcut şifremizi gönderek bir sonraki level için şifreyi bulmak.
>
> İhtiyaçımız olabilecek komutlar: `ssh`, `telnet`, `nc`, `openssl`, `s_client`,

## Kullanacağımız Komutlar

1. `ls`: 1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat`: Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd`: Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar. Daha fazlası için `man cd` komutunu kullanabilirsiniz.
4. `nc`: Netcat'in kısaltmasıdır. Bir çok parametresi bulunuyor. Bu parametreler sayesinde farklı işlemler yapmamızı sağlıyor. Daha fazlası için `man nc` komutunu kullanabilirsiniz.

## Şifre Bulma

Burada öncekiler gibi tek bir shell kullanmayacağız. Birinci Shell üzerinde `netcat` ile belirtiğimiz portu dinleme işleme yapacağız. İkinci Shell üzerinde ise `suconnect` ile port üzerine bağlanacağız.

İlk başta `netcat` ile dinleme işlemi yapalım. Burada `-l` parametresi ile dinleme işlemini başlattık. `-v` parametresi ile de verbose modda çalıştırdık. Bu sayede bağlantı geldiğinde bize bilgi verecek. `-p` parametresi ile de dinlemek istediğimiz portu belirttik.

```bash
bandit20@bandit:~$ nc -lv -p 31548
Listening on 0.0.0.0 31548
```

Dinleme işlemine başladık şimdi başta bir terminal üzerinden tekrar SSH ile bandit20'ye bağlanıp `suconnect` dosyasını çalıştıralım ve dinlediğimiz parametreyi girelim.

```bash
bandit20@bandit:~$ ./suconnect 31548
```

Bunu yaptıktan sorna ilk terminalde `Connection received on localhost 48766` mesajını görmüş olacaksınız.Bu mesaj ardından mevcut şifremizi girersek bir sonraki levelin şifresini bize döndürmüş olacak.

İlk Terminal

```bash
bandit20@bandit:~$ nc -lvp 31548                                                              Listening on 0.0.0.0 31548                                                                    Connection received on localhost 48766                                                        VxCazJaVykI6W36BkBU0mJTCM8rR95XT                                          NvEJF7oVjkddltPSrdKEFOllh9V1IBcq
```

İkinci Terminal
```bash
bandit20@bandit:~$ ./suconnect 31548
Read: VxCazJaVykI6W36BkBU0mJTCM8rR95XT
Password matches, sending next password
```

İlk terminalde aldığımız şifre ile bir sonraki levele geçebiliriz.


<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*
