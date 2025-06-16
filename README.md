# Xiaomi AX3200 için Türkçe OpenWRT Kurulum Rehberi

Bu rehberimizde Xiaomi AX3200 cihazınıza OpenWRT yüklemeniz için izlemeniz gereken tüm adımlar yer almaktadır.    
*OpenWRT kurulumu cihazınızı garanti dışı bırakabilir, oluşabilecek tüm komplikasyonlar sizin sorumluluğunuzdadır.*  
*Konu ile ilgili hiçbir sorumluluk kabul etmiyoruz. Rehberimizi kaynak göstererek paylaşmanız önemle rica olunur.* 🙏

<p align="left">
  <a href="https://discord.gg/k6y5MBKCPW"><img src="https://img.shields.io/badge/Discord-Yardım İçin-blue?logo=discord&logoColor=white"/></a>
</p>

<details>
  <summary>📋 İçindekiler</summary>
  <ol>
    <li>
      <a href="#-başlarken">✨ Başlarken</a>
      <ul>
        <li><a href="#️-cihaz-özellikleri">⚙️ Cihaz Özellikleri</a></li>
        <li><a href="#-gereksinimler">📦 Gereksinimler</a></li>
      </ul>
    </li>
    <li>
      <a href="#-kuruluma-hazırlık">🪄 Kuruluma Hazırlık</a>
      <ul>
        <li><a href="#-unlock-script-miwifi-root-erişimi">🔓 Unlock Script (MiWiFi Root Erişimi)</a></li>
        <li><a href="#-xmir-patcher-ile-exploit-yükleme">💥 Xmir Patcher ile Exploit Yükleme</a></li>
      </ul>
    </li>
    <li>
      <a href="#-openwrt-kurulumu---i̇ndir">🚀 OpenWRT Kurulumu</a>
      <ul>
        <li><a href="#-ssh-ile-cihaza-erişim">📡 SSH ile Cihaza Erişim</a></li>
        <li><a href="#-yerel-http-sunucusu-başlatma">🖥️ Yerel HTTP Sunucusu Başlatma</a></li>
        <li><a href="#-erken-kurulum-ayarları">📇 Erken Kurulum Ayarları</a></li>
        <li><a href="#-openwrt-flashlama">🔁 OpenWRT Flashlama</a></li>
      </ul>
    </li>
    <li>
      <a href="#-kurulum-sonrası">💾 Kurulum Sonrası</a>
      <ul>
        <li><a href="#️-kalıcı-firmware-sysupgrade-yükleme">📌 Kalıcı Firmware (sysupgrade) Yükleme</a></li>
        <li><a href="#-notlar">📝 Notlar</a></li>
      </ul>
    </li>
    <li>
      <a href="#️-kaynaklar">🗃️ Kaynaklar</a>
    </li>
  </ol>
</details>


# ✨ Başlarken

### ⚙️ Cihaz Özellikleri
- CPU: 1350 Mhz MediaTek MT7622B
- RAM: 256 MB
- FLASH: 128 MB
- 2.4 GHz: MediaTek MT7622B
- 5 GHz: MediaTek MT7915E
- Ethernet: 4x1000 Mbps LAN/WAN

### 📦 Gereksinimler

