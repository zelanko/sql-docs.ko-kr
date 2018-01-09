---
title: "외부 데이터 원본 (Transact SQL) ALTER | Microsoft Docs"
ms.custom: 
ms.date: 01/09/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL DATA SOURCE
- ALTER_EXTERNAL_DATA_SOURCE
dev_langs: TSQL
helpviewer_keywords:
- polybase, alter external data source statement
- ALTER EXTERNAL DATA SOURCE statement
ms.assetid: a34b9e90-199d-46d0-817a-a7e69387bf5f
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9257f2747d29933ce04f8e7faa2112c3f4231eaf
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="alter-external-data-source-transact-sql"></a>ALTER 외부 데이터 원본 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  외부 테이블을 만드는 데 외부 데이터 원본을 수정 합니다. 외부 데이터 원본에는 Hadoop 또는 Azure blob 저장소 (WASB) 될 수 있습니다.
  
## <a name="syntax"></a>구문  
  
```  
-- Modify an external data source
-- Applies to: SQL Server (2016 or later)
ALTER EXTERNAL DATA SOURCE data_source_name SET
    {   
        LOCATION = 'server_name_or_IP' [,] |
        RESOURCE_MANAGER_LOCATION = <'IP address;Port'> [,] |
        CREDENTIAL = credential_name
    }  
    [;]  

-- Modify an external data source pointing to Azure Blob storage
-- Applies to: SQL Server (starting with 2017)
ALTER EXTERNAL DATA SOURCE data_source_name
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://storage_account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
```  
  
## <a name="arguments"></a>인수  
 data_source_name는 데이터 원본에 대 한 사용자 정의 이름을 지정합니다. 이름은 고유해야 합니다.
  
 위치 = 'server_name_or_IP' 또는 IP 주소는 서버 이름을 지정 합니다.
  
 RESOURCE_MANAGER_LOCATION = '\<IP 주소입니다. 포트 >' Hadoop 리소스 관리자 위치를 지정 합니다. 을 지정 하면 쿼리 최적화 프로그램은 미리 Hadoop의 계산 기능을 사용 하 여 PolyBase 쿼리를 위해 데이터를 처리 하도록 선택할 수 있습니다. 이것은 비용 기반 결정 합니다. 조건자 푸시 다운이 수 Hadoop과 SQL을 간에 전송 되는 데이터 양이 크게 줄일를 호출한 따라서 쿼리 성능을 향상 시킵니다.
  
 자격 증명 이름이 지정 된 자격 증명 Credential_Name 지정 = 합니다. 참조 [CREATE DATABASE SCOPED credential&#40; Transact SQL &#41; ](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

형식 = BLOB_STORAGE   
**적용 대상:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]을 참조하세요.
대량 작업에 `LOCATION` 유효 해야 Azure Blob 저장소 URL입니다. 에 두지 마십시오  **/** , 파일 이름, 또는 공유 액세스 서명 매개 변수 끝에 `LOCATION` URL입니다.
사용 하 여을 사용 하는 자격 증명을 만들어야 `SHARED ACCESS SIGNATURE` id로 합니다. 공유 액세스 서명에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)을 참조하세요.

  
  
## <a name="remarks"></a>주의
 한 번에 하나의 소스만 수정할 수 있습니다. 동일한 소스를 수정 하는 동시 요청 발생 한 문이 기다려야 합니다. 그러나 서로 다른 소스는 동시에 수정할 수 있습니다. 이 문은 다른 문을 동시에 실행할 수 있습니다.
  
## <a name="permissions"></a>Permissions  
 ALTER ANY EXTERNAL DATA SOURCE 권한이 필요합니다.
 > [!IMPORTANT]  
 >  ALTER ANY EXTERNAL DATA SOURCE 사용 권한을 부여의 보안 주체를 만들고 모든 외부 데이터 원본 개체를 수정 하는 기능 하 고 따라서 데이터베이스의 모든 데이터베이스 범위 자격 증명에 액세스할 수 있도록도 부여 합니다. 높은 권한이 있지만 고 따라서에서 부여 해야 신뢰할 수 있는 보안 주체에만 시스템에는이 사용 권한을 고려 되어야 합니다.

  
## <a name="examples"></a>예  
 다음 예제에서는 위치 및 기존 데이터 원본의 리소스 관리자 위치를 변경합니다.
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
     LOCATION = 'hdfs://10.10.10.10:8020',
     RESOURCE_MANAGER_LOCATION = '10.10.10.10:8032'
    ;
  
```  

 다음 예제에서는 기존 데이터 원본에 연결할 자격 증명을 변경 합니다.
  
```  
ALTER EXTERNAL DATA SOURCE hadoop_eds SET
   CREDENTIAL = new_hadoop_user
    ;
```