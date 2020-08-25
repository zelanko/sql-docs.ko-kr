---
description: 시스템 버전 임시 테이블의 스키마 변경
title: 시스템 버전 임시 테이블의 스키마 변경 | Microsoft 문서
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 9dbe5a21-9335-4f8b-85fd-9da83df79946
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 41fde9a9177aab888e7ae06c2d2cce662b2e794b
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646685"
---
# <a name="changing-the-schema-of-a-system-versioned-temporal-table"></a>시스템 버전 관리 temporal 테이블의 스키마 변경


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

**ALTER TABLE** 문을 사용하여 열을 추가, 변경 또는 제거합니다.

## <a name="examples"></a>예제

다음은 temporal 테이블의 스키마를 변경하는 몇 가지 예입니다.

```sql
ALTER TABLE dbo.Department
    ALTER COLUMN DeptName varchar(100);

ALTER TABLE dbo.Department
    ADD WebAddress nvarchar(255) NOT NULL
    CONSTRAINT DF_WebAddress DEFAULT 'www.mycompany.com';

ALTER TABLE dbo.Department
    ADD TempColumn INT;

GO

ALTER TABLE dbo.Department
    DROP COLUMN TempColumn;

/* Setting IsHidden property for period columns.
Use ALTER COLUMN <period_column> DROP HIDDEN to clear IsHidden flag */

ALTER TABLE dbo.Department
    ALTER COLUMN SysStartTime ADD HIDDEN;

ALTER TABLE dbo.Department
    ALTER COLUMN SysEndTime ADD HIDDEN;
```

### <a name="important-remarks"></a>중요한 주의 사항

- temporal 테이블의 스키마를 변경하려면 현재 및 기록 테이블에 대한**CONTROL** 권한이 필요합니다.
- **ALTER TABLE** 작업 중 시스템은 두 테이블에 스키마 잠금을 유지합니다.
- 지정된 스키마 변경은 적절하게 기록 테이블에 전파됩니다(변경 유형에 따라).
- Null을 허용하지 않는 열을 추가하거나 Null을 허용하지 않게 되도록 기존 열을 변경하는 경우 기존 행에 대한 기본값을 지정해야 합니다. 시스템은 동일한 값으로 추가 기본값을 생성하고 기록 테이블에 적용합니다. **DEFAULT** 를 비어 있지 않은 테이블에 추가하는 것은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition 이외의 모든 버전에서 데이터 작업의 크기입니다(메타데이터 작업임).
- 기본값으로 varchar(max), nvarchar(max), varbinary(max) 또는 XML 열을 추가하는 것은 모든 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업데이트 데이터 작업이 됩니다.
- 열 추가 후 행 크기가 행 크기 제한을 초과하는 경우 새 열을 온라인에 추가할 수 없습니다.
- 새 NOT NULL 열로 테이블을 확장한 후 해당 테이블의 모든 열은 시스템에서 자동으로 채워지므로 기록 테이블에 기본 제약 조건을 삭제하는 것이 좋습니다.
- 시스템 버전 관리 temporal 테이블에서는 Online 옵션 (**WITH (ONLINE = ON**)이 **ALTER TABLE ALTER COLUMN** 에 영향을 주지 않습니다. ONLINE 옵션에 지정된 값과 관계없이 열 변경은 온라인으로 수행되지 않습니다.
- **ALTER COLUMN** 을(를) 사용하여 기간 열에 대한 **IsHidden** 속성을 변경할 수 있습니다.
- 다음 스키마 변경에 **ALTER** 을(를) 직접 사용할 수 없습니다. 이러한 종류의 변경은 **SYSTEM_VERSIONING = OFF**를 설정합니다.

  - 계산 열 추가
  - **IDENTITY** 열 추가
  - 기록 테이블이 **DATA_COMPRESSION = PAGE** 또는 **DATA_COMPRESSION = ROW**로 설정된 경우 **SPARSE** 열 추가 또는 **SPARSE**가 되도록 기존 열 변경은 기록 테이블에 대한 기본값입니다.
  - **COLUMN_SET**추가
  - **ROWGUIDCOL** 열 추가 또는 **ROWGUIDCOL**이(가) 되도록 기존 열 변경

다음 예제에서는 설정 **SYSTEM_VERSIONING = OFF** 가 여전히 필요한 스키마 변경을 보여 줍니다( **IDENTITY** 열 추가). 이 예제에서는 데이터 일관성 확인을 사용하지 않도록 설정합니다. 동시 데이터 변경이 발생할 수 없으므로 트랜잭션 내에서 스키마 변경을 수행하는 경우 이 검사는 필요하지 않습니다.

```sql
    BEGIN TRAN
        ALTER TABLE [dbo].[CompanyLocation] SET (SYSTEM_VERSIONING = OFF);
        ALTER TABLE [CompanyLocation] ADD Cntr INT IDENTITY (1,1);
        ALTER TABLE [dbo].[CompanyLocationHistory] ADD Cntr INT NOT NULL DEFAULT 0;
        ALTER TABLE [dbo].[CompanyLocation]
    SET
         (
            SYSTEM_VERSIONING = ON
           ( HISTORY_TABLE = [dbo].[CompanyLocationHistory])
         );
    COMMIT ;
```

## <a name="next-steps"></a>다음 단계

- [Temporal 테이블](../../relational-databases/tables/temporal-tables.md)
 [시스템 버전 관리 temporal 테이블 시작](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [시스템 버전 관리된 임시 테이블에서 기록 데이터의 보존 관리](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [메모리 액세스에 최적화된 테이블을 포함한 시스템 버전 임시 테이블](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)
- [시스템 버전 임시 테이블 만들기](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
- [시스템 버전 임시 테이블의 데이터 수정](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
- [시스템 버전 임시 테이블의 데이터 쿼리](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [시스템 버전 임시 테이블에서 시스템 버전 관리 중지](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)
