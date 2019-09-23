---
title: 메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블 | Microsoft 문서
ms.custom: ''
ms.date: 07/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 23274522-e5cf-4095-bed8-bf986d6342e0
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b66b63e0667cdb7c12e8675ce935ddc9b69d8bed
ms.sourcegitcommit: d1bc0dd1ac626ee7034a36b81554258994d72c15
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70958325"
---
# <a name="system-versioned-temporal-tables-with-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [메모리 최적화 테이블](../../relational-databases/in-memory-oltp/memory-optimized-tables.md) 에 대한 시스템 버전 temporal 테이블은 메모리 내 OLTP 작업으로 수집한 데이터 위에 [데이터 감사 및 특정 시간 분석](https://msdn.microsoft.com/library/mt631669.aspx) 이 필요한 시나리오에 대해 비용 효율적인 솔루션을 제공하기 위한 것입니다. 이는 높은 트랜잭션 처리량, 잠금 없는 동시성 및 동시에 쉽게 쿼리할 수 있는 대량의 기록 데이터를 저장하는 기능을 제공합니다.  
  
## <a name="overview"></a>개요

 시스템 버전 temporal 테이블은 자동으로 데이터 변경 내용에 대한 전체 기록을 유지하며 특정 시간 분석에 대해 편리한 TRANSACT-SQL 확장을 적용합니다. 일반적인 시나리오에서는 데이터 기록이 정기적으로 쿼리되지 않더라도 매우 긴 시간(여러 달, 심지어 수 년) 동안 보존됩니다.  
  
 데이터 감사 및 시간 기반 분석은 서로 다른 환경, 특히 매우 많은 수의 요청을 처리하는 OLTP 시스템에서, 그리고 메모리 내 OLTP 기술을 사용하는 경우에 필요할 수 있습니다. 그러나 메모리 최적화 테이블을 임시 시나리오에 사용하는 것은 일반적으로 막대한 양의 기록 데이터가 생성되어 사용 가능 RAM 메모리의 한계를 초과하기 때문에 어려울 수 있습니다. 동시에 자주 액세스하지 않아서 오래된 읽기 전용 기록 데이터를 RAM에 저장하는 것은 최적의 솔루션이 아닙니다.  
  
 메모리 최적화 테이블에 관한 시스템 버전 관리 temporal 테이블은 높은 트랜잭션 처리량, 잠금 없는 동시성 및 동시에 현재 데이터(temporal 테이블)에 메모리 내 테이블을 사용하고 기록 데이터에 디스크 기반 테이블을 사용하여 대량의 기록 데이터를 저장하는 기능을 제공합니다. DML 작업에 미치는 영향은 최근 기록을 저장하고 고유하게 컴파일된 코드에서 DML을 실행할 수 있도록 하는 내부의 자동 생성된 메모리 최적화 문자열 테이블을 사용하면 최소화됩니다.  
  
 다음 다이어그램은 이 아키텍처를 보여 줍니다.![임시 메모리 내 아키텍처](../../relational-databases/tables/media/temporal-in-memory-architecture.png "Temporal In-Memory Architecture")  
  
## <a name="implementation-details"></a>구현 정보

 메모리 최적화 테이블을 포함한 시스템 버전 관리 temporal 테이블에 관한 다음 사실은 시스템 버전 관리 메모리 최적화 테이블을 만들 때 주의해야 하는 고려사항입니다. 구문 옵션 및 예제는 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)을 참조하세요.  
  
- 내구성 있는 메모리 최적화 테이블만이 시스템 버전 관리가 가능합니다(**DURABILITY = SCHEMA_AND_DATA**).  
  
- 메모리 최적화 시스템 버전 관리 테이블에 대한 기록 테이블은 만든 주체가 최종 사용자이든 또는 시스템이든 상관없이 디스크 기반이어야 합니다.  
  
