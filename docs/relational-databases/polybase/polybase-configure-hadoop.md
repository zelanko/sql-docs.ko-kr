---
title: Hadoop의 외부 데이터에 액세스하도록 PolyBase 구성 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2dd074f4cd7d3d9042e5f0deb3de6ee0731c4af9
ms.sourcegitcommit: 70e47a008b713ea30182aa22b575b5484375b041
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49806723"
---
# <a name="configure-polybase-to-access-external-data-in-hadoop"></a>Hadoop의 외부 데이터에 액세스하도록 PolyBase 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server 인스턴스에서 PolyBase를 사용하여 Hadoop에서 외부 데이터를 쿼리하는 방법을 설명합니다.

## <a name="prerequisites"></a>사전 요구 사항

- PolyBase를 설치하지 않은 경우 [PolyBase 설치](polybase-installation.md)를 참조하세요. 설치 문서에서는 필수 구성 요소를 설명합니다.

<!--SQL Server 2019-->
::: moniker range=">= sql-server-ver15 || =sqlallproducts-allversions"

- SQL Server 2019부터 [PolyBase 기능도 사용하도록 설정](polybase-installation.md#enable)해야 합니다.

::: moniker-end

- PolyBase는 HDP(Hortonworks Data Platform) 및 CDH(Cloudera Distributed Hadoop)의 두 가지 Hadoop 공급자를 지원합니다. Hadoop은 새 릴리스의 "Major.Minor.Version" 패턴을 따르며, 지원되는 주/부 릴리스 내의 모든 버전이 지원됩니다. 다음 Hadoop 공급자가 지원됩니다.

  - Linux/Windows Server에서 Hortonworks HDP 1.3  
  - Linux에서 Hortonworks HDP 2.1 - 2.6
  - Windows Server에서 Hortonworks HDP 2.1 - 2.3  
  - Linux에서 Cloudera CDH 4.3  
  - Linux에서 Cloudera CDH 5.1 – 5.5, 5.9 - 5.13

> [!NOTE]
> PolyBase는 SQL Server 2016 SP1 CU7 및 SQL Server 2017 CU3부터 Hadoop 암호화 영역을 지원합니다. [PolyBase 스케일 아웃 그룹](polybase-scale-out-groups.md)을 사용 중인 경우 모든 계산 노드도 Haddop 암호화 영역 지원을 포함하는 빌드에 있어야 합니다.

### <a name="configure-hadoop-connectivity"></a>Hadoop 연결 구성

먼저 특정 Hadoop 공급자를 사용하도록 SQL Server PolyBase를 구성합니다.

1. ‘hadoop connectivity’를 사용하여 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 실행하고 사용 중인 공급자에 적합한 값을 설정합니다. 공급자의 값을 찾으려면 [PolyBase 연결 구성](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)을 참조하세요. 기본적으로 Hadoop 연결은 7로 설정됩니다.

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. **services.msc**를 사용하여 SQL Server를 다시 시작해야 합니다. SQL Server를 다시 시작하면 다음 서비스도 다시 시작됩니다.  

   - SQL Server PolyBase 데이터 이동 서비스  
   - SQL Server PolyBase 엔진  
  
   ![services.msc에서 PolyBase 서비스 중지 및 시작](../../relational-databases/polybase/media/polybase-stop-start.png "stop and start PolyBase services in services.msc")  
  
## <a id="pushdown"></a> 푸시다운 계산 사용  

쿼리 성능을 향상하려면 Hadoop 클러스터에 대한 푸시다운 계산을 사용하도록 설정합니다.  
  
1. SQL Server 설치 경로에서 **yarn-site.xml** 파일을 찾습니다. 일반적인 경로는 다음과 같습니다.  

   ```xml  
   C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\PolybaseHadoopconf  
   ```  

1. Hadoop 컴퓨터의 Hadoop 구성 디렉터리에서 동일한 파일을 찾습니다. 이 파일에서 구성 키 yarn.application.classpath의 값을 찾아서 복사합니다.  
  
1. SQL Server 컴퓨터의 **yarn.site.xml 파일** 에서 **yarn.application.classpath** 속성을 찾은 다음 Hadoop 컴퓨터의 값을 value 요소에 붙여넣습니다.  
  
1. 모든 CDH 5.X 버전에서 mapreduce.application.classpath 구성 매개 변수를 yarn.site.xml 파일의 끝이나 mapred-site.xml 파일에 추가해야 합니다. HortonWorks는 yarn.application.classpath 구성 내에 이러한 구성을 포함하고 있습니다. 예제는 [PolyBase 구성](../../relational-databases/polybase/polybase-configuration.md)을 참조하세요.

## <a name="configure-an-external-table"></a>외부 테이블 구성

Hadoop 데이터 원본에서 데이터를 쿼리하려면 Transact-SQL 쿼리에 사용할 외부 테이블을 정의해야 합니다. 다음 단계에서는 외부 테이블을 구성하는 방법을 설명합니다.

1. 데이터베이스에 마스터 키가 없는 경우 하나 만듭니다. 이 키는 자격 증명 비밀을 암호화하는 데 필요합니다.

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';  
     ```
    ## <a name="arguments"></a>인수
    PASSWORD ='password'

    데이터베이스의 마스터 키를 암호화하는 데 사용되는 암호입니다. password는 SQL Server의 인스턴스를 호스팅하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족해야 합니다.
1. Kerberos 보안 Hadoop 클러스터의 데이터베이스 범위 자격 증명을 만듭니다.

   ```sql
   -- IDENTITY: the Kerberos user name.  
   -- SECRET: the Kerberos password  
   CREATE DATABASE SCOPED CREDENTIAL HadoopUser1
   WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
   ```

2. [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)를 사용하여 외부 데이터 원본을 만듭니다.

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

3. [CREATE EXTERNAL FILE FORMAT](../../t-sql/statements/create-external-file-format-transact-sql.md)을 사용하여 외부 파일 형식을 만듭니다.

   ```sql
   -- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

4. [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md)을 사용하여 Hadoop에 저장된 데이터를 가리키는 외부 테이블을 만듭니다. 이 예제에서 외부 데이터는 차량 센서 데이터를 포함합니다.

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

5. 외부 테이블에 대한 통계를 만듭니다.

   ```sql
   CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
   ```

## <a name="polybase-queries"></a>PolyBase 쿼리

세 가지 함수가 PolyBase에 적합합니다.  
  
- 외부 테이블에 대한 임시 쿼리  
- 데이터 가져오기  
- 데이터 내보내기  

다음 쿼리는 가상 차량 센서 데이터를 포함하는 예제를 제공합니다.

### <a name="ad-hoc-queries"></a>임시 쿼리  

다음 임시 쿼리는 Hadoop 데이터와 관계형으로 조인됩니다. 이 쿼리는 35mph보다 빠르게 주행하는 고객을 선택한 후 SQL Server에 저장된 구조화된 고객 데이터를 Hadoop에 저장된 차량 센서 데이터와 조인합니다.  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
OPTION (FORCE EXTERNALPUSHDOWN);   -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
```  

### <a name="importing-data"></a>데이터 가져오기  

다음 쿼리는 외부 데이터를 SQL Server로 가져옵니다. 이 예제에서는 자세한 심층 분석을 위해 빠른 운전자의 데이터를 SQL Server로 가져옵니다. 성능을 향상시키기 위해 Columnstore 기술을 활용합니다.  

```sql
SELECT DISTINCT
      Insured_Customers.FirstName, Insured_Customers.LastName,   
      Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
INTO Fast_Customers from Insured_Customers INNER JOIN   
(  
      SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
ORDER BY YearlyIncome  
  
CREATE CLUSTERED COLUMNSTORE INDEX CCI_FastCustomers ON Fast_Customers;  
```  

### <a name="exporting-data"></a>데이터 내보내기  

다음 쿼리는 SQL Server의 데이터를 Hadoop으로 내보냅니다. 이를 수행하려면 먼저 PolyBase 내보내기를 사용하도록 설정해야 합니다. 데이터를 내보내기 전에 대상의 외부 테이블을 만듭니다.

```sql
-- Enable INSERT into external table  
sp_configure ‘allow polybase export’, 1;  
reconfigure  
  
-- Create an external table.
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] (  
      [FirstName] char(25) NOT NULL,
      [LastName] char(25) NOT NULL,
      [YearlyIncome] float NULL,
      [MaritalStatus] char(1) NOT NULL  
)  
WITH (  
      LOCATION='/old_data/2009/customerdata',  
      DATA_SOURCE = HadoopHDP2,  
      FILE_FORMAT = TextFileFormat,  
      REJECT_TYPE = VALUE,  
      REJECT_VALUE = 0  
);  

-- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
INSERT INTO dbo.FastCustomer2009  
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  

## <a name="view-polybase-objects-in-ssms"></a>SSMS에서 PolyBase 개체 보기  

SSMS에서 외부 테이블은 별도 폴더인 **외부 테이블**에 표시됩니다. 외부 데이터 원본 및 외부 파일 형식은 **외부 리소스**의 하위 폴더에 있습니다.  
  
![SSMS의 PolyBase 개체](media/polybase-management.png)  

## <a name="next-steps"></a>다음 단계

다음 문서에서 PolyBase를 사용 및 모니터링하는 추가 방법을 알아봅니다.

[PolyBase 스케일 아웃 그룹](../../relational-databases/polybase/polybase-scale-out-groups.md)  
[PolyBase 문제 해결](polybase-troubleshooting.md)  
