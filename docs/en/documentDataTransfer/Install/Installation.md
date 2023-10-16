## Installation and Deployment

### Deploying DDT on CentOS

#### JDK Installation

1. Download JDK 11 tgz package:

```bash
wget https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.9_linux-x64_bin.tar.gz
```

2. Extract the downloaded tar package:

```bash
tar -zxvf openjdk-11.0.9_linux-x64_bin.tar.gz
```

3. Move the extracted directory:

```bash
mv jdk-11.0.9 /usr/local/jdk11
```

4. Configure environment variables:

```bash
vi /etc/profile
export JAVA_HOME=/usr/local/jdk11
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
```

5. Refresh the environment:

```bash
source /etc/profile
```

6. Verify the installation:

```bash
java --version
```

#### Running DDT

##### Prerequisites

Ensure that the installation and configuration files are in place and the Java environment is correctly set up before starting the DDT process.

##### Starting the Service

1. Navigate to the `bin` directory.
2. Run the startup script: `./start-DDT.sh`. This starts the data transfer functionality.
3. Run the startup script: `./start-monitor.sh`. This starts the web monitoring functionality.

##### Stopping the Service

1. Navigate to the `bin` directory.
2. Run the shutdown script: `./stop-DDT.sh`. This stops the data transfer functionality.
3. Run the shutdown script: `./stop-monitor.sh`. This stops the web monitoring functionality.

#### DDT Features

1. DDT supports full, real-time, full + incremental, and full + real-time synchronization modes. Incremental mode refers to real-time synchronization with a time range restriction on the Oplog.
2. DDT currently supports MongoDB versions 3.2 to 6.0. Newer version features such as time-series tables and bucket tables are fully supported for synchronization.
3. During real-time synchronization, users can customize the synchronization of specific DDL operations. Additionally, DDL operations are logged for auditing purposes.

Currently, synchronizing data with the same version has no impact. When synchronizing from a higher version to a lower version, new types introduced in the higher version cannot be synchronized to the lower version. Similarly, when synchronizing from a lower version to a higher version, certain types removed in the higher version cannot be synchronized. For example, deleting an index in version 3.2 or adding a time-series table in version 5.0.