# API-RouterOS-dan-Hotspot-untuk-absensi-v1.1

Gateway Absensi adalah aplikasi yang bertujuan untuk merekap data kehadiran absensi mahasiswa/i. rekap data ini dibuat dengan menggunakan data dari Mikrotik Router OS melalui layanan API, dan di kombinasikan dengan hotspot authentication sebagai data kehadiran mahasiswa/i. Tujuan dari dibuatnya aplikasi ini adalah untuk studi kasus karya ilmiah oleh mahasiswa STIKOM Poltek Cirebon T/A 2020 dibuat menggunakan library Pear2 dan bahasa pemrograman PHP serta framework Bootstrap.


# Petunjuk Penggunaan
1. Konfigurasi Perangkat Mikrotik dari Internet Gateway s/d Hotspot <br/>
requiretment : <br/>
dns name : absensi.gate <br/>
ip hotspot : 10.1.1.1 <br/>
html-directory : hotspot scan <br/>
2. Copy script authentikasi ke terminal router mikrotik : <br/>
/system script add name=authentikasi source={:local mac $"mac-address"; /ip hotspot user set mac-address=$mac [find where name=$user];
:local comment [ /ip hotspot user get [/ip hotspot user find where name="$user"] comment];
:local server [ /ip hotspot user get [/ip hotspot user find where name="$user"] server];
:local profile [ /ip hotspot user get [/ip hotspot user find where name="$user"] profile];
:local ruang [ /ip hotspot get [/ip hotspot find where name=$server] profile];
:local date [/system clock get date ];:local time [/system clock get time ];[/system script add name="$date-|-$time-|-$server-|-$profile-|-$user-|-$comment-|-$ruang" owner="$user" source="$date | $time" comment="Absensi Gateway"];
:for j from=1 to=4 step=1 do={
   :for i from=2000 to=50 step=-400 do={
     :beep frequency=$i length=11ms;
     :delay 11ms;
   }
   :for i from=800 to=2000 step=400 do={
     :beep frequency=$i length=11ms;
     :delay 11ms;
   }
 };}
2. login ke aplikasi menggunakan ip, username dan password router mikrotik
3. tambah ruangan
4. tambah mata kuliah
5. tambah kelas
6. tambah mahasiswa
7. login hotspot jika berhasil database report akan dibuat

# Program ini masih dalam tahap pengembangan
tested rb951ui 2hnd routeros v.42.10
terima kasih atas kontribusinya


 
