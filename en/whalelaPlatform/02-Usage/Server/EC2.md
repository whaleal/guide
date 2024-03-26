### EC2

 Adding a host can deploy mongodb to your own resource environment

![](../../../../images/whalealPlatformImages/EC2.png)

**Add host**

There are two ways to add a host provider. After selecting the project to generate the agentid, follow the prompt information and click OK.

1、method one:

![](../../../../images/whalealPlatformImages/cEC2.png)

* Log in to the server to download the agent

  ![](../../../../images/whalealPlatformImages/agent.png)

* After executing the script, check whether the agent program is started.

  ![](../../../../images/whalealPlatformImages/1agent.png)

* Log in to the WAP platform to view

  ![](../../../../images/whalealPlatformImages/3agent.png)

2、Method 2:

Need to manually install the java environment and plug-ins

![](../../../../images/whalealPlatformImages/c2EC2.png)

* Download and install java environment

  ```
  tar -zxvf jdk-11.0.9_linux-x64_bin.tar.gz -C /usr/local/
  
  vi /etc/profile
  # Add the following configuration to the last line
  export JAVA_HOME=/usr/local/jdk-11.0.9
  export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
  export PATH=$PATH:$JAVA_HOME/bin
  
  source /etc/profile
  
  # View current version
  java --version
  ```

* Install ioStat plug-in

  ```
  yum install sysstat
  ```

* Download agent package

  ![](../../../../images/whalealPlatformImages/4agent.png)

* Check the platform after startup

  ![](../../../../images/whalealPlatformImages/6agent.png)