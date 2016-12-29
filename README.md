# SPARK

## Spark Source Code Installation
1. Download the spark source code from [**here**](http://spark.apache.org/downloads.html)
2. Unzip the downloaded tar: 

`tar -xvzf spark-2.0.1.tgz`
3. Enter the spark directory: 

`cd spark-2.0.1`
4. Build the source code: 
`./build/mvn -Pyarn -Phadoop-2.6  -Dhadoop.version=2.6.0  -Phive -Phive-thriftserver -DskipTests  package`
	
	
## Spark Shell
`cd spark-2.0.1`

`./bin/spark-shell`

This will open the spark shell where you can code in scala.

You might see the following warning: `WARN NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable`
  * This warning won't cause any issues unless your code doesn't depend on a binary like libsnappy.so which is present in native-hadoop library location.
  * To resolve this warning, include the native-hadoop library location in the cluster's LD_LIBRARY_PATH variable:
  
  `export LD_LIBRARY_PATH=/opt/cloudera/parcels/CDH/lib/hadoop/lib/native:$LD_LIBRARY_PATH`