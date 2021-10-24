# Laporan Praktikum-1

​       		Kelompok 14

Axel Gavan dan Charisma Ilham Saputra





1. step pertama yaitu, ubahlah nama ubuntu_php5.6 menjadi ubuntu_landing. (1)

```
sudo lxc-copy -R ubutnu_php5.6 name -N ubuntu_landing
```

![1](D:\Charisma\kuliah\SMT 5\SAS\laprak\1.PNG)

![2](D:\Charisma\kuliah\SMT 5\SAS\laprak\2.PNG)

2. setelah berganti menjadi ubuntu_landing,  cobalah menyalakan ubuntu_landing (1)

```
sudo lxc-attach -n ubuntu_landing
```

![3](D:\Charisma\kuliah\SMT 5\SAS\laprak\3.png)

3. setelah ubuntu_landing menyala, step selanjutnya yaitu mengganti ip di ubuntu_landing (1)

```
nano /etc/network/interfaces
```

![4](D:\Charisma\kuliah\SMT 5\SAS\laprak\4.PNG)

4. setelah mengganti ip di ubuntu_landing lakukan Reboot untuk menyalakan ulang dan terlihat ip telah berganti (1)

```
reboot
```

![5](D:\Charisma\kuliah\SMT 5\SAS\laprak\5.PNG)

5. setelah berhasil mengganti ip kita coba ping ke google.com untuk mengecek apakah ada koneksi antara komputer klien dengan komputer server yang terhubung ke sebuah jaringan (1)

```
ping google.com
```

![6](D:\Charisma\kuliah\SMT 5\SAS\laprak\6.PNG)

 

6. step selanjutnya yaitu membuat dan mengunduh debian_php5.6 (2)

```
sudo lxc-create -n debian_php5.6 -t download -- --dist debian --release stretch --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```

 ![7](D:\Charisma\kuliah\SMT 5\SAS\laprak\7.PNG)



7. setelah itu kita bisa mengecek kontainer untuk melihat apakah benar-benar berhasil mengunduh debian_php5.6 atau tidak (2)

```
Sudo lxc-ls -f
```

![8](D:\Charisma\kuliah\SMT 5\SAS\laprak\8.PNG)

8. setelah berhasil mengunduh debian_php5.6, kita coba jalankan debian_php5.6 (2)

```
Sudo lxc-attach -n debian_php5.6
```

 

9. saat sudah berjalan, kita lanjut install tools net-tools pada debian_php5.6 (3)

```
Apt install nano net-tools curl -y
```

![10](D:\Charisma\kuliah\SMT 5\SAS\laprak\10.PNG)

10. setelah berhasil terinstal, kita bisa mengatur dan mengubah ip  pada debian_php5.6 (3)

```
nano /etc/network/interfaces
```

![11](D:\Charisma\kuliah\SMT 5\SAS\laprak\11.PNG)

 

11. jika ingin mengecek apakah ip pada debian_php5.6 berhasil diganti atau tidak, bisa menggunakan ifconfig (3)

```
ifconfig
```

![12](D:\Charisma\kuliah\SMT 5\SAS\laprak\12.PNG)



12. setelah itu kita lanjut menginstall nginx pada debian_php5.6

```
apt install nginx nginx-extras -y
```

![13](D:\Charisma\kuliah\SMT 5\SAS\laprak\13.PNG)

 

13. setelah berhasil diinstal, selanjutnya kita setting nginx (3)

```
cd /etc/nginx/sites-available
touch lxc_php5.6.dev
nano lxc_php5.6.dev
```

![15](D:\Charisma\kuliah\SMT 5\SAS\laprak\15.PNG)

```
cd ../sites-enabled
ln -s /etc/nginx/sites-available/lxc_php5.6.dev .
nginx -t
nginx -s reload
```

![16](D:\Charisma\kuliah\SMT 5\SAS\laprak\16.PNG)



14. selanjutnya setting hosts (3)

```
nano /etc/hosts
```

![17](D:\Charisma\kuliah\SMT 5\SAS\laprak\17.PNG)

 

16. tidak lupa setting index.html pada debian_php5.6 (3)

```
cd /var/www/html
mkdir lxc_php5.6
cd lxc_php5.6
```

![18](D:\Charisma\kuliah\SMT 5\SAS\laprak\18.PNG)

 

17. setelah berhasil kita setting, selanjutnya kita mengisi file index.html (3)

![18](D:\Charisma\kuliah\SMT 5\SAS\laprak\19.PNG)

 

