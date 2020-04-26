### Lec-02 In-memory Databases

[video](https://www.bilibili.com/video/BV1Y7411o7GN?p=2)

### Disk-oriented DBMS(������̵����ݿ�)

#### Buffer Pool Issue

- ������Ҫ���ڷ���ʧ�Դ洢��(HDD,SSD),��Page or FrameΪ��λ���洢
- ʹ�����ڴ��еĻ����(Buffer Pool)���������Դ��̵�page
- ������ѯ���̣�

1.�����ݿ������в��Ҷ�Ӧ��¼��Page Id��slot (��������Ľڵ�û�м��ص��ڴ��У���Ҫ�Ӵ����м���)

2.ȥҳ���в�ѯ��Page�Ƿ��Ѿ����ص��ڴ�

3.���û�еĻ����Ӵ������ҵ���ҳ�����Ҹ��Ƶ�����ص�һ֡��(frame)

4.��������û�пյ�frame����һ���滻ԭ��evictĳҳ(LRU,FIFO,CLOCK)�����һ�Ҫ����page table

5.���page��dirty�ļ����޸Ĺ�������Ҫ�Ѷ�Ӧ�޸ĺ������д�ش�����

- ���ּܹ��Ļ�����

Every tuple access has to go through the buffer pool manager regardless of whether that data will
always be in memory.

���۲�ѯԪ���Ƿ����ڴ��ж���Ҫȥbuffer pool�в���

#### Concurrency Control Issue

������̵����ݿ�ٶ��ڳ��Է���û�м��ص��ڴ�����ݵ�ʱ������ᡰstall��

��ȻϵͳΪ��������ܻ�����һ������stall��ʱ��ͬʱִ���������񣬿�������ʵ��ACID��

���洢��in-memory��һ��hash-table����lock manager,���������ݱ�swap��������

**All the info about lock is in memory!**

#### Logging & Recovery Issue

- �����ύǰ�����޸�д��Write-ahead-log(WAL)��WAL����undo log �� redo log
- ÿһ��log entry���������޸�ǰ�����ݵľ���
- The DBMS flushes WAL pages to disk separately from corresponding modified database pages, so it takes extra
  work to keep track of what log record is responsible for what page

�������ύ֮ǰ��WAL��Ҫ��flush��������

��Ҫά��log record�Ǹ�����һ��page����Ϣ������LSM log sequence number��

#### �����Ƚ�

���������disk flushing,����������ݿ⿪����Ҫ�����ڣ�

BUFFER POOL 34%

LATCHING 14% (��������߳�,��֤�����̲߳����ٽ���Դ����ȷ��)

LOCKING 16% (�����������һ����ס�������ݿ�ı���)

LOGGING 12% 

B-TREE KEYS 16% ��������ʱ��

CPU 7% 

### In-memory DBMS

������DRAM�ķ�չ���۸���������԰��������ݿ�����ݶ��洢���ڴ���

��ʱ�����IO���������ݿ����ܵ�ƿ��,����Ҫ�������¿����Ż�������ƿ��

- Locking/Latching
- Cache-line misses
- Pointer chasing
- Predicate evaluation
- Data movement and copying
- Networking 

��Ϊ�������ݶ���memory����˲��������ҳ��Ҳ����Ҫά��undo log��Ϣ��Ҳ����ҪLSN����



������һ��������������ݿ��һЩ��ͬ

- Data Organization

1.��Index�в�������ָ�����ڵ�Block Id��Offset

2.����block id��offset�ҵ�����ָ����ڴ��ַ,ָ��洢��Fixed-Length Data Blocks

3.�������64-bitsָ��ȥVariable-Length Data BlocksȥѰ������������

![1587904937780](C:\Users\AlexanderChiu\AppData\Roaming\Typora\typora-user-images\1587904937780.png)



- Indexes

In-memory DBMS�������¼�����ĸ��£���������ʱ�򣬵��������ݼ��ص��ڴ�֮��ֱ�����ڴ����ؽ����������

- Query Processing

�������ݶ����ڴ��У�������ʵ��ٶȲ�����˳�����Ҫ��

- Logging & Revocery

1.��Ȼ��Ҫά��WAL�����޸����ݿ�֮ǰ,���޸ļ�¼д��WALȻ��ͬ�����ڴ���

2.ʹ�����ύ���ύWAL����̯fsyncϵͳ���õĿ���

3.Ҳ����ʹ�ø���������logging���ԣ�ֻ�洢redo��Ϣ

- Concurrency control�����ṩԭ�����������

��������̵����ݿ��У����Ǵ��������һ���ڴ��е�hash�������ݼ�¼�����Ƿֿ����洢�ġ���Ϊ��¼�ǿ��ܱ�swap����档

����IMDB�У��������ݼ�¼һֱ���ڴ��У�����swap����棬��˿��԰Ѽ�¼�йص�������Ϣ���¼һ�𱣴档

���Գ���ȡ����Ч��=���Ի�����ݵ�Ч��

ƿ�����ڣ��������ͬʱ���Է���ĳ�����ݣ�ֻ��һ��������������

�����mutexʵ�ֵĻ�����̫����������CAS����֤�����ͬ��

#### CAS

```
__sync_bool_compare_and_swap(&M, 20, 30);
```

���ҽ���M��ַ�����ֵ����20��ʱ�򣬰�M��ַ���ڵ�ֵ��Ϊ30.

����ʧ�ܣ���Ϊ�����ڵĻ�˵�����ֵ�϶�������߳��޸���



�������Ļ���ϸ���۲������Ƶ�һЩ���ԣ�

- ���۲��ԡ���2 PHASE LOCKING

��������֮ǰһ����������

2PL����������ֲ��ԣ�

1.����̽��

ά��һ�����У����д����������������һ����̨�߳�������ɨ������е����񣬿���Щ����

�����У���Щstall����Ϳ����ҵ���������������

2.����Ԥ��

�ڷ�����֮ǰ����û�����������Ѿ��õ�������������������ò�����

1���ȴ�

2����ɱ

3��ɱ������һ������������

- �ֹ۲��ԡ���ʱ�������

�������ݲ������������ύ��ʱ��Ƚ�ʱ���

#### Basic T/O Protocol

ÿһ�����񶼻����һ��ʱ�����ÿһ����¼��ͷ��ά����һ�����������ʱ�����Ȼ�������ʱ������в�����ʱ�򣬱Ƚ����������ʱ������¼ͷ����ǰ��ʱ�����

#### �ֹ۲�������

```
1. Read Phase: Transaction��s copy tuples accessed to private work space to ensure repeatable reads, and
keep track of read/write sets.

2. Validation Phase: When the transaction invokes COMMIT, the DBMS checks if it conflicts with other
transactions. Parallel validation means that each transaction must check the read/write set of other
transactions that are trying to validate at the same time. Each transaction has to acquire locks for its
write set records in some global order. Original OCC uses serial validation.
The DBMS can proceed with the validation in two directions:
? Backward Validation: Check whether the committing transaction intersects its read/write sets
with those of any transactions that have already committed.
? Forward Validation: Check whether the committing transaction intersects its read/write sets with
any active transactions that have not yet committed.

3. Write Phase: The DBMS propagates the changes in the transactions write set to the database and
makes them visible to other transactions�� items. As each record is updated, the transaction releases
the lock acquired during the Validation Phase
```

������Բο�slides�Ĺ���

#### ʱ����ķ������

- ���ڻ��������������ܵ�
- ԭ�ӼӲ���:   CAS����ȥά��һ��ȫ�ּ�����
- ����ԭ�ӼӲ���
- Ӳ��CLOCK:  Intel CPU only
- Ӳ��������: ��δ��Ӳ��ʵ��



#### �������Ƶ�����ƿ��

- Lock Thrashing

������

Each transaction waits longer to acquire locks, causing other transaction to wait longer to acquire
locks.

Can measure this phenomenon by removing deadlock detection/prevention overhead. 

solution�� force txns to acquire locks in primary key order

- Memory Allocation

�ڴ����

Copying data on every read/write access slows down the DBMS because of contention on the memory
controller.

Default libc malloc is slow. Never use it 

- Timestamp Allocation

ʱ�������

