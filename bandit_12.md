# Bandit Over The Wire **12**

### Bu Leveldeki Amacımız
> SSH Kullanarak bandit12 bağlanıp `Home directory` içerisinde tekrar tekar sıkıştırılmış bir dosyanın `hexdump'ı ` olan `data.txt` dosyası bulunuyor. Bu dosyayı açarak bir sonraki levelin şifresini elde etmek. 
>
>İhtiyaçımız olabilecek komutlar: `grep`, `sort`, `uniq`, `strings`, `base64`, `tr`, `tar`, `gzip`, `bzip2`, `xxd`, `mkdir`, `cp`, `mv`, `file`

## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cat` : Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
3. `cd` : Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar.  Daha fazlası için `man cd` komutunu kullanabilirsiniz.
4. `mkdir`: Make Directory'nin kısatlmasıdır. Dizin oluşturmamızı sağlar. Daha fazlası için `man mkdir` komutunu kullanabilirsiniz.
5. `cp` : Copy'nin kısaltmasıdır. Dosya veya dizinleri kopyalamamızı sağlar. Daha fazlası için `man cp` komutunu kullanabilirsiniz.
6. `mv` : Move'nin kısaltmasıdır. Dosya veya dizinleri taşımamızı sağlar. Daha fazlası için `man mv` komutunu kullanabilirsiniz.
7. `file` : Dosya türünü belirlememizi sağlar. Daha fazlası için `man file` komutunu kullanabilirsiniz.
8. `xxd` : Dosyaları hexdump formatına çevirmemizi sağlar. Daha fazlası için `man xxd` komutunu kullanabilirsiniz.
9. `tar` : Dosyaları sıkıştırmamızı sağlar. Daha fazlası için `man tar` komutunu kullanabilirsiniz.
10. `gzip` : Dosyaları sıkıştırmamızı sağlar. Daha fazlası için `man gzip` komutunu kullanabilirsiniz.
11. `bzip2` : Dosyaları sıkıştırmamızı sağlar. Daha fazlası için `man bzip2` komutunu kullanabilirsiniz.

## Bilinmesi Gerekenler
- Hexdump Nedir ?
> Bilgisayar verilerinin hexadecimal formatta bir metin olarak görüntülenmesidir. Bu, genellikle bir dosyanın veya karakter dizisinin içeriğini görmek için kullanılır. Hexdump, hata ayıklama, tersine mühendislik veya dijital adli tıp gibi çeşitli amaçlar için kullanılabilir.
- tar, gzip ve bzip2 Nedir ? Farkları nelerdir ?
> `tar`, dosyaları ve dizinleri bir arşive birleştirmek için kullanılır. Arşivlenen dosyalar ve dizinler, arşiv içinde ayrı dosyalara veya dizinlere kaydedilebilir. Tar, sıkıştırma yapmaz, sadece dosyaları ve dizinleri bir araya getirir.
>
> `gzip` ve `bzip2` ise dosyaları ve dizinleri sıkıştırmak için kullanılır. Sıkıştırma, dosyaların boyutunu küçülterek depolama alanını ve aktarım hızını artırır. `gzip` ve `bzip2`, farklı sıkıştırma algoritmaları kullanırlar. `gzip`, daha hızlı bir sıkıştırma algoritması kullanır, ancak `bzip2`, `gzip'e` göre daha iyi bir sıkıştırma oranı sağlar.
>
> Temel olarak farklarını aşağıdaki tabloda görebilirsiniz.
>
>|                         |Tar                                 |Gzip                               |Bzip2                              |
>|-------------------------|------------------------------------|-----------------------------------|-----------------------------------|
>|İşlev                    |Dosyaları ve dizinleri birleştirir  |Dosyaları ve dizinleri sıkıştırır  |Dosyaları ve dizinleri sıkıştırır  |
>|Sıkıştırma               |Yapmaz                              |Yapar                              |Yapar                              |
>|Sıkıştırma algoritması   |Yok                                 |DEFLATE                            |BZ2                                |
>|Hız                      |Orta                                |Yavaş                              |Orta                               |

