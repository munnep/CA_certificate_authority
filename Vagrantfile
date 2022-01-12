Vagrant.configure("2") do |config|
  config.vm.box = "alvaro/bionic64"
  config.vm.hostname = "mynginx"
  config.vm.network "private_network", ip: "192.168.56.50"

  config.vm.provision "shell", path: "vagrant_scripts/install_nginx.sh"
  config.vm.provision "shell", path: "vagrant_scripts/configure_nginx.sh"
  config.vm.provision "shell", path: "vagrant_scripts/configure_ca_certificate.sh"

end