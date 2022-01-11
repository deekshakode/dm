gopu,20,3.9f 
arun,18,4.0f 
alice,21,3.8f
bob,22,5.5f
kumar,19,3.8f 
john,18,3.8f
jackson,18,3.8f


hdfs dfs -mkdir /pig
hdfs dfs -put pigexercise.txt /pig/pigexercise.txt





grunt> A = LOAD '/pig/pigexercise.txt/ USING PigStorage (',') AS (name:chararray,age:int,gpa:float);
grunt>DUMP A
grunt>B = GROUP A BY age; 
grunt>DUMP B



grunt> customers = LOAD '/pig/customers.txt' USING PigStorage(',') as (id:int, name:chararray, age:int, address:chararray, salary:int);
  
grunt> orders = LOAD '/pig/orders.txt' USING PigStorage(',') as (oid:int, date:chararray, customer_id:int, amount:int);

grunt> customer_orders = JOIN customers BY id, orders BY customer_id;


grunt> Dump customer_orders

(2,Khilan,25,Delhi,1500,101,2009-11-20 00:00:00,2,1560)
(3,kaushik,23,Kota,2000,100,2009-10-08 00:00:00,3,1500)
(3,kaushik,23,Kota,2000,102,2009-10-08 00:00:00,3,3000)
(4,Chaitali,25,Mumbai,6500,103,2008-05-20 00:00:00,4,2060)



grunt> student_details = LOAD /pig/StudentDetails.txt' USING PigStorage(',')as (id:int, firstname:chararray, lastname:chararray,age:int, phone:chararray, city:chararray);

grunt> order_by_data = ORDER student_details BY age DESC;

grunt> Dump order_by_data;








**********************************************************


habase



To start the HBase environment type hbase shell in the terminal
$hbase shell
hbase(main):001:0>

Use the create command to create a new table. You must specify the table name and the ColumnFamily name.
hbase(main):001:0> create 'student', 'name', 'subject'
0 row(s) in 0.4170 seconds

=> Hbase::Table - student

Use the list command to confirm your table exists
hbase(main):002:0> list 'student'
TABLE
student
1 row(s) in 0.0180 seconds

=> ["test"]


To put data into your table, use the put command.
We are storing data for student 1
hbase(main):003:0> put 'student', '001', 'name:firstname', 'Arunkumar'
0 row(s) in 0.0850 seconds

hbase(main):004:0> put 'student', '001', 'name:lastname', 'Gopu'
0 row(s) in 0.0110 seconds

hbase(main):005:0> put 'student', '001', 'name:fullname', 'Arunkumar Gopu'
0 row(s) in 0.0100 seconds

hbase(main):003:0> put 'student', '001', 'subject:s1', 'Data Analytics'
0 row(s) in 0.0650 seconds

hbase(main):003:0> put 'student', '001', 'subject:s2', 'Data mining'
0 row(s) in 0.0450 seconds

hbase(main):003:0> put 'student', '001', 'subject:s3', 'Operating system'
0 row(s) in 0.01050 seconds

Inserting data for second student
hbase(main):003:0> put 'student', '002', 'name:firstname', 'David Jackson'
0 row(s) in 0.0850 seconds

hbase(main):004:0> put 'student', '002', 'name:lastname', 'Samuel'
0 row(s) in 0.0110 seconds

hbase(main):005:0> put 'student', '002', 'name:fullname', 'David Jackson Samuel'
0 row(s) in 0.0100 seconds

hbase(main):003:0> put 'student', '002', 'subject:s1', 'Computer Networks'
0 row(s) in 0.0650 seconds

hbase(main):003:0> put 'student', '002', 'subject:s2', 'R programming'
0 row(s) in 0.0450 seconds

hbase(main):003:0> put 'student', '002', 'subject:s3', 'Data Analytics'
0 row(s) in 0.01050 seconds


Scan the table for all data at once. One of the ways to get data from HBase is to scan. Use the scan command to scan the table for data.
hbase(main):006:0> scan 'student'
ROW                                      COLUMN+CELL
 001                                    column=name:firstname, timestamp=1421762485768, value=Arunkumar
 001                                    column=name:lastname, timestamp=1421762494563, value=Gopu
 001                                    column=name:fullname, timestamp=1421762492345, value=Arunkumar Gopu
001                                    column=subject:s1, timestamp=1421762487389, value=Data Analytics
 001                                    column=subject:s2, timestamp=1421762492834, value=Data mining
 001                                    column=subject:s3, timestamp=1421762437483, value=Operating system
002                                    column=name:firstname, timestamp=1421762485768, value=David Jackson
 002                                    column=name:lastname, timestamp=1421762494563, value=Samuel
 002                                    column=name:fullname, timestamp=1421762492345, value=David Jackson Samuel
