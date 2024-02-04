# Component identification

- [Services](#services)
- [Network dependencies](#network_dependencies)


## Services

In order to list services related to the use of Thingsboard inside Docker Linux :

```bash
docker-compose config --services
```

Result expected : `mytb`
In our case, ***mytb*** is the name of the service who's using the docker image "thingsboard/tb-postgres".

## Network dependencies

In order to list network dependencies (namely opened ports, redirections and protocols) declared inside ***docker-compose.yml*** :
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
