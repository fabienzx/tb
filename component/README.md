# Component identification

- [Services](#services)
- [Network dependencies](#network-dependencies)
- [Layers and build](#layers-and-build)
- [Overall configuration](#overall-configuration)


## Services

In order to list services related to the use of Thingsboard inside Docker Linux :

```bash
docker-compose config --services
```

Result expected : `mytb`

In our case, ***mytb*** is the name of the service who's using the docker image "thingsboard/tb-postgres".

## Network dependencies

In order to list network dependencies (namely opened ports, redirections and protocols) declared inside [docker-compose.yml](https://github.com/fabienzx/tb/blob/main/component/docker-compose.yml) (in a friendly way) :
```bash
docker-compose config | awk '/^\s+ports:/ {flag=1; next} /^\S/ {flag=0} flag && /published|target|protocol/ {print}'
```

Result expected :
```yaml
- published: 8080
  target: 9090
- published: 1883
  target: 1883
- published: 7070
  target: 7070
- protocol: udp
  published: 5683
  target: 5683
- protocol: udp
  published: 5684
  target: 5684
- protocol: udp
  published: 5685
  target: 5685
- protocol: udp
  published: 5686
  target: 5686
- protocol: udp
  published: 5687
  target: 5687
- protocol: udp
  published: 5688
  target: 5688
```

## Layers and build

In order to display the history of the Docker image layers, showing the commands run in each layer during the image build process :
```bash
docker history thingsboard/tb-postgres
```

Result expected :
```bash
IMAGE          CREATED        CREATED BY                                      SIZE      COMMENT
0a58a12b9016   2 months ago   CMD ["start-tb.sh"]                             0B        buildkit.dockerfile.v0
<missing>      2 months ago   VOLUME [/data]                                  0B        buildkit.dockerfile.v0
<missing>      2 months ago   EXPOSE map[5685/udp:{}]                         0B        buildkit.dockerfile.v0
<missing>      2 months ago   EXPOSE map[5683/udp:{}]                         0B        buildkit.dockerfile.v0
<missing>      2 months ago   EXPOSE map[1883/tcp:{}]                         0B        buildkit.dockerfile.v0
<missing>      2 months ago   EXPOSE map[9090/tcp:{}]                         0B        buildkit.dockerfile.v0
<missing>      2 months ago   USER thingsboard                                0B        buildkit.dockerfile.v0
<missing>      2 months ago   RUN /bin/sh -c apt-get update     && apt-get…   419MB     buildkit.dockerfile.v0
<missing>      2 months ago   COPY logback.xml thingsboard.conf start-db.s…   201MB     buildkit.dockerfile.v0
<missing>      2 months ago   ENV PGLOG=/var/log/postgres                     0B        buildkit.dockerfile.v0
<missing>      2 months ago   ENV SPRING_DATASOURCE_PASSWORD=postgres         0B        buildkit.dockerfile.v0
<missing>      2 months ago   ENV SPRING_DATASOURCE_USERNAME=thingsboard      0B        buildkit.dockerfile.v0
<missing>      2 months ago   ENV SPRING_DATASOURCE_URL=jdbc:postgresql://…   0B        buildkit.dockerfile.v0
<missing>      2 months ago   ENV SPRING_DRIVER_CLASS_NAME=org.postgresql.…   0B        buildkit.dockerfile.v0
<missing>      2 months ago   ENV PATH=/usr/local/sbin:/usr/local/bin:/usr…   0B        buildkit.dockerfile.v0
<missing>      2 months ago   ENV PGDATA=/data/db                             0B        buildkit.dockerfile.v0
<missing>      2 months ago   ENV DATABASE_TS_TYPE=sql                        0B        buildkit.dockerfile.v0
<missing>      2 months ago   ENV HTTP_BIND_PORT=9090                         0B        buildkit.dockerfile.v0
<missing>      2 months ago   ENV DATA_FOLDER=/data                           0B        buildkit.dockerfile.v0
<missing>      2 months ago   ENV PG_MAJOR=12                                 0B        buildkit.dockerfile.v0
<missing>      3 months ago   RUN /bin/sh -c apt-get update && apt-get ins…   443MB     buildkit.dockerfile.v0
<missing>      3 months ago   ENV JAVA_DEBIAN_VERSION=11.0.20+8-1~deb11u1     0B        buildkit.dockerfile.v0
<missing>      3 months ago   ENV JAVA_VERSION=11.0.20                        0B        buildkit.dockerfile.v0
<missing>      3 months ago   ENV JAVA_HOME=/docker-java-home                 0B        buildkit.dockerfile.v0
<missing>      3 months ago   ENV LANG=C.UTF-8                                0B        buildkit.dockerfile.v0
<missing>      8 months ago   RUN /bin/sh -c apt-get update     && apt-get…   1.96MB    buildkit.dockerfile.v0
<missing>      9 months ago   /bin/sh -c #(nop)  CMD ["bash"]                 0B        
<missing>      9 months ago   /bin/sh -c #(nop) ADD file:a2378c1b12e95db69…   80.5MB
```

## Overall configuration

In order to get detailed information about the Docker container, including its configuration, network settings, volumes, and more (in a friendly json way) :
```bash
docker inspect --format='{{json .Config}}' thingsboard/tb-postgres | jq .
```

Result expected :
```json
{
  "Hostname": "",                                                                                                                               
  "Domainname": "",                                                                                                                             
  "User": "thingsboard",                                                                                                                        
  "AttachStdin": false,                                                                                                                         
  "AttachStdout": false,                                                                                                                        
  "AttachStderr": false,                                                                                                                        
  "ExposedPorts": {                                                                                                                             
    "1883/tcp": {},                                                                                                                             
    "5683/udp": {},                                                                                                                             
    "5685/udp": {},                                                                                                                             
    "9090/tcp": {}                                                                                                                              
  },                                                                                                                                            
  "Tty": false,                                                                                                                                 
  "OpenStdin": false,                                                                                                                           
  "StdinOnce": false,                                                                                                                           
  "Env": [                                                                                                                                      
    "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/lib/postgresql/12/bin",                                             
    "LANG=C.UTF-8",                                                                                                                             
    "JAVA_HOME=/docker-java-home",                                                                                                              
    "JAVA_VERSION=11.0.20",                                                                                                                     
    "JAVA_DEBIAN_VERSION=11.0.20+8-1~deb11u1",                                                                                                  
    "PG_MAJOR=12",                                                                                                                              
    "DATA_FOLDER=/data",                                                                                                                        
    "HTTP_BIND_PORT=9090",                                                                                                                      
    "DATABASE_TS_TYPE=sql",                                                                                                                     
    "PGDATA=/data/db",                                                                                                                          
    "SPRING_DRIVER_CLASS_NAME=org.postgresql.Driver",                                                                                           
    "SPRING_DATASOURCE_URL=jdbc:postgresql://localhost:5432/thingsboard",                                                                       
    "SPRING_DATASOURCE_USERNAME=thingsboard",                                                                                                   
    "SPRING_DATASOURCE_PASSWORD=postgres",                                                                                                      
    "PGLOG=/var/log/postgres"                                                                                                                   
  ],                                                                                                                                            
  "Cmd": [                                                                                                                                      
    "start-tb.sh"                                                                                                                               
  ],                                                                                                                                            
  "ArgsEscaped": true,                                                                                                                          
  "Image": "",                                                                                                                                  
  "Volumes": {                                                                                                                                  
    "/data": {}                                                                                                                                 
  },                                                                                                                                            
  "WorkingDir": "",                                                                                                                             
  "Entrypoint": null,                                                                                                                           
  "OnBuild": null,                                                                                                                              
  "Labels": null                                                                                                                                
}
```
---

<br>

So that we can then tell the following :

    Exposed Ports:
        The container exposes the following ports:
            1883/tcp: MQTT, used for IoT communication.
            5683/udp: CoAP, used for IoT communication.
            5685/udp: CoAP, used for IoT communication.
            9090/tcp: HTTP_BIND_PORT, used to access the web app.

    Environment Variables:
        The environment variables indicate specific Thingsboard and PostgreSQL configurations:
            JAVA_HOME is set to version 11 of the JDK.
            The PostgreSQL data directory is set to "/data/db".
            PostgreSQL database connection information is provided in the variables SPRING_DATASOURCE_URL, SPRING_DATASOURCE_USERNAME, and SPRING_DATASOURCE_PASSWORD.
            The HTTP_BIND_PORT is configured to 9090.
            The database type is specified as TimescaleDB in DATABASE_TS_TYPE.
            PGLOG indicates the PostgreSQL log directory.

    Execution Command:
        The execution command is "start-tb.sh," likely used to start Thingsboard.

    Volumes:
        The container mounts a volume at "/data," suggesting that data, including database data, is persistent.
