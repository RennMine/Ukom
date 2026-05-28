1. Konfigurasi MikroTik
    <ol type="1">
        <li>dhcp client ether 1 (mendapatkan ip WAN)</li>
        <li>buat vlan di interface > vlan</li>  
    <dd>VLAN1 VLAN ID = 1</dd>
    <dd>VLAN10 VLAN ID = 10</dd>
    VLAN20 VLAN ID = 20  
    VLAN30 VLAN ID = 30  
    </pre>


3. Konfigurasi IP
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
    IP > Firewall > Nat > + > General = srcnat > Action =
  	masquerade
    DNS = Allow Remote Request

6. Konfigurasi SWOS
    1.	Buka Browser  
    2.	ketik 192.168.88.1  
    3.	masuk SWOS jika tidak masuk pindahkan ip ether 2 ke          vlan 1  
    4.	menu vlan > VLAN Mode enable port 1 - 4, Default
        VLAN ID 1,10,20,30
      	
5.	menu vlans;


 





6.	Konfigurasi Proxmox
    1.	ketik di tab baru browser IP Proxmox
    2.	ketik 192.168.10.2:8006
    3.	masuk ke proxmox
    4.	login.....

7.	Konfigurasi Ubuntu Server di Proxmox
    1.	Klik menu Create CT
    2.	isi host name=nama, dan password & confirm password
        next
    4.	Template pilih Ubuntu-22.04-standar next
    5.	Disk Size=24 next
    6.	CPU biarkan 1 next
    7.	Memory Size=2048, Swap= 2048 next
    8.	Network isi IP 192.168.10.x/24 bebas selain 1 dan
        254, Gateway= 192.168.10.1 next
    9.	DNS Server= 8.8.8.8 next
    10.	Finish, Tunggu hingga Task Ok
        
 8. Install Apache, MySql, PHP
    1.	Masuk ke Ubuntu yang sudah dibuat
    2.	klik Start lalu console

    login : root
    password : (password yang sudah dibuat)

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

