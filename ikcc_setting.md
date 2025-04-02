
> vagrant 계정
```
$ sudo adduser ubuntu
Adding user `ubuntu' ...
Adding new group `ubuntu' (1001) ...
Adding new user `ubuntu' (1001) with group `ubuntu' ...
Creating home directory `/home/ubuntu' ...
Copying files from `/etc/skel' ...
New password:
Retype new password:
passwd: password updated successfully
Changing the user information for ubuntu
Enter the new value, or press ENTER for the default
Full Name []:
Room Number []:
Work Phone []:
Home Phone []:
Other []:
Is the information correct? [Y/n] y

$ sudo usermod -aG sudo ubuntu
```


> ubuntu
```
$ sudo apt update
$ cd /usr/local
$ sudo mkdir openjdk8
$ cd openjdk8
$ sudo wget https://github.com/adoptium/temurin8-binaries/releases/download/jdk8u392-b08/OpenJDK8U-jdk_x64_linux_hotspot_8u392b08.tar.gz
$ sudo tar -xvzf OpenJDK8U-jdk_x64_linux_hotspot_8u392b08.tar.gz
$ sudo mv jdk8u392-b08 jdk8
$ sudo update-alternatives --install /usr/bin/java java /usr/local/openjdk8/jdk8/bin/java 1
$ sudo update-alternatives --install /usr/bin/javac javac /usr/local/openjdk8/jdk8/bin/javac 1
$ java -version
openjdk version "1.8.0_392"
OpenJDK Runtime Environment (Temurin)(build 1.8.0_392-b08)
OpenJDK 64-Bit Server VM (Temurin)(build 25.392-b08, mixed mode)
$ sudo apt install -y maven
$ echo "export JAVA_HOME=/usr/local/openjdk8/jdk8" | sudo tee -a /etc/profile
$ echo "export PATH=\$JAVA_HOME/bin:\$PATH" | sudo tee -a /etc/profile
$ source /etc/profile
$ sudo apt install -y maven
$ mvn -v
**Apache Maven 3.6.3**
Maven home: /usr/share/maven
Java version: 1.8.0_392, vendor: Temurin, runtime: /usr/local/openjdk8/jdk8/jre
Default locale: en_US, platform encoding: UTF-8
OS name: "linux", version: "5.15.0-102-generic", arch: "amd64", family: "unix"
$ sudo apt install -y tomcat9
$ sudo vi /etc/tomcat9/web.xml
**<context-param>**
**<param-name>**spring.profiles.active**</param-name>**
**<param-value>**dev**</param-value>**
**</context-param>**
$ sudo vi /etc/tomcat9/server.xml
**<Context** docBase="/var/www/repository/images"  path="/REPOSITORY/IMAGES"  reloadable="true"**/>**
**<Context** docBase="/var/www/repository/files"  path="/REPOSITORY/FILES"  reloadable="true"**/>**
$ sudo mkdir /var/www/repository/images
$ sudo mkdir /var/www/repository/files
$ sudo systemctl restart tomcat9

$ sudo tail -f /var/log/tomcat9/catalina.out
```