- [Python (3.x)](https://www.python.org/downloads/) (`winget install Python.Python.3.13`)  
- `requests` paketi (`pip install requests`)  
- [PuTTY](https://www.putty.org/) (`winget install PuTTY.PuTTY`)  
- Xmir Patcher aracı ([Releases](https://github.com/frudotz/openwrt-xiaomi-ax3200/releases/download/OpenWRTKurulum/ax3200-mt7622b-openwrt-kurulum.zip) dosyasında)  

## 📥 Kurulum dosyalarını [indirmek için tıklayın.](https://github.com/frudotz/openwrt-xiaomi-ax3200/releases/download/OpenWRTKurulum/ax3200-mt7622b-openwrt-kurulum.zip)  

# 🪄 Kuruluma Hazırlık

> OpenWRT kurulumuna başlamadan önce MiWifi kurulumunu tamamlamanız gerekmektedir.  
> Kurulum sırasında kolay bir arayüz şifresi belirleyebilirsiniz. (Örn. 123456789)  

### 🔓 Unlock Script (MiWiFi Root Erişimi)

Python'u sisteminize indirin ve kurun: [https://www.python.org/downloads/](https://www.python.org/downloads/)  
Kurulum dosyalarını içeren `.zip` arşivini kolay erişilebilir bir dizine çıkartın.  
Bu dizin içinde bir terminal veya PowerShell penceresi açın.  
Aşağıdaki komutları çalıştırın:  

```bash
pip install requests
python unlock.py -p ARAYUZ_SIFRESI
```

<p align="left">
  <img width="auto" height="147" src="https://github.com/frudotz/openwrt-xiaomi-ax3200/blob/main/IMGs/1.png">
  <img width="auto" height="147" src="https://github.com/frudotz/openwrt-xiaomi-ax3200/blob/main/IMGs/2.png">
  <img width="auto" height="147" src="https://github.com/frudotz/openwrt-xiaomi-ax3200/blob/main/IMGs/3.png">
</p>

### 💥 Xmir Patcher ile Exploit Yükleme

Xmir Patcher’ı bir klasöre ayıklayın ve `START.bat` dosyasını çalıştırın.  
- Açılan menüden `2 - Connect to device (install exploit)` seçeneğini seçin.
- Arayüz şifresi tekrar sorulacaktır, girin.

Aşağıdaki mesajı gördüğünüzde işlem başarıyla tamamlanmıştır:  

```
SSH and Telnet services are activated!
```

<p align="left">
  <img width="auto" height="222" src="https://github.com/frudotz/openwrt-xiaomi-ax3200/blob/main/IMGs/4.png">
  <img width="auto" height="222" src="https://github.com/frudotz/openwrt-xiaomi-ax3200/blob/main/IMGs/5.png">
</p>

# 🚀 OpenWRT Kurulumu - [İndir](https://github.com/frudotz/openwrt-xiaomi-ax3200/releases/download/OpenWRTKurulum/ax3200-mt7622b-openwrt-kurulum.zip)

### 📡 SSH ile Cihaza Erişim

PuTTY veya terminal üzerinden aşağıdaki giriş bilgilerini kullanarak cihaza bağlanın:

- **Kullanıcı adı:** `root`
- **Şifre:** `root`

<p align="left">
  <img width="auto" height="350" src="https://github.com/frudotz/openwrt-xiaomi-ax3200/blob/main/IMGs/7.png">
</p>

### 🖥️ Yerel HTTP Sunucusu Başlatma

Kurulum dosyalarının bulunduğu dizinde terminal açın.
Aşağıdaki komutu çalıştırarak yerel bir HTTP sunucusu başlatın:

```bash
python -m http.server
```

<p align="left">
  <img width="auto" height="350" src="https://github.com/frudotz/openwrt-xiaomi-ax3200/blob/main/IMGs/6.png">
</p>

Yeni bir terminal açın ve aşağıdaki komutla IP adresinizi öğrenin:

```bash
ipconfig
```

> **Not:** IP adresiniz genelde `192.168.31.xxx` şeklindedir.

### 📇 Erken Kurulum Ayarları

SSH bağlantısı üzerinden aşağıdaki komutları girin:

```bash
nvram set ssh_en=1
nvram set uart_en=1
nvram set boot_wait=on
nvram set flag_boot_success=1
nvram set flag_try_sys1_failed=0
nvram set flag_try_sys2_failed=0
nvram commit
```

> Eğer OpenWRT flashlama adımından sonra cihazı yeniden başlattığınızda arayüze erişemiyorsanız  
> Kuruluma baştan başlayıp aşağıdaki kodları da ekleyerek girmeyi deneyebilirsiniz. 

```bash
nvram set flag_ota_reboot=1
nvram set "boot_fw1=run boot_rd_img;bootm"
nvram commit
```

<p align="left">
  <img width="auto" height="250" src="https://github.com/frudotz/openwrt-xiaomi-ax3200/blob/main/IMGs/8.png">
  <img width="auto" height="250" src="https://github.com/frudotz/openwrt-xiaomi-ax3200/blob/main/IMGs/9.png">
</p>

### 🔁 OpenWRT Flashlama

SSH bağlantısı üzerinden aşağıdaki komutları girin:

```bash
cd /tmp
wget http://<Bilgisayar_IP_adresi>:8000/immo.bin
mtd -r write immo.bin firmware
```

> `immo.bin` dosyası, sizin için önceden hazırlanmıştır ve kurulum arşivinin içindedir.

<p align="left">
  <img width="auto" height="250" src="https://github.com/frudotz/openwrt-xiaomi-ax3200/blob/main/IMGs/10.png">
  <img width="auto" height="250" src="https://github.com/frudotz/openwrt-xiaomi-ax3200/blob/main/IMGs/11.png">
</p>

# 💾 Kurulum Sonrası

Cihaz yeniden başladıktan sonra arayüze erişemiyorsanız,  
Kurulum işlemlerini **baştan uygulayın** ve yukarıdaki `mtd` komutlarını tekrar çalıştırın.

> Bu aşamada yüklenen sistem **factory** modundadır ve geçicidir.

### 📌 Kalıcı Firmware (Sysupgrade) Yükleme

Cihaz OpenWRT'den açıldığında öncelikle cihaza tekrar SSH ile bağlanarak aşağıdaki komutları girin:

```bash
fw_setsys telnet_en 1
fw_setsys ssh_en 1
fw_setsys uart_en 1
fw_setsys boot_wait on
fw_setenv telnet_en 1
fw_setenv ssh_en 1
fw_setenv uart_en 1
fw_setenv boot_wait on
fw_setenv bootdelay 5
fw_setenv bootmenu_delay 30
fw_setenv boot_fw1 "run boot_rd_img; bootm"
fw_setenv flag_try_sys1_failed 8
fw_setenv flag_try_sys2_failed 8
fw_setenv flag_boot_rootfs 0
fw_setenv flag_boot_success 1
fw_setenv flag_last_success 1
```

<p align="left">
  <img width="auto" height="222" src="https://github.com/frudotz/openwrt-xiaomi-ax3200/blob/main/IMGs/12.png">
  <img width="auto" height="222" src="https://github.com/frudotz/openwrt-xiaomi-ax3200/blob/main/IMGs/13.png">
</p>

Kodları girdikten sonra OpenWRT web arayüzüne girin:

- `System > Backup / Flash Firmware` menüsüne gidin.
- `immortalwrt-24.10.1-mediatek-mt7622-xiaomi_redmi-router-ax6s-squashfs-sysupgrade.itb` dosyasını yükleyin.

<p align="left">
  <img width="auto" height="147" src="https://github.com/frudotz/openwrt-xiaomi-ax3200/blob/main/IMGs/14.png">
  <img width="auto" height="147" src="https://github.com/frudotz/openwrt-xiaomi-ax3200/blob/main/IMGs/15.png">
  <img width="auto" height="147" src="https://github.com/frudotz/openwrt-xiaomi-ax3200/blob/main/IMGs/16.png">
</p>

### 📝 Notlar

- İşlem sırasında cihazı **fişten çekmeyin.**
- İşlemler arasında cihazın IP adresi değişebilir, kontrol etmeyi unutmayın.
- Tüm işlemlerden önce cihazın arayüz şifresini bildiğinizden emin olun.

Kurulum başarıyla tamamlandığında cihazınız artık ImmortalWRT ile çalışıyor olacaktır. 🎉

# 🗃️ Kaynaklar
  - [OpenWRT Wiki](https://openwrt.org/toh/xiaomi/ax3200)  
   
-----------
🎀 Rehberimizi okuduğunuz için teşekkür ederiz!  
⭐ İçeriği faydalı bulduysanız desteklemek için **Star** verebilirsiniz.  
