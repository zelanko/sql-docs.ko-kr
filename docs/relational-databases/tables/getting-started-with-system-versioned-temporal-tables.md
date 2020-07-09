---
title: 시스템 버전 관리 임시 테이블 시작 | Microsoft 문서
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: d431f216-82cf-4d97-825e-bb35d3d53a45
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bed32b21fe1e6c249c6de30779c28d0350e2a639
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85977222"
---
# <a name="getting-started-with-system-versioned-temporal-tables"></a>시스템 버전 관리 temporal 테이블 시작

[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

시나리오에 따라 새 시스템 버전 관리 temporal 테이블을 만들 수도 있고 기존 테이블 스키마에 임시 특성을 추가하여 기존 테이블을 수정할 수도 있습니다. temporal 테이블의 데이터를 수정하면 시스템은 애플리케이션과 최종 사용자는 확인할 수 없는 버전 기록을 작성합니다. 따라서 시스템 버전 temporal 테이블 작업 시에는 테이블이 수정되는 방식이나 데이터의 최신(실제) 상태를 쿼리하는 방법을 변경할 필요가 없습니다.

임시 테이블에서는 일반적인 DML 및 쿼리 기능뿐 아니라, 확장된 Transact-SQL 구문을 통해 데이터 기록에서 정보를 확인하는 편리하고 간편한 방법도 제공합니다. 모든 시스템 버전 테이블에는 기록 테이블이 할당되어 있습니다. 그러나 사용자가 추가 인덱스를 만들거나 다른 스토리지 옵션을 선택하여 작업 성능 또는 스토리지 공간을 최적화하려는 경우가 아니면 이 테이블은 사용자에게 전혀 표시되지 않습니다.

아래 다이어그램에는 시스템 버전 관리 temporal 테이블의 일반적인 워크플로가 나와 있습니다. ![임시 시작하기](../../relational-databases/tables/media/getting-started-with-temporal.png "Temporal 시작")

이 항목은 다음의 5개 하위 항목으로 이루어져 있습니다.

- [시스템 버전 임시 테이블 만들기](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
- [시스템 버전 임시 테이블의 데이터 수정](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
- [시스템 버전 임시 테이블의 데이터 쿼리](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [시스템 버전 임시 테이블의 스키마 변경](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)
- [시스템 버전 임시 테이블에서 시스템 버전 관리 중지](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)

## <a name="next-steps"></a>다음 단계

- [임시 테이블](../../relational-databases/tables/temporal-tables.md)
- [임시 테이블 시스템 일관성 검사](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [임시 테이블을 사용하여 분할](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [임시 테이블 고려 사항 및 제한 사항](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [임시 테이블 보안](../../relational-databases/tables/temporal-table-security.md)
- [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [임시 테이블 메타데이터 뷰 및 함수](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
