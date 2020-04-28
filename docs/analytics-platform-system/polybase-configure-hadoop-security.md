---
title: PolyBase Hadoop 보안 구성
description: 외부 Hadoop에 연결 하도록 병렬 데이터 웨어하우스에서 PolyBase를 구성 하는 방법을 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/26/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: f275c77556e8abe8932e241075b9e24e2ae5db77
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "79289681"
---
# <a name="polybase-configuration-and-security-for-hadoop"></a>Hadoop에 대한 PolyBase 구성 및 보안

이 문서에서는 Hadoop에 대 한 APS PolyBase 연결에 영향을 주는 다양 한 구성 설정에 대 한 참조를 제공 합니다. PolyBase에 대 한 연습은 [polybase 란?](configure-polybase-connectivity-to-external-data.md)을 참조 하세요.

> [!NOTE]
> APS에서 XML 파일에 대 한 변경 내용은 모든 계산 노드 및 제어 노드에 필요 합니다.
> 
> AP에서 XML 파일을 수정할 때 특히 주의 해야 합니다. 누락 된 태그나 원치 않는 문자는 기능의 hindering xml 파일을 무효화할 수 있습니다.
> Hadoop 구성 파일은 다음 경로에 있습니다.  
> ```  
> C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf 
> ``` 
> Xml 파일을 변경 하면 서비스를 다시 시작 해야 적용 됩니다.

## <a name="hadooprpcprotection-setting"></a><a id="rpcprotection"></a> Hadoop.RPC.Protection 설정

Hadoop 클러스터에서 통신을 보호하는 일반적인 방법은 '개인 정보' 또는 '무결성' hadoop.rpc.protection 구성을 변경하는 것입니다. 기본적으로 PolyBase는 구성이 '인증'으로 설정되었다고 가정합니다. 이 기본값을 재정의하려면 core-site.xml 파일에 다음 속성을 추가합니다. 이 구성을 변경하면 SQL Server에 대한 SSL 연결 및 Hadoop 노드 간에 안전한 데이터 전송을 활성화합니다.

```xml
<!-- RPC Encryption information, PLEASE FILL THESE IN ACCORDING TO HADOOP CLUSTER CONFIG -->
   <property>
     <name>hadoop.rpc.protection</name>
     <value></value>
   </property> 
```

## <a name="kerberos-configuration"></a><a id="kerberossettings"></a>Kerberos 구성  

PolyBase가 Kerberos로 보호되는 클러스터에 인증하는 경우 기본적으로 hadoop.rpc.protection 설정이 인증이어야 합니다. 이렇게 하면 암호화되지 않은 Hadoop 노드 간의 데이터 통신이 유지됩니다. hadoop.rpc.protection에 대한 '개인 정보' 또는 '무결성' 설정을 사용하려면 PolyBase 서버에서 core-site.xml 파일을 업데이트합니다. 자세한 내용은 이전 섹션 [Hadoop.rpc.protection을 사용하여 Hadoop 클러스터에 연결](#rpcprotection)을 참조하세요.

MIT KDC를 사용 하 여 Kerberos 보안 Hadoop 클러스터에 연결 하려면 모든 APS 계산 노드 및 제어 노드에서 다음과 같이 변경 해야 합니다.

1. APS의 설치 경로에서 Hadoop 구성 디렉터리를 찾습니다. 일반적인 경로는 다음과 같습니다.  

   ```  
   C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf  
   ```  

2. 아래 표에 나와 있는 구성 키의 Hadoop 쪽 구성 값을 찾습니다. 구성 파일은 Hadoop 컴퓨터의 Hadoop 구성 디렉터리에서 찾을 수 있습니다.  
   
3. 구성 값을 SQL Server 컴퓨터의 해당 파일 내 value 속성에 복사합니다.  
   
   |**#**|**구성 파일**|**구성 키**|**동작**|  
   |------------|----------------|---------------------|----------|   
   |1|core-site.xml|polybase.kerberos.kdchost|KDC 호스트 이름을 지정합니다. 예를 들면 kerberos.your-realm.com과 같습니다.|  
   |2|core-site.xml|polybase.kerberos.realm|Kerberos 영역을 지정합니다. 다음은 그 예입니다.  YOUR-REALM.COM|  
   |3|core-site.xml|hadoop.security.authentication|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 다음은 그 예입니다.  KERBEROS<br></br>**보안 정보:** KERBEROS는 대문자로 작성해야 합니다. 소문자로 작성되면 실행되지 않을 수 있습니다.|   
   |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예: hdfs/_HOST@YOUR-REALM.COM|  
   |5|mapred-site.xml|mapreduce.jobhistory.principal|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예: mapred/_HOST@YOUR-REALM.COM|  
   |6|mapred-site.xml|mapreduce.jobhistory.address|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 다음은 그 예입니다.  10.193.26.174:10020|  
   |7|yarn-site.xml yarn|yarn.resourcemanager.principal|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예: yarn/_HOST@YOUR-REALM.COM|  

**core-site.xml**
```xml
<property>
  <name>polybase.kerberos.realm</name>
  <value></value>
</property>
<property>
  <name>polybase.kerberos.kdchost</name>
  <value></value>
</property>
<property>
    <name>hadoop.security.authentication</name>
    <value>KERBEROS</value>
</property>
```

**hdfs-site.xml**
```xml
<property>
  <name>dfs.namenode.kerberos.principal</name>
  <value></value> 
</property>
```

**mapred-site.xml**
```xml
<property>
  <name>mapreduce.jobhistory.principal</name>
  <value></value>
</property>
<property>
  <name>mapreduce.jobhistory.address</name>
  <value></value>
</property>
```

**yarn-site.xml**
```xml
<property>
  <name>yarn.resourcemanager.principal</name>
  <value></value>
</property>
```

4. 데이터베이스 범위 자격 증명 개체를 만들어 각 Hadoop 사용자에 대해 인증 정보를 지정합니다. [PolyBase T-SQL 개체](../relational-databases/polybase/polybase-t-sql-objects.md)를 참조하세요.

## <a name="hadoop-encryption-zone-setup"></a><a id="encryptionzone"></a>Hadoop 암호화 영역 설정
Hadoop 암호화 영역을 사용 하는 경우 core-site.xml 및 hdfs-site.xml를 다음과 같이 수정 합니다. 해당 포트 번호를 사용 하 여 KMS 서비스를 실행 하는 ip 주소를 제공 합니다. CDH의 KMS에 대 한 기본 포트는 16000입니다.

**core-site.xml**
```xml
<property>
  <name>hadoop.security.key.provider.path</name>
  <value>kms://http@<ip address>:16000/kms</value> 
</property>
```

**hdfs-site.xml**
```xml
<property>
  <name>dfs.encryption.key.provider.uri</name>
  <value>kms://http@<ip address>:16000/kms</value>
</property>
<property>
  <name>hadoop.security.key.provider.path</name>
  <value>kms://http@<ip address>:16000/kms</value>
  </property>
```