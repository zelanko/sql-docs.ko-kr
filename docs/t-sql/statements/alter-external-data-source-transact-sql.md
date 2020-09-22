---
description: ALTER EXTERNAL DATA SOURCE(Transact-SQL)
title: ALTER EXTERNAL DATA SOURCE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL DATA SOURCE
- ALTER_EXTERNAL_DATA_SOURCE
dev_langs:
- TSQL
helpviewer_keywords:
- polybase, alter external data source statement
- ALTER EXTERNAL DATA SOURCE statement
ms.assetid: a34b9e90-199d-46d0-817a-a7e69387bf5f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5d90bacf17953eee4874343fadf2e9daf97a8664
ms.sourcegitcommit: ac9feb0b10847b369b77f3c03f8200c86ee4f4e0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90688419"
---
# <a name="alter-external-data-source-transact-sql"></a>ALTER EXTERNAL DATA SOURCE(Transact-SQL)
[!INCLUDE [sqlserver2016-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdbmi-asa-pdw.md)]

  외부 테이블을 만드는데 사용되는 외부 데이터 원본을 수정합니다. 외부 데이터 원본은 SQL SERVER용 Hadoop 또는 Azure Blob Storage (WASBS)이거나 Azure SQL Data Warehouse용 Azure Blob Storage (WASBS) 또는 Azure Data Lake 스토리지(ABFSS/ADL)일 수 있습니다. 

## <a name="syntax"></a>구문  

```syntaxsql
-- Modify an external data source
-- Applies to: SQL Server (2016 or later) and APS
ALTER EXTERNAL DATA SOURCE data_source_name SET
    {   
        LOCATION = '<prefix>://<path>[:<port>]' [,] |
        RESOURCE_MANAGER_LOCATION = <'IP address;Port'> [,] |
        CREDENTIAL = credential_name
    }  
    [;]  

-- Modify an external data source pointing to Azure Blob storage
-- Applies to: SQL Server (starting with 2017)
ALTER EXTERNAL DATA SOURCE data_source_name
    SET
        LOCATION = 'https://storage_account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ] 

-- Modify an external data source pointing to Azure Blob storage or Azure Data Lake storage
-- Applies to: Azure SQL Data Warehouse
ALTER EXTERNAL DATA SOURCE data_source_name
    SET
        [LOCATION = '<location prefix>://<location path>']
        [, CREDENTIAL = credential_name ] 
```

## <a name="arguments"></a>인수  
 data_source_name은 데이터 원본에 대한 사용자 정의 이름을 지정합니다. 이름은 고유해야 합니다.

 LOCATION = '<prefix>://<path>[:<port>]' 외부 데이터 원본에 대한 연결 프로토콜, 경로 및 포트를 제공합니다. 유효한 위치 옵션은 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](create-external-data-source-transact-sql.md#location--prefixpathport)을 참조하세요.

 RESOURCE_MANAGER_LOCATION = '\<IP address;Port>'(Azure SQL Data Warehouse에 적용되지 않음) Hadoop Resource Manager 위치를 지정합니다. 지정된 경우 쿼리 최적화 프로그램은 Hadoop의 계산 기능을 사용하여 PolyBase 쿼리의 데이터를 사전 처리하도록 선택할 수 있습니다. 이것은 비용 기반 결정입니다. 조건자 푸시 다운이라는 이 기능은 Hadoop과 SQL 간에 전송되는 데이터 양을 크게 줄여 쿼리 성능을 향상시킬 수 있습니다.

 CREDENTIAL = Credential_Name은 명명된 자격 증명을 지정합니다. [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)을 참조하세요.

TYPE = [HADOOP | BLOB_STORAGE]   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].
대량 작업의 경우에만 `LOCATION`은 Azure Blob 스토리지의 URL에 유효해야 합니다. `LOCATION` URL 끝에 **/** , 파일 이름 또는 공유 액세스 서명 매개 변수를 두지 마십시오.
사용되는 자격 증명은 `SHARED ACCESS SIGNATURE`을 ID로 사용하여 만들어져야 합니다. 공유 액세스 서명에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)을 참조하세요.

  

## <a name="remarks"></a>설명
 한 번에 하나의 원본만 수정할 수 있습니다. 동일한 원본을 수정하기 위한 동시 요청은 하나의 명령문이 기다려야 합니다. 그러나 다른 원본은 동시에 수정할 수 있습니다. 이 명령문은 다른 명령문과 동시에 실행할 수 있습니다.

## <a name="permissions"></a>사용 권한  
 ALTER ANY EXTERNAL DATA SOURCE 권한이 필요합니다.
 > [!IMPORTANT]  
 > ALTER ANY EXTERNAL DATA SOURCE 권한은 보안 주체에 대해 외부 데이터 원본 개체를 만들고 수정하는 권한을 부여하며, 따라서 데이터베이스의 모든 데이터베이스 범위 자격 증명에 액세스하는 권한도 부여합니다. 이 권한은 높은 수준의 권한으로 간주되어야 하므로, 시스템의 신뢰할 수 있는 보안 주체에만 부여되어야 합니다.


## <a name="examples"></a>예제  
 다음 예제에서는 기존 데이터 원본의 위치 및 리소스 관리자 위치를 변경합니다.

```sql  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
     LOCATION = 'hdfs://10.10.10.10:8020',
     RESOURCE_MANAGER_LOCATION = '10.10.10.10:8032'
    ;
```

 다음 예제에서는 자격 증명을 변경하여 기존 데이터 원본에 연결합니다.

```sql 
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
   CREDENTIAL = new_hadoop_user
    ;
```

 다음 예제에서는 자격 증명을 새 위치로 변경 합니다. 이 예제는 Azure SQL Data Warehouse에 대해 생성되는 외부 데이터 원본입니다. 

```sql  
ALTER EXTERNAL DATA SOURCE AzureStorage_west SET
   LOCATION = 'wasbs://loadingdemodataset@updatedproductioncontainer.blob.core.windows.net',
   CREDENTIAL = AzureStorageCredential
```