18. setelah selesai mengisi file index.html, kita bisa mengecek isinya menggunakan perintah curl -I (3)

```
curl -i http://lxc_php5.dev 
```

 ![20](D:\Charisma\kuliah\SMT 5\SAS\laprak\20.PNG)



19. step selanjutnya yaitu, masuk ubuntu_landing (4)

![21](D:\Charisma\kuliah\SMT 5\SAS\laprak\21.PNG)

 

20. setelah berhasil masuk, selanjutnya setting lxc_landing (4)

```
nano lxc_5.6.dev
```

![22](D:\Charisma\kuliah\SMT 5\SAS\laprak\22.PNG)

 

21. setelah itu kita juga setting hosts landing

```
cd ../sites-enabled
rm lxc_php5.6.dev
ln -s /etc/nginx/sites-available/lxc_php5.6.dev
nginx -t
nginx -s reload

```

![23](D:\Charisma\kuliah\SMT 5\SAS\laprak\23.PNG)

 

22. selanjutnya kita masuk index.html

```
cd /var/www/html/lxc_php5.6
```

![24](D:\Charisma\kuliah\SMT 5\SAS\laprak\24.PNG)

 

23. setelah masuk file index.html, maka selanjutnya kita setting file index landing

![25](D:\Charisma\kuliah\SMT 5\SAS\laprak\25.PNG)

 

24. untuk mengecek apakah settingan kita berhasil atau tidak, kita bisa memberi perintah Curl -i

```
curl -i http://lxc_landing.dev 
```

![26](D:\Charisma\kuliah\SMT 5\SAS\laprak\26.PNG)

 

25. lxc ubuntu_landing harus menyala otomatis ketika vm dinyalakan (5)

```
lxc-ls -f
echo “lxc.start.auto =1” >> /var/lib/lxc/ubuntu_landing/config
lxc-ls -f
```

![27](D:\Charisma\kuliah\SMT 5\SAS\laprak\27.PNG)

 

26. step selanjutnya, kita setup nginx pada vm.local untuk mengkonfigurasi proxy(6)

```
sudo nano /etc/hosts
```

 

![30](D:\Charisma\kuliah\SMT 5\SAS\laprak\30.PNG)

 

27. selanjutnya kita jalankan ubuntu_php7.4

```
sudo lxc-start -n ubuntu_php7.4
sudo lxc-start -n ubuntu_php5.6
lxc-ls -f
```

![29](D:\Charisma\kuliah\SMT 5\SAS\laprak\29.PNG)

 

28. lalu masuk ke vm.local

```
sudo nano vm.local
```

 

29. setelah masuk, kita setup vm.local

![35](D:\Charisma\kuliah\SMT 5\SAS\laprak\35.PNG)



30. setelah setup vm.local, kita cek menggunakan perintah curl -i 

```
curl -i http://vm.local
```

![31](D:\Charisma\kuliah\SMT 5\SAS\laprak\31.PNG)

 

31. begitu juga denan curl vm.local/app

```
curl -i http://vm.local/app
```

![33](D:\Charisma\kuliah\SMT 5\SAS\laprak\33.PNG)



32. tidak lupa curl vm.local/blog

```
curl -i http://vm.local/blog
```

![34](D:\Charisma\kuliah\SMT 5\SAS\laprak\34.PNG)



##### #Analisa

1. Mengapa untuk kebutuhan php5.6 tidak bisa menggunakan ubuntu 16.04, sehingga perlu diganti os ke debian 9?
2. Kenapa harus menggunakan virtualisasi LXC pada skema website yang akan didevelop?
3. Apa yang dimaksud dengan proxy server? kenapa vm.local bisa kita anggap sebagai proxy server?

##### #Jawaban

1. karena ubuntu 16.04 akan dihapus dan memasuki akhir layanan, juga tidak mampu mengikuti update-update yang akan datang.
2. karena LXC merupakan teknologi virtualisasi yang ringan dan menyediakan software gratis bagi pengguna Linux. Di LXC juga melakukan isolasi kernel yang dimana pengguna dapat menjalankan beberapa unit virtual / wadah secara bersamaan pada satu host yang sama.
3. proxy server adalah perangkat atau tools untuk penghubung juga meningkatkan proteksi keamanan perangkat pengguna ketika mengakses internet. karena vm.local dapat  melakukan hampir semua hal yang dilakukan mesin fisik  dan jika ingin menggunakan vm.local sebagai server proxy hanya perlu menemukan jaringan yang tepat dengan mesin fisik dan internet.