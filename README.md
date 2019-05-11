# sonarQube scanner docker

A sonarQube scanner docker image.

The image is available on docker hub [pierdipi/sonar-scanner](https://hub.docker.com/r/pierdipi/sonar-scanner)

## Getting Started

These instructions will get you a copy of the project up and running on your local machine.

### Prerequisites

- [x] docker
- [x] git

### Verify prerequisites

```bash
docker --version
git --version
```

### Installing

Get the Dockerfile:

* By cloning: 
```bash 
git clone https://github.com/pierDipi/sonarqube-scanner-docker.git
```
* By adding as submodule:
```bash 
git submodule add https://github.com/pierDipi/sonarqube-scanner-docker.git
```
And then run the following commands order to build the `sonar-scanner:3.2.0`:

```bash
cd sonarqube-scanner-docker

docker build -t sonar-scanner:3.2.0 .
```

### Running the container

When you run the container the `run.sh` file sleeps 2 minutes 
in order to wait sonarQube server to be up and running.

Replace `$(pwd)/src` with your directory that you want analyze.

```bash
docker run -it --rm --name sonar-scanner -v $(pwd)/src:/sonar/app/src sonar-scanner:3.2.0
```


### Using with docker-compose

Replace `./src` to the line `- ./src:/sonar/app/src` with your directory that you want analyze.

```dockerfile
version: '3.4'
services:
  sonarqube:
    image: sonarqube:7.7-community
    ports:
      - "9000:9000"
    links:
      - sonar-scanner
  sonar-scanner:
    image: pierdipi/sonar-scanner:3.2.0
    volumes:
      - ./src:/sonar/app/src
    restart: on-failure
```


## Built With

* [Docker](https://www.docker.com/)
* [SonarQube](https://www.sonarqube.org/)
* [CentOS](https://www.centos.org/)

## Contributing

* Open issues.
* Submit PRs.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

