## spring-boot-eb-demo-app

To deploy spring boot application on [AWS-elasticbeanstalk](https://aws.amazon.com/elasticbeanstalk/) through [AWS eb cli](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3.html) follow the following steps.


## Deploy on AWS ElasticBeanstalk through EB Cli
* Install EB CLI <br/>
To install EB CLI [Here is a complete guide](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install.html)

* Clone this repository & unzip, open terminal at root directory of repository.

* Create your elastic beanstalk app 
```bash
apidemo-app $ eb init
```
at this level you need to select region, application name, platform (Choose Java as your application platform), platform version (Choose Java 8), SSH creation. 

Once this is doone you will find ```.elasticbeanstalk``` hidden directory at root level of project, open this directory there will be one yml file ```config.yml``` open this file in your fevrate editor & add following lines.

```yml
deploy:
    artifact: target/apidemo-app-0.0.1-SNAPSHOT.jar
```
complete file should look like this.
```yml
branch-defaults:
  default:
    environment: null
    group_suffix: null
deploy:
    artifact: target/apidemo-app-0.0.1-SNAPSHOT.jar
global:
  application_name: dotest
  branch: null
  default_ec2_keyname: aws-eb
  default_platform: Java 8
  default_region: us-west-2
  include_git_submodules: true
  instance_profile: null
  platform_name: null
  platform_version: null
  profile: eb-cli
  repository: null
  sc: null
  workspace_type: Application
```
* Create the resources and launch the application

```bash
apidemo-app $ eb create
```
You need to provide name of enviornment, DNS CNAME, load balancer type, Spot Fleet requests etc. 

check the application status 
```bash
apidemo-app $ eb status
```
If you are changing the code then package application with maven ``` mvn package ```and deploy it again with ``` eb deploye``` 

For android client [AndroidRestClientDemo](https://github.com/afsaredrisy/AndroidRestClientDemo)
