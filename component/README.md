# Component identification

- [Services](#services)
- [Network dependencies](#network_dependencies)


## Services

In order to list services related to the use of Thingsboard inside Docker Linux :
`docker-compose config --services`

Result expected :
`mytb`


## Network dependencies

In order to list network dependencies declared inside ***docker-compose.yml*** :
`docker-compose config`

Result expected :
```yaml
services:
  mytb:
    environment:
      TB_QUEUE_TYPE: in-memory
    image: thingsboard/tb-postgres
    ports:
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
    restart: always
    volumes:
      - /home/kali/.mytb-data:/data:rw
      - /home/kali/.mytb-logs:/var/log/thingsboard:rw
  version: '3.0'
