Install vagrant-auto_network```vagrant plugin install vagrant-auto_network```Bring up Vagrant```vagrant up```Clone base repo into sites```git clone ssh://git@stash.vmlapps.com/~msmith/d8dockerbase.git Sites/dev.something.com```Edit the Provision data for your new site to give it a URL..
```vim Sites/dev.something.com/provision/codeship-services.yml```

Just change the 'dev.something.com' to whatever your site is.

Add the site to your hosts file
```10.20.1.3 dev.cpt.com```

Install a website in Sites/dev.something.com/docroot.

Note that if it's Drupal, setup the settings.php file to point to 'mysql' as the host, 'drupal' as the DB, 'root' as the username and password.

SSH into Vagrant
```vagrant ssh```

Change directory to the Sites/dev.something.com/provision directory.
```cd /opt/sites/dev.something.com/provision```

Start your server ...
```jet run app```




If you need direct access to the webserver, you can see the docker provisions running by typing ```docker ps``` inside of Vagrant's ssh. You can attach a shell process to that server by using ```docker exec -i -t <CONTAINER_ID> bash```

Drush8 is already setup in the container. XDebug is already installed and setup. Just configure your reciever to listen on port 9000.
