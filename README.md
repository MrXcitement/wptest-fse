# Wordpress Test of Full Site Editing
A WordPress installation used for working through the [WordPress Full Site Editor course](https://learn.wordpress.org/courses/#using-the-site-editor).

## Summary
This repository contains a docker compose v2 file that will spin up a WordPress and MariaDB server. This WordPress server will be used to work through the WordPress FSE tutorials.

## Requirements
- Docker Desktop >= v4 or Docker Engine >= v20 with the compose plugin installed

## Usage
- Clone this repository
- Create the required secrets files, edit if you wish
  ```
  cp example_secrets_db_password secrets_db_password
  cp example_secrets_db_root_password secrets_db_root_password
  ```
- From a terminal, start the WordPress server:
  ```
  docker compose up -d
  ```
- Connect to the server by browsing to: http://localhost:8080
    - Suggested Admin Account
        - username: wptest@mailinator.com
        - password: Wptest-Password1
- From a terminal, when done you can stop the WordPress server:
  ```
  docker compose down
  ```

## Notes
### Wordpress Login Credentials
I am using [mailinator.com](https://www.mailinator.com/v4/public/inboxes.jsp?to=wptest) to host *public* email accounts for this test server. **DO NOT** use this for a production site. The *test* server is not able to send emails by default, however if this ability is configured, the emails provided would allow emails to be received and viewed *by anyone* that knows the email's address. so *be careful* here.

### Docker Compose Secrets files
The `compose.yaml` file is using Docker secrets stored in plain text files to pass the database's root and WordPress passwords into the containers. These passwords are expected to be found in the files: `secrets_db_password` and `secrets_db_root_password` respectively. Any file that starts with `secrets_` is ignored by git, however there are examples for these files with default values provided. The example files have been prefixed with `example_` and can be copied to the above file names, without the `example-` prefix. If you want to use this mechanism in production, you should use stronger passwords than provided here and review how these secrets files are used, including the CI/CD recommendations that the Docker project provides.

### Docker Volume storage
The data files for the database and WordPress service are stored in separate docker volumes: `wptest-fse_db_data` and `wptest-fse_wp_data`. They will be created the first time you bring up the services. If you wish to start over from a fresh system, you can delete them. There is no built in mechanism to backup the data in these volumes, however there are many articles that explain how to mount these volumes from other containers and backup/restore the data.

## References
- [WordPress Full Site Editor course](https://learn.wordpress.org/courses/#using-the-site-editor)
- [How to Quickly Deploy WordPress as a Docker Container](https://www.howtogeek.com/devops/how-to-quickly-deploy-wordpress-as-a-docker-container/)
- [How to Secure Sensitive Data With Docker Compose Secrets](https://www.howtogeek.com/devops/how-to-secure-sensitive-data-with-docker-compose-secrets/)
- [Docker Compose overview](https://docs.docker.com/compose/)
- [Docker Volumes](https://docs.docker.com/storage/volumes/)
- [Wordpress Images](https://hub.docker.com/_/wordpress)
- [MariaDB Images](https://hub.docker.com/_/mariadb)
