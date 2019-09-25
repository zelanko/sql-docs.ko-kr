---
title: Hadoop의 외부 데이터에 액세스하도록 PolyBase 구성 | Microsoft Docs
description: 외부 Hadoop에 연결 하도록 병렬 데이터 웨어하우스에서 PolyBase를 구성 하는 방법을 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ceaa1cbe04148443dd7a60b8d2b7936dc0a2cf55
ms.sourcegitcommit: 853c2c2768caaa368dce72b4a5e6c465cc6346cf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71227132"
---
# <a name="configure-polybase-to-access-external-data-in-hadoop"></a>Hadoop의 외부 데이터에 액세스하도록 PolyBase 구성

이 문서에서는 APS 어플라이언스에서 PolyBase를 사용 하 여 Hadoop의 외부 데이터를 쿼리 하는 방법을 설명 합니다.

## <a name="prerequisites"></a>사전 요구 사항

PolyBase는 HDP(Hortonworks Data Platform) 및 CDH(Cloudera Distributed Hadoop)의 두 가지 Hadoop 공급자를 지원합니다. Hadoop은 새 릴리스의 "Major.Minor.Version" 패턴을 따르며, 지원되는 주/부 릴리스 내의 모든 버전이 지원됩니다. 다음 Hadoop 공급자가 지원됩니다.
 - Linux/Windows Server에서 Hortonworks HDP 1.3  
 - Linux에서 Hortonworks HDP 2.1-2.6
 - Linux에서 Hortonworks HDP 3.0-3.1
 - Windows Server에서 Hortonworks HDP 2.1 - 2.3  
 - Linux에서 Cloudera CDH 4.3  
 - Linux에서 Cloudera CDH 5.1-5.5, 5.9-5.13, 5.15 & 5.16

### <a name="configure-hadoop-connectivity"></a>Hadoop 연결 구성

먼저 특정 Hadoop 공급자를 사용 하도록 AP를 구성 합니다.

1. ‘hadoop connectivity’를 사용하여 [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 실행하고 사용 중인 공급자에 적합한 값을 설정합니다. 공급자의 값을 찾으려면 [PolyBase 연결 구성](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)을 참조하세요. 

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 and 3.0 - 3.1 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. [어플라이언스 Configuration Manager](launch-the-configuration-manager.md)의 서비스 상태 페이지를 사용 하 여 APS 영역을 다시 시작 합니다.
  
## <a id="pushdown"></a> 푸시다운 계산 사용  

쿼리 성능을 향상하려면 Hadoop 클러스터에 대한 푸시다운 계산을 사용하도록 설정합니다.  
  
1. PDW 제어 노드에 대 한 원격 데스크톱 연결을 엽니다.

2. 컨트롤 노드에서 **yarn-site.xml** 파일을 찾습니다. 일반적인 경로는 다음과 같습니다.  

   ```xml  
   C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf\  
   ```  

3. Hadoop 컴퓨터의 Hadoop 구성 디렉터리에서 동일한 파일을 찾습니다. 이 파일에서 구성 키 yarn.application.classpath의 값을 찾아서 복사합니다.  
  
4. Control 노드의 yarn 파일에서 **yarn** 속성을 찾습니다. **이 파일** 은 Hadoop 컴퓨터의 값을 value 요소에 붙여넣습니다.  
  
5. 모든 CDH 5.X 버전에서 mapreduce.application.classpath 구성 매개 변수를 yarn.site.xml 파일의 끝이나 mapred-site.xml 파일에 추가해야 합니다. HortonWorks는 yarn.application.classpath 구성 내에 이러한 구성을 포함하고 있습니다. 예제는 [PolyBase 구성](../relational-databases/polybase/polybase-configuration.md)을 참조하세요.

## <a name="example-xml-files-for-cdh-5x-cluster-default-values"></a>CDH 5.x 클러스터 기본값에 대 한 예제 XML 파일

yarn.application.classpath 및 mapreduce.application.classpath 구성이 포함된 Yarn-site.xml입니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
   <property>
      <name>yarn.resourcemanager.connect.max-wait.ms</name>
      <value>40000</value>
   </property>
   <property>
      <name>yarn.resourcemanager.connect.retry-interval.ms</name>
      <value>30000</value>
   </property>
<!-- Applications' Configuration-->
   <property>
     <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
      <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
      <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
      <name>yarn.application.classpath</name>
      <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/,$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH*</value>
   </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
   <property>
      <name>yarn.resourcemanager.principal</name>
      <value></value>
   </property>
-->
</configuration>
```

두 구성 설정을 mapred-site.xml 및 yarn-site.xml로 분할 하도록 선택 하는 경우 파일은 다음과 같습니다.

**yarn-site.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
   <property>
      <name>yarn.resourcemanager.connect.max-wait.ms</name>
      <value>40000</value>
   </property>
   <property>
      <name>yarn.resourcemanager.connect.retry-interval.ms</name>
      <value>30000</value>
   </property>
<!-- Applications' Configuration-->
   <property>
     <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
      <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
      <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
      <name>yarn.application.classpath</name>
      <value>$HADOOP_CLIENT_CONF_DIR,$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/*,$HADOOP_COMMON_HOME/lib/*,$HADOOP_HDFS_HOME/*,$HADOOP_HDFS_HOME/lib/*,$HADOOP_YARN_HOME/*,$HADOOP_YARN_HOME/lib/*</value>
   </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
   <property>
      <name>yarn.resourcemanager.principal</name>
      <value></value>
   </property>
-->
</configuration>
```

**mapred-site.xml**

mapreduce.application.classpath 속성이 추가되었습니다. CDH 5.x에서 Ambari의 동일한 명명 규칙에 따라 구성 값을 찾을 수 있습니다.

```xml
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
<configuration xmlns:xi="http://www.w3.org/2001/XInclude">
   <property>
     <name>mapred.min.split.size</name>
       <value>1073741824</value>
   </property>
   <property>
     <name>mapreduce.app-submission.cross-platform</name>
     <value>true</value>
   </property>
<property>
     <name>mapreduce.application.classpath</name>
     <value>$HADOOP_MAPRED_HOME/*,$HADOOP_MAPRED_HOME/lib/*,$MR2_CLASSPATH</value>
   </property>


<!--kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
   <property>
     <name>mapreduce.jobhistory.principal</name>
     <value></value>
   </property>
   <property>
     <name>mapreduce.jobhistory.address</name>
     <value></value>
   </property>
-->
</configuration>
```

## <a name="example-xml-files-for-hdp-3x-cluster-default-values"></a>HDP 1.x 클러스터 기본값에 대 한 예제 XML 파일

**yarn-site.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<!-- Put site-specific property overrides in this file. -->
 <configuration>
  <property>
     <name>yarn.resourcemanager.connect.max-wait.ms</name>
     <value>40000</value>
  </property>
  <property>
     <name>yarn.resourcemanager.connect.retry-interval.ms</name>
     <value>30000</value>
  </property>
<!-- Applications' Configuration-->
  <property>
    <description>CLASSPATH for YARN applications. A comma-separated list of CLASSPATH entries</description>
     <!-- Please set this value to the correct yarn.application.classpath that matches your server side configuration -->
     <!-- For example: $HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$HADOOP_YARN_HOME/share/hadoop/yarn/*,$HADOOP_YARN_HOME/share/hadoop/yarn/lib/* -->
     <name>yarn.application.classpath</name>
     <value>$HADOOP_CONF_DIR,/usr/hdp/3.1.0.0-78/hadoop/*,/usr/hdp/3.1.0.0-78/hadoop/lib/*,/usr/hdp/current/hadoop-hdfs-client/*,/usr/hdp/current/hadoop-hdfs-client/lib/*,/usr/hdp/current/hadoop-yarn-client/*,/usr/hdp/current/hadoop-yarn-client/lib/*,/usr/hdp/3.1.0.0-78/hadoop-mapreduce/*,/usr/hdp/3.1.0.0-78/hadoop-yarn/*,/usr/hdp/3.1.0.0-78/hadoop-yarn/lib/*,/usr/hdp/3.1.0.0-78/hadoop-mapreduce/lib/*,/usr/hdp/share/hadoop/common/*,/usr/hdp/share/hadoop/common/lib/*,/usr/hdp/share/hadoop/tools/lib/*</value>
  </property>

<!-- kerberos security information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG
  <property>
     <name>yarn.resourcemanager.principal</name>
     <value></value>
  </property>
-->
</configuration>
```

## <a name="configure-an-external-table"></a>외부 테이블 구성

Hadoop 데이터 원본에서 데이터를 쿼리하려면 Transact-SQL 쿼리에 사용할 외부 테이블을 정의해야 합니다. 다음 단계에서는 외부 테이블을 구성하는 방법을 설명합니다.

1. 데이터베이스에 마스터 키를 만듭니다. 자격 증명 암호를 암호화 해야 합니다.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

2. Kerberos 보안 Hadoop 클러스터의 데이터베이스 범위 자격 증명을 만듭니다.

   ```sql
   -- IDENTITY: the Kerberos user name.  
   -- SECRET: the Kerberos password  
   CREATE DATABASE SCOPED CREDENTIAL HadoopUser1
   WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
   ```

3. [CREATE EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md)를 사용하여 외부 데이터 원본을 만듭니다.

   ```sql
   -- LOCATION (Required) : Hadoop Name Node IP address and port.  
   -- RESOURCE MANAGER LOCATION (Optional): Hadoop Resource Manager location to enable pushdown computation.  
   -- CREDENTIAL (Optional):  the database scoped credential, created above.  
   CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (  
         TYPE = HADOOP,
         LOCATION ='hdfs://10.xxx.xx.xxx:xxxx',
         RESOURCE_MANAGER_LOCATION = '10.xxx.xx.xxx:xxxx',
         CREDENTIAL = HadoopUser1
   );  
   ```

4. [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md)을 사용하여 외부 파일 형식을 만듭니다.

   ```sql
   -- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

5. [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md)을 사용하여 Hadoop에 저장된 데이터를 가리키는 외부 테이블을 만듭니다. 이 예제에서 외부 데이터는 차량 센서 데이터를 포함합니다.

   ```sql
   -- LOCATION: path to file or directory that contains the data (relative to HDFS root).  
   CREATE EXTERNAL TABLE [dbo].[CarSensor_Data] (  
         [SensorKey] int NOT NULL,
         [CustomerKey] int NOT NULL,
         [GeographyKey] int NULL,
         [Speed] float NOT NULL,
         [YearMeasured] int NOT NULL  
   )  
   WITH (LOCATION='/Demo/',
         DATA_SOURCE = MyHadoopCluster,  
         FILE_FORMAT = TextFileFormat  
   );  
   ```

6. 외부 테이블에 대한 통계를 만듭니다.

   ```sql
   CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
   ```

## <a name="polybase-queries"></a>PolyBase 쿼리

세 가지 함수가 PolyBase에 적합합니다.  
  
- 외부 테이블에 대 한 임시 쿼리  
- 데이터 가져오기  
- 데이터 내보내기  

다음 쿼리는 가상 차량 센서 데이터를 포함하는 예제를 제공합니다.

### <a name="ad-hoc-queries"></a>임시 쿼리  

다음 임시 쿼리는 Hadoop 데이터와의 관계를 조인 합니다. 35입니다 보다 빠르게 구동 되는 고객을 선택 하 고, APS에 저장 된 구조적 고객 데이터를 Hadoop에 저장 된 자동차 센서 데이터로 조인 합니다.  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
OPTION (FORCE EXTERNALPUSHDOWN);   -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
```  

### <a name="importing-data"></a>데이터 가져오기  

다음 쿼리는 외부 데이터를 APS로 가져옵니다. 이 예제에서는 fast driver에 대 한 데이터를 AP로 가져와서 심층 분석을 수행 합니다. 성능 향상을 위해 AP의 Columnstore 기술을 활용 합니다.  

```sql
CREATE TABLE Fast_Customers
WITH
(CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH (CustomerKey))
AS
SELECT DISTINCT
      Insured_Customers.CustomerKey, Insured_Customers.FirstName, Insured_Customers.LastName,   
      Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
from Insured_Customers INNER JOIN   
(  
      SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
```  

### <a name="exporting-data"></a>데이터 내보내기  

다음 쿼리는 APS에서 Hadoop으로 데이터를 내보냅니다. 관계형 데이터를 계속 쿼리할 수 있지만 Hadoop에 보관 하는 데 사용할 수 있습니다.

```sql
-- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] 
WITH (  
      LOCATION='/archive/customer/2009',  
      DATA_SOURCE = HadoopHDP2,  
      FILE_FORMAT = TextFileFormat
)  
AS
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  

## <a name="view-polybase-objects-in-ssdt"></a>SSDT에서 PolyBase 개체 보기  

SQL Server Data Tools에서 외부 테이블은 별도의 폴더 **외부 테이블**에 표시 됩니다. 외부 데이터 원본 및 외부 파일 형식은 **외부 리소스**의 하위 폴더에 있습니다.  
  
![SSDT의 PolyBase 개체](media/polybase/external-tables-datasource.png)  

## <a name="next-steps"></a>다음 단계

Hadoop 보안 설정의 경우 [hadoop 보안 구성](polybase-configure-hadoop-security.md)을 참조 하세요.<br>
PolyBase에 대한 자세한 내용은 [PolyBase란?](../relational-databases/polybase/polybase-guide.md)을 참조하세요. 
 
