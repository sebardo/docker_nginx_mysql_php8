# Setup Infrastructure

## Requirements

You'll need the following software installed on your machine:

* [Docker](https://docs.docker.com/install/)
* [Docker Compose](https://docs.docker.com/compose/install/)
* [PHP Coding Standards Fixer](http://cs.sensiolabs.org/)

## Docker

Create docker-compose environment file based on `dist.env`

```bash
cp infra/docker/local/dist.env infra/docker/local/.env
```

Change the environment variables if needed. Defaults may suit your needs.

Build the containers, if you see any problem you can provide the `no-cache` argument  (this action may take several minutes)

```bash
bin/docker build
```

In case that Firefox still doesn't recognices the certificate, it must be added by hand `https://cdn.acilia.es/rootCA.crt` in Preferences -> Privacy and Security -> [Certificates] See Certificates -> Authorities -> Import.

Start up the containers

```bash
bin/docker up
```

Add entries to your `/etc/hosts` file:

```bash
127.0.0.1 project-name.loc
```

## Database

```bash
echo "CREATE DATABASE IF NOT EXISTS project_name" | bin/docker db-load
echo "GRANT ALL ON project_name.* TO 'project_name'@'%' IDENTIFIED BY 'project_name'" | bin/docker db-load
```

To turn containers down

```bash
bin/docker down
```

---

### Development mailer service

Docker compose includes mailcatcher as the mailer service.
Access service:

```bash
http://project-name.loc:1080/
```
