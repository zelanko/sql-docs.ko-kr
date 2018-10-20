---
title: Hadoop의 외부 데이터에 액세스하도록 PolyBase 구성 | Microsoft Docs
description: 외부 Hadoop 연결할 Parallel Data Warehouse에서 PolyBase를 구성 하는 방법을 설명 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 89ce9402540c21a9f9eedbba4f488ea1c3350956
ms.sourcegitcommit: ef78cc196329a10fc5c731556afceaac5fd4cb13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49460883"
---
# <a name="configure-polybase-to-access-external-data-in-hadoop"></a>Hadoop의 외부 데이터에 액세스하도록 PolyBase 구성

이 문서는 PolyBase를 사용 하 여 Hadoop에서 외부 데이터를 쿼리 하는 APS 어플라이언스 방법을 설명 합니다.

## <a name="prerequisites"></a>필수 구성 요소

PolyBase는 HDP(Hortonworks Data Platform) 및 CDH(Cloudera Distributed Hadoop)의 두 가지 Hadoop 공급자를 지원합니다. Hadoop은 새 릴리스의 "Major.Minor.Version" 패턴을 따르며, 지원되는 주/부 릴리스 내의 모든 버전이 지원됩니다. 다음 Hadoop 공급자가 지원됩니다.
 - Linux/Windows Server에서 Hortonworks HDP 1.3  
 - Linux에서 Hortonworks HDP 2.1 - 2.6
 - Windows Server에서 Hortonworks HDP 2.1 - 2.3  
 - Linux에서 Cloudera CDH 4.3  
 - Linux에서 Cloudera CDH 5.1 – 5.5, 5.9 - 5.13

### <a name="configure-hadoop-connectivity"></a>Hadoop 연결 구성

먼저 특정 Hadoop 공급자를 사용 하는 AP를 구성 합니다.

1. ‘hadoop connectivity’를 사용하여 [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 실행하고 사용 중인 공급자에 적합한 값을 설정합니다. 공급자의 값을 찾으려면 [PolyBase 연결 구성](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)을 참조하세요. 

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. AP 지역에서 서비스 상태 페이지를 사용 하 여 다시 시작 [구성 관리자 어플라이언스](launch-the-configuration-manager.md)합니다.
  
## <a id="pushdown"></a> 푸시다운 계산 사용  

쿼리 성능을 향상하려면 Hadoop 클러스터에 대한 푸시다운 계산을 사용하도록 설정합니다.  
  
1. PDW 제어 노드에 대 한 원격 데스크톱 연결을 엽니다.

2. 파일을 찾을 **yarn-site.xml** 제어 노드에 있습니다. 일반적인 경로는 다음과 같습니다.  

   ```xml  
   C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf\  
   ```  

3. Hadoop 컴퓨터의 Hadoop 구성 디렉터리에서 동일한 파일을 찾습니다. 이 파일에서 구성 키 yarn.application.classpath의 값을 찾아서 복사합니다.  
  
4. 제어 노드에서는 **yarn.site.xml 파일** 찾을 합니다 **yarn.application.classpath** 속성. Hadoop 컴퓨터의 값을 value 요소에 붙여넣습니다.  
  
5. 모든 CDH 5.X 버전에서 mapreduce.application.classpath 구성 매개 변수를 yarn.site.xml 파일의 끝이나 mapred-site.xml 파일에 추가해야 합니다. HortonWorks는 yarn.application.classpath 구성 내에 이러한 구성을 포함하고 있습니다. 예제는 [PolyBase 구성](../relational-databases/polybase/polybase-configuration.md)을 참조하세요.

## <a name="configure-an-external-table"></a>외부 테이블 구성

Hadoop 데이터 원본에서 데이터를 쿼리하려면 Transact-SQL 쿼리에 사용할 외부 테이블을 정의해야 합니다. 다음 단계에서는 외부 테이블을 구성하는 방법을 설명합니다.

1. 데이터베이스에 마스터 키를 만듭니다. 자격 증명 비밀을 암호화 해야 합니다.

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

5. [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md)을 사용하여 Hadoop에 저장된 데이터를 가리키는 외부 테이블을 만듭니다. 이 예제에서는 외부 데이터는 차량 센서 데이터를 포함합니다.

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
  
- 외부 테이블에 대 한 임시 쿼리 합니다.  
- 데이터 가져오기  
- 데이터 내보내기  

다음 쿼리는 가상 차량 센서 데이터를 포함하는 예제를 제공합니다.

### <a name="ad-hoc-queries"></a>임시 쿼리  

다음 임시 쿼리에 Hadoop 데이터를 사용 하 여 관계형 조인합니다. 35 속도로, Hadoop에 저장 된 차량 센서 데이터를 사용 하 여 AP에 저장 된 구조화 된 고객 데이터를 조인 보다 더 빠르게 드라이브 고객을 선택 합니다.  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
OPTION (FORCE EXTERNALPUSHDOWN);   -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
```  

### <a name="importing-data"></a>데이터 가져오기  

다음 쿼리는 AP에 외부 데이터를 가져옵니다. 이 예제에서는 자세한 심층 분석을 위해 AP에 빠른 드라이버에 대 한 데이터를 가져옵니다. 성능 향상을 위해 AP의 Columnstore 기술을 활용 합니다.  

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

다음 쿼리는 Hadoop에 AP에서 데이터를 내보냅니다. Hadoop에 관계형 데이터를 보관할 수는 수를 쿼리할 수 있습니다.

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

## <a name="view-polybase-objects-in-ssdt"></a>SSDT에서 PolyBase 개체를 보려면  

SQL Server Data Tools, 외부 테이블을 별도 폴더에 표시 됩니다 **외부 테이블**합니다. 외부 데이터 원본 및 외부 파일 형식은 **외부 리소스**의 하위 폴더에 있습니다.  
  
![SSDT에서 PolyBase 개체](media/polybase/external-tables-datasource.png)  

## <a name="next-steps"></a>다음 단계

PoliyBase에 대 한 자세한 내용은 참조는 [PolyBase 란?](../relational-databases/polybase/polybase-guide.md)합니다. 
 
