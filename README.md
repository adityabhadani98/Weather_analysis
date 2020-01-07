# NCDC-weather-dataset-Hadoop-MapReduce-Pig-Hive

This is an Hadoop Map/Reduce application for Working on weather data It reads the text input files, breaks each line into stations weather data and finds average for temperature , dew point , wind speed. The output is a locally sorted list of stations and its 12 attribute vector of average temperature , dew , wind speed of 4 sections for each month.

Installation

Since this a Map reduce Project , please install Apache Hadoop , Refere the below site for more details

https://hadoop.apache.org/docs/current/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html

The National Climatic Data Center (NCDC) is the world's largest active archive of weather data. I downloaded the NCDC data for year 1930 and loaded it in HDFS system. I implemented MapReduce program and Pig, Hove scripts to findd the Min, Max, avg temparature for diffrent stations.

Compiled the Java File: javac -classpath /home/student3/hadoop-common-2.6.1.jar:/home/student3/hadoop-mapreduce-client-core-2.6.1.jar:/home/student3/commons-cli-2.0.jar -d .  MaxTemperature.java MaxTemperatureMapper.java  MaxTemperatureReducer.java

Created the JAR file: jar -cvf hadoop-project.jar *class

Executed the jar file: hadoop jar hadoop-project.jar MaxTemperature  /home/student3/Project/ /home/student3/Project_output111

Copy the output file to local
hdfs dfs -copyToLocal /home/student3/Project_output111/part-r-00000

PIG Script

Pig -x local
grunt> records = LOAD '/home/student3/Project/Project_Output/output111.txt'
AS (year:chararray, temperature:int);
grunt> DUMP records;
grunt> grouped_records = GROUP records BY year;
grunt> DUMP grouped_records;
grunt> max_temp = FOREACH grouped_records GENERATE group,
>> MAX(filtered_records.temperature);
grunt> DUMP max_temp;
grunt> min_temp = FOREACH grouped_records GENERATE group,
>>  MIN(records.temperature);
grunt> DUMP min_temp;