## Şifre Bulma
İlk olarak `data.txt` dosyasının içeriğine bakalım.
```bash
bandit12@bandit:~$ cat data.txt
00000000: 1f8b 0808 6855 1e65 0203 6461 7461 322e  ....hU.e..data2.
00000010: 6269 6e00 013d 02c2 fd42 5a68 3931 4159  bin..=...BZh91AY
00000020: 2653 5948 1b32 0200 0019 ffff faee cff7  &SYH.2..........
00000030: f6ff e4f7 bfbc ffff bff7 ffb9 39ff 7ffb  ............9...
...
```

Burada `hexdump` verileri olduğunu görüyoruz bunları oluşturmak ve çözmek için `xxd` komutunu kullanacağız. `-r` parametresi ile `hexdump` verilerini çözeceğiz.

```bash
bandit12@bandit:~$ xxd -r data.txt
23d*58~ASZP^luYBr$FP!%s��h)[=hO(B2A)tZc:pã)AZˈ0΅AyjeϢx,(zE+"2/-e"^tj$d@dJơ'7\$m1c#>aԽEVFOCӐc@MC]Y2^h8D=~     OINDpF+|b#JvdLފW$Û͖y`\&     [@*wM0θnr��C`e$b~{`<a?e:TeT4±b)@ِx=
```

Burada komudu çalıştırdığımız zaman `hexdumplı` veriyi çözdük ama bunu sonra kullanmak için bir dosyaya kaydetmemiz lazım bunuda `>` operatörü ile yapacağız. Bu operatörün `2>` versiyonu ile hata çıktılarını başka bir dosyaya kaydetmiştik(yok etmiştik).Linux çıktı yönlendirme hakkında daha fazla bilgiye [buradan](https://www.yusufsezer.com.tr/linux-cikti-yonlendirme/ "Türkçe") ulabilirsiniz.
 
```bash
bandit12@bandit:~$ xxd -r data.txt > data2.txt
-bash: data2: Permission denied
```
Burada `data2.txt` dosyasına çözülmüş veriyi kaydetmeye çalıştık ama izinlerimiz yetersiz olduğu için hata aldık. Bu hatayı çözmek için bize en başta söylediği gibi `/tmp` klasörünün altında yapacağız.

İlk önce `/tmp` dizini'nin altında düzgün bir işlem yapabilmek için kendimize bir dizin oluşturalım. Bunun için `mkdir` komutunu kullanacağız. Daha fazlası için `man mkdir` komutunu kullanabilirsiniz.
```bash
bandit12@bandit:~$ mkdir /tmp/ersagun
```
Dosya oluştuğuna göre  `data.txt` dosyasını `/tmp/ersagun` altına kopyalalım ve `cd` komutu ile bu dizine gidelim.
```bash	
bandit12@bandit:~$ cp data.txt /tmp/ersagun
bandit12@bandit:~$ cd /tmp/ersagun
bandit12@bandit:~$ ls
data.txt

