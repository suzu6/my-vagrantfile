Vagrant.configure("2") do |config|

    # VagrantBox
    config.vm.box = "centos/7"

    
    config.vm.network "private_network", ip: "192.168.33.10"
    config.vm.network :forwarded_port, guest: 80, host: 10080 # HTTP
    config.vm.network :forwarded_port, guest: 433, host: 10433 # HTTPS
    config.vm.network :forwarded_port, guest: 3306, host: 13306 # MySQL

    # 共有フォルダを作成
    config.vm.provision "shell", inline: <<-SHELL
      mkdir -p /srv/app
      chmod 777 /srv/app
    SHELL

    # 共有フォルダの指定[mount_options]はstorageへの読み書き権限用
    config.vm.synced_folder "Path to App directry",
                            "/srv/app",
                            :mount_options => ["dmode=777,fmode=777"]

    # [初回のみ実行]必要なパッケージのインストール等初期設定
    # config.vm.provision :shell, :path => "init/init.sh"
end
