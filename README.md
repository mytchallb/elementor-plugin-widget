# Dockerized WordPress for Elementor Plugin Development

Edit the installed plugin under `wordpress/wp-content/plugins/elementor-awesomesauce` to develop your own plugin.
<https://developers.elementor.com/docs/getting-started/first-addon/>
<https://www.benmarshall.me/create-an-elementor-widget/>

## Initial Setup

Clone this repository to use as your docker base for WordPress-enabled sites. Launch docker and create a network:

```
docker network create amp-wp
```

Update the environment variables inside `secret/dev.env` to suit your needs.

Start and run the containers:

```
docker-compose up -d
```

## Persisting Data

To avoid this loss of data, volumes are mounted that will persist even after the containers were removed.

```
docker-wp
|- data
|- wordpress
\-docker-compose.yml
```

## Local Access

Access the site through http://localhost/ in your browser and you should see the WordPress setup page on initial run. Proceed with the installation procedure until you have successfully logged inside the WordPress admin panel.

To access the database, use an SQL client and enter the following info:

```
Hostname: 127.0.0.1
Port: 8890
Username: root
Password: root123!
```

If you changed the default values in the `secret/dev.env` file, use those values instead.

Do not use the default SQL port (3306) - it will not work when accessing the database container. Use the assigned port in the `docker-compose.yml` file. The port number can be changed as long as you know what you are doing but for the purpose of this docker base, let's keep it as it is.

For security reasons, it is advisable to use SSH tunneling to access the database server for production use.

## Custom Directives

If your site requires specific PHP directives (e.g., increased memory size), you can manage directive overrides through the provided `custom.ini` file.

