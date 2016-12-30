Given below are some spark-shell samples. 

##### Reading a local file line-by-line and showing its content
```
val fileRDD = sc.textFile("README.md")
fileRDD.collect()
``` 

##### Count the number lines which contain spark
```
val fileRDD = sc.textFile("README.md")
val filterRDD = fileRDD.filter(line => line.contains("spark"))
filterRDD.count()
```


##### Find the line with most words
```
val fileRDD = sc.textFile("README.md")
fileRDD.map(line => line.split(" ").size).reduce((a,b) => if (a > b) a else b)
```


##### Per-word count in a file
```
val fileRDD = sc.textFile("README.md")
fileRDD.flatMap(line => line.split(" ")).map(word => (word,1)).reduceByKey((a,b) => a+b).collect()
```

##### Lines with 'a'
```
val fileRDD = sc.textFile("README.md")
fileRDD.filter(line => line.contains("a")).count()
```