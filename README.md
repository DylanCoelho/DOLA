# DOLA
# 20 commands of linux
```
ifconfig
mkdir hi
ls
cd hi
pwd
nano hi.txt
touch test.txt
echo "hello" > file3.txt
cp hi.txt file6.txt
mv hi.txt file7.txt
df
du
rm file6.txt
mkdir bye
rmdir bye
man pwd
pwd --help
uname
sudo apt-get update
```
# git
```
git config --global user.name "your_username"
git config --global user.email "your_email_address@example.com"
git init

##create doc file in local drive
git add .
git status
git commit -m "comment"
git push
git remote add origin url
git push --set-upstream origin master

##change to master branch in git hub repo and check if file is added
## add a new file 
git fetch
git merge 

## make another file 
git pull
git log

##to create a new branch
git -b anybranchname
git checkout abovebranchname
git remote -v
git branch -vv
git ls -files

## to restore modified file, modify content of a file in local
git status
git restore filename
git status

git clone url
cd
```
# java jenkins
### without parameters
```
#freestyle
create java file in local
build ->ecute windows batch command
D:
cd D:\foldername
javac filename.java
java filename
```
### with parameters
```
make java file for parameters
This project is parameterized
add parameter->string parameter
string1
string2

class StringArguments
{
    public static void main(String args[])
    {
        System.out.println("My name is "+args[0]);
        System.out.println("My surname is "+args[1]);
    }
}

build -> execute windows batch command
D:
cd D:\foldername
javac filename.java
java filename %string1% %string2%
```
# batch jenkins
### for parameters code
```
#freestyle
#This project is parameterized
#add parameter->string parameterx2(str1,str2),choice(city),boolean(student)
#build -> execute windows batch command
echo "Your name is %str1%"
echo "Your Surname is %str2%"
echo "Your Favorite City is %city%"
echo "Are you a student %student%"
```
#python
```
#implecit
#build->execute python script
print("hello world")

#explicit
#create simple python file in local
#build -> execute windows batch command
D:
cd D:\foldername
python filename.py

```
# maven and ant
### maven
```
source code management: GIT
enter git link for maven(reposetory url): https://github.com/DylanCoelho/java-maven-junit-helloworld.git
goals and options: clean compile test package

output directory : C:\ProgramData\Jenkins\.jenkins\workspace\maventry\target
```
### ant
```
#freestyle
Source code management: GIT
enter git link for ant(Reposetory url): https://github.com/DylanCoelho/rps-ant.git
build: invoke ant
ant version :ant
targets: clean compile test package war
```

# pipeline with stages and parameters
```
#To create a pipeline script and build a pipeline of jobs in Jenkins
#build->howwer->proceed
#This project is parameterised(with parameters: Person, STUDENT, DIVISION, PID)
#pipeline
pipeline {
  agent any
  stages {
    stage('Form') {
      input {
        message "Please fill this form"
        parameters {
          string(name: 'PERSON', defaultValue: '', description: 'Your Name: ')
          booleanParam(name: 'STUDENT', defaultValue: true, description: 'Student')
          choice(name: 'DIVISION', choices: ['A', 'B'], description: 'Pick division')
          text(name: 'PID', defaultValue: '', description: 'Enter your PID')
        }
      }
      steps {
        echo "Hello, ${params.PERSON}"
        echo "Toggle: ${params.STUDENT}"
        echo "Choice: ${params.DIVISION}"
        echo "PID: ${params.PID}"
      }
    }
    stage('info') {
            steps {
                echo 'This was your information'
            }
        }
    stage('Bye') {
            steps {
                echo 'Bye'
            }
        }
  }
  post {
    failure {
      echo 'The build was unsuccessful, try again later.'
    }
  }
}
```
# Jenkinsfile
```
#To create a Jenkinsfile and build a pipeline of jobs in Jenkins
##pipeline
build triggers : github hook trigger for gitscm polling
pipeline: defn: pipeline script from scm
scm git
repo url: https://github.com/DylanCoelho/jenkins-pipeline-tutorial.git
script path: hello-world/Jenkinsfile
build manually once
FInally update github repo
```
#WebHooks
```
#In Jenkins, show changes in a project with the help of webhooks.Also show how builds can be scheduled with cron commands
##pipeline
build triggers : github hook trigger for gitscm polling
#jenkins-pipeline-tutorial->settings->webhook->addwebhook
#download ngrok -> cmd here
ngrok http 8080
#copy http link+: /github-webhook/ -> paste in add webhook 
#coontent type: applicaton json ->add webhook
#create file and commit in repo
#check if changes reflect in jenkins

```

#AWS
```
### Commands to run on puppet Master
sudo apt-get update
wget https://apt.puppetlabs.com/puppet-release-bionic.deb
sudo dpkg -i puppet-release-bionic.deb
sudo apt-get install puppetmaster
apt policy puppetmaster
sudo systemctl status puppet-master.service
sudo nano /etc/default/puppet-master
Add this line in the puppet master file: JAVA_ARGS="-Xms512m -Xmx512m"
sudo systemctl restart puppet-master.service
sudo ufw allow 8140/tcp
sudo nano /etc/hosts
add line here "master-ip puppet"


Run these two commands at the end(after every slave command is executed)
sudo puppet cert list
sudo puppet cert sign --all
```

```
### Commands to run on slave node/ puppet agent
sudo apt-get update
wget https://apt.puppetlabs.com/puppet-release-bionic.deb
sudo dpkg -i puppet-release-bionic.deb
sudo apt-get install puppet
sudo nano /etc/hosts
add line here "master-ip puppet"

sudo systemctl start puppet
sudo systemctl enable puppet
sudo puppet agent --test
```
# Puppet Manifest
### On Master terminal
```
sudo mkdir -p /etc/puppet/code/environments/production/manifests/
cd /etc/puppet/code/environments/production/manifests/
sudo nano site.pp
```
### Following manifests to be written in site.pp
### Manifest 1
```
file {'/tmp/hi.txt':
ensure => present,
mode =>  '0644',
content => "it works on ${ipaddress_eth0}! \n",
}
```
### Manifest 2
```
node default{
package {'nginx':
ensure => installed,
}
file {'/tmp/status.txt':
content => 'nginx installed',
mode =>  '0644',
}
}
```
### Manifest 3
```
node default {
exec { 'apt-update': 
# exec resource named 'apt-update'
command => '/usr/bin/apt-get update' 
# command this resource will run
}
# install apache2 package
package { 'apache2':
require => Exec['apt-update'], 
# require 'apt-update' before install$
ensure => installed,
}
}
```
### On slave terminal
```
After writing every manifest, sudo puppet agent --test
```

### After every manifest
##### For 1st manifest - On slave
```
cd
cd /tmp
cat hi.txt
```

##### For 2nd manifest - On browser
```
go to Slave's Ip address
nginx webpage shows
```

##### For 3rd manifest - On browser
```
go to Slave's Ip address
Apache2 webpage shows
```