002                                    column=subject:s1, timestamp=1421762487389, value=Computer Networks
 002                                    column=subject:s2, timestamp=1421762492834, value=R programming
 002                                    column=subject:s3, timestamp=1421762437483, value=Data Analytics
3 row(s) in 0.0230 seconds

To get a single row of data at a time, use the get command.
hbase(main):007:0> get 'student', '001'
COLUMN                                   CELL
name:firstname 	timestamp=1421762485768, value=Arunkumar
name:lastname 	timestamp=1421762482362, value=Gopu
name:fullname timestamp=1421762487287, value=Arunkumar Gopu
subject:s1 	timestamp=1421762485345, value=Data Analytics
subject:s2 	timestamp=1421762482367, value=Data mining
subject:s3 	timestamp=1421762488736, value=Operating system
6 row(s) in 0.0350 seconds

If you want to delete a table or change its settings, as well as in some other situations, you need to disable the table first, using the disable command. You can re-enable it using the enable command.
hbase(main):008:0> disable 'student'
0 row(s) in 1.1820 seconds

hbase(main):009:0> enable 'student'
0 row(s) in 0.1770 seconds

To drop (delete) a table, use the drop command.
hbase(main):011:0> drop 'student'
0 row(s) in 0.1370 seconds

To exit the HBase Shell and disconnect from your cluster, use the quit command. HBase is still running in the background.
hbase(main):008:0>quit
$stop-hbase.sh
stopping hbase....................
$stopCDH.s

*******************************************************************************************************************************************************************



Start the hive environment
hadoop@hadoop-laptop:~$ hive

Creating and deletion of databases and tables
hive> show databases;
OK
default
Time taken: 3.602 seconds

hive> create schema vrsec;
OK
Time taken: 0.082 seconds

hive> drop database if exists vrsec;
OK
Time taken: 0.838 seconds

hive> create database student;      
OK
Time taken: 0.024 seconds

Selecting a database and inserting rows into table
hive> use student;
OK
Time taken: 0.0070 seconds

hive> show tables;
OK
Time taken: 0.074 seconds

hive> create table marks(regno string, sub1 int, sub2 int, sub3 int);
OK
Time taken: 0.191 seconds

hive> describe marks;
OK
regno	string	
sub1	int	
sub2	int	
sub3	int	
Time taken: 0.139 seconds 

Altering the tables in database
hive> alter table marks rename to subjectmarks;
OK
Time taken: 0.349 seconds

hive> describe marks;                          
OK
Table marks does not exist	 	 
Time taken: 0.064 seconds

hive> describe subjectmarks;
OK
regno	string	
sub1	int	
sub2	int	
sub3	int	
Time taken: 0.079 seconds

hive> show tables;
OK
subjectmarks
Time taken: 0.061 seconds

hive> alter table subjectmarks add columns(sub4 int);
OK
Time taken: 0.087 seconds

hive> describe subjectmarks;                         
OK
regno	string	
sub1	int	
sub2	int	
sub3	int	
sub4	int	
Time taken: 0.069 seconds

hive> alter table subjectmarks replace columns(name string, total int);
OK
Time taken: 0.063 seconds

hive> describe subjectmarks;                                           
OK
name	string	
total	int	
Time taken: 0.051 seconds

Importing data from csv file to a table
hive> create table studentdetails(id string, name string, age int) row format delimited fields terminated by ',' stored as textfile;
OK
Time taken: 0.051 seconds

hive> show tables;
OK
studentdetails
subjectmarks
Time taken: 0.047 seconds

hadoop@hadoop-laptop:~/Desktop$ touch hivefile.txt
hadoop@hadoop-laptop:~/Desktop$ nano hivefile.txt
hadoop@hadoop-laptop:~/Desktop$ cat hivefile.txt
001,arun,30
002,siddhu,27
003,magilan,35
004,mark,39
hadoop@hadoop-laptop:~/Desktop$ hdfs dfs -put hivefile.txt /hivefile.txt

hive> load data inpath '/hivefile.txt' overwrite into table studentdetails;                    
Loading data to table student.studentdetails
rmr: DEPRECATED: Please use 'rm -r' instead.
Deleted /user/hive/warehouse/student.db/studentdetails
OK
Time taken: 0.235 seconds

Selecting, displaying the content stored in tables.
hive> select * from studentdetails;
OK
001	arun	30
002	siddhu	27
003	magilan	35
004	mark	39
Time taken: 0.162 seconds

