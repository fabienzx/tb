# Component identification

- [Services](#services)
- [Network dependencies](#network_dependencies)


## Services

In order to list services related to the use of Thingsboard inside Docker Linux :
`docker-compose config --services`

Result expected :
```bash
mytb
```

## Network dependencies

In order to list network dependencies declared inside ***docker-compose.yml*** :
```bash
docker-compose config | grep -E '^\s+ports:' -A 20 | grep -E 'published|target'
```

Result expected :
```yaml
- published: 8080
      target: 9090
    - published: 1883
      target: 1883
    - published: 7070
      target: 7070
      published: 5683
      target: 5683
      published: 5684
      target: 5684
      published: 5685
      target: 5685
      published: 5686
      target: 5686
      published: 5687
```
