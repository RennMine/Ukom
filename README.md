1. Konfigurasi MikroTik
    <ol type="1">
        <li>dhcp client ether 1 (mendapatkan ip WAN)</li>
        <li>buat vlan di interface > vlan</li>  
    <dd>VLAN1 VLAN ID = 1</dd>
    <dd>VLAN10 VLAN ID = 10</dd>
    <dd>VLAN20 VLAN ID = 20</dd>
    <dd>VLAN30 VLAN ID = 30</dd>
    </ol>
2. Konfigurasi IP
    ether 2 = 192.168.88.254/24  
    vlan10 = 192.168.10.1/24  
    vlan20 = 192.168.20.1/24  
    vlan30 = 192.168.30.1/24  
    ether 3 = 192.168.40.1/24  

4. Konfigurasi DHCP Server
    vlan10  
    vlan20  
    vlan30  
    ether 3  

5. Konfigurasi Firewall
    <dd>IP > Firewall > Nat > + > General = srcnat > Action =
  	masquerade</dd>
    <dd>DNS = Allow Remote Request</dd>

6. Konfigurasi SWOS
    <ol type="1">
        <li>Buka Browswe</li> 
        <li>ketik 192.168.88.1</li>
        <li>masuk SWOS jika tidak masuk pindahkan ip ether 2 ke vlan 1</li>  
        <li>menu vlan > VLAN Mode enable port 1 - 4, Default
        VLAN ID 1,10,20,30</li>
    </ol>
      	
7. menu vlans;


 





6.	Konfigurasi Proxmox
    <ol type="1">
        <li>ketik di tab baru browser IP Proxmox</li>
        <li>ketik 192.168.10.2:8006</li>
        <li>masuk ke proxmox</li>
        <li>login.....</li>
    </ol>

8.	Konfigurasi Ubuntu Server di Proxmox
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
        
9.  Install Apache, MySql, PHP
    <ol type="1">
        <li>Masuk ke Ubuntu yang sudah dibuat</li>
        <li>klik Start lalu console</li>
   
    <dd>login : root</dd>
    <dd>password : (password yang sudah dibuat)</dd>
    </ol>
    
    # Update Sistem & Install Apache, MySqlServer, PHPMyAdmin  
      apt update  
      apt install apache2  
      apt install mysql-server  
      apt install php  
      apt install phpMyAdmin  

    # Masuk ke MySQL
      sudo mysql -u root -p  
  	
    # Buat Database
      CREATE DATABASE wordpress;  
  	
    # Buat User
      CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';  
  	
    # Berikan Hak Akses
      GRANT ALL PRIVILEGES ON wordpress.* TO 'user'@'localhost';  
    # Refresh Hak Akses
      FLUSH PRIVILEGES;
  	
    # Keluar
      exit 

    # Install & Konfigurasi WordPress  
      cd /tmp  
      wgt https://wordpress.org/latest.tar.gz  

    # Extract WP
      tar -xzvf latesttar.gz  

    # Memindahkan Folder  
      sudo mv wordpress /var/www/html/  

    # Merubah kepemilikan  
      Chown -R www-data:www-data /var/www/html/wordpress/  
   	  Chmod -R 755 /var/www/html/wordpress  

    # Masuk ke wordpress
      Masukan ip yang dibuat di proxmox 192.168.10.x/wordpress/  
      Lanjutkan installasi sampai bisa posting

9#_X$@_!0*&%~?

