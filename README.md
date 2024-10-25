
企业一旦发展到了一定规模，就会衍生软件100%合规正版化的需求。
![FM-DBO](https://img2023.cnblogs.com/blog/635610/202410/635610-20241024221425449-1520847348.jpg)
而对于使用到Oracle的用户，当然，具体核定的购买数量和off等商务问题，需要客户管理层直接和对应的Oracle销售代表进行商务谈判。


理想情况下，一旦用户面临这个场景，就需要安排自己的技术负责人提前梳理清楚公司目前到底都用了哪些付费选件和管理包，并清楚Oracle计算价格的规则。


因为Oracle是Paper license，很多中小客户早期很可能都没这个意识，所以一旦在某个重要节点被提出来合规要求，都显得有些手足无措，尤其对Oracle一系列复杂的细分产品选件细节定义顿感头痛。


有些客户也会选择邀请我们专门给他们培训解释这些规则。为了让更多有需求的客户能在未来正式的商务谈判中不至于太被动，优雅地达成合规正版化。


这里介绍下如何下功夫先自行梳理一番，做到自己心中有数。


好在这些产品定义信息并不是秘密，规则也都是公开透明的，甚至连列表价都是公网可查的：


# Oracle Technology Global Price List


目前能查到的最新版本，发布时间是June 13, 2024，在公网也能直接搜索到。这里贴出最普遍的Oracle数据库部分来举例说明：


![](https://img2023.cnblogs.com/blog/635610/202410/635610-20241024221425432-1909357389.jpg)


细节在官方文档有非常清晰的描述，比如Oracle数据库的所有license细节都可以在这篇文档中找到依据：


# Database Licensing Information User Manual


* [https://docs.oracle.com/en/database/oracle/oracle\-database/23/dblic/Licensing\-Information.html](https://github.com)


本文挑重点部分聊下，通常有哪些困惑和常见的误解。


* 1\.Partitioning是指分区？分区还收费？
* 2\.RAT是指啥？咋小老鼠还收费呐？
* 3\.ADG中链路压缩还需要高级压缩选件？
* 4\.高级安全都有啥？
* 5\.In\-Memory的免费使用条件？
* 6\.Diagnostic Pack是必选项？
* 7\.Tuning Pack能不用吗？
* 彩蛋1：Oracle产品是都按照Core收费吗？
* 彩蛋2：警惕那些看起来人畜无害的小参数！


## 1\.Partitioning是指分区？分区还收费？


是的，就是针对表或索引的各种分区，都是算Partitioning这个选件中的。
很多用户会很容易认同RAC、ADG这种看着就很大的功能，作为Option还很好理解，而误以为分区是数据库内部很基础的功能，应该归属于DBEE的功能中，但实际上，它也是在DBEE之外，作为一个独立的付费Option。


参考官方文档内容：



```
These are some of the features that make use of Oracle Partitioning:

Table Partitions and Subpartitions

Global and Local Index Partitions and Subpartitions

Transactional Event Queues (TxEventQ)

Zone Maps and Automatic Zone Maps (Available only on EE-ES and ExaDB; requires Exadata or Supercluster)

```

## 2\.RAT是指啥？咋小老鼠还收费呐？


谈到RAC基本人尽皆知，但说到RAT可能还真不能算耳熟能详，他当然不是小老鼠，而是Real Application Testing的缩写。
可能大家直观感觉连听都没听过，那自己肯定也不会使用到，但实际上，如果讲到RAT中的SPA，基本做过稍微正式点的系统升级迁移项目，都会用到SPA工具来评估迁移前后不同环境下的性能情况，做到心中有数。
当然，RAT中还有个重磅的DB Replay的功能，但是在使用上要复杂些，常规项目中实际用的的确很少。


参考官方文档内容：



```
The full functionality of Oracle Real Application Testing is available only on Oracle Database 11g Release 1 or higher. Partial functionality of Oracle Real Application Testing is available to customers wishing to upgrade from Oracle9i Database Release 2 or Oracle Database 10g.

The functionality available on Oracle9i Database Release 2 is as follows:

Database Replay: Only the Workload Capture feature is supported, and the captured workload may only be replayed only on Oracle Database 11g. This feature can be used only to facilitate upgrades from Oracle 9i Database Release 2 to Oracle Database 11g or higher.

The functionality available on Oracle Database 10g Release 2 is as follows:

Database Replay: Only the Workload Capture feature is supported, and the captured workload may be replayed only on Oracle Database 11g. This feature can be used only to facilitate upgrades from Oracle Database 10g Release 2 to Oracle Database 11g.

SQL Performance Analyzer: Only the Remote SQL Test Execute and SQL Capture into SQL Tuning Set features are supported. These features can be used only to facilitate upgrades from Oracle9i Database Release 2 and Oracle Database 10g Release 1 to Oracle Database 10g Release 2 or higher. When upgrading to Oracle Database 10g Release 2 from earlier releases (Oracle 9i Database or Oracle Database 10g Release 1), Oracle Database 11g is needed to remotely execute SQL on the target database (that is, Oracle Database 10g Release 2). Oracle Real Application Testing licensing is required for both systems, Oracle Database 10g Release 2 and Oracle Database 11g.

```

## 3\.ADG中链路压缩还需要高级压缩选件？


是的，高级压缩不仅针对表或索引的高级压缩，就是做RMAN备份用到高级压缩也算，甚至，你配置的ADG的链路如果开启了压缩选项，也都是算在高级压缩这个Option中的。
很多客户不能理解这点，尤其是已经购买了ADG的用户，很多会认为对ADG链路的一个压缩选项，就一个参数控制，理应包含在ADG之中。但实际上并不是这样，具体在官方文档中有明确的说明 \- Data Guard Redo Transport Compression。


参考官方文档内容：



```
Oracle Advanced Compression includes the following features:

Advanced Row Compression

Advanced LOB Compression

Advanced LOB Deduplication

RMAN Backup Compression (RMAN DEFAULT COMPRESS does not require the Oracle Advanced Compression option)

Data Pump Export Data Compression (COMPRESSION=METADATA_ONLY does not require the Oracle Advanced Compression option)

Automatic Data Optimization (Not available with Oracle Database Free)

Data Guard Redo Transport Compression

Advanced Network Compression

Optimization for Flashback Time Travel History Tables (Not available with Oracle Database Free)

Storage Snapshot Optimization (Not available with Oracle Database Free)

Online Move Partition (to any compressed format)

Exadata Flash Cache Compression (This feature can be enabled only on Exadata storage servers, and all database processors that access the Exadata storage servers must be licensed for Oracle Advanced Compression.)

Advanced Index Compression

Row-Level Locking for Hybrid Columnar Compression (Requires Exadata, Supercluster, Oracle Database Appliance, ZFS, or FS1 storage)

Note: The use of Hybrid Columnar Compression without Row-Level Locking does not require a license for Oracle Advanced Compression.

```

## 4\.高级安全都有啥？


像TDE这种透明加密的功能，算在高级安全中比较容易理解。
其他的功能用到高级安全选件的还有针对RMAN、DataPump导出文件的加密、Data Redaction等功能。


参考官方文档内容：



```
Oracle Advanced Security includes the following features:

Transparent Data Encryption (TDE) for columns and tablespaces (including Oracle SecureFiles)

DataPump Export File encryption

RMAN backup encryption to disk

Encrypted Database File System (DBFS)

Data Redaction of sensitive data returned to applications (Full, Partial, Regular Expression, and Random techniques)

Oracle Advanced Security includes a restricted use license for certain Oracle Enterprise Manager features. Refer to Oracle Advanced Security in "Restricted Use Licenses" for more information.

Note: Network encryption (native network encryption, network data integrity, and SSL/TLS) and strong authentication services (Kerberos, PKI, and RADIUS) are no longer part of Oracle Advanced Security and are available in all licensed editions of all supported releases of Oracle Database.

```

## 5\.In\-Memory的免费使用条件？


这个Option，为了推广使用，在19c特定版本下，可以享受到16GB免费使用的情况，但是有一定功能上的限制，而且一旦超过就需要付费。


参考官方文档内容：



```
Allows you to experiment with Oracle Database In-Memory features without purchasing the Oracle Database In-Memory option. The following restrictions apply:

The size of the In-Memory area (INMEMORY_SIZE) cannot exceed 16 GB for a CDB. In an Oracle RAC environment, the size is limited to 16 GB for each instance.
The compression level for all objects and columns is automatically and transparently set to QUERY LOW.
The Automatic In-Memory feature is disabled.
In-Memory Column Store feature tracking is tracked for "In-Memory Base Level" rather than "In-Memory Column Store."
The CellMemory feature is disabled for Oracle Exadata.
CLOUD: Only available in OCI

```

## 6\.Diagnostic Pack是必选项？


这个其实基本每个Oracle用户都会使用，而且默认也是开启的。比如常用的AWR、ADDM 和 ASH 工具，减少手动排查时间并提高系统稳定性，对于诊断数据库问题来说必不可少。


很多用户会误以为这个管理包在Database Enterprise Management下，而自己并没有使用EM，是不是就不用购买呢？实际上，跟是否使用EM无关，即便你是使用命令行调用，这点在文档中也有明确的说明：


参考官方文档内容：



```
Oracle Diagnostics Pack includes the following features:

Performance monitoring and diagnostics (database and host)

Automatic Workload Repository (AWR)

AWR Warehouse

Automatic Database Diagnostic Monitor (ADDM)

Compare Period ADDM

Real Time ADDM

ADDM Spotlight

Active Session History (ASH)

ASH analytics

Performance Hub

Top Activity Lite

Exadata Cell Grid Administration

Exadata Cell Grid Performance

Exadata Cell Group Health Overview page

Exadata Resource Utilization

Blackouts

Notifications

Metric and Alert/Event history

User-Defined Metrics and Metric Extensions

Management Connectors

Dynamic metric baselines and Adaptive metric thresholds

Monitoring templates and Template Collections

Replay Compare Period Report

Supporting functionality to perform per stream bottleneck detection and per component top wait event analysis

In order to use the features listed above, you must purchase licenses for Oracle Diagnostics Pack. A new initialization parameter, CONTROL_MANAGEMENT_PACK_ACCESS, controls access to Oracle Diagnostics Pack and Oracle Tuning Pack. This parameter can be set to one of three values:

DIAGNOSTIC+TUNING: Oracle Diagnostics Pack and Oracle Tuning Pack functionally is enabled in the database server.

DIAGNOSTIC: Only Oracle Diagnostics Pack functionality is enabled in the server.

NONE: Oracle Diagnostics Pack and Oracle Tuning Pack functionally is disabled in the database server.

Any and all methods of accessing Oracle Diagnostics Pack functionality, whether through Enterprise Manager Console, Desktop Widgets, command-line APIs, or direct access to the underlying data, requires an Oracle Diagnostics Pack license.

```

## 7\.Tuning Pack能不用吗？


这个其实也基本上每个Oracle用户都会使用到，而且要买它，文档有明确说，需要同时购买Diagnostic Pack才行。
所以，基本上，这两个都是成对购买的。


很多客户说我不用SQL Tuning Advisor这种工具，但是像SQL Profiles这种很难规避不使用，因为你总会遇到需要稳固SQL执行计划的场景。建议选用，确保后期使用无忧。


参考官方文档内容：



```
Oracle Tuning Pack includes the following features:

SQL Access Advisor

SQL Tuning Advisor

Oracle Database In-Memory Advisor

Automatic SQL Tuning

SQL Profiles

Real-time SQL and PL/SQL Monitoring

Real-time Database Operations Monitoring

Reorganize objects

A new initialization parameter, CONTROL_MANAGEMENT_PACK_ACCESS, is introduced to control access to Oracle Diagnostics Pack and Oracle Tuning Pack in the database server. This parameter can be set to one of three values:

DIAGNOSTIC+TUNING: Oracle Diagnostics Pack and Oracle Tuning Pack functionally is enabled in the database server.

DIAGNOSTIC: Only Oracle Diagnostics Pack functionality is enabled in the server.

NONE: Oracle Diagnostics Pack and Oracle Tuning Pack functionally is disabled in the database server.

Any and all methods of accessing Oracle Tuning Pack functionality, whether through Enterprise Manager Console, Desktop Widgets, command-line APIs, or direct access to the underlying data, requires an Oracle Tuning Pack license.

Prerequisites:

Oracle Tuning Pack requires Oracle Diagnostics Pack.

```

关于Option和管理包的基本常见误解就这些，最后再给大家来个彩蛋吧。


## 彩蛋1：Oracle产品是都按照Core收费吗？


很多人都“知道”Oracle产品都是按"Cores"收费的（这里暂不考虑极少数的NUP购买方式），简单说的确是这样。
但实际上看到列表价是写的"Processor"，这个"Processor"到底理解为啥是有很多种误解的，主流误解如下：


### 误解1: Processor就是Core的数量


这个误解实际上是最接近真相的，但实际并不是真相。
你想，如果Processor就是Core，那干嘛不直接叫Core？


### 误解2: Processor就是超线程后的数量


这个流传非常广泛，早些年笔者也被这种传言洗脑，信以为真。


后来得知真相后，推测这个流传的事实依据，很可能是因为像Linux这种主流操作系统，在针对物理Core超线程之后，在系统中显示的每个lcpu就是Processor这个词，所以巧合的对应上了Oracle list price的这个词。


再加上，江湖中总是有很多人，出于各种目的，大肆宣传Oracle价格有多么的“贵”，这样的解释可以充分论证“贵”的事实。


### 误解3: Processor就是CPU物理个数


这个就不好评论了，如果按CPU物理个数，再加上off，那就真的没其他数据库什么事情了。。
而且这样计价，Oracle会泛滥成那种传统烟囱式的建设，一个系统搞一套。


那么，正解究竟又是如何呢？
其实这里针对不同平台，有个Factor的概念。


### 正解：Processor是依据core的数量 \* Factor算出来的


为啥叫Processor，因为是想对某些平台更实惠，比如像Oracle Exadata使用的X86架构，可以有个0\.5的Factor，也就是说，假设你的机器共有2颗CPU，每棵CPU上有24个Cores，那么总共就是48个Cores，因为是X86架构可以乘以0\.5的Factor，就是只需要购买24个Processor。
而针对比较强悍的大机、小机之类，那么Factor就是1，就是同样48Cores的机器，就需要购买48个Processor。


## 彩蛋2：警惕那些看起来人畜无害的小参数！


有些参数看似很小，但修改它也可能需要用到某些付费选件或管理包，比如最让人觉得不可思议的ENABLE\_DDL\_LOGGING这个参数，默认值是FALSE，但见过太多客户都会将其设置为TRUE，这是因为很多第三方最佳实践中会推荐设置，方便在alert日志实时看到DDL操作提升可观测性，可是没想到吧？启用这个小小的参数，也会使用到Oracle Database Lifecycle Management Pack for Oracle Database这个收费的管理包。


参考官方文档内容：



```
The init.ora parameter ENABLE_DDL_LOGGING is licensed as part of Oracle Database Lifecycle Management Pack for Oracle Database when set to TRUE. When set to TRUE, the database reports schema changes in real time into the database alert log under the message group schema_ddl. The default setting is FALSE.

```

所以，如果您所在的企业是非常重视合规的，一定要搞清楚当前买了哪些收费选件，切记不要轻易修改任何数据库配置，哪怕只是一个简单的参数，如果数据库是第三方负责运维，要做好这方面的审计工作。
如果不确认，可以提交SR给官方做确认，因为这些看似微小的操作，也是极可能会触发用到什么收费的功能选件。


 本博客参考[西部世界官网](https://tianchuang88.com)。转载请注明出处！