hive> select * from studentdetails where id='001';
Total MapReduce jobs = 1
Launching Job 1 out of 1
Number of reduce tasks is set to 0 since there's no reduce operator
Starting Job = job_1613923031783_0001, Tracking URL = http://localhost:8088/proxy/application_1613923031783_0001/
Kill Command = /home/hadoop/Training/CDH4/hadoop-2.0.0-cdh4.0.0/bin/hadoop job  -Dmapred.job.tracker=localhost:10040 -kill job_1613923031783_0001
Hadoop job information for Stage-1: number of mappers: 1; number of reducers: 0
2021-02-21 11:08:28,236 Stage-1 map = 0%,  reduce = 0%
2021-02-21 11:08:32,474 Stage-1 map = 100%,  reduce = 0%, Cumulative CPU 0.53 sec
MapReduce Total cumulative CPU time: 530 msec
Ended Job = job_1613923031783_0001
MapReduce Jobs Launched: 
Job 0: Map: 1   Accumulative CPU: 0.53 sec   HDFS Read: 0 HDFS Write: 0 SUCESS
Total MapReduce CPU Time Spent: 530 msec
OK
001	arun	30
Time taken: 9.764 seconds

hive> select * from studentdetails sort by id;
Total MapReduce jobs = 1
Launching Job 1 out of 1
Number of reduce tasks not specified. Estimated from input data size: 1
In order to change the average load for a reducer (in bytes):
  set hive.exec.reducers.bytes.per.reducer=<number>
In order to limit the maximum number of reducers:
  set hive.exec.reducers.max=<number>
In order to set a constant number of reducers:
  set mapred.reduce.tasks=<number>
Starting Job = job_1613923031783_0002, Tracking URL = http://localhost:8088/proxy/application_1613923031783_0002/
Kill Command = /home/hadoop/Training/CDH4/hadoop-2.0.0-cdh4.0.0/bin/hadoop job  -Dmapred.job.tracker=localhost:10040 -kill job_1613923031783_0002
Hadoop job information for Stage-1: number of mappers: 1; number of reducers: 1
2021-02-21 11:08:46,430 Stage-1 map = 0%,  reduce = 0%
2021-02-21 11:08:50,622 Stage-1 map = 100%,  reduce = 0%, Cumulative CPU 0.64 sec
2021-02-21 11:08:51,659 Stage-1 map = 100%,  reduce = 0%, Cumulative CPU 0.64 sec
2021-02-21 11:08:52,713 Stage-1 map = 100%,  reduce = 100%, Cumulative CPU 1.62 sec
MapReduce Total cumulative CPU time: 1 seconds 620 msec
Ended Job = job_1613923031783_0002
MapReduce Jobs Launched: 
Job 0: Map: 1  Reduce: 1   Accumulative CPU: 1.62 sec   HDFS Read: 0 HDFS Write: 0 SUCESS
Total MapReduce CPU Time Spent: 1 seconds 620 msec
OK
001	arun	30
002	siddhu	27
003	magilan	35
004	mark	39
Time taken: 11.034 seconds

hive> select * from studentdetails order by name;
Total MapReduce jobs = 1
Launching Job 1 out of 1
Number of reduce tasks determined at compile time: 1
In order to change the average load for a reducer (in bytes):
  set hive.exec.reducers.bytes.per.reducer=<number>
In order to limit the maximum number of reducers:
  set hive.exec.reducers.max=<number>
In order to set a constant number of reducers:
  set mapred.reduce.tasks=<number>
Starting Job = job_1613923031783_0003, Tracking URL = http://localhost:8088/proxy/application_1613923031783_0003/
Kill Command = /home/hadoop/Training/CDH4/hadoop-2.0.0-cdh4.0.0/bin/hadoop job  -Dmapred.job.tracker=localhost:10040 -kill job_1613923031783_0003
Hadoop job information for Stage-1: number of mappers: 1; number of reducers: 1
2021-02-21 11:09:09,729 Stage-1 map = 0%,  reduce = 0%
2021-02-21 11:09:12,863 Stage-1 map = 100%,  reduce = 0%, Cumulative CPU 0.51 sec
2021-02-21 11:09:13,932 Stage-1 map = 100%,  reduce = 0%, Cumulative CPU 0.51 sec
2021-02-21 11:09:14,966 Stage-1 map = 100%,  reduce = 0%, Cumulative CPU 0.51 sec
2021-02-21 11:09:16,016 Stage-1 map = 100%,  reduce = 100%, Cumulative CPU 1.85 sec
MapReduce Total cumulative CPU time: 1 seconds 850 msec
Ended Job = job_1613923031783_0003
MapReduce Jobs Launched: 
Job 0: Map: 1  Reduce: 1   Accumulative CPU: 1.85 sec   HDFS Read: 0 HDFS Write: 0 SUCESS
Total MapReduce CPU Time Spent: 1 seconds 850 msec
OK
001	arun	30
003	magilan	35
004	mark	39
002	siddhu	27
Time taken: 11.05 seconds




