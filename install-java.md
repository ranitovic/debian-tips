# Install Java Server

#### Extract file to /usr/lib/jvm and rename it to java-8-oracle

```console
mkdir /usr/lib/jvm
tar zxvf server-jre-8u201-linux-x64.tar.gz -C /usr/lib/jvm/
mv /usr/lib/jvm/jdk1.8.0_201 /usr/lib/jvm/java-8-oracle
```

#### Show Java alternatives
```console
update-alternatives --config java
```

#### Add Java 8 JRE to Java alternatives
```console
update-alternatives --install /usr/bin/java java /usr/lib/jvm/java-8-oracle/bin/java 1
```

#### Choose Java 8 as the default JRE if there are other alternatives
```console
update-alternatives --config java
```

#### Test the installation
```console
java -version
```

#### Java location
```console
/usr/lib/jvm/java-8-oracle/bin/java
```
