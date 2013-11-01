# -*- mode: ruby -*-
# vi: set ft=ruby :

#### ----------------------------------------
# CONFIGURATION
#### ----------------------------------------
LARAVEL_PROJECT = true
LARAVEL_ENV = "local"
MYSQL_PASSWORD = "root"
MYSQL_DATABASE = "vagrant"
#### ----------------------------------------

##################################################################
# DO NOT EDIT BELOW THIS LINE UNLESS YOU KNOW WHAT YOU'RE DOING
##################################################################

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "base"

    config.vm.box_url = "http://files.vagrantup.com/precise32.box"

    config.vm.network :forwarded_port, guest: 80, host: 8080

    config.vm.synced_folder "./", "/vagrant", id: "vagrant-root", :owner => "vagrant", :group => "www-data"

    if LARAVEL_PROJECT
        config.vm.synced_folder "./app/storage", "/vagrant/app/storage", id: "vagrant-storage",
            :owner => "vagrant",
            :group => "www-data",
            :mount_options => ["dmode=775","fmode=664"]

        config.vm.synced_folder "./public", "/vagrant/public", id: "vagrant-public",
            :owner => "vagrant",
            :group => "www-data",
            :mount_options => ["dmode=775","fmode=664"]
    end

    config.vm.provision :shell do |shell|
        shell.path = "vagrant/provision.sh"
        if LARAVEL_PROJECT
            shell.args = ["-l true", "-e", LARAVEL_ENV, "-p", MYSQL_PASSWORD, "-d", MYSQL_DATABASE].join(" ")
        else
            shell.args = ["-p", MYSQL_PASSWORD, "-d", MYSQL_DATABASE].join(" ")
        end
    end

end
