# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    # /*=====================================
    # =            FREE VERSION!            =
    # =====================================*/
    # This is the free (still awesome) version of Scotch Box.
    # Please go Pro to support the project and get more features.
    # Check out https://box.scotch.io to learn more. Thanks

    config.vm.box = "scotch/box"
    config.vm.network "private_network", ip: "192.168.33.10"
    config.vm.hostname = "phpmyadmintest.vagrant"
    #config.vm.synced_folder ".", "/var/www", :mount_options => ["dmode=777", "fmode=666"]

    # Optional NFS. Make sure to remove other synced_folder line too
    config.vm.synced_folder ".", "/var/www", :nfs => { :mount_options => ["dmode=777","fmode=666"] }

    config.vm.provision "shell", inline: <<-SHELL	
		phpmyadmin="/etc/phpmyadmin"
		if [ -d "$phpmyadmin" ]
		then
			echo "PHPMyAdmin already installed."
		else
			echo "Installing PHPMyAdmin..."
			sudo debconf-set-selections <<< "phpmyadmin phpmyadmin/dbconfig-install boolean true"
			sudo debconf-set-selections <<< "phpmyadmin phpmyadmin/app-password-confirm password root"
			sudo debconf-set-selections <<< "phpmyadmin phpmyadmin/mysql/admin-pass password root"
			sudo debconf-set-selections <<< "phpmyadmin phpmyadmin/mysql/app-pass password root"
			sudo debconf-set-selections <<< "phpmyadmin phpmyadmin/reconfigure-webserver multiselect apache2"
			sudo apt-get -y update
			sudo apt-get -y install phpmyadmin
		fi
		
		echo 'Provisioning complete.'
		
    SHELL

end
