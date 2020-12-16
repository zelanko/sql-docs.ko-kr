---
description: 시스템 버전 임시 테이블에서 시스템 버전 관리 중지
title: 시스템 버전 임시 테이블에서 시스템 버전 관리 중지 | Microsoft 문서
ms.custom: ''
ms.date: 04/28/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: dddd707e-bfb1-44ff-937b-a84c5e5d1a94
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c486e78d8cd05d4af130626586e8a9817ab779a1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464494"
---
# <a name="stopping-system-versioning-on-a-system-versioned-temporal-table"></a>시스템 버전 관리 temporal 테이블에서 시스템 버전 관리 중지


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]


temporal 테이블의 버전 관리를 일시적으로나 영구적으로 중지하려는 경우가 있습니다. **SYSTEM_VERSIONING** 절을 **OFF** 로 설정하여 이를 수행할 수 있습니다.

## <a name="setting-system_versioning--off"></a>SYSTEM_VERSIONING = OFF로 설정

temporal 테이블에 대해 특정 유지 관리 작업을 수행하려는 경우 또는 버전이 있는 테이블이 더 이상 필요하지 않은 경우 시스템 버전 관리를 중지합니다. 이 작업을 수행하면 독립적인 테이블 두 개가 생성됩니다.

- 기간이 정의된 현재 테이블

- 기록 테이블(일반 테이블)

### <a name="important-remarks"></a>중요한 주의 사항

- 기록 테이블은 **SYSTEM_VERSIONING = OFF** 기간 동안 업데이트를 **중단** 합니다.
- **SYSTEM_VERSIONING = OFF** 를 설정하거나 **SYSTEM_TIME** 기간을 삭제할 때 **temporal 테이블** 에서 데이터 손실이 발생하지 않습니다.
- **SYSTEM_VERSIONING = OFF** 로 설정하고 **SYSTEM_TIME** 기간을 제거/삭제하지 않으면 시스템은 모든 삽입 및 업데이트 작업에 대해 기간 열을 계속 업데이트합니다. 현재 테이블에서 수행하는 삭제 작업은 영구적인 작업입니다.
- 기간 열을 완전히 제거하려면 **SYSTEM_TIME** 기간을 삭제합니다.
- **SYSTEM_VERSIONING = OFF** 로 설정하면 충분한 권한이 있는 모든 사용자가 기록 테이블의 내용과 스키마를 수정하거나 기록 테이블을 완전히 삭제할 수 있습니다.
- **SYSTEM_TIME** 참조와 같이 임시 쿼리 확장을 사용하여 SCHEMABINDING으로 만든 다른 개체가 있는 경우에는 **SYSTEM_VERSIONING = OFF** 를 설정할 수 없습니다. 이러한 제한은 **SYSTEM_VERSIONING = OFF** 를 설정한 경우 다른 개체가 실패하는 것을 방지합니다.

### <a name="permanently-remove-system_versioning"></a>영구적으로 SYSTEM_VERSIONING 제거

이 예에서는 SYSTEM_VERSIONING을 영구적으로 제거하고 기간 열을 완전히 제거합니다. 기간 열은 필요에 따라 제거하면 됩니다.

```sql
ALTER TABLE dbo.Department SET (SYSTEM_VERSIONING = OFF);
/*Optionally, DROP PERIOD if you want to revert temporal table to a non-temporal*/
ALTER TABLE dbo.Department
DROP PERIOD FOR SYSTEM_TIME;
```

### <a name="temporarily-remove-system_versioning"></a>임시로 SYSTEM_VERSIONING 제거

시스템 버전 관리를 **OFF** 로 설정해야 하는 작업의 목록은 다음과 같습니다.

- 기록에서 불필요한 데이터 제거(**DELETE** 또는 **TRUNCATE**)
- 버전을 관리하지 않고 현재 테이블에서 데이터 제거(**DELETE**, **TRUNCATE**)
- 현재 테이블에서 **SWITCH OUT** 분할
- 기록 테이블로 **SWITCH IN** 분할

이 예에서는 특정 유지 관리 작업을 수행할 수 있도록 SYSTEM_VERSIONING을 임시로 중지합니다. 테이블 유지 관리를 위한 필수 구성 요소로 버전 관리를 임시로 중지하는 경우에는 데이터 일관성을 유지할 수 있도록 트랜잭션 내에서 중지를 수행하는 것이 좋습니다.

> [!NOTE]
> 시스템 버전 관리를 다시 켤 때 HISTORY_TABLE 인수를 지정하는 것을 잊지마세요. 이렇게 하지 않으면 새 기록 테이블이 만들어지고 현재의 테이블과 연결됩니다. 원래 기록 테이블은 여전히 일반 테이블로 존재하지만 현재 테이블과 연결되지는 않습니다.

```sql
BEGIN TRAN
ALTER TABLE dbo.Department SET (SYSTEM_VERSIONING = OFF);
TRUNCATE TABLE [History].[DepartmentHistory]
WITH (PARTITIONS (1,2))
ALTER TABLE dbo.Department SET
(
SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.DepartmentHistory)
);
COMMIT ;
```

## <a name="next-steps"></a>다음 단계

- [임시 테이블](../../relational-databases/tables/temporal-tables.md)
- [시스템 버전 관리 임시 테이블 시작](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [시스템 버전 임시 테이블 만들기](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
- [시스템 버전 임시 테이블의 데이터 수정](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
- [시스템 버전 임시 테이블의 데이터 쿼리](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [시스템 버전 임시 테이블의 스키마 변경](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)