- 현재 테이블(메모리 내)에만 영향을 주는 쿼리를 [고유하게 컴파일된 T-SQL 모듈](https://msdn.microsoft.com/library/dn133184.aspx)에서 사용할 수 있습니다. FOR SYSTEM TIME 절을 사용하는 임시 쿼리는 고유하게 컴파일된 모듈에서 지원되지 않습니다. 임시 쿼리 및 비네이티브 모듈에서 메모리 최적화 테이블이 포함된 FOR SYSTEM TIME 절을 사용할 수 있습니다.  
  
- **SYSTEM_VERSIONING = ON**의 경우, 메모리 최적화 현재 테이블에 대한 업데이트 및 삭제 연산의 결과인 최근 시스템 버전 관리 변경 내용을 수용하기 위해 메모리 최적화 준비 테이블이 자동으로 생성됩니다.  
  
- 내부 메모리 최적화 준비 테이블의 데이터는 비동기 데이터 플러시 태스크에 의해 정기적으로 디스크 기반 기록 테이블로 이동됩니다. 이 데이터 플러시 메커니즘의 목표는 내부 메모리 버퍼를 상위 개체의 메모리 소비량의 10% 미만으로 유지하는 것입니다. [sys.dm_db_xtp_memory_consumers&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-memory-consumers-transact-sql.md)를 쿼리하고 메모리 최적화 준비 테이블 및 현재 temporal 테이블에 대한 데이터를 요약하면 메모리 최적화 시스템 버전 관리 temporal 테이블의 총 메모리 소비량을 추적할 수 있습니다.  
  
- [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md)를 호출하면 데이터 플러시를 적용할 수 있습니다.  
  
- **SYSTEM_VERSIONING = OFF** 의 경우 또는 시스템 버전 관리 테이블의 스키마가 열 추가, 삭제 또는 변경에 의해 수정된 경우 내부 준비 버퍼의 전체 내용이 디스크 기반 기록 테이블로 이동됩니다.  
  
- 기록 데이터 쿼리는 결과적으로 스냅샷 격리 수준 아래에 있으며 언제나 메모리 내 준비 버퍼와 디스크 기반 테이블 사이의 합집합을 중복 없이 반환합니다.
  
- 내부적으로 테이블 스키마를 변경하는**ALTER TABLE** 작업은 작업 기간이 오래 걸릴 수 있는 데이터 플래시를 수행해야 합니다.  
  
## <a name="the-internal-memory-optimized-staging-table"></a>내부 메모리 액세스에 최적화된 준비 테이블

 내부 메모리 최적화 준비 테이블은 DML 작업을 최적화하기 위해 시스템에 의해 생성된 내부 개체입니다.  
  
- 테이블 이름은 **Memory_Optimized_History_Table_<object_id>** 형식으로 생성됩니다. 여기서 *<object_id>* 는 현재 temporal 테이블의 ID입니다.  
  
- 테이블은 현재 temporal 테이블에 BIGINT 열 한 개를 더한 스키마를 복제합니다. 이 추가 열은 내부 기록 버퍼로 이동되는 행의 고유성을 보장합니다.  
  
- 추가 열 이름의 형식은 **Change_ID[_< suffix>]** 입니다. 여기서 *_\<suffix>* 는 테이블에 *Change_ID* 열이 이미 있는 경우에 선택적으로 추가됩니다.  
  
- 시스템 버전 관리 메모리 최적화 테이블에 대한 최대 행 크기는 준비 테이블의 추가 BIGINT 열 때문에 8 바이트만큼 감소합니다. 새 최대값은 이제 8052 바이트입니다.  
  
- 내부 메모리 최적화 준비 테이블은 SQL Server Management Studio의 개체 탐색기에 표시되지 않습니다.  
  
- 이 테이블에 관한 메타데이터뿐만 아니라 현재 temporal 테이블과의 연결도 [sys.internal_tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-tables-transact-sql.md)에서 찾을 수 있습니다.  
  
## <a name="the-data-flush-task"></a>데이터 플러시 작업

 데이터 플러시는 메모리 최적화 테이블이 메모리 크기 기반 데이터 이동 조건을 만족하는지 여부를 검사하는 정기적으로 활성화되는 태스크입니다. 데이터 이동은 내부 준비 테이블의 메모리 소비량이 현재 temporal 테이블의 메모리 소비량의 8%에 도달할 때 시작됩니다.  
  
 데이터 플러시 작업은 기존 작업을 기반으로 변화하는 일정을 사용하여 정기적으로 활성화됩니다. 매 5초마다 자주 수행되는 많은 작업 및 매 1분마다 가끔 수행되는 적은 작업의 경우. 정리가 필요한 각 내부 메모리 최적화 준비 테이블에 대해 스레드 한 개가 생성됩니다.  
  
 데이터 플러시는 현재 실행 중인 가장 오래된 트랜잭션보다 더 오래된 메모리 내 내부 버퍼의 모든 레코드를 삭제하여 이러한 레코드를 디스크 기반 기록 테이블로 이동합니다.  
  
 **sys.sp_xtp_flush_temporal_history@schema_name, @object_name**과 같이 [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md)를 호출하고 스키마 및 테이블 이름을 지정하여 데이터 플러시를 적용할 수 있습니다. 이 사용자 실행 명령을 사용하면 내부 일정에 따라 시스템에 의해 데이터 플러시 태스크를 호출할 때와 같은 데이터 이동 프로세스가 호출됩니다.  
  
## <a name="see-also"></a>참고 항목

- [임시 테이블](../../relational-databases/tables/temporal-tables.md)
- [시스템 버전 관리 임시 테이블 시작](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [임시 테이블 사용 시나리오](../../relational-databases/tables/temporal-table-usage-scenarios.md)
- [임시 테이블 시스템 일관성 검사](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [임시 테이블을 사용하여 분할](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [임시 테이블 고려 사항 및 제한 사항](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [임시 테이블 보안](../../relational-databases/tables/temporal-table-security.md)
- [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [임시 테이블 메타데이터 뷰 및 함수](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
