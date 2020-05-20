---
title: 시스템 테이블 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server]
- tables [SQL Server], system tables
- information retrieval [SQL Server]
- status information [SQL Server], system tables
- system information [SQL Server]
- system tables [SQL Server]
- system tables [SQL Server], about system tables
- system tables [SQL Server], retrieving information from
- retrieving system table information
ms.assetid: 56b8ad51-930c-4e5c-8d99-8c939d5b70ac
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 62343279fafbfce00376c34bd8398ebcacfeb7d9
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82803087"
---
# <a name="system-tables-transact-sql"></a>시스템 테이블(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 섹션의 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 시스템 테이블에 대해 설명합니다.  
  
 사용자는 시스템 테이블을 직접 변경해서는 안 됩니다. 예를 들어 DELETE, UPDATE 또는 INSERT 문이나 사용자 정의 트리거를 사용하여 시스템 테이블을 수정하려고 시도하지 마십시오.  
  
 시스템 테이블에서 문서화된 열의 참조는 허용됩니다. 그러나 시스템 테이블의 열은 대부분 문서화되어 있지 않습니다. 애플리케이션이 문서화되지 않은 열을 직접 쿼리하도록 작성해서는 안됩니다. 대신 애플리케이션은 시스템 테이블에 저장된 정보를 검색하기 위해 다음 구성 요소 중 하나를 사용해야 합니다.  
  
-   시스템 저장 프로시저  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 및 함수  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMO(Management Objects)(!!)  
  
-   RMO(복제 관리 개체)  
  
-   데이터베이스 API 카탈로그 함수  
  
 이러한 구성 요소는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 시스템 정보를 가져오기 위해 게시된 API를 구성합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)]는 이러한 구성 요소의 릴리스 간 호환성을 유지합니다. 시스템 테이블의 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 내부 아키텍처에 따라 달라지며 릴리스에 따라 변경될 수 있습니다. 따라서 시스템 테이블의 문서화되지 않은 열을 직접 액세스하는 애플리케이션은 상위 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 액세스하기 전에 변경되어야 할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 시스템 테이블 항목은 다음 기능 영역에 의해 구성됩니다.  
  
|||  
|-|-|  
|[Transact-sql&#41;&#40;테이블 백업 및 복원](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)|[로그 전달 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-tables-transact-sql.md)|  
|[변경 데이터 캡처 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/change-data-capture-tables-transact-sql.md)|[복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)|  
|[Transact-sql&#41;의 데이터베이스 유지 관리 계획 테이블 &#40;](../../relational-databases/system-tables/database-maintenance-plan-tables-transact-sql.md)|[Transact-sql&#41;&#40;테이블 SQL Server 에이전트](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)|  
|[SQL Server 확장 이벤트 테이블&#40;Transact-SQL&#41;](../../relational-databases/extended-events/xevents-references-system-objects.md#system-tables)|[sysoledbusers &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-sysoledbusers-transact-sql.md)|  
|[Transact-sql&#41;&#40;테이블 Integration Services](../../relational-databases/system-tables/integration-services-tables-transact-sql.md)|[systranschemas &#40;Transact-sql&#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;호환성 뷰](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
