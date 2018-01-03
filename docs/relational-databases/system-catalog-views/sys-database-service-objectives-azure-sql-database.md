---
title: "sys.database_service_objectives (Azure SQL 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 08/30/2016
ms.prod: 
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "탄력적 풀"
- "탄력적 풀 관리"
f1_keywords: DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
caps.latest.revision: "16"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 72cc970e8e6b37988399707b5cef77cbda3afd36
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="sysdatabaseserviceobjectives-azure-sql-database"></a>sys.database_service_objectives (Azure SQL 데이터베이스)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스에 대 한 버전 (서비스 계층), (가격 책정 계층) 서비스 목표 및 탄력적인 풀 이름을 반환 합니다. Azure SQL 데이터베이스 서버에서 master 데이터베이스에 로그온 하는 경우 모든 데이터베이스에서 정보를 반환 합니다. Azure SQL 데이터 웨어하우스에 대 한 master 데이터베이스에 연결 합니다.  
  
  
 가격 책정에 대 한 정보를 참조 하십시오. [SQL 데이터베이스 옵션 및 성능: SQL 데이터베이스 가격 정보](https://azure.microsoft.com/en-us/pricing/details/sql-database/) 및 [SQL 데이터 웨어하우스 가격](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)합니다.  
  
 서비스 설정을 변경 하려면 참조 [ALTER DATABASE (Azure SQL 데이터베이스)](../../t-sql/statements/alter-database-azure-sql-database.md) 및 [ALTER DATABASE (Azure SQL 데이터 웨어하우스)](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)합니다.  
  
 Sys.database_service_objectives 보기는 다음과 같은 열을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id|ssNoversion|Azure SQL 데이터베이스 서버 인스턴스 내에서 고유한 데이터베이스의 ID입니다. 으로 참가할 수 있는 [sys.databases&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|버전|sysname|데이터베이스 또는 데이터 웨어하우스에 대 한 서비스 계층: **기본**, **표준**, **프리미엄** 또는 **데이터 웨어하우스**합니다.|  
|service_objective|sysname|데이터베이스의 가격 책정 계층입니다. 데이터베이스는 탄력적인 풀에 포함 된 경우 반환 **ElasticPool**합니다.<br /><br /> 에 **기본** 계층 반환 **기본**합니다.<br /><br /> **Standard 서비스 계층에서 단일 데이터베이스** 다음 중 하나를 반환 합니다: S0, S1, S2 또는 s 3입니다.<br /><br /> **프리미엄 계층에서 단일 데이터베이스** 다음 반환: P1, P2, P4, P6/P3 또는 P11 합니다.<br /><br /> **SQL 데이터 웨어하우스** DW2000 통해 DW100를 반환 합니다.|  
|elastic_pool_name|sysname|이름에서 [탄력적 풀](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/) 에 속하는 데이터베이스입니다. 반환 **NULL** 데이터베이스가 단일 데이터베이스 또는 데이터 warehoue 경우.|  
  
## <a name="permissions"></a>Permissions  
 필요한 **dbManager** master 데이터베이스에 대 한 권한이 있습니다.  데이터베이스 수준에서 작성자 또는 소유자 사용자 여야 합니다.  
  
## <a name="examples"></a>예  
 이 예제에서는 사용자 데이터베이스 또는 master 데이터베이스에서 실행할 수 있습니다. 쿼리 이름, 서비스 및 데이터베이스의 성능 계층 정보를 반환합니다.  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
