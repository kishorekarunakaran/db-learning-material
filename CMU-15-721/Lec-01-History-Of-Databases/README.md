
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








### ref

https://www.dazhuanlan.com/2019/10/16/5da61be779020/