---
title: 데이터베이스 미러링 시스템 개체 참조 | Microsoft Docs
description: 데이터베이스 미러링 시스템 개체인 시스템 카탈로그 뷰, 시스템 동적 관리 뷰 및 시스템 테이블 관련 정보를 확인합니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c37c75f9824f85705f92d1fabb6519303a76fafb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754718"
---
# <a name="database-mirroring-system-object-reference"></a>데이터베이스 미러링 시스템 개체 참조
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="system-catalog-views"></a>시스템 카탈로그 뷰

| 시스템 카탈로그 뷰 | Description|
| :------ | :----------------------------- |
| [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   | 서버가 데이터베이스 미러링 파트너 역할을 하는 각 모니터 역할에 대한 행을 포함합니다. |
| &nbsp; | &nbsp; |

## <a name="system-dynamic-management-views"></a>시스템 동적 관리 뷰

| 시스템 동적 관리 뷰 | Description|
| :------ | :----------------------------- |
| [sys.dm_db_mirroring_auto_page_repair](../../relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-auto-page-repair.md)   | 서버 인스턴스의 미러된 데이터베이스에 대한 각 자동 페이지 복구 시도당 하나의 행을 반환합니다.  |
| [sys.dm_db_mirroring_connections](../../relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-connections.md)    | 데이터베이스 미러링에 설정된 각 연결에 대해 하나의 행을 반환합니다. |
| &nbsp; | &nbsp; |

## <a name="system-tables"></a>시스템 테이블

| 시스템 테이블 | Description|
| :------ | :----------------------------- |
| [sysdbmaintplan_databases](../../relational-databases/system-tables/sysdbmaintplan-databases-transact-sql.md)   | 데이터베이스 미러링 유지 관리 플랜에 대한 정보를 반환합니다. |
| [sysdbmaintplan_history](../../relational-databases/system-tables/sysdbmaintplan-history-transact-sql.md)    | 데이터베이스 미러링 유지 관리 플랜 기록에 대한 정보를 반환합니다. |
| [sysdbmaintplan_jobs](../../relational-databases/system-tables/sysdbmaintplan-jobs-transact-sql.md)    |데이터베이스 미러링 유지 관리 플랜 작업에 대한 정보를 반환합니다.  |
| [sysdbmaintplans](../../relational-databases/system-tables/sysdbmaintplans-transact-sql.md)    | 데이터베이스 미러링 플랜에 대한 정보를 반환합니다.  |
| &nbsp; | &nbsp; |


## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   

  
  
