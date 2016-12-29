# SPARK

## Spark Source Code Installation
1. Download the source code from [here](http://spark.apache.org/downloads.html)
2. Unzip the downloaded tar: `tar -xvzf spark-2.0.1.tgz`
3. Enter the spark directory: `cd spark-2.0.1.tgz`
4. Build the source code: `./build/mvn -Pyarn -Phadoop-2.6  -Dhadoop.version=2.6.0  -Phive -Phive-thriftserver -DskipTests  package`
	