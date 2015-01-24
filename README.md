This fork adds a vagrant box configuration so the project can be fully configured (and isolated) with just a few commands.
- An nginx webserver will be running the project and make it accessible through the URL: http://high-quality-bundles/dev.
- A mysql database is automatically created and configured, and the `parameters.yml.dist` file was adjusted to inherit
these values making further (manual) configuration unnecessary.
- Powered by [Puphpet's](http://www.puphpet.com) configuration so additional packages and services could be installed at
will (see `puphet/config.yml`).


# Getting started

1. Create a new project:

```sh
composer create-project cleentfaar/high-quality-bundles-project
```

2. Launch the box:

```sh
cd high-quality-bundles-project
vagrant up && vagrant ssh
```

4. You should now be logged into the virtual machine, sitting inside the project directory. See if everything works:
```sh
app/console
```

5. If you get the familiar list of commands, open a separate terminal window and adjust your (real) machine's hosts-file:
```
sudo echo "192.168.56.101    high-quality-bundles.dev" >> /etc/hosts
```

6. The project should now be accessible by visiting `http://high-quality-bundles.dev`.
   If it isn't, make sure to clear your browser cache or restart it.
