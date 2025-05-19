Vagrant.configure("2") do |config|
  # Общие настройки
  config.vm.box = "debian/bullseye64"  # Используем официальный образ Debian Bullseye

  # Первая VM
  config.vm.define "vm1" do |vm1|
    vm1.vm.hostname = "vm1"
    vm1.vm.network "private_network", ip: "192.168.56.101"
    vm1.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end

    # Скрипт для автоматической настройки
    vm1.vm.provision "shell", inline: <<-SHELL
      # Обновляем систему и устанавливаем нужные пакеты
      sudo apt-get update
      sudo apt-get install -y wget rsync

      # Скачиваем файл из веб-источника
      wget -O /home/vagrant/file_from_web.txt http://example.com/file.txt

      # Создаем папку для обмена файлами
      mkdir -p /home/vagrant/shared

      # Настраиваем SSH ключи для rsync (опционально)
      # Можно использовать passwordless SSH или rsync по SSH
    SHELL
  end

  # Вторая VM
  config.vm.define "vm2" do |vm2|
    vm2.vm.hostname = "vm2"
    vm2.vm.network "private_network", ip: "192.168.56.102"
    vm2.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end

    # Скрипт для автоматической настройки
    vm2.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y wget rsync

      # Создаем папку для обмена файлами
      mkdir -p /home/vagrant/shared

      # Можно настроить SSH ключи или использовать пароль для rsync по SSH (здесь предполагается, что SSH настроен)
    SHELL
  end

  # Общий скрипт для настройки rsync между машинами (после запуска обеих)
  config.vm.provision "shell", run: "always", inline: <<-SHELL
    echo "Настройка обмена файлами через rsync"

    # На первой машине (vm1) запустите команду:
    if hostnamectl | grep -q 'vm1'; then
      echo "Настраиваем rsync сервер на vm1"
      
      # Запускаем rsync daemon или используем ssh для синхронизации
      
      # Для простоты используем синхронизацию по ssh:
      
      # На второй машине (vm2) выполните:
      
      echo "Чтобы синхронизировать папки, выполните на vm2:"
      echo "rsync -avz /home/vagrant/shared/ vagrant@192.168.56.101:/home/vagrant/shared/"
      
    fi
  SHELL

end