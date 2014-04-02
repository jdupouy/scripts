# How to install correctly a JDK

Before using these tools download the jdk from wherever you want, oracle for instance (http://www.oracle.com/technetwork/java/javase/downloads/index.html).

Once downloaded extract it to your favorite location

```
cd /opt/
sudo mv ~/downloads/jdk-8-linux-x64.tar.gz .
sudo tar -xvf jdk-8-linux-x64.tar.gz
sudo ln -s /opt/jdk1.8.0 oracle-java8-jdk
```

In order to be able to use `update-java-alternatives` to switch easily from a version to another we have to locate everything in the `/usr/lib/jvm/` forlder.

```
cd /usr/lib/jvm/
sudo ln -s /opt/oracle-java8-jdk oracle-java8-jdk
```

Then for each executables available in the jvm we have to create an alternative by using the classical `update-alternatives` tool. To avoid doing it manually for all the executable bundled in the JVM archive we can make use of the script `install-java-alternatives` available.

```
sudo install-java-alternatives /usr/lib/jvm/oracle-java8-jdk
```

For the `update-java-alternatives` tool to work corectly it need a `.jinfo` file. This will is specific to each JVM and can be generated automatically by using the `mkjinfo` tool as follow.

```
mkjinfo /usr/lib/jvm/oracle-java8-jdk oracle-java8-jdk
```

This wiil generate the convenient `.oracle-java8-jdk.jinfo` file to place in the `/usr/lib/jvm` folder. you can edit this file manually to change some options like the priority of your JVM or the name, etc...

Once this file is in place you can use the `update-java-aleternatives` command to set up your jave environment. Here below you will find a list of usefull commands that can be used to update your Java environment.

List all installed packages:
```
update-java-alternatives -l
```

Set all alternatives of a registered jre/sdk installation:
```
sudo update-java-alternatives -s oracle-java8-jdk
```

Check if everything is working nicely:
```
java -version
```
