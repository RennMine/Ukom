**1. Konfigurasi MikroTik**
    <ol type="1">
        <li>dhcp client ether 1 (mendapatkan ip WAN)</li>
        <li>buat vlan di interface > vlan</li>
    <dd>VLAN1 VLAN ID = 1</dd>
    <dd>VLAN10 VLAN ID = 10</dd>
    <dd>VLAN20 VLAN ID = 20</dd>
    <dd>VLAN30 VLAN ID = 30</dd>
    </ol>
**2. Konfigurasi IP**  
&nbsp;&nbsp;&nbsp;&nbsp;ether 2 = 192.168.88.254/24  
&nbsp;&nbsp;&nbsp;&nbsp;vlan10 = 192.168.10.1/24  
&nbsp;&nbsp;&nbsp;&nbsp;vlan20 = 192.168.20.1/24  
&nbsp;&nbsp;&nbsp;&nbsp;vlan30 = 192.168.30.1/24  
&nbsp;&nbsp;&nbsp;&nbsp;ether 3 = 192.168.40.1/24  

**3. Konfigurasi DHCP Server**  
&nbsp;&nbsp;&nbsp;&nbsp;vlan10  
&nbsp;&nbsp;&nbsp;&nbsp;vlan20  
&nbsp;&nbsp;&nbsp;&nbsp;vlan30  
&nbsp;&nbsp;&nbsp;&nbsp;ether 3  

**4. Konfigurasi Firewall**  
&nbsp;&nbsp;&nbsp;&nbsp;IP > Firewall > Nat > + > General = srcnat > Action = masquerade  
&nbsp;&nbsp;&nbsp;&nbsp;DNS = Allow Remote Request

**5. Konfigurasi SWOS**  
    <ol type="1">
        <li>Buka Browser</li> 
        <li>ketik 192.168.88.1</li>
        <li>masuk SWOS jika tidak masuk pindahkan ip ether 2 ke vlan 1</li>
        <li>menu vlan > VLAN Mode=enable port 1 - 4, Default VLAN ID=1,10,20,30</li>
      	<li>menu vlans;</li>
    </ol>  
    
**6. Konfigurasi Proxmox**  
    <ol type="1">
        <li>ketik di tab baru browser IP Proxmox</li>
        <li>ketik 192.168.10.2:8006</li>
        <li>masuk ke proxmox</li>
        <li>login.....</li>
    </ol>

**7. Konfigurasi Ubuntu Server di Proxmox**  
    <ol type="1">
        <li>Klik menu Create CT</li>
        <li>isi host name=nama, dan password & confirm password, next</li>
        <li>Template pilih Ubuntu-22.04-standar, next</li>
        <li>Disk Size=24, next</li>
        <li>CPU biarkan 1, next</li>
        <li>Memory Size=2048, Swap= 2048, next</li>
        <li>Network isi IP 192.168.10.x/24 bebas selain 1 dan
        254, Gateway= 192.168.10.1, next</li>
        <li>DNS Server= 8.8.8.8, next</li>
        <li>Finish, Tunggu hingga Task Ok</li>
    </ol>
    
**8. Install Apache, MySql, PHP**  
    <ol type="1">
        <li>Masuk ke Ubuntu yang sudah dibuat</li>
        <li>klik Start lalu console</li>  
* Login: root
* Password: (Password yang sudah dibuat)
        </ol>
    
    ## Update Sistem & Install Apache, MySql, PHP  
      apt update  
      apt install apache2  
      apt install mysql-server  
      apt install php  
      apt install phpMyAdmin  

    ## Masuk ke MySQL  
      sudo mysql -u root -p  
  	
    ## Buat Database  
      CREATE DATABASE wordpress;  
  	
    ## Buat User  
      CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';  
  	
    ## Berikan Hak Akses  
      GRANT ALL PRIVILEGES ON wordpress.* TO 'user'@'localhost';  
    ## Refresh Hak Akses  
      FLUSH PRIVILEGES;
  	
    ## Keluar  
      exit 

    ## Install & Konfigurasi WordPress  
      cd /tmp  
      wget https://wordpress.org/latest.tar.gz  

    ## Extract WP  
      tar -xzvf latest.tar.gz  

    ## Memindahkan Folder  
      sudo mv wordpress /var/www/html/  

    ## Merubah kepemilikan  
      chown -R www-data:www-data /var/www/html/wordpress/  
   	  chmod -R 755 /var/www/html/wordpress  

    ## Masuk ke wordpress  
  &nbsp;&nbsp;&nbsp;&nbsp;Masukan ip yang dibuat di proxmox 192.168.10.x/wordpress/  
  &nbsp;&nbsp;&nbsp;&nbsp;Lanjutkan installasi sampai bisa posting

**%#&&$?&#_@?$**

