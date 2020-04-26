
### Study Notes on Course1

[Video-bilibili](https://www.bilibili.com/video/BV1Wz411b7sD?from=search&seid=1785395184520069316)

#### Course Topics

Focus on internals of single nodes in-memory database system.

Not distributed Systems.


### �����Ķ��ʼ�

��What's really new with NewSQL��

##### NoSQL

* ��ͳ��ϵģ����ǿ����֤��Լ�������ܺͿ���չ�ԣ��߿�����

* NoSQL�ĵ����˼����һ��������ǿ����֤��������������׷���������һ���ԡ�
��һ���棬������ͳ��ϵģ�ͣ��������ֵ�ԣ�ͼ�����ĵ�����ģ������֯���ݡ�

* ��Google��BigTable,�Լ�������������Hbase,Cassandra���ĵ������ݿ�MongoDB,
��ֵ�����ݿ�Redis

##### NewSQL

* NoSQL��ȱ�㣺��������Ҫ����������дcode���������ݲ�һ�µ����,�������з���
���Ǳ�֤�����Ի�ȽϺ�

* NewSQL�Ķ����ǣ�

1.���ֹ�ϵģʽ�����Ƕ�OLTP�ṩ��NoSQL��ͬ�Ŀ���չ����

2.��֤�����ACID����

˵���˾��Ǽ�Ҫ���ִ�ͳ��ϵģʽ��ͬʱ׷����NoSQLһ�������������չ�ԣ���������Ҳ����Ҫд�����code����֤����һ���ԡ�

�Ǿ���NewSQL DBMS��Ҫ����ʲô���ԣ�

1.��д������short-lived��

2.ÿ��ֻ����subset����,һ�������������ҳ�����������ȫ��ɨ����ߴ��ģ�ķֲ�ʽjoin

3.������ͬ��queryҪִ�ж�Σ�����ÿ�ε�input����ͬ

��Ϊnarrow��definition����

�ṩ�����Ĳ������Ʋ���

��Ҫ��shared nothing architecture


ʲô��**shared nothing architecture**��


ÿ���ڵ㶼�Ƕ����ġ����͵�SNAϵͳ�Ἧ�д洢״̬����Ϣ���磺���ݿ��У��ڴ�cache�У����ڽڵ��ϱ���״̬����Ϣ�� 
����server��Ⱥ������session��״̬�����ڸ����ڵ��ϣ���ô�����ڵ��session���ƻἫ���Ӱ�����ܣ�������SNA������ÿ���ڵ����״̬�ԣ�����ʹ��session������ȫ�ֵ�״̬�����ǽ�sessionֱ�ӷ������ݿ��У������ݿ�ǰ�ټ�һ��ֲ�ʽCache���Ƽ�ʹ��memcached��
���������ɼ����������ܣ����ı�session�еĶ���ʱ��ͬ����cache�����ݿ⡣

shared nothing��Ҫȷ��һ�ַ�Ƭ���ԣ�ʹ�����ݲ�ͬ�ķ�Ƭ���ԣ�������Դ������
���ֻ����ķ�Ƭ���Խṹ��

1) ���ܷ�Ƭ
���ݶ�����ܻ��಻�ص����ص���з�Ƭ�����ַ�ʽ��ebayȡ�þ޴�ɹ���ȱ������Ҫ�������Ӧ�����򣬲��ܸ��õط�Ƭ��

2) ��ֵ��Ƭ
���������ҵ�һ�����Ծ��ȷֲ���������Ƭ�еļ�ֵ��

3) ���
�ڼ�Ⱥ����һ���ڵ�䵱Ŀ¼��ɫ�����ڲ�ѯ�ĸ��ڵ�ӵ���û�Ҫ���ʵ����ݡ�ȱ�������������ܳ�Ϊ����ϵͳ��ƿ��������ʧЧ�㡣


Ȼ��������ϸ������NewSQL�����ܹ����ص�

#### New Architecture

All of the DBMSs in this category are based
on distributed architectures that operate on shared-nothing resources and contain components to support multi-node concurrency control, fault tolerance through replication, flow control, and distributed query processing.

* �ֲ�ʽSNA�ܹ�

* �ṩ�ֲ�ʽ���񣨶�ڵ㲢�����ƣ�

* ���ƻ�������֤�ݴ�

* ��������(flow control)

* �ֲ�ʽSQL executor


This means that the DBMS
is responsible for distributing the database across its resources
with a custom engine instead of relying on an off-the-shelf distributed filesystem (e.g., HDFS) or storage fabric (e.g., Apache
Ignite). 

* newSQL ��������Լ���storage�������������ⲿ�洢(HDFS)

* DBMS����send the query to the data��,������"send the data to the query"

* ��ô���ĺô��ǿ��Դ��������紫����(��һ�����л����query�ܱ�Ҫ��һ�����ݻ������������ﻯ��ͼҪǿ)

#### Transparent Sharding Middleware

NewSQL֮ǰͨ��sharding�����м������ɣ�����ÿ���ڵ㻹��Ҫʹ�ô�ͳ��DBMS��

