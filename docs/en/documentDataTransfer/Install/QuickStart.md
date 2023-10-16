## QuickStart

## Startup Steps

#### 1. Download DDT

Visit https://github.com/whaleal/DocumentDataTransfer/releases

Download the latest version of DDT.tar.gz.

#### 2. Extract

```bash
mkdir DDT
tar -zxvf DDT.tar.gz -C DDT
```

#### 3. Modify Configuration Files
[Introduction to Configuration](Configuring.md)

```bash
cd DDT/config
vi DDT.properties
```

#### 4. Prepare to Start

```bash
cd bin
./start-all.sh
```

#### 5. Check the Running Status

Access the web monitoring page:
http://bind_ip:58000/DDT_WEB/#/home

#### 6. Check the Data Consistency of the Target

1. Use the built-in validation tool of MongoDB (may lock the database):

```javascript
use xxx
db.runCommand({ dbHash: 1 })
```

2. Manually validate the data:

```bash
java -jar checkData.jar /path/to/configuration/DDT.properties
```

Please replace `/path/to/configuration/DDT.properties` with the actual path to your DDT configuration file.