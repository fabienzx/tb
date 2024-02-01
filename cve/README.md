# CVE Identification

- [Trivy](#trivy)


## Trivy

Installation according to :
https://aquasecurity.github.io/trivy/v0.49/getting-started/installation/

In order to use Trivy to find already known CVE within TB container, we first need to pull Trivy's latest build image

```bash
docker pull aquasec/trivy:0.49.0 
```

Then we can run the following command to make Trivy analyze the container :

```bash
docker run -v /var/run/docker.sock:/var/run/docker.sock -v $HOME/Library/Caches:/root/.cache/ aquasec/trivy:0.49.0 image thingsboard/tb-postgres --format json > rapport_vulnerabilites.json
```

Result expected : Available in **rapport_vulnerabilities.json**

