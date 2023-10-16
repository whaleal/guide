## JDK Installation and Deployment

It is recommended to install JDK 11.

### 1. Dependency Environment
For open-source JDK, font library support is required. If it is already present on the Linux system, there's no need to install it.
```bash
yum install fontconfig
fc-cache --force
fc-cache -f
```

### 2. Extract JDK Installation Package
```bash
tar -zxvf jdk-11.0.9_linux-x64_bin.tar.gz -C /usr/local/
```

### 3. Configure Environment Variables
Open the profile configuration file:
```bash
vi /etc/profile
```
Add the following configurations at the end of the file:
```bash
export JAVA_HOME=/usr/local/jdk-11.0.9
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$PATH:$JAVA_HOME/bin
```
Refresh the configuration to make it effective:
```bash
source /etc/profile
```

### 4. Verification
Check the installed Java version:
```bash
java -version
```

Please note that when copying and pasting these commands, ensure that the formatting remains consistent, and adjust paths and filenames as needed for your system.