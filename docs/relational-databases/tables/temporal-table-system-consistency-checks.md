---
title: 임시 테이블 시스템 일관성 검사 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ec081d42-57e4-43c7-9e1c-317ba8f23437
caps.latest.revision: 10
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c2a7f6ac5747568531410c4edc7674357c236a3
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="temporal-table-system-consistency-checks"></a>임시 테이블 시스템 일관성 검사
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  temporal 테이블을 사용하는 경우 시스템은 다양한 일관성 검사를 수행하여 스키마가 임시 요구 사항에 따라 컴파일되고 데이터가 일관적이며 일관성을 유지함을 보장할 수 있습니다. 또한, **DBCC CHECKCONSTRAINTS** 문에 임시 검사가 추가되었습니다.  
  
## <a name="system-consistency-checks"></a>시스템 일관성 검사  
 **SYSTEM_VERSIONING** 을 **ON**으로 설정하기 전에 기록 테이블 및 현재 테이블에서 일련의 검사가 수행됩니다. 이러한 검사는 스키마 검사 및 데이터 검사로 그룹화됩니다(기록 테이블이 비어 있지 않은 경우). 또한, 시스템은 런타임 일관성 검사를 수행합니다.  
  
### <a name="schema-check"></a>스키마 검사  
 temporal 테이블을 만들거나 테이블을 변경하여 temporal 테이블로 변경할 때 시스템은 다음 요구 사항의 충족 여부를 확인합니다.  
  
1.  열 이름 및 개수가 현재 테이블 및 기록 테이블에서 동일합니다.  
  
2.  데이터 유형이 현재 테이블과 기록 테이블 사이에 있는 각 열에 일치합니다.  
  
3.  기간 열이 **NOT NULL**(으)로 설정됩니다.  
  
4.  현재 테이블에 기본 키 제약 조건이 있고 기록 키에 기본 키 제약 조건이 없습니다.  
  
5.  기록 테이블에는 **IDENTITY** 열이 정의되지 않습니다.  
  
6.  기록 테이블에는 트리거가 정의되지 않습니다.  
  
7.  기록 테이블에는 외래 키가 정의되지 않습니다.  
  
8.  기록 테이블에는 테이블 또는 열 제약 조건이 정의되지 않습니다. 그러나 기록 테이블의 기본 열 값은 허용되지 않습니다.  
  
9. 기록 테이블은 읽기 전용 파일 그룹에 배치되지 않습니다.  
  
10. 기록 테이블은 변경 추적 또는 변경 데이터 캡처를 위해 구성되지 않습니다.  
  
### <a name="data-consistency-check"></a>병렬 일관성 검사  
 **SYSTEM_VERSIONING** 을 **ON** 으로 설정하고 DML 작업의 일부로 설정하기 전에 시스템은 **SysEndTime** ≥**SysStartTime**검사를 수행합니다.  
  
 기존 기록 테이블에 대한 링크를 만드는 경우 데이터 일관성 검사를 수행하도록 선택할 수 있습니다. 이 데이터 일관성 검사는 기존 레코드가 겹치지 않고 모든 개별 레코드에서 임시 요구 사항이 충족되는지 확인합니다. 기본값은 데이터 일관성 검사를 수행하는 것입니다. 일반적으로 기록 데이터로 채워지는 기존 기록 테이블을 통합하는 경우와 같이 현재 테이블과 기록 테이블 사이에서 데이터 동기화가 이루어지지 않을 때마다 데이터 일관성을 검사하는 것이 좋습니다.  
  
> [!WARNING]  
>  시스템 클록을 수동으로 변경하면 겹침 상태(득, 레코드의 종료 시간이 시작 시간 이전이 아님)가 실패하는 것을 방지하기 위해 런타임 데이터 일관성 검사가 수행되어 시스템이 예기치 않게 실패할 수 있습니다.  
  
## <a name="dbcc-checkconstraints"></a>DBCC CHECKCONSTRAINTS  
 **DBCC CHECKCONSTRAINTS** 명령에는 임시 데이터 일관섬 검사가 포함됩니다. 자세한 내용은 [DBCC CHECKCONSTRAINTS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [임시 테이블](../../relational-databases/tables/temporal-tables.md)   
 [시스템 버전 관리 임시 테이블 시작](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [임시 테이블을 사용하여 분할](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [임시 테이블 고려 사항 및 제한 사항](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [임시 테이블 보안](../../relational-databases/tables/temporal-table-security.md)   
 [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [임시 테이블 메타데이터 뷰 및 함수](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
