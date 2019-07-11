---
title: sys.database_service_objectives (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.service: sql-database
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.topic: conceptual
keywords:
- 탄력적 풀
- 탄력적 풀 관리
f1_keywords:
- DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 1bd16b4ac7fb0b27296fb2cc7e47ec683d761ed4
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716650"
---
# <a name="sysdatabaseserviceobjectives-azure-sql-database"></a>sys.database_service_objectives (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Azure SQL database 또는 Azure SQL Data Warehouse에 대 한 버전 (서비스 계층), 서비스 목표 (가격 책정 계층) 및 탄력적 풀 이름을 반환 합니다. Azure SQL Database 서버에서 master 데이터베이스에 로그온 하는 경우 모든 데이터베이스에서 정보를 반환 합니다. Azure SQL Data Warehouse에 대 한 master 데이터베이스에 연결 해야 합니다.  
  
  
 가격 책정 정보를 참조 하세요. [SQL Database 옵션 및 성능: SQL Database 가격 책정](https://azure.microsoft.com/pricing/details/sql-database/) 하 고 [SQL Data Warehouse 가격 책정](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)합니다.  
  
 서비스 설정을 변경 하려면을 참조 하세요 [ALTER DATABASE (Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md) 하 고 [ALTER DATABASE (Azure SQL Data Warehouse)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)합니다.  
  
 Sys.database_service_objectives 뷰에서 다음 열을 있습니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|database_id|ssNoversion|Azure SQL Database 서버 인스턴스 내에서 고유한 데이터베이스의 ID입니다. 사용 하 여 조인 가능 [sys.databases &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)합니다.|  
|버전|sysname|데이터베이스 또는 데이터 웨어하우스에 대 한 서비스 계층: **기본**, **표준**, **Premium** 하거나 **Data Warehouse**합니다.|  
|service_objective|sysname|데이터베이스의 가격 책정 계층입니다. 데이터베이스가 탄력적 풀에 있으면 반환 **ElasticPool**합니다.<br /><br /> 에 **기본적인** 계층을 반환 **기본**입니다.<br /><br /> **단일 데이터베이스를 standard 서비스 계층에서** 다음 중 하나를 반환 합니다. S0, S1, S2, S3, S4, S6, S7, S9 또는 S12 합니다.<br /><br /> **프리미엄 계층에서 단일 데이터베이스** 다음 반환: P1, P2, P4, P6, P11 또는 P15입니다.<br /><br /> **SQL Data Warehouse** DW30000c 통해 DW100를 반환 합니다.|  
|elastic_pool_name|sysname|이름을 합니다 [탄력적 풀](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/) 에 속하는 데이터베이스입니다. 반환 **NULL** 데이터베이스가 단일 데이터베이스 또는 데이터 warehoue 있는 경우.|  
  
## <a name="permissions"></a>사용 권한  
 필요 **dbManager** master 데이터베이스에 대 한 권한이 있습니다.  데이터베이스 수준에서 사용자 작성자 또는 소유자 여야 합니다.  
  
## <a name="examples"></a>예  
 이 예제에서는 master 데이터베이스 또는 Azure SQL Database 사용자 데이터베이스에서 실행할 수 있습니다. 쿼리 이름, 서비스 및 데이터베이스의 성능 계층 정보를 반환합니다.  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
