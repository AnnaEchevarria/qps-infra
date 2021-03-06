QPS Infrastructure
==================

QPS-Infra is a dockerized QA infrastructure solution for Test Automation. It is integrated by default with [carina-core](http://www.carina-core.io) open source solution and uses jenkins as CI Tool.

* QPS-Infra is built on top of popular docker solutions, it includes Postgres database, [Zafira Reporting Tool](http://qaprosoft.github.io/zafira), Jenkins Master/Slaves Nodes, Selenium Hub, SonarQube, Rabbitmq, etc.

* All components are deployed under NGINX WebServer which can be configured in fully secured environment

* QPS-Infra and its subcomponents all together can be used as effective Test Automation infrastructure for test automation development, execution, managing, etc.

![Alt text](./qps-infra.png?raw=true "QPS-Infra")

## Contents
* [Software prerequisites](#software-prerequisites)
* [Initial setup](#initial-setup)
* [Services start/stop/restart](#services-startstoprestart)
* [Env details](#env-details)
* [License](#license)


## Software prerequisites
* Docker requires to use user with uid=1000 and gid=1000 for simple volumes sharing etc.
  Note: to verify current user uid/gid execute
  ```
  ubuntu:~/tools/qps-infra$ id
  uid=1000(ubuntu) gid=1000(ubuntu) groups=1000(ubuntu),4(adm),20(dialout),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),102(netdev),999(docker
  ```
* Install [docker](http://www.techrepublic.com/article/how-to-install-docker-on-ubuntu-16-04/) and [docker-composer](https://docs.docker.com/compose/install/#install-compose)


## Initial setup
* Clone [qps-infra](https://github.com/qaprosoft/qps-infra). Optionally create your private repo for it to have easily migrated infrastructure
* Goto qps-infra folder and launch setup.sh script providing your hostname or ip address as argument
```
git clone https://github.com/qaprosoft/qps-infra.git
cd qps-infra
./setup.sh myhost.domain.com
```
* Optional: update default credentials if neccessary (strongly recommended for publicly available environments)
  Note: If you changed ZAFIRA_RABBITMQ_USER and ZAFIRA_RABBITMQ_PASS please update them in config/definitions.json as well
* Optional: adjust docker-compose.yml file by removing unused services. By default it contains:
  nginx, postgres, zafira/zafira-ui/zafira-batch, jenkins-master, jenkins-slave, selenium hub, sonarqube, rabbitmq, elasticsearch
* Execute ./start.sh to start all containers
* Open http://myhost.domain.com to get access to direct links to the sub-components: zafira, jenkins etc


## Services start/stop/restart
* Use ./stop.sh script to stop everything
* Opional: it is recommended to remove old containers during restart
* Use ./start.sh to start all containers
```
./stop.sh
docker-compose rm -g
./start.sh
```

## Env details
* After QPS-Infra startup the following components are available. Take a look at variables.env for default credentials:
* [Jenkins](http://demo.qaprosoft.com/jenkins)
* [Selenium Grid](http://demo.qaprosoft.com/grid/console)
* [Zafira Reporting Tool](http://demo.qaprosoft.com/zafira)
* [SonarQube](http://demo.qaprosoft.com/sonarqube)
  Note: admin/qaprosoft are hardcoded sonarqube credentials and they can be updated inside Sonar Adminisration panel

## License
Code - [Apache Software License v2.0](http://www.apache.org/licenses/LICENSE-2.0)

Documentation and Site - [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/deed.en_US)
