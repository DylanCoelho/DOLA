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