```
Şimdi `xxd` komutunu çalıştıralım ve çıktıyı `data2` dosyasına yönlendirelim.
```bash
bandit12@bandit:/tmp/ersagun$ xxd -r data.txt > data2
```
Şimdi `file` ile  `data2` dosyasının türüne bakalım.
```bash
bandit12@bandit:/tmp/ersagun$ file data2
data2: gzip compressed data, was "data2.bin", last modified: Thu Oct  5 06:19:20 2023, max compression, from Unix, original size modulo 2^32 573
```
Burada `gzip` ile sıkıştırılmış bir dosya olduğunu görüyoruz ama bu dosyanın uzantısı `.gz ` olmadığı için `gzip` ile açamıyoruz. Bunun için `mv` komutu ile dosyanın uzantısını `.gz` olarak değiştirelim.
```bash
bandit12@bandit:/tmp/ersagun$ mv data2 data2.gz
```
Şimdi `gunzip`(gzip ile sıkıştırılmış dosyaları açmak için kullanılır) komutu ile dosyayı açalım.
```bash
bandit12@bandit:/tmp/ersagun$ gunzip data2.gz
```
Tekar `file` ile dosyanın türüne bakalım.
```bash
bandit12@bandit:/tmp/ersagun$ file data2
data2: bzip2 compressed data, block size = 900k
```
Burada `bzip2` ile sıkıştırılmış bir dosya olduğunu görüyoruz. `bzip2` ile açmak için `bzip2` komutunu kullanacağız. `-d` parametresi ile dosyayı açacağız.
```bash
bandit12@bandit:/tmp/ersagun$ bzip2 -d data2 
bzip2: Can't guess original name for data2 -- using data2.out
```
Burada `bzip2` dosyanın orjinal ismini tahmin edemediğini söylüyor. Bu yüzden dosyanın ismini `data2.out` olarak değiştirdi. Şimdi `file` ile dosyanın türüne bakalım.
```bash
bandit12@bandit:/tmp/ersagun$ file data2.out
data2c.out: gzip compressed data, was "data4.bin", last modified: Thu Oct  5 06:19:20 2023, max compression, from Unix, original size modulo 2^32 20480
```
Tekrar `gzip` ile sıkıştırlımış bir dosya görüyoruz yukarıda yaptığımız işlemleri burada uygulayarak bu dosyayı da açalım ve `file` ile türüne bakalım.
```bash
bandit12@bandit:/tmp/ersagun$ mv data2.out data2.out.gz
bandit12@bandit:/tmp/ersagun$ gunzip data2.out.gz
bandit12@bandit:/tmp/ersagun$ file data2.out
data2.out: POSIX tar archive (GNU)
```
Bu seferde `tar` ile sıkıştırılmış bir dosya görüyoruz. `tar` ile açmak için `tar` komutunu kullanacağız. `-xvf` parametresi ile dosyayı açacağız.
Bu parametrenin anlamı şu şekildedir.
- `x` : Arşivden dosyaları çıkartır.
- `v` : İşlemi ayrıntılı olarak gösterir.
- `f` : Arşiv dosyasının adını belirtir.

```bash
bandit12@bandit:/tmp/ersagun$ tar -xvf data2.out
data5.bin
bandit12@bandit:/tmp/ersagun$ file data5.bin
data5.bin: POSIX tar archive (GNU)
```
Tekrar  `tar` ile şifrelenmiş bir dosya buluyoruz bunu tekrar açalım.
```bash
bandit12@bandit:/tmp/ersagun$ tar -xvf data5.bin
data6.bin
bandit12@bandit:/tmp/ersagun$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
```
Burada `bzip2` ile sıkıştırılmış bir dosya görüyoruz. `bzip2` ile açmak için `bzip2` komutunu kullanacağız. `-d` parametresi ile dosyayı açacağız.
```bash
bandit12@bandit:/tmp/ersagun$ bzip2 -d data6.bin
bzip2: "Can't guess original name for data6.bin -- using data6.bin.out"
bandit12@bandit:/tmp/ersagun$ file data6.bin.out
data6.bin.out: POSIX tar archive (GNU)
```
Burada da `tar` ile sıkıştırılmış bir dosya görüyoruz bunu da açalım.
```bash
bandit12@bandit:/tmp/ersagun$ tar -xvf data6.bin.out
data8.bin
bandit12@bandit:/tmp/ersagun$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin", last modified: Thu Oct  5 06:19:20 2023, max compression, from Unix, original size modulo 2^32 49
```
Burada yine `gzip` ile sıkıştırılmış bir dosya görüyoruz bunuda `gzip` ile açıp `file` ile türüne bakalım.
```bash
bandit12@bandit:/tmp/ersagun$ mv data8.bin data8.bin.gz
bandit12@bandit:/tmp/ersagun$ gunzip data8.bin.gz
bandit12@bandit:/tmp/ersagun$ file data8.bin
data8.bin: ASCII text
```
Burada `ASCII` text görüyoruz. Yani artık şifreye ulaştık bu dosyayı `cat` ile içeriğini okuyalım
```bash
bandit12@bandit:/tmp/ersagun$ cat data8.bin
The password is wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw
```
Sonunda şifreyi bulduk ve bir sonraki levele geçebiliriz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com](mailto:ersagun@ersaguntosun.com)*   
