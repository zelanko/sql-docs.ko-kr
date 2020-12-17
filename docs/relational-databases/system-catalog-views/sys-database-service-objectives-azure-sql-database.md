---
description: sys.database_service_objectives(Azure SQL Database)
title: sys.database_service_objectives
titleSuffix: Azure SQL Database
ms.date: 03/21/2018
ms.service: sql-database
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.topic: conceptual
keywords:
- 탄력적 풀
- 탄력적 풀, 관리
f1_keywords:
- DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
author: markingmyname
ms.author: maghan
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = azure-sqldw-latest
ms.openlocfilehash: 6435440b60c7b90d78f8050d64b5b580e610f017
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97643333"
---
# <a name="sysdatabase_service_objectives-azure-sql-database"></a>sys.database_service_objectives(Azure SQL Database)
[!INCLUDE [asdb-asdbmi-asa](../../includes/applies-to-version/asdb-asdbmi-asa.md)]

Azure SQL database 또는 Azure Synapse Analytics의 버전 (서비스 계층), 서비스 목표 (가격 책정 계층) 및 탄력적 풀 이름 (있는 경우)을 반환 합니다. Azure SQL Database 서버의 마스터 데이터베이스에 로그인하면 모든 데이터베이스에 대한 정보를 반환합니다. Azure Synapse Analytics의 경우 master 데이터베이스에 연결 해야 합니다.  
  
  
 가격 책정에 대 한 자세한 내용은 [SQL Database 옵션 및 성능: SQL Database 가격](https://azure.microsoft.com/pricing/details/sql-database/) 책정 및 [Azure Synapse Analytics 가격 책정](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)을 참조 하세요.  
  
 서비스 설정을 변경 하려면 [ALTER database (Azure SQL Database)](../../t-sql/statements/alter-database-transact-sql.md) 및 [Alter Database (Azure Synapse Analytics)](../../t-sql/statements/alter-database-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)를 참조 하세요.  
  
 Sys.database_service_objectives 뷰에는 다음 열이 포함 되어 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id|int|Azure SQL Database server의 인스턴스 내에서 고유한 데이터베이스 ID입니다. 조인 가능를 사용 하 여 [transact-sql&#41;&#40;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|edition|sysname|데이터베이스 또는 데이터 웨어하우스의 서비스 계층: **Basic**, **Standard**, **Premium** 또는 **data warehouse**.|  
|service_objective|sysname|데이터베이스의 가격 책정 계층입니다. 데이터베이스가 탄력적 풀에 있는 경우 **ElasticPool** 를 반환 합니다.<br /><br /> **기본** 계층에서 **basic** 을 반환 합니다.<br /><br /> **표준 서비스 계층의 단일 데이터베이스** 는 S0, S1, S2, S3, S4, S6, S7, S9 또는 s 12 중 하나를 반환 합니다.<br /><br /> **프리미엄 계층의 단일 데이터베이스** 는 P1, P2, P4, P6, P11 또는 P15을 반환 합니다.<br /><br /> **Azure Synapse Analytics** 는 DW30000c를 통해 DW100를 반환 합니다.<br /><br /> 자세한 내용은 [단일 데이터베이스](/azure/sql-database/sql-database-dtu-resource-limits-single-databases/), [탄력적 풀](/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools/), [데이터 웨어하우스](/azure/sql-data-warehouse/what-is-a-data-warehouse-unit-dwu-cdwu/) 를 참조 하세요.|  
|elastic_pool_name|sysname|데이터베이스가 속한 [탄력적 풀](/azure/azure-sql/database/elastic-pool-overview) 의 이름입니다. 데이터베이스가 단일 데이터베이스 또는 데이터 웨어하우스 인 경우 **NULL** 을 반환 합니다.|  
  
## <a name="permissions"></a>사용 권한  
 Master 데이터베이스에 대 한 **dbManager** 권한이 필요 합니다.  데이터베이스 수준에서 사용자는 작성자 또는 소유자 여야 합니다.  
  
## <a name="examples"></a>예  
 이 예는 master 데이터베이스 또는 Azure SQL Database 사용자 데이터베이스에서 실행할 수 있습니다. 이 쿼리는 데이터베이스의 이름, 서비스 및 성능 계층 정보를 반환 합니다.  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
