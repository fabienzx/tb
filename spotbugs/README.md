# Static code analysis Spotbugs

## Summary
- [Installation](#installation)
- [Scan](#scan)
- [Results](#results) 


## Installation

```bash
git clone https://github.com/spotbugs/spotbugs.git
```


Then you can unzip the package

```bash
unzip spotbugs-* 
```


Once that's done, you can access the app folder, grant yourself exec permission on ./spotbugs 

```bash
cd spotbugs-(X.Y.Z) && chmod +x bin/spotsbugs
```

You can open SpotBugs graphical interface with (*pwd: spotbugs-X.Y.Z/bin*)

```bash
./spotbugs
```

## Scan

We first need to locate the ***jar file*** from thingsboard application.

To do this, we need to search for that file in the container thingsboard/tb-postgres

```bash
find / -name "*.jar"
```
>find: ‘/proc/tty/driver’: Permission denied
>
>/usr/lib/jvm/java-11-openjdk-amd64/lib/jrt-fs.jar
>
>**/usr/share/thingsboard/bin/thingsboard.jar**
>
>/usr/share/ca-certificates-java/ca-certificates-java.jar
>
>find: ‘/etc/ssl/private’: Permission denied
>
>find: ‘/var/lib/postgresql/12/main’: Permission denied
>
>find: ‘/var/cache/ldconfig’: Permission denied
>
>find: ‘/var/cache/apt/archives/partial’: Permission denied
>
>find: ‘/root’: Permission denied

---

Now we need to extract this jar file from the container to our host machine, to do this :

```bash
docker ps   # then get the id of the container (let it be e.g. 123456789)
docker cp 123456789:/usr/share/thingsboard/bin/thingsboard.jar .
```

After this command, you should have the jar file in your current directory.

When this is done, you can open SpotBugs, create a project, choose the JAR file, and proceed to start the scan.


## Results

The GUI will be displaying a tree of vulnerabilities, issues, code flaws, recommendations.

You can then export the results as XML or HTML webpage for instance.

>Webpage available [here](sbugs-result.xml.html)

>XML (less readable) available [here](sbugs-result.xml)



