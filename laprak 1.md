# Laporan Praktikum-1

​       		Kelompok 14

Axel Gavan dan Charisma Ilham Saputra





1. step pertama yaitu, ubahlah nama ubuntu_php5.6 menjadi ubuntu_landing. (1)

```
sudo lxc-copy -R ubutnu_php5.6 name -N ubuntu_landing
```

![1](https://user-images.githubusercontent.com/93067446/138607582-06db35a7-0f53-43a4-abcb-3e53df1c2358.PNG)

![2](https://user-images.githubusercontent.com/93067446/138607593-34a341f5-5144-4e3d-ba9e-40628d26e927.PNG)

2. setelah berganti menjadi ubuntu_landing,  cobalah menyalakan ubuntu_landing (1)

```
sudo lxc-attach -n ubuntu_landing
```

![3](https://user-images.githubusercontent.com/93067446/138607605-127abbf4-2ce2-42bc-98ca-40f6def8805b.png)

3. setelah ubuntu_landing menyala, step selanjutnya yaitu mengganti ip di ubuntu_landing (1)

```
nano /etc/network/interfaces
```

![4](https://user-images.githubusercontent.com/93067446/138607620-103e4aba-5db3-4cd5-b83f-5bc83f08edd3.PNG)

4. setelah mengganti ip di ubuntu_landing lakukan Reboot untuk menyalakan ulang dan terlihat ip telah berganti (1)

```
reboot
```

![5](https://user-images.githubusercontent.com/93067446/138607626-638c29fc-ae66-437b-8210-17184d5ac292.PNG)

5. setelah berhasil mengganti ip kita coba ping ke google.com untuk mengecek apakah ada koneksi antara komputer klien dengan komputer server yang terhubung ke sebuah jaringan (1)

```
ping google.com
```

![6](https://user-images.githubusercontent.com/93067446/138607633-41fdabb0-f702-4690-b60d-2d0b25f75d68.PNG)

 

6. step selanjutnya yaitu membuat dan mengunduh debian_php5.6 (2)

```
sudo lxc-create -n debian_php5.6 -t download -- --dist debian --release stretch --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```

![7](https://user-images.githubusercontent.com/93067446/138607645-a5f09219-3221-419b-827c-91d707c3c04a.PNG)



7. setelah itu kita bisa mengecek kontainer untuk melihat apakah benar-benar berhasil mengunduh debian_php5.6 atau tidak (2)

```
Sudo lxc-ls -f
```

![8](https://user-images.githubusercontent.com/93067446/138607651-c033471a-5bd7-4429-8511-7bdece150c6f.PNG)


8. setelah berhasil mengunduh debian_php5.6, kita coba jalankan debian_php5.6 (2)

```
Sudo lxc-attach -n debian_php5.6
```

 

9. saat sudah berjalan, kita lanjut install tools net-tools pada debian_php5.6 (3)

```
Apt install nano net-tools curl -y
```

![10](https://user-images.githubusercontent.com/93067446/138607658-806e7928-e1af-453c-a28a-3af5d42c5d45.PNG)


10. setelah berhasil terinstal, kita bisa mengatur dan mengubah ip  pada debian_php5.6 (3)

```
nano /etc/network/interfaces
```

![11](https://user-images.githubusercontent.com/93067446/138607660-98aab25c-369e-40d9-a313-56aefea32687.PNG)


 

11. jika ingin mengecek apakah ip pada debian_php5.6 berhasil diganti atau tidak, bisa menggunakan ifconfig (3)

```
ifconfig
```

![12](https://user-images.githubusercontent.com/93067446/138607670-949d0b40-e498-457c-bddb-eaa557208b10.PNG)




12. setelah itu kita lanjut menginstall nginx pada debian_php5.6

```
apt install nginx nginx-extras -y
```

![13](https://user-images.githubusercontent.com/93067446/138607679-77bd911f-a007-4b5d-adb7-8aa2c0e4b364.PNG)

 

13. setelah berhasil diinstal, selanjutnya kita setting nginx (3)

```
cd /etc/nginx/sites-available
touch lxc_php5.6.dev
nano lxc_php5.6.dev
```

![15](https://user-images.githubusercontent.com/93067446/138607684-e176a481-8286-4ab0-bad8-5c5d4d59debf.PNG)

```
cd ../sites-enabled
ln -s /etc/nginx/sites-available/lxc_php5.6.dev .
nginx -t
nginx -s reload
```

![16](https://user-images.githubusercontent.com/93067446/138607690-ae2e8166-20f2-4208-9bad-a1f99fe39b5d.PNG)



14. selanjutnya setting hosts (3)

```
nano /etc/hosts
```

![17](https://user-images.githubusercontent.com/93067446/138607694-f6bb1bbb-955a-468f-ad55-232ea5456955.PNG)

 

16. tidak lupa setting index.html pada debian_php5.6 (3)

```
cd /var/www/html
mkdir lxc_php5.6
cd lxc_php5.6
```

![18](https://user-images.githubusercontent.com/93067446/138607700-6d2fa2c3-32d5-4fa8-9bfd-367105f5c980.PNG)

 

17. setelah berhasil kita setting, selanjutnya kita mengisi file index.html (3)

![19](https://user-images.githubusercontent.com/93067446/138607708-e5258315-73c2-4d74-b81a-c8e6b6c181c7.PNG)

 

18. setelah selesai mengisi file index.html, kita bisa mengecek isinya menggunakan perintah curl -I (3)

```
curl -i http://lxc_php5.dev 
```

![20](https://user-images.githubusercontent.com/93067446/138607717-201283a7-955c-4dde-933b-e6519795bec4.PNG)




19. step selanjutnya yaitu, masuk ubuntu_landing (4)

![21](https://user-images.githubusercontent.com/93067446/138607723-f2874ed8-7308-4ff2-b453-2aea4d738f5a.PNG)


 

20. setelah berhasil masuk, selanjutnya setting lxc_landing (4)

```
nano lxc_5.6.dev
```

![22](https://user-images.githubusercontent.com/93067446/138607730-60c8be08-642f-49df-a769-bbe7e3909920.PNG)


 

21. setelah itu kita juga setting hosts landing

```
cd ../sites-enabled
rm lxc_php5.6.dev
ln -s /etc/nginx/sites-available/lxc_php5.6.dev
nginx -t
nginx -s reload

```

![23](https://user-images.githubusercontent.com/93067446/138607734-19610ec7-ccfd-4215-acbf-8fe3609e88cc.PNG)


 

22. selanjutnya kita masuk index.html

```
cd /var/www/html/lxc_php5.6
```

![24](https://user-images.githubusercontent.com/93067446/138607745-0951be78-469e-4be7-9a18-28e5ad4a7d48.PNG)


 

23. setelah masuk file index.html, maka selanjutnya kita setting file index landing

![25](https://user-images.githubusercontent.com/93067446/138607749-8b0e047b-eb13-4012-a8e6-f971b9ce4be5.PNG)

 

24. untuk mengecek apakah settingan kita berhasil atau tidak, kita bisa memberi perintah Curl -i

```
curl -i http://lxc_landing.dev 
```

![26](https://user-images.githubusercontent.com/93067446/138607756-7b0951c1-cb5b-4c5a-bf8b-d474e699c16b.PNG)


 

25. lxc ubuntu_landing harus menyala otomatis ketika vm dinyalakan (5)

```
lxc-ls -f
echo “lxc.start.auto =1” >> /var/lib/lxc/ubuntu_landing/config
lxc-ls -f
```

![27](https://user-images.githubusercontent.com/93067446/138607763-aa62e8b5-9396-459b-ac3c-c892cf124640.PNG)


 

26. step selanjutnya, kita setup nginx pada vm.local untuk mengkonfigurasi proxy(6)

```
sudo nano /etc/hosts
```

 

![30](https://user-images.githubusercontent.com/93067446/138607775-0306b659-c918-42aa-8196-b9ea44973127.PNG)


 

27. selanjutnya kita jalankan ubuntu_php7.4

```
sudo lxc-start -n ubuntu_php7.4
sudo lxc-start -n ubuntu_php5.6
lxc-ls -f
```

![29](https://user-images.githubusercontent.com/93067446/138607792-349a56da-80dd-4e9e-abbe-6a6f2ec26fb4.PNG)


 

28. lalu masuk ke vm.local

```
sudo nano vm.local
```

 

29. setelah masuk, kita setup vm.local

![35](https://user-images.githubusercontent.com/93067446/138607801-0256453a-dd9f-4927-9a5a-874a6f1bd223.PNG)




30. setelah setup vm.local, kita cek menggunakan perintah curl -i 

```
curl -i http://vm.local
```

![31](https://user-images.githubusercontent.com/93067446/138607810-123c8f19-d92c-463f-85ca-e3385b9fa4ed.PNG)


 

31. begitu juga denan curl vm.local/app

```
curl -i http://vm.local/app
```

![33](https://user-images.githubusercontent.com/93067446/138607813-f411feca-5f8a-42f0-b2db-0eb2a19a8527.PNG)




32. tidak lupa curl vm.local/blog

```
curl -i http://vm.local/blog
```

![34](https://user-images.githubusercontent.com/93067446/138607820-9a544454-b0d6-408f-9761-47bd4a34bd1e.PNG)




##### #Analisa

1. Mengapa untuk kebutuhan php5.6 tidak bisa menggunakan ubuntu 16.04, sehingga perlu diganti os ke debian 9?
2. Kenapa harus menggunakan virtualisasi LXC pada skema website yang akan didevelop?
3. Apa yang dimaksud dengan proxy server? kenapa vm.local bisa kita anggap sebagai proxy server?

##### #Jawaban

1. karena ubuntu 16.04 akan dihapus dan memasuki akhir layanan, juga tidak mampu mengikuti update-update yang akan datang.
2. karena LXC merupakan teknologi virtualisasi yang ringan dan menyediakan software gratis bagi pengguna Linux. Di LXC juga melakukan isolasi kernel yang dimana pengguna dapat menjalankan beberapa unit virtual / wadah secara bersamaan pada satu host yang sama.
3. proxy server adalah perangkat atau tools untuk penghubung juga meningkatkan proteksi keamanan perangkat pengguna ketika mengakses internet. karena vm.local dapat  melakukan hampir semua hal yang dilakukan mesin fisik  dan jika ingin menggunakan vm.local sebagai server proxy hanya perlu menemukan jaringan yang tepat dengan mesin fisik dan internet.
