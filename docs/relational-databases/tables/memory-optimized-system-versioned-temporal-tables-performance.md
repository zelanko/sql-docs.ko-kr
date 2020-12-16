---
description: 메모리 액세스에 최적화된 시스템 버전 관리 임시 테이블 성능
title: 메모리 액세스에 최적화된 시스템 버전 관리 임시 테이블 성능 | Microsoft 문서
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 2e110984-7703-4806-a24b-b41e8c3018c6
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6a81d2b397418a934e51a7e9e0f8491d10e0cdba
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462594"
---
# <a name="memory-optimized-system-versioned-temporal-tables-performance"></a>메모리 액세스에 최적화된 시스템 버전 관리 임시 테이블 성능


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]


이 항목에서는 시스템 버전 메모리 최적화 temporal 테이블을 사용할 때 고려해야 하는 몇 가지 성능 관련 사항에 대해 설명합니다.

- 기록 테이블은 자동으로 업데이트되므로 기존의 비temporal 테이블에 시스템 버전 지정 기능을 추가하면 업데이트 및 삭제 작업의 성능에 영향을 줄 수 있습니다.
- 모든 업데이트 및 삭제 작업은 내부의 메모리 최적화 테이블에 기록되므로 작업 시 업데이트와 삭제를 많이 수행하는 경우 메모리가 예상보다 많이 사용될 수 있습니다. 그러므로 다음 규칙을 따르는 것이 좋습니다.

  - 공간을 정리하여 사용 가능한 RAM을 늘리기 위해 현재 테이블에서 많은 삭제를 수행하지 않습니다. [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md)를 호출하거나 **SYSTEM_VERSIONING = OFF** 로 설정한 상태로 데이터를 여러 번의 일괄 처리로 삭제하고 각 일괄 처리 사이에 수동으로 호출한 데이터 플러시를 수행하는 것이 좋습니다.
  - 대량 테이블 업데이트를 동시에 수행하지 마세요. 비임시 메모리 최적화 테이블을 업데이트하는 데 필요한 메모리 양보다 메모리가 두 배 더 사용될 수 있습니다. 이처럼 메모리 사용량이 두 배 증가하는 것은 일시적인 현상입니다. 내부 준비 테이블의 메모리 사용량을 안정적 상태의 예상 메모리 사용량 경계(현재 temporal 테이블 메모리 사용량의 약 10%) 이내로 유지하기 위해 데이터 플러시 작업이 정기적으로 수행되기 때문입니다. 업데이트를 통해 새로 추가된 열의 기본값 설정 등의 대량 업데이트를 수행하는 경우 일괄 처리를 여러 번 진행하거나 **SYSTEM_VERSIONING = OFF** 로 설정한 상태로 업데이트하는 것이 좋습니다.

- 데이터 플러시 태스크의 활성화 기간은 구성할 수 없지만, [sp_xtp_flush_temporal_history](../../relational-databases/system-stored-procedures/temporal-table-sp-xtp-flush-temporal-history.md)로 설정한 상태로 데이터를 여러 번의 일괄 처리로 삭제하고 각 일괄 처리 사이에 수동으로 호출한 데이터 플러시를 수행하는 것이 좋습니다.
- 특히 집계 함수나 기간 이동 함수를 사용하는 분석 쿼리를 기록 데이터에 대해 실행하려는 경우에는 디스크 기반 기록 테이블용 스토리지 옵션으로 클러스터형 columnstore를 사용하는 것이 좋습니다. 클러스터형 columnstore는 효율적인 데이터 압축 기능을 제공하며 기록 데이터가 생성되는 방식에 적합한 삽입 중심 방식으로 동작하므로 이러한 경우 기록 테이블에 사용하면 효율적인 옵션입니다.

## <a name="see-also"></a>참고 항목

- [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [메모리 액세스에 최적화된 시스템 버전 임시 테이블 만들기](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)
- [메모리 액세스에 최적화된 시스템 버전 임시 테이블로 작업](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)
- [메모리 액세스에 최적화된 시스템 버전 임시 테이블 모니터링](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)
- [임시 테이블](../../relational-databases/tables/temporal-tables.md)
- [임시 테이블 시스템 일관성 검사](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [임시 테이블 메타데이터 뷰 및 함수](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