��ЩDBMS�ǻ���**disk-oriented**�ļܹ���������ǲ��ܹ�Ӧ��һЩר�Ÿ�**memory-oriented**

��storage manager���߲������Ʋ��ԡ�

��һ���棬Ӧ�ô�ͳ��ϵDBMS��ʹ����չ�Ժ͸߿����Ժܲ��ΪҪ����һ���ԣ�����CAP���۵Ļ���Ҫ����A

��������NoSQL������һ����C����˿���չ�Ծͻ��ǿ

���ֲ�ʽSQLִ�����Ǹ���ϵͳ���ص㣬�������ݿ���ֱ�ӽ������ݶ�����ʹ���м������

#### Database-as-a-service

* ʹ�����������ƶ�VM�������ݿ⣬Ҳ����Ҫ���Լ�˽�е�Ӳ����maintan DBMS

* �����ṩ����Ҫά�����ݿ������(�绺��صĴ�С�������뱸��)

* �ͻ�ʹ�÷�ֻ��Ҫһ��URL�Ϳ�������DBMS��һ��dashboardӦ�ý���ʵʱ��غ�API���ٿ����ݿ⡣


������������������NewSQL DBMS��һЩ������

#### Main Memory Storage �����ڴ�Ĵ洢����

* ��ͳ��DBMS����disk-oriented���������

�ص��ǣ�

1.��Ҫ�洢���Կ�ΪѰַ������λ��HDD����SSD

2.ʹ���ڴ����ѴӴ��̶�ȡ�Ŀ黺������,������ĸ�����buffer

* NewSQL��main memory storage architecture

�����ڴ���Ż����Բ����ٿ��Ƕ����ݵĵȴ����Լ����ô���buffer pool�Ĺ���ͷǳ����صĲ�������ģʽ��

�ص���:

1.���ݶ��洢���ڴ���

�ڴ治����ô�죿

2.֧�ְ��ڴ��е�ĳЩ������������̭���־û���(����Ӳ��)

The general approach is to use an internal tracking mechanism inside of the system to identify which tuples
are not being accessed anymore and then chose them for eviction

�������Ҳ��"anti-caching"����ʵ���ǰѲ����ڴ�swap�����̣�������Ҫά��һ���ڴ�׷��ϵͳ

3.��һ�ֲ����ǣ���MemSQL������ʽ�洢��ʹ��LSM�洢������update�Ŀ���
�����ﲻ̫��

#### Partitioning/Sharding ���ڷ�����Ƭ��ˮƽ����չ��

NewSQLͨ����ͨ�������ͷ�Ƭ��ʵ����߿���չ�Եġ�

һ��ˮƽ������Ƭ�Ĺ���ԭ��

* The database��s tables are horizontally divided into multiple
  fragments whose boundaries are based on the values of one (or
  more) of the table��s columns 
  
* The DBMS assigns each tuple to a fragment based on the values of these attributes using either 
**range or hash partitioning**
  
* Related fragments from multiple tables are combined together
  to form a partition that is managed by a single node
  
* That node is responsible for executing any query that needs to access data
  stored in its partition
  
����������ݾ����ܷ���һ��shard�У���ô�Ϳ��Ծ�����query��ִ���·ŵ�һ���ڵ���,����Ҫ
2PC��ά���ֲ�ʽ�����ԭ����

����򵥽�����NuoDB��MemSQL�ļܹ�

* NuoDB

1.��һ�������ڵ��Ϊstorage managers(SM),ÿһ��SM
�洢��һ������

2.SM�����ݿ⻮�ֳ�һ����block,����atom

3.�����ڵ��Ϊtransaction engines(TE),��atom���ڴ澵��

4.�ṩload balance��������֤���ݹ̶��ֲ���ĳЩ�ڵ���

* MemSQL

�ۼ��ڵ㸺��ִ��

Ҷ�ӽڵ㸺��洢

* NewSQL�ķ�����֧������Ǩ�ƣ���������Ǩ�ƺ�rebalance


#### ��������

* �ṩԭ���Ժ͸����Եı�֤

* ��Ϊ���Ļ���ȥ���Ļ�����������ֻ���

* ���Ļ����������

���������������Ҫͨ������Э����������

��Э���������������Ƿ�ִ��

* ȥ���Ļ����������

ÿ���ڵ㶼��ά��һ������״̬����ͨ���������ڵ�ͨ�������������Ƿ��ͻ

����չ�ã�������Ҫǿͬ����ʱ��ϵͳ����������ȫ��˳������


Ϊ�β���2-phase Locking����������������⣿

�����󣬴����������ӡ�

NewSQL���õ�˼·��ʹ��MVCC��д����������������������

Ҳ�еĽ��MVCC+2PL

���������,�ٽ��������ʱ����Ȼ��Ҫ����2PL���������޸�ĳ���¼��ʱ��
����������¼��һ���°汾��

��ô��������ʱ����Ҫ�������ʹ�û���Time Order��MVCC��ȡ�汾����

