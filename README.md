This fork adds a vagrant box configuration so the project can be fully configured (and isolated) with just a few commands.
- An nginx webserver will be running the project and make it accessible through the URL: http://high-quality-bundles.dev.
- A mysql database is automatically created and configured, and the `parameters.yml.dist` file was adjusted to inherit
these values making further (manual) configuration unnecessary.
- Powered by [Puphpet's](http://www.puphpet.com) configuration so additional packages and services could be installed at
will (see `puphet/config.yml`).


# Getting started

1) Clone this fork:

```sh
git clone https://github.com/cleentfaar/high-quality-bundles-project.git
```

2) Launch the box:

```sh
cd high-quality-bundles-project
vagrant up && vagrant ssh
```

3) You should now be logged into the virtual machine, sitting inside the project directory. See if everything works:
```sh
app/console
```

4) If you get the familiar list of commands, open a separate terminal window and adjust your (real) machine's hosts-file:
```
sudo echo "192.168.56.101    high-quality-bundles.dev" >> /etc/hosts
```

5) The project should now be accessible by visiting http://high-quality-bundles.dev.
   If it isn't, make sure to clear your browser cache or restart it.


## Windows users

This box configuration uses NFS synchronization by default. However, NFS is not supported on Windows machines.

So, before launching the box, open the `puphpet/config.yml` file and locate the `synced_folder` configuration (see below),
there you should change the value of `sync_type` (nfs) to `default`:
```yml
synced_folder:
  hPKsrYuSvfjo:
    owner: www-data
      # ...
      sync_type: nfs # change this to 'default'!
```


## Remaining issues

Although Puphpet promotes the use of scripts in the `startup-once` (`execute-once`, etc.) directories,
they never seemed to be executed when I tried to use them for configuring the project. If someone can get a working
set-up using scripts in these directories I'd be happy to merge it. The current workaround is adding the commands to the
`dot/.bash_aliases` file, which isn't really acceptable.
