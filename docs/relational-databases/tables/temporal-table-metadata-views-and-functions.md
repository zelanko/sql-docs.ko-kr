---
title: "임시 테이블 메타데이터 뷰 및 함수 | Microsoft 문서"
ms.custom: 
ms.date: 03/28/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e5d23ec9-7d18-40f6-add4-bea13132d0b9
caps.latest.revision: "9"
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1f1fb41f4c5919f61b4ce3a64d83e8d41de64f29
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="temporal-table-metadata-views-and-functions"></a>임시 테이블 메타데이터 뷰 및 함수
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  
            [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 및 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]에는 관리자가 temporal 테이블에 대한 정보를 검색할 수 있는 다양한 메타베이스 뷰 및 함수가 포함됩니다.  
  
 temporal 테이블에 대한 정보는 다음 메타데이터 뷰에 노출됩니다.  
  
-   [sys.tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)  
  
-   [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
-   [sys.periods&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-periods-transact-sql.md)  
  
 temporal 테이블에 대한 정보는 다음 메타데이터 함수에 노출됩니다.  
  
-   [OBJECTPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)  
  
-   [OBJECTPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
-   [COLUMNPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [임시 테이블](../../relational-databases/tables/temporal-tables.md)   
 [시스템 버전 관리 임시 테이블 시작](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [임시 테이블 시스템 일관성 검사](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [임시 테이블을 사용하여 분할](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [임시 테이블 고려 사항 및 제한 사항](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [임시 테이블 보안](../../relational-databases/tables/temporal-table-security.md)   
 [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)  
  
  
