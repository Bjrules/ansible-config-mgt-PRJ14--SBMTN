
## Project has been renamed from *ansible-config-mgt-3* to *ansibleconfig-mgt-4*
## the complete work can be found in the branch jenkinspipeline-stages of 
## https://github.com/Bjrules/ansible-config-mgt-4.git
## and https://github.com/Bjrules/php-todo.git (main branch)


## IMPORTANT

1. Make sure you instance is either t2.medum or t3.medium
2. make sure it is phpunit6.* that you install on jenkins
3. make sure it is php7.4 you are using
4. install mysql-client on the jenkins machine
5. modify the .env.sapmle for the database details
6. install zip on the jenkins machine.
7. make sure you install java jdk 11 on jenkins
8. Dont forget to create inbound rules on the EC2 instances, Artifactory is 8082, MySQL is 3306, jenkins is 8080 and Sonarqube is 9000
9.  Install these jenkins plugins: Blue Ocean, Plot, Ansible, Artifactory, Sonar Scanner 






### Installing JAVA
====================================

sudo yum install java-11-openjdk-devel -y




### Install php
=====================================

yum module reset php -y
yum module enable php:remi-7.4 -y
yum install -y php php-common php-mbstring php-opcache php-intl php-xml php-gd php-curl php-mysqlnd php-fpm php-json
systemctl start php-fpm
systemctl enable php-fpm



### Install phpunit, phploc
=====================================

sudo dnf --enablerepo=remi install php-phpunit-phploc
wget -O phpunit https://phar.phpunit.de/phpunit-6.phar
chmod +x phpunit
sudo yum install php-xdebug



### sonar properties
=================================== 
sonar.host.url=http://3.125.17.131:9000/sonar/ 
sonar.projectKey=php-todo 
#----- Default source code encoding sonar.sourceEncoding=UTF-8 
sonar.php.exclusions=**/vendor/** 
sonar.php.coverage.reportPaths=build/logs/clover.xml 
sonar.php.tests.reportPath=build/logs/junit.xml



### open the bash profile and paste
sudo vi .bash_profile

export JAVA_HOME=$(dirname $(dirname $(readlink $(readlink $(which javac))))) 
export PATH=$PATH:$JAVA_HOME/bin 
export CLASSPATH=.:$JAVA_HOME/jre/lib:$JAVA_HOME/lib:$JAVA_HOME/lib/tools.jar

### reload the bash profile
source ~/.bash_profile