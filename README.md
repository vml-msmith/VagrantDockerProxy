Install vagrant-auto_network
```vagrant plugin install vagrant-auto_network```Bring up Vagrant```vagrant up```SSH into Vagrant
```vagrant ssh```Note the IP address of your Vagrant box. It'll be eth0.
Add the site to your local hosts file
```10.20.1.3 dev.d8.com```

Change directory to dev.d8.com
```cd /opt/sites/dev.d8.com```

Start your server:
```docker-compose up devd8```




If you need direct access to the webserver, you can see the docker provisions running by typing ```docker ps``` inside of Vagrant's ssh. You can attach a shell process to that server by using ```docker exec -i -t <CONTAINER_PID> bash```

Drush8, composer and NPM are already installed in the new container.
