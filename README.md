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
