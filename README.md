# SPARK

## [Spark Documentation](http://spark.apache.org/docs/2.0.1/)

## Spark Source Code Installation
1. Download the spark source code from [**here**](http://spark.apache.org/downloads.html)
2. Unzip the downloaded tar: 
`tar -xvzf spark-2.0.1.tgz`
3. Enter the spark directory: 
`cd spark-2.0.1`
4. Build the source code: 
`./build/mvn -Pyarn -Phadoop-2.6  -Dhadoop.version=2.6.0  -Phive -Phive-thriftserver -DskipTests  package`
	
	
## Spark Shell
```
cd spark-2.0.1
./bin/spark-shell
```

This will open the spark shell where you can code in scala.

You might see the following warning when the spark shell is starting up: `WARN NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable`
  * This warning won't cause any issues unless your code depends on a binary like libsnappy.so which is present under native-hadoop library location.
  * To resolve this warning, include the native-hadoop library location in the cluster's LD_LIBRARY_PATH environment variable:
  
  `export LD_LIBRARY_PATH=/opt/cloudera/parcels/CDH/lib/hadoop/lib/native:$LD_LIBRARY_PATH`
  

## SBT (Scala Build Tool)
SBT is a tool to build your spark application (coded in scala) into a jar. The built jar can then be run using spark-submit.

1. Download SBT from [**here**](http://www.scala-sbt.org/0.13/docs/Installing-sbt-on-Linux.html)
2. Unzip the downloaded tar: `tar -xvzf <file.tgz>`
3. Add sbt executable location to PATH variable: `export PATH=/data/home/devbld/sbt-launcher-packaging-0.13.13/bin:$PATH`

**NOTE** - Don't use the SBT that comes with spark installation. There are certain bugs in there. 



## Self-Contained Spark Application

* Let's suppose that we have a created a spark application in scala by the name of **SimpleApplication.scala**. To build it, we will be using SBT.
* SBT requires a configuration file. Let's call it simple.sbt whose content is:
```
name := "Simple Project"

version := "1.0"

scalaVersion := "2.11.7"

libraryDependencies += "org.apache.spark" %% "spark-core" % "2.0.1"
```

* For SBT to build our spark code correctly and produce a jar, we need to put SimpleApp.scala and simple.sbt in a typical directory structure:
```
$ find .
.
./simple.sbt
./src
./src/main
./src/main/scala
./src/main/scala/SimpleApp.scala
./project
./target
```

* We will use sbt to package our spark application
```
$ sbt package
```

This will generate a jar under `./target/scala-2.11`

* We will use spark-submit to run the application
```
$ $SPARK_HOME/bin/spark-submit --class "SimpleApp" --master local[4] target/scala-2.11/simple-project_2.11-1.0.jar
```
 