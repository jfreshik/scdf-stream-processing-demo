# SpringCloud DataFlow - Stream Processing Demo

## 1. Build & install application packages.

```shell script
$ ./mvnw clean install
```
**Note:** install application packages(source-app, processor-app, sink-app) into local maven repository. 

## 2. Start RabbitMQ.

#### start
```shell script
$ docker-compose up -d
```

#### admin
* URL: [http://localhost:15672](http://localhost:15672)
* id/pw: guest/guest


## 3. SpringCloud DataFlow Start.

#### 1) SpringCloud DataFlow manual install
https://dataflow.spring.io/docs/installation/local/manual

* download server jars
```shell script
wget https://repo.spring.io/release/org/springframework/cloud/spring-cloud-dataflow-server/2.5.3.RELEASE/spring-cloud-dataflow-server-2.5.3.RELEASE.jar
wget https://repo.spring.io/release/org/springframework/cloud/spring-cloud-dataflow-shell/2.5.3.RELEASE/spring-cloud-dataflow-shell-2.5.3.RELEASE.jar
wget https://repo.spring.io/release/org/springframework/cloud/spring-cloud-skipper-server/2.5.0/spring-cloud-skipper-server-2.5.0.jar
```
* running command 

#### 2) Start Skipper
```shell script
$ java -jar spring-cloud-skipper-server-2.5.0.jar
```

#### 3) Start DataFlow Server
```shell script
$ java -jar spring-cloud-dataflow-server-2.5.3.RELEASE.jar
```

#### 4) Start Shell

```shell script
$ java -jar spring-cloud-dataflow-shell-2.5.3.RELEASE.jar
```

## 4. Deploy apps.

#### 1) Register apps
```shell script
dataflow:>app register --name source-app --type source --uri maven://com.example:source-app:jar:1.0-SNAPSHOT
dataflow:>app register --name processor-app --type processor --uri maven://com.example:processor-app:jar:1.0-SNAPSHOT
dataflow:>app register --name sink-app --type sink --uri maven://com.example:sink-app:jar:1.0-SNAPSHOT
```

#### 2) Create stream
```shell script
dataflow:>stream create --name log-data --definition 'source-app | processor-app | sink-app'
```

#### 3) Deploy stream
```shell script
stream deploy --name log-data
```


## 5. Using SpringCloud DataFlow Dashboard.
http://localhost:9393/dashboard






Ref: [Spring Cloud Tutorial - Stream Processing Using Spring Cloud Data Flow](https://www.javainuse.com/spring/cloud-data-flow)