Ҳ�����д������и��š�InnoDB������ô���ġ�


��ôʲô��2PL��

���׶εĺ�����ָ��ͬһ�������ڣ������漰����������������ȼ�����Ȼ��Ŷ����е����������

�ҵ�����ǣ������ͽ������ܴ������


�ܵ���˵��NewSQL�Ĳ������Ʋ�û��ʲô�µ�IDEA���ܴ�̶��϶��ǲ���ԭ����DBMS��2PL,MVCC


#### ��������

�ڷֲ�ʽDBMS��������Ҫ���ǵ���:

* ��ʲô�ط��洢�����������

* �����������ά��

��������Ļ���coordinator,�����������Դ洢��Э���߽ڵ����Ƭ�ڵ��ϡ�

���ַ����ĺô���������ϵͳ��ֻ��һ�����������İ汾������ά��

����NewSQL��ȥ���Ļ��Ĳ���ʹ�÷����Ķ�����������������ÿ���ڵ�ӵ��������һ���ֶ�������������

���ַ�ʽ�ڲ������ݵ�ʱ�����Ҫ���Ҷ���ڵ㣬���¾�ֻ����һ���ڵ�

���Ʒ�ʽ��ֻ����һ���ڵ㣬���µĻ����и�����Ҫ����

�ܽ᣺

��Ƭ�洢��������


#### ����

���ƻ��ƿ��ǵ���DBMS��α�֤�ڵ������һ����

��ǿһ���Ե�DBMS��,�����д�����ύ֮ǰ����Ҫ���нڵ㶼ͬ�⡣ͨ������2PC��һ������������Ĵ�
����������Ϊ����������ϳ�������

����NewSQL������ʹ����һ����(����һ����)ģ��,�����ύ����֮ǰ����Ҫ�������ݽڵ��ͬ��

* active-active����

���и��ƽڵ�ִ����ͬ��query�����Ǻ��ѱ�֤��ͬ�ڵ��ִ��˳�����ϸ�һ�µģ����ǵ������ӳ٣�ʱ�Ӳ�ͬ�������⡣

* active-passive����

NewSQLͨ�����õ��ǵڶ��֣�����д��Ȼ�����������״̬��

#### 崻��ָ�

���ڵ��DBMS崻��ָ�����ͨ���Ǽ��ش����ϵ�checkpointȻ������ָ��WAL�е�����ʹ��״̬�ָ���崻�֮ǰ��

���Ƿֲ�ʽDBMS���ܼ򵥲������ֲ��ԣ���Ϊmaster����֮���ӽڵ��ѡ�ٳ�һ���µ�master����ôԭmaster
�ָ���ʱ�򣬻���Ҫ��masterͬ�����µ�����(����崻��ڼ�����ϵͳ��������)

2 potential way:

1.�ָ��ڵ����ck��ִ��WAL��Ȼ���master�ڵ�pull崻��ڼ��log entries

ֱ��Ӧ����־�ĸ���ԶԶ������ִ��ԭ����SQLҪ��

2.ֱ�Ӵ�master�ڵ����������״̬�Ľڵ���checkpoint��ɾ���Լ�ԭ����checkpoint

����Ҳ��ϵͳ���¼���һ���ڵ������

ͨ��������zookeeper,Raft�������Լ�ʵ��Paxos

#### Future Trends

HTAP hybrid and transaction-analytical processing

read-time analytics 

ͬʱ��ʵʱ���ݺ���ʷ��������������

ʵ��HTAP�ļ���idea:

1.ʵ������DBMS

һ���������������(OLTP),һ��������(OLAP)

ǰ��OLTP DBMS�洢�������������

OLTP����������Ǩ����OLAP�������ӷ���������slow down OLTP�Ĵ�������

Ȼ��OLAP������������push��ǰ�˵�OLTP

2.Lambda �ܹ�

��������

��Hadoop,Spark��ִ�����������񣬴�����ʷ����

��Storm,Spark Streaming,Flink��������ʽ����

�����ַ�����ȱ�������ҪΪ��������ϵͳά����ͬ�Ĵ��룬����Ҫ�Ļ�������ϵͳ֮��
����Ǩ������һP

3.�����־�����һ��ͳһ��HTAP DBMS

ͬʱ֧�ָ����µ��ӳٵ�OLTP�͸��ӳ�ʱ�����е�OLAP

�����OLTP��OLAPһЩ�Ƚ��µļ�����

OLTP:in-memory storage,lock-free execution

OLAP:���л��

�Ƚϵ��͵Ĳ�Ʒ��SAP HANA��Mem SQL

HANA achieves this
by using multiple execution engines internally: one engine for
row-oriented data that is better for transactions and a different
engine for column-oriented data that is better for analytical
queries


### In summary

NewSQL DBMS are relational DBMS combined with 
OLAP,high scalability and high performance.

* Main memory storage engine

* Secondary Indexes

* Replication

* Concurrency control

* Crash Recovery

* Partitioning/Sharding


### ref

https://www.dazhuanlan.com/2019/10/16/5da61be779020/