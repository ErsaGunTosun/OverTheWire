# Bandit Over The Wire **31**
### Bu Leveldeki Amacımız
> SSH ile bandit31 bağlanıp `ssh://bandit31-git@localhost/home/bandit31-git/repo` adresinde bulanan dosyaları git ile çekip mevcut şifreyi bulmak.


## Kullanacağımız Komutlar
1. `ls` : Bulunduğumuz dizindeki dosyaları listeler. Bir çok parametresi bulunuyor. Bu parametreler sayesinde dosyaları farklı şekillerde listelememizi sağlıyor. Daha fazlası için `man ls` komutunu kullanabilirsiniz.
2. `cd`: Change Directory kısaltmasıdır. Bulunduğumuz dizini değiştirmemizi sağlar. Daha fazlası için `man cd` komutunu kullanabilirsiniz.
3. `cat`: Bir dosya içeriğini ekrana yazdırır. Daha fazlası için `man cat` komutunu kullanabilirsiniz.
4. `git`: Git'in bir çok parametresi bulunuyor. Bu parametreler sayesinde farklı işlemler yapmamızı sağlıyor. Daha fazlası için `man git` komutunu kullanabilirsiniz.


## Şifre Bulma
Daha öncekiler de yaptığımız gibi  `/tmp` klasörünün altına gidip bize verilen adresten dosyaları kopyalıyoruz.

```bash
bandit31@bandit:~$ cd /tmp
bandit31@bandit:/tmp$ git clone ssh://bandit31-git@localhost:2220/home/bandit31-git/repo bandit31kolaydi

bandit31@bandit:/tmp$ cd bandit31kolaydi
bandit31@bandit:/tmp/bandit31kolaydi$ ls
README.md
```
`cat` ile `README.md` dosyasının içeriğini okuyalım.

```bash
bandit31@bandit:/tmp/bandit31kolaydi$ cat README.md
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master
```
Burada bizden `key.txt` isimli bir dosya oluturmamızı, bu dosya içine `May I come in?` yazıp `git` ile pushlamaımızı istiyor.

```bash
bandit31@bandit:/tmp/bandit31kolaydi$ echo "May I come in?" > key.txt
bandit31@bandit:/tmp/bandit31kolaydi$ git add -f key.txt
bandit31@bandit:/tmp/bandit31kolaydi$ git commit -m "key.txt added"
[master 1d9e0e5] key.txt added
 1 file changed, 1 insertion(+)
 create mode 100644 key.txt
```
```bash
bandit31@bandit:/tmp/bandit31kolaydi$ git push origin master
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 2 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 321 bytes | 321.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: ### Attempting to validate files... ####
remote:
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote:
remote: Well done! Here is the password for the next level:
remote: rmCBvG56y58BXzv98yZGdO7ATVL5dW8y
remote:
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote:
To ssh://localhost:2220/home/bandit31-git/repo
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'ssh://localhost:2220/home/bandit31-git/repo'
```
Burada bir sonraki levelin şifrenisi buluyoruz.

<hr/>

Hata ve geri dönüşler için: *[ersagun@ersaguntosun.com ](mailto:ersagun@ersaguntosun.com)*

