A flagship and Capstone Project so far.
**Set up a Jenkins Ansible server**
**Ensure to use jenkins t3.medium in aws because  t2.micro will become slow after installing Absible and other software on the machine**

[How to install Jenkins on Linux (ubuntu or RHEL or debian)](https://www.jenkins.io/doc/book/installing/linux/)

[Install ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-and-upgrading-ansible)

![Alt text](IMG/Screenshot_20230604_180859.png)
![Alt text](IMG/Screenshot_20230604_181016.png)

[Title](README-2.md) ![Title](IMG/Screenshot_20230604_181033.png) ![Title](IMG/Screenshot_20230604_181512.png) ![Title](IMG/Screenshot_20230604_181632.png)

**Install Blue Ocean plugins in jenkins**
*Then install tghe following Plugins in jenkins: *Plot, Ansible, Blue Ocean , SonarQube Scanner*
![Alt text](IMG/Screenshot_20230604_181745.png)

[Title](README-2.md) ![Alt text](IMG/Screenshot_20230604_183447.png) 
![Alt text](IMG/Screenshot_20230604_183511.png) 
![Alt text](IMG/Screenshot_20230604_183701.png) 
![Alt text](IMG/Screenshot_20230604_183736.png) 
![Alt text](IMG/Screenshot_20230604_184000.png) 
![Alt text](IMG/Screenshot_20230604_184804.png)
![Alt text](IMG/Screenshot_20230609_091236.png)
![Alt text](IMG/Screenshot_20230609_091338.png)
![Alt text](IMG/Screenshot_20230609_093835.png)

**Updating the jenkins file with pipeline script**
![Alt text](IMG/Screenshot_20230609_094324.png)
![Alt text](IMG/Screenshot_20230609_093905.png)
![Alt text](IMG/Screenshot_20230609_095601.png)
![Alt text](IMG/Screenshot_20230609_094339.png)
![Alt text](IMG/Screenshot_20230609_095601.png) 
![Alt text](IMG/Screenshot_20230609_095741.png)

**Install and configure Ansible Plugin in jenkins**

![Alt text](IMG/Screenshot_20230609_102245.png) 
![Alt text](IMG/Screenshot_20230609_103629.png) 
![Alt text](IMG/Screenshot_20230609_190042.png) 
![Alt text](IMG/Screenshot_20230621_121546.png) 
![Alt text](IMG/Screenshot_20230621_121900.png) 
![Alt text](IMG/Screenshot_20230621_122210.png) 
![Alt text](IMG/Screenshot_20230621_122308.png) 
![Alt text](IMG/Screenshot_20230621_122422.png)

**Using 'ansible-galaxy collection install Role-name' to install Ngnix Webserver and MySQL Database**
![Alt text](IMG/Screenshot_20230621_135539.png)
![Alt text](IMG/Screenshot_20230621_134436.png)
![Alt text](IMG/Screenshot_20230622_105006.png)
![Alt text](IMG/Screenshot_20230622_105048.png)
![Alt text](IMG/Screenshot_20230622_105128.png) 
![Alt text](IMG/Screenshot_20230622_105134.png) 

*I had to add Sonarqube role and Artifactory role to my repository at this point and configure it as well*

![Alt text](IMG/Screenshot_20230712_112345.png)
![Alt text](IMG/Screenshot_20230712_112432.png)

![Alt text](IMG/Screenshot_20230712_120635.png)

![Alt text](IMG/Screenshot_20230712_112446.png)

*after modifying jenkins file to include the ${WORKSPACE} and ${inventory} variables, I can now 'build with parameters'*
![Alt text](IMG/Screenshot_20230622_123139.png)

** cloning the github repository php-todo which was forked from Darey so as to use it in VScode
![Alt text](IMG/Screenshot_20230622_200225.png) 
![Alt text](IMG/Screenshot_20230622_204817.png)

### Installation of Plot and Artifactory plugin
![Alt text](IMG/Screenshot_20230622_205800.png) 
![Alt text](IMG/Screenshot_20230622_205618.png)

**Installing artifactory roles using 'ansible-galaxy collection install jfrog.platform' and copying it to roles directory of my ansible-config-mgt-3*
![Alt text](IMG/Screenshot_20230622_213517.png) 
![Alt text](IMG/Screenshot_20230703_215430.png) 
![Alt text](IMG/Screenshot_20230704_090713.png)
![Alt text](IMG/Screenshot_20230704_090722.png)

![Alt text](IMG/Screenshot_20230704_222322.png) 
![Alt text](IMG/Screenshot_20230704_222328.png) 
![Alt text](IMG/Screenshot_20230704_222331.png)

![Alt text](IMG/Screenshot_20230704_091339.png)
![Alt text](IMG/Screenshot_20230704_120323.png)

*login and creating repository key in artifactroy after creating an inbound TCP rule on port 8082*
![Alt text](IMG/Screenshot_20230704_120337.png) 
![Alt text](IMG/Screenshot_20230704_120750.png) 
![Alt text](IMG/Screenshot_20230704_121106.png) 
![Alt text](IMG/Screenshot_20230704_121113.png) 
![Alt text](IMG/Screenshot_20230704_121412.png)


### configure Artifactory in jenkins
![Alt text](IMG/Screenshot_20230704_123344.png) 
![Alt text](IMG/Screenshot_20230704_123456.png) 
![Alt text](IMG/Screenshot_20230704_135235.png)

*Installing MySQL database to create User and Database 'homestead' using ansible role*
![Alt text](IMG/Screenshot_20230704_205626.png) 
![Alt text](IMG/Screenshot_20230704_205633.png) 
![Alt text](IMG/Screenshot_20230704_205637.png) 
![Alt text](IMG/Screenshot_20230704_205646.png) 
![Alt text](IMG/Screenshot_20230704_205703.png) 
![Alt text](IMG/Screenshot_20230704_205716.png) 
![Alt text](IMG/Screenshot_20230704_205722.png) 
![Alt text](IMG/Screenshot_20230704_205729.png)

### at this point my jenkins initial jenkins cannot use the t2.micro free-tier so I started afresh but this time with RHEL8 t3.medium and I install php on it **Note that php 7.4 is the compatible and stable version for this project**
![Alt text](IMG/Screenshot_20230705_001037.png) *please do not install version8.* for the sake of this project*
![Alt text](IMG/Screenshot_20230705_002714.png) *installed php7.4 and composer*
*at this point I added the git cloned php-todo to my workspace and created a jenkins file in it* 
### create another pipeline job in jenkins for the php-todo application
![Alt text](IMG/Screenshot_20230705_011709.png)


 *if the 'php artisan migrate' throws an error then check the /etc/my.cnf file and set the bind address to 0.0.0.0 also check the .env.sample files(in the php-todo Directory) for sql login config settings(not forgetting to set inbound rule of port 3306 on EC2)*
![Alt text](IMG/Screenshot_20230706_115726.png)

![Alt text](IMG/Screenshot_20230706_121935.png)

### install mysql client in the jenkins server and test connection with the login particulars
![Alt text](IMG/Screenshot_20230706_121611.png)

*I had to comment the first three lines in the 'Prepare Dependencies' stage because I had performed them on my terminal*
![Alt text](IMG/Screenshot_20230712_150326.png)

### while installing phpunit, mfor the purpose of this project make sure it is phpunit version 6.* for compatibility sake , also remember that it is phpunit that installed phploc automatically (NB: phpunit is the tool used to perform unit test)
![Alt text](IMG/Screenshot_20230706_132507.png)
![Alt text](IMG/Screenshot_20230706_122302.png) 
![Alt text](IMG/Screenshot_20230706_122321.png) 
![Alt text](IMG/Screenshot_20230706_123657.png)


![Alt text](IMG/Screenshot_20230706_141037.png) 
![Alt text](IMG/Screenshot_20230707_141435.png) 
![Alt text](IMG/Screenshot_20230707_142120.png) 
![Alt text](IMG/Screenshot_20230707_142223.png) 
![Alt text](IMG/Screenshot_20230707_142251.png)

![Alt text](IMG/Screenshot_20230707_144905.png) 
![Alt text](IMG/Screenshot_20230707_145006.png) 
![Alt text](IMG/Screenshot_20230707_145031.png) 
![Alt text](IMG/Screenshot_20230707_145037.png) 
![Alt text](IMG/Screenshot_20230707_160957.png)

**Installation of Httpd, php, and Downloading and unziping Artifact from Repository 'firstkey' to TODO server*
![Alt text](IMG/Screenshot_20230707_163943.png) 
![Alt text](IMG/Screenshot_20230707_164101.png) 
![Alt text](IMG/Screenshot_20230707_170631.png) 
![Alt text](IMG/Screenshot_20230707_190341.png) 
![Alt text](IMG/Screenshot_20230707_190412.png) 
![Alt text](IMG/Screenshot_20230707_190418.png) 
![Alt text](IMG/Screenshot_20230707_190425.png)

*app deployed to Todo server successfully*
![Alt text](IMG/Screenshot_20230707_191312.png)


*spin up an EC2 use the sonarqube role in Ansible to set it up in jenkins
![Alt text](IMG/Screenshot_20230707_211317.png) 
![Alt text](IMG/Screenshot_20230707_213043.png) 
![Alt text](IMG/Screenshot_20230707_220318.png) 
![Alt text](IMG/Screenshot_20230707_221446.png) 
![Alt text](IMG/Screenshot_20230707_221618.png)

![Alt text](IMG/Screenshot_20230707_222918.png) 
![Alt text](IMG/Screenshot_20230707_223412.png) 
![Alt text](IMG/Screenshot_20230707_224240.png) 
![Alt text](IMG/Screenshot_20230710_122312.png) 
![Alt text](IMG/Screenshot_20230710_122536.png)

![Alt text](IMG/Screenshot_20230710_123010.png) 

### EXTRA INFO: this very screenshot explains how you can have different version of java(jdk) installed while you can choose any as default for your system
![Alt text](IMG/Screenshot_20230710_123049.png) 
![Alt text](IMG/Screenshot_20230710_124114.png)

###copy and paste this in the slaves 

*sudo vi ./bash_profile*

*export JAVA_HOME=$(dirname $(dirname $(readlink $(readlink $(which javac))))) 
export PATH=$PATH:$JAVA_HOME/bin 
export CLASSPATH=.:$JAVA_HOME/jre/lib:$JAVA_HOME/lib:$JAVA_HOME/lib/tools.jar*

### Reload 
*source ~/.bash_profile*

![Alt text](IMG/Screenshot_20230711_162626.png) 
![Alt text](IMG/Screenshot_20230711_163147.png) 
![Alt text](IMG/Screenshot_20230711_170940.png) 
![Alt text](IMG/Screenshot_20230711_173756.png) 
![Alt text](IMG/Screenshot_20230711_173801.png)
