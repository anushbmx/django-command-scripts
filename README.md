# Scripts

Some bash scripts to perform useful magic.

To keep consistency and easy of maintenance of execution commands for django and other applications in a project across different environment like staging, production, CI/CD etc.

| File     |      Usecase      |
|----------|-------------------|
| prepare_environment.sh    | Environment checks and prepares log files |
| run_app_celery_beat.sh    | Celery Beat starter |
| run_app_celery_dev.sh     | Celery Beat and Celery worker only for dev environment  |
| run_app_celery_worker.sh  | Celery Worker |
| run_app_collect_static.sh | Django collect static function to transfer static files to web server or CDN |
| run_app_development.sh    | Django Development version starter |
| run_app_elastic_rebuild.sh| Elastic Search index rebuild |
| run_app_production.sh     | Django production app starter |
| wait-for-it.sh            | Check if a service on any IP:Port is returning success response. Used by micro-services to determine if dependend services are running or continue waiting |


### wait-for-it.sh

A bash script that will wait on the availability of a host and TCP port. It is useful for synchronizing the 
spin-up of interdependent services, such as linked docker containers. Since it is a pure bash script, it does not have any external dependencies.

#### Why use wait-for-it.sh

Docker Compose can control the order of service startup with the depends_on option but compose does not wait until a 
container is "ready", in other words the application is booted up.

The startup times of different service in container can take different time to boot up so, wait-for-it.sh pings the IP 
address host or container passed in Env variable `WAIT_FOR` until a success ping is received it repeatedly pings the host. 


#### Note on File Structure

It's a very common scenario to detemine which directory to place these scripts and how to execue them.

1. The scripts assume directory of django application is ```app``` and its inside directory ```app``` ( see below for file structure)
2. The scripts are executed from root directory by Docker, kubernets or any tool you use to orchestrate the project.

Project directory assumed for the project

```
.
+-- root
|	+-- django
|	|	+-- app (Django directory)
|	|	|	+-- app
|	|	|	+-- manage.py
|	|	|	+-- scripts
+-- docker-compose.yml
```

Rename the directory name and references in each of scripts files according your structure.

