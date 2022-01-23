# DevOps Prerequisites in Linux System

DevOps Prerequisites learn forest

<br>

### Notes

Cool stuff to learn: Linux, Docker, Kubernetes, AWS! 
All lecture slides from KodeKloud's Mumshad with freeCodeCamp. See reference below.

<br>

### <span id="top">Content</span>

[[Setup]](#setup)   
[[Basics]](#basics)   
[[Commands]](#command)s  
[[Pakcage Managers]](#package)  
[[Services]](#services)  
[[VirtualBox]](#virtualbox)  
[[Networking]](#networking)  

  - Switching
  - Routing and Gateway

[[DNS]](#DNS)  
[[Applications]](#Applications)  
[[]](#)  
[[]](#)  
[[]](#)  
[[References]](#ref)   


<br>

### <span id='setup'>Setup</span>

[[☝️top]](#top)

<br>

## <span id="basics">Basics</span>

[[☝️top]](#top)

Things covered:

- Vinux CLI
- VI Editor
- [Package Management](#package)  
- Service Management

CentOS is a free Red hat-developed community version of Linux. 

<br>


## <span id="commands">Commands</span>

[[☝️top]](#top)

### Basic operations

- `echo $SHELL`: check your shell version.
  - `/bin/bash`
- `echo`: print to screen
- `command 1; command 2; command 3; ...`: multiple commands

- `ls`
- `cd`
- `pwd`
- `mkdir`
  - `mkdir -p /tmp/asia/india/bangalore`
- `rm -r`
- `cp -r file_1 /new_path/file_1`: copy file

<br>

### Files

- `touch new_file.txt`: creates a new file (no content)
- `cat > new_file.txt`: concatenates content to file
- `cat new file.txt`: view content of file
  
      input
      ctrl + D

- `cp new_file.txt ./new_path/new_file.txt`: copy
- `mv old_path /new_path`: move file to a different location.

<br>

### User accounts

- `whoami`: Check the current account name
- `id`
- `su user_name`: switch user
- `ssh user_name@xxx.xxx.xx.xx`: switch user and system.

- `ls /root`
  - `ls: cannot open directory '/root': Permission denied`

<br>

### Download files

- `curl https://url -O`: the Capital `-O` at the end saves the url content to a file in the current location.
- `wget https://url -O file.txt`

<br>

### Check OS versionls 

- `ls /etc/*release*`: check your OS version.

      `/etc/lsb-release  /etc/os-release`

- `cat /etc/*release*`: check more detail

      DISTRIB_ID=Ubuntu
      DISTRIB_RELEASE=20.04
      DISTRIB_CODENAME=focal
      DISTRIB_DESCRIPTION="Ubuntu 20.04.3 LTS"
      NAME="Ubuntu"
      VERSION="20.04.3 LTS (Focal Fossa)"
      ID=ubuntu
      ID_LIKE=debian
      PRETTY_NAME="Ubuntu 20.04.3 LTS"
      VERSION_ID="20.04"

<br>

## <span id="package">Package Managers</span>

[[☝️top]](#top)

### RPM (Red Hat Package Manager)

- `rpm -i telnet.rpm`: install package
- `rpm -e telnet.rpm`: uninstall package
- `rpm -q telnet.rpm`: query package

<br>

- `rpm -q openssh-server python3 ansible telnet`: (-q = query)
- `sudo rpm -i /opt/ftp-0.17-67.el7.x86_64.rpm`
- `sudo rpm -e /opt/ftp-0.17-67.el7.x86_64`

### YUM

a high-level package manager that uses RPM underneath.

The Yellowdog Updater, Modified is a free and open-source command-line package-management utility for computers running the Linux operating system using the RPM Package Manager. 

- `yum repolist`
- `ls /etc/yum.repos.d`
- `cat /etc/yum.repos.d/CentOS-Base.repo`

- `yum list ansible`
- `yum remove ansible`
- `yum --showduplicates list ansible`
- `yum instal ansible-2.4.2.0`

<br>

- `sudo yum install ansible`

      Installed:
        ansible.noarch 0:2.9.25-1.el7                                                                                    

      Dependency Installed:
        PyYAML.x86_64 0:3.10-11.el7                               libyaml.x86_64 0:0.1.4-11.el7_0                       
        make.x86_64 1:3.82-24.el7                                 openssl.x86_64 1:1.0.2k-24.el7_9                      
        python-babel.noarch 0:0.9.6-8.el7                         python-cffi.x86_64 0:1.6.0-5.el7                      
        python-enum34.noarch 0:1.0.4-1.el7                        python-idna.noarch 0:2.4-1.el7                        
        python-jinja2.noarch 0:2.7.2-4.el7                        python-markupsafe.x86_64 0:0.11-10.el7                
        python-paramiko.noarch 0:2.1.1-9.el7                      python-ply.noarch 0:3.4-11.el7                        
        python-pycparser.noarch 0:2.14-1.el7                      python-six.noarch 0:1.9.0-2.el7                       
        python2-cryptography.x86_64 0:1.7.2-2.el7                 python2-httplib2.noarch 0:0.18.1-3.el7                
        python2-jmespath.noarch 0:0.9.4-2.el7                     python2-pyasn1.noarch 0:0.1.9-7.el7                   

      Dependency Updated:
        openssl-libs.x86_64 1:1.0.2k-24.el7_9                                                                            

      Complete!

<br>

### Questions

Q. Which version of ansible is installed with yum _**on host01 server**_ in previous step?

`2.9.25`

<br>

Q. Remove `ansible` with yum.

      sudo yum remove -y ansible

Q. Install `ansible` version 2.8.11.

      sudo yum install -y ansible-2.8.11

<br>

## <span id="services">Services</span>

[[☝️top]](#top)


### `Httpd`

HTTPd is a software program that usually runs in the background, as a process, and plays the role of a server in a client-server model using the HTTP and/or HTTPS network protocol(s).

The process waits for the incoming client requests and for each request it answers by replying with requested information, including the sending of the requested web resource, or with an HTTP error message.

HTTPd stands for Hypertext Transfer Protocol daemon.

It usually is the main software part of an HTTP server better known as a web server.

<br>

### Daemon 

In multitasking computer operating systems, a daemon is a computer program that runs as a background process, rather than being under the direct control of an interactive user. 

<br>

### Service Commands

`systemctl` command is the key management tool for init system control.

- `service httpd start`: start HTTPD service
- `systemctl start httpd`: start HTTPD service
- `systemctl stop httpd`: stop HTTPD service
- `systemctl status httpd`: check HTTPD service status

      ● httpd.service - The Apache HTTP Server
        Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
        Active: inactive (dead)
          Docs: man:httpd(8)
                man:apachectl(8)

- `systemctl enable httpd`: configure HTTPD to start on reboot

      Created symlink from /etc/systemd/system/multi-user.target.wants/httpd.service to /usr/lib/systemd/system/httpd.service.

- `systemctl disable httpd`: configure HTTPD to not start on reboot

- `systemctl start my_app`
- `systemctl stop my_app`

      my_app.service

      Unit configuration file:
      
      [Service]
      ExecStart=/usr/bin/pytohn3 /opt/code/my_app.py

- `systemctl deamon-reload`: let the system D know there is a new service configured.
- `systemctl start my_app`
- `systemctl status app_name`

      ● app.service - My python web application
      Loaded: loaded (/usr/lib/systemd/system/app.service; disabled; vendor preset: disabled)
      Active: inactive (dead)

<br>

      systemctl status app.service

      ● app.service - My python web application
      Loaded: loaded (/usr/lib/systemd/system/app.service; disabled; vendor preset: disabled)
      Active: inactive (dead)


### Questions

Q. You decide to use dedicated python flask app instead of apache and want to stop the `httpd` service. What do you do?

- The Apache HTTP Server ("httpd") was launched in 1995 and it has been the most popular web server on the Internet since April 1996.


      sudo systemctl stop httpd


Q. Enable/disable `httpd` service so it does/doesn't auto-start on boot. 

      sudo systemctl enable httpd

      Created symlink from /etc/systemd/system/multi-user.target.wants/httpd.service to /usr/lib/systemd/system/httpd.service.

<br>

      sudo systemctl disable httpd
      
      Removed symlink /etc/systemd/system/multi-user.target.wants/httpd.service.

Q. Is the service running? 

`/usr/lib/systemd/system/app.service`

      systemctl status app

      ● app.service - My python web application
      Loaded: loaded (/usr/lib/systemd/system/app.service; disabled; vendor preset: disabled)
      Active: inactive (dead)


Q. Look at the service configuration (in `systemd` unit file). Figure out the order of service execution. 

You want to check the `app.service` file. 

- `cat [FULL_PATH]`
- `systemctl cat [FILE_NAME]`

And look for: `ExecStart`, `ExecStartPre`, `ExecStartPost`

      cat /usr/lib/systemd/system/app.service
      systemctl cat /usr/lib/systemd/system/app.service

<br>

      app.service

      [Unit]
      Description=My python web application

      [Service]
      ExecStart=/usr/bin/python3 /opt/code/my_app.py
      ExecStartPre=/bin/bash /opt/code/configure_db.sh
      ExecStartPost=/bin/bash /opt/code/email_status.sh
      Restart=always

      [Install]
      WantedBy=multi-user.target



Q. Once everything is configured, set the app to auto-start on reboot. 

      sudo systmctl enable app

      Created symlink from /etc/systemd/system/multi-user.target.wants/app.service to /usr/lib/systemd/system/app.service.


<br>

## <span id="virtualbox">VirtualBox</span>

[[☝️top]](#top)

- Deploying VMs
- Multiple VMs
- Networking and troubleshooting network
- Snapshots and restore VMs

<br>

### Virtualisation S/W

Type 1: VMware, Microsoft Hyper-v
Type 2: Oracle VirtualBox, VMWare Workstation
  - Host is the operating system. 

<br>

### Setup

1. Install `VirtualBox` at https://www.virtualbox.org/wiki/Downloads.

- The VM itself and its disks are installed on the host OS.
- Creating a virtual machine is like buying a new computer wihtout an OS installed in it. 

<br>

## <span id="networking">Networking</span>
<br> 

**Jump Host**

A jump server, jump host or jump box is a system on a network used to access and manage devices in a separate security zone. A jump server is a hardened and monitored device that spans two dissimilar security zones and provides a controlled means of access between them. The most common example is managing a host in a DMZ from trusted networks or computers.


### `Switching`: Inter-system networking setup

<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%2001.png" width=1000 />
<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%2009.png" width=1000 />


| system 1   |  system 2  |
| -- | -- |
| `ip link`   | `ip link`   |
| `ip addr add 192.168.1.10/24 dev eth0`   |  `ip addr add 192.168.1.11/24 dev eth0`  |
| `ping 192.168.1.11`   |    |

<br>

### `Routing` and `Gateway`: Inter-network networking setup

<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%2002.png" width=1000 />
<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%2003.png" width=1000 />
<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%2004.png" width=1000 />
<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%2005.png" width=1000 />

- Each network gets assigned an IP. 
- How does the system 1 know where the router is to send the packets through to communicate with the system 3?
- The router is just another device in the network. 
- And we **configure** the system's `gateway` or `route`.
- If a network is a room, a gateway is a door to the outside world (internet). 
  - The systems need to know where they need to go to go through it. 

| system 1 in network A  |  system 3 in network B |
| -- | -- |
| `ip link`   | `ip link`   |
| `ip addr add 192.168.1.10/24 dev eth0`   |  `ip addr add 192.168.1.11/24 dev eth0`  |
| `ping 192.168.1.11`   |    |

- A gateway can connect a system to the internet.

<br>

### Commands

      ip route add 192.168.2.0/24 via 192.168.1.1
      
      route
      Destination       Gateway           Genmask           Iface
      192.168.2.0       192.168.1.1       255.255.255.0     eth0

If you want to assign an IP address to a system, a system must have a physical or virtual network interface attached to it. There are other interfaces such as `eth`, `veth`, and `lo`.

      ip link 

      1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
         link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
      19: eth0@if20: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP mode DEFAULT group default 
         link/ether 02:42:ac:10:ee:0a brd ff:ff:ff:ff:ff:ff link-netnsid 0
      23: eth1@if24: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP mode DEFAULT group default 
         link/ether 02:42:ac:11:00:05 brd ff:ff:ff:ff:ff:ff link-netnsid 0

<br>

- `ip route`

      default via 172.16.238.1 dev eth0 
      172.16.238.0/24 dev eth0 proto kernel scope link src 172.16.238.10 
      172.17.0.0/16 dev eth1 proto kernel scope link src 172.17.0.5 

- `route`: displays IP route table.

      Kernel IP routing table
      Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
      default         gateway         0.0.0.0         UG    0      0        0 eth0
      172.16.238.0    0.0.0.0         255.255.255.0   U     0      0        0 eth0
      172.17.0.0      0.0.0.0         255.255.0.0     U     0      0        0 eth1

<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%2006.png" width=1000 />
<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%2007.png" width=1000 />

<br>
<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%2010.png" width=1000 />


## <span id="DNS">DNS</span>

[[☝️top]](#top)

- `DNS`: resolves IP of a domain name. 
- `ping`: a computer network administration software utility used to test the reachability of a host on an Internet Protocol (IP) network.
- `/etc/hosts`: points domains/hostnames to IPs locally.
- `/etc/resolv.conf`: contains information about dns server (nameserver).

<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%20011.png" width=1000 />
<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%20012.png" width=1000 />
<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%20013.png" width=1000 />
<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%20014.png" width=1000 />
<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%20015.png" width=1000 />
<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%20016.png" width=1000 />
<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%20017.png" width=1000 />
<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%20018.png" width=1000 />
<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%20019.png" width=1000 />
<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%2020.png" width=1000 />


<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%2023.png" width=1000 />

To edit `/etc/hosts`, you can do, for example: 

      sudo vi /etc/hosts

      127.0.0.1       localhost
      ::1     localhost ip6-localhost ip6-loopback
      fe00::0 ip6-localnet
      ff00::0 ip6-mcastprefix
      ff02::1 ip6-allnodes
      ff02::2 ip6-allrouters
      172.16.xxx.x    imaginary_website.com host01
      172.17.x.x      imaginary_website.com host01
      127.0.0.1       www.google.com host01

### Search Domain 

<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%2022.png" width=1000 />

If you want to omit the default domain name when searching on address bar, 
you can have the `/etc/resolv.conf` append the default domain name by adding the following line - `search [default_domian_name]`:

      [/etc/resolv.conf]

      search stratos.xfusioncorp.com
      nameserver 127.0.0.11
      nameserver 8.8.8.8
      search google.com
      options ndots:0

Now if you search `drive`, for instance, the browser will direct you to `drive.google.com`.

### NSLoopup

<img src="https://github.com/Coding-Forest/2022-Linux/blob/main/images/Linux%2021.png" width=1000 />

- `dig`: is a network administration command-line tool for querying the Domain Name System (DNS). dig is useful for network troubleshooting and for educational purposes. 

<br>


## <span id="Applications">Applications</span>

[[☝️top]](#top)

- Python
- NodeJS
- Java

- Building and Deployment
- Troubleshooting Applications

<br>

- `Python` > intermediary `byte code` > `machine code`

<br>

### Packages / modules / libraries

- `Filesystems`
- `Math`
- `Operating system`
- `HTTP`
- `Security`
- `Networking`

<br>

### Build

- process: `develope` > `compile` > `package` > `document`
  - `...` > `javac Class.java` > `jar cf Class.jar` > `javadoc Class.java`

- Procedure involves...

  - Compile
  - Run tests
  - Vulnerability tests
  - Code signing
  - Package
  - Delivery

- Build Tools

<br>

### Java

**Setup**

1. Manually download the `tar` file at https://jdk.java.net/17/.
2. [Terminal]> `tar -xvf openjdk-17.0.2_linux-aarch64_bin.tar.gz`

<br>

**JDK (Java Development Kit)**

- develop
  - `jdb`: java debugger
  - `jdvadoc`: java source code documentation tool

- build
  - `javac`: build and compile
  - `jar`: archive the developed and dependencies into a single `jar` file. 

- run
  - `JRE`: Java Runtime Environment. Needed to run a java programme in ANY given system.  
  - `java`: java command line utility (loader)

<br>

**Instal Java**

1. Manually click-download `tar` file at https://openjdk.java.net/install/
2. [Terminal] > `tar -xvf openjdk-17*_bin.tar.gz`

<br>

**Problem**

- Install java 17 inside `/opt` on `app_server1` server.

Solution:
1. `ssh app_server1`: you need to change account; hence, `ssh username`.
2. `sudo curl https://download.java.net/.../openjdk-17_linux-x64_bin.tar.gz --output /opt/openjdk-17_linux-x64_bin.tar.gz`: download the file.

        Warning: Binary output can mess up your terminal. Use "--output -" to tell 
        Warning: curl to output it to your terminal anyway, or consider "--output 
        Warning: <FILE>" to save to a file.

3. `sudo tar -xf /opt/openjdk-17_linux-x64_bin.tar.gz -C /opt/`: uncompress the file. 
4. `/opt/jdk-17/bin/java -version`: Check version. 
5. `export PATH=$PATH:/opt/jdk-13.0.2/bin`: set java binary path in environment PATH variable to use java binaries wihtout using the full path to run it.

<br>

### Compiling in `java`


        > WeatherApp.class     WeatherApp.java

<br>

**Compare `source code` and `byte code`**

Source code

        public class WeatherApp {
        public static void main(String[] args) {
              System.out.println("Today's Weather");
            }
        }

Byte code

        java/lang/Object<init>()V


        java/lang/SystemoutLjava/io/PrintStreamToday's Weather

        java/io/PrintStreamprintln(Ljava/lang/String;)WeatherAppCodeLineNumberTablemain([Ljava/lang/String;)V
        SourceFile
              WeatherApp.java!*  


<br>

### Packaging in `java`

`JAR`: Java Archive. Packages up multiple files and required dependencies into a single "**distributable**" package. 
`Main-Class`property in `manifest.mf`: specifies the entry point for the distributed package (`Forecast` in this case).

      jar cf WeatherApp.jar Weather.class Forecast.class WeatherStation.class ...
      > WeatherApp.jar

      > META-INF/MANIFEST.MF
            Manifest-Version: 1.0
            Created-By: 1.8.0_242 (Private Build)
            Main-Class: Weather

<br>

If you are running a jar file, you can run it like this: 

      java -jar WeatherApp.jar
      >> programme runs...

<br>

**Java Build Tools**

Build tools help automate the build process (`compile` > `package` > `document`). 

- `Maven`
- `Gradle`
- `ANT`

Let's install build automation tools: `Ant` & `Maven`

      sudo install -y ant
      sudo install -y maven

Examine the `build.xml` file: `cat build.xml`

      <?xml version="1.0"?>
      <project name="Ant" default="main" basedir=".">
      <!-- Compiles the java code (including the usage of library for JUnit -->
      <target name="compile">
            <javac srcdir="/opt/ant/src" destdir="/opt/ant/build">
            </javac>
      </target>
      <!-- Creates Javadoc -->
      <target name="docs" depends="compile">
            <javadoc packagenames="src" sourcepath="/opt/ant/src" destdir="/opt/ant/docs">
                  <!-- Define which files / directory should get included, we include all -->
                  <fileset dir="/opt/ant/src">
                  <include name="**" />
                  </fileset>
            </javadoc>
      </target>
      <!--Creates the deployable jar file  -->
      <target name="jar" depends="compile">
            <jar basedir="/opt/ant/build" destfile="/opt/ant/dist/WeatherApp.jar" >
                  <manifest>
                  <attribute name="Main-Class" value="WeatherApp" />
                  </manifest>
            </jar>
      </target>
      <target name="run" depends="jar">
            <java jar="/opt/ant/dist/WeatherApp.jar" fork="true" />
      </target>
      <target name="main" depends="compile, jar, docs, run">
            <description>Main target</description>
      </target>
      </project>

<br>

Now compile your app using `ant`.

      ant compile jar

Now runt `ant`.

      ant

<br>

      Buildfile: /opt/ant/build.xml

      compile:
      [javac] /opt/ant/build.xml:5: warning: 'includeantruntime' was not set, defaulting to build.sysclasspath=last; set to false for repeatable builds

      jar:

      docs:
      [javadoc] Generating Javadoc
      [javadoc] Javadoc execution
      [javadoc] Loading source file /opt/ant/src/WeatherApp.java...
      [javadoc] Constructing Javadoc information...
      [javadoc] Standard Doclet version 1.8.0_312
      [javadoc] Building tree for all the packages and classes...
      [javadoc] Building index for all the packages and classes...
      [javadoc] Building index for all classes...

      run:
      [java] Today's Weather...

      main:

      BUILD SUCCESSFUL
      Total time: 1 second

<br>

      <?xml version="1.0" encoding="UTF-8"?>

      <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
            <modelVersion>4.0.0</modelVersion>

            <groupId>org.WeatherFoundation.Weatherapp</groupId>
            <artifactId>WeatherApp</artifactId>
            <version>1.0-SNAPSHOT</version>ForestFoundation
            <url>http://www.ForestFoundation.org</url>

            <properties>
            <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
            <maven.compiler.source>1.7</maven.compiler.source>
            <maven.compiler.target>1.7</maven.compiler.target>
            </properties>

            <dependencies>
            <dependency>
                  <groupId>junit</groupId>
                  <artifactId>junit</artifactId>
                  <version>4.11</version>
                  <scope>test</scope>
            </dependency>
            </dependencies>
            
            <build>
            ...
            </build>
      </project>

<br>

Compile & package application. 

      cd /dest_path/WeatherApp/
      sudo mvn package

      [INFO] Building jar: /opt/maven/WeatherApp/target/WeatherApp-1.0-SNAPSHOT.jar
      [INFO] ------------------------------------------------------------------------
      [INFO] BUILD SUCCESS
      [INFO] ------------------------------------------------------------------------
      [INFO] Total time: 8.181s
      [INFO] Finished at: Fri Jan 21 18:16:39 UTC 2022
      [INFO] Final Memory: 24M/1481M
      [INFO] ------------------------------------------------------------------------

<br>

Run application.

      java -cp /opt/maven/WeatherApp/target/WeatherApp-1.0-SNAPSHOT.jar org.ForestFoundation.app.App


<br>

**Example DevOps operations**

- Automating a build process with CI/CD pipelines 
  - (continuous integration and either continuous delivery or continuous deployment)
- Containerising an application with Docker

<br>

**Documentation**

      javadoc -d doc Forecast.java

      Loading source file Forecast.java...
      Constructing Javadoc information...
      Creating destination directory: "doc/"
      Standard Doclet version 13.0.2
      Building tree for all the packages and classes...
      Generating doc/Forecast.html...
      Generating doc/package-summary.html...
      Generating doc/package-tree.html...
      Generating doc/constant-values.html...
      Building index for all the packages and classes...
      Generating doc/overview-tree.html...
      Generating doc/deprecated-list.html...
      Generating doc/index-all.html...
      Building index for all classes...
      Generating doc/allclasses-index.html...
      Generating doc/allpackages-index.html...
      Generating doc/index.html...
      Generating doc/help-doc.html...

<br>




## <span id=""></span>

[[☝️top]](#top)

<br>

### <span id="ref">References</span>

[[☝️top]](#top)

  - freeCodeCamp.org (2020) DevOps Prerequisites Course - Getting started with DevOps https://www.youtube.com/watch?v=Wvf0mBNGjXY