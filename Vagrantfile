Vagrant.configure("2") do |config|
    # Base Box
    config.vm.box = "ubuntu/trusty64"
    config.vm.synced_folder ".", "/var/www"
    
    config.vm.provider "virtualbox" do |v|
        v.memory = 1024 
    end 

    #Provisioning
    # First Time Provision
    config.vm.provision :shell, path: "bootstrap.sh"

    # Subsequent Provisioning
    config.vm.provision "shell", inline: "cd /var/www && python manage.py runserver --host='0.0.0.0'",
        run: "always"
    
    # Port Forwarding
    # Allows you to go to localhost:5000 to view the app
    config.vm.network :forwarded_port, guest: 5000, host: 5000
    config.vm.network :forwarded_port, guest: 8000, host: 8000
    # Allows you to connect to the DB using pgAdmin
    config.vm.network :forwarded_port, guest: 5432, host:15432
end