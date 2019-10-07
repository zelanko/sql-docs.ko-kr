---
title: Hadoop에 대한 PolyBase 구성 및 보안 | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 726b9c7ab8e5eddde8fe4b4ab7b545dda35cad1e
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710642"
---
# <a name="polybase-configuration-and-security-for-hadoop"></a>Hadoop에 대한 PolyBase 구성 및 보안

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 PolyBase-Hadoop 연결에 영향을 주는 다양한 구성 설정의 참조를 제공합니다. Hadoop에서 PolyBase를 사용하는 방법에 대한 연습 과정은 [Hadoop의 외부 데이터에 액세스하도록 PolyBase 구성](polybase-configure-hadoop.md)을 참조하세요.

## <a id="rpcprotection"></a> Hadoop.RPC.Protection 설정

Hadoop 클러스터에서 통신을 보호하는 일반적인 방법은 '개인 정보' 또는 '무결성' hadoop.rpc.protection 구성을 변경하는 것입니다. 기본적으로 PolyBase는 구성이 '인증'으로 설정되었다고 가정합니다. 이 기본값을 재정의하려면 core-site.xml 파일에 다음 속성을 추가합니다. 이 구성을 변경하면 SQL Server에 대한 SSL 연결 및 Hadoop 노드 간에 안전한 데이터 전송을 활성화합니다.

```xml
<!-- RPC Encryption information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG -->
   <property>
     <name>hadoop.rpc.protection</name>
     <value></value>
   </property> 
```

hadoop.rpc.protection에 대해 ‘개인 정보’ 또는 ‘무결성’을 사용하려면 SQL Server가 SQL Server 2016 SP1 CU7, SQL Server 2016 SP2 또는 SQL Server 2017 CU3 이상이어야 합니다.

## <a name="example-xml-files-for-cdh-5x-cluster"></a>CDH 5.X 클러스터의 예제 XML 파일

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

mapred-site.xml 및 yarn-site.xml로 두 가지 구성 설정을 분리하도록 선택한 경우 파일은 다음과 같습니다.

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

mapreduce.application.classpath 속성이 추가되었습니다. CDH 5.x에서 Ambari의 동일한 명명 규칙에서 구성 값을 찾을 수 있습니다.

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

## <a name="kerberos-configuration"></a>Kerberos 구성  

PolyBase가 Kerberos로 보호되는 클러스터에 인증하는 경우 기본적으로 hadoop.rpc.protection 설정이 인증이어야 합니다. 이렇게 하면 암호화되지 않은 Hadoop 노드 간의 데이터 통신이 유지됩니다. hadoop.rpc.protection에 대한 '개인 정보' 또는 '무결성' 설정을 사용하려면 PolyBase 서버에서 core-site.xml 파일을 업데이트합니다. 자세한 내용은 이전 섹션 [Hadoop.rpc.protection을 사용하여 Hadoop 클러스터에 연결](#rpcprotection)을 참조하세요.

MIT KDC를 사용하여 Kerberos로 보호되는 Hadoop 클러스터에 연결하려면 다음을 수행합니다.

1. SQL Server의 설치 경로에서 Hadoop 구성 디렉터리를 찾습니다. 일반적인 경로는 다음과 같습니다.  

   ```  
   C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\PolyBase\Hadoop\conf  
   ```  

2. 아래 표에 나와 있는 구성 키의 Hadoop 쪽 구성 값을 찾습니다. 구성 파일은 Hadoop 컴퓨터의 Hadoop 구성 디렉터리에서 찾을 수 있습니다.  
   
3. 구성 값을 SQL Server 컴퓨터의 해당 파일 내 value 속성에 복사합니다.  
   
   |**#**|**구성 파일**|**구성 키**|**동작**|  
   |------------|----------------|---------------------|----------|   
   |1|core-site.xml|polybase.kerberos.kdchost|KDC 호스트 이름을 지정합니다. 예를 들면 kerberos.your-realm.com과 같습니다.|  
   |2|core-site.xml|polybase.kerberos.realm|Kerberos 영역을 지정합니다. 예를 들어 YOUR-REALM.COM|  
   |3|core-site.xml|hadoop.security.authentication|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예를 들어 KERBEROS<br></br>**보안 정보:** KERBEROS는 대문자로 작성해야 합니다. 소문자로 작성되면 실행되지 않을 수 있습니다.|   
   |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예: hdfs/_HOST@YOUR-REALM.COM|  
   |5|mapred-site.xml|mapreduce.jobhistory.principal|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예: mapred/_HOST@YOUR-REALM.COM|  
   |6|mapred-site.xml|mapreduce.jobhistory.address|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예를 들어 10.193.26.174:10020|  
   |7|yarn-site.xml yarn|yarn.resourcemanager.principal|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예: yarn/_HOST@YOUR-REALM.COM|  

4. 데이터베이스 범위 자격 증명 개체를 만들어 각 Hadoop 사용자에 대해 인증 정보를 지정합니다. [PolyBase T-SQL 개체](../../relational-databases/polybase/polybase-t-sql-objects.md)를 참조하세요.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="next-steps"></a>다음 단계  

자세한 내용은 다음 문서를 참조하세요.

[Hadoop의 외부 데이터에 액세스하도록 PolyBase 구성](polybase-configure-hadoop.md)
[PolyBase 개요](../../relational-databases/polybase/polybase-guide.md)
