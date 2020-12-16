---
title: 메모리 내 OLTP에 지원되는 데이터 형식 | Microsoft Docs
description: 최적화 테이블 및 고유하게 컴파일된 T-SQL 모듈의 메모리 내 OLTP 기능에 지원되지 않는 데이터 형식에 대해 알아봅니다.
ms.custom: ''
ms.date: 06/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cdbcd80b0cb369607dc7b38cc524f53fdaed3a79
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97485155"
---
# <a name="supported-data-types-for-in-memory-oltp"></a>메모리 내 OLTP에 지원되는 데이터 형식
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  이 문서에서는 다음 항목의 메모리 내 OLTP 기능에 대해 지원되지 않는 데이터 형식을 소개합니다.  
  
-   메모리 최적화 테이블  
  
-   고유하게 컴파일된 T-SQL 모듈  
  
## <a name="unsupported-data-types"></a>지원되지 않는 데이터 형식  
 다음 데이터 형식은 지원되지 않습니다.  

:::row:::
    :::column:::
        [datetimeoffset&#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)

        [hierarchyid&#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)

        [sql_variant&#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)
    :::column-end:::
    :::column:::
        [geography&#40;Transact-SQL&#41;](../../t-sql/spatial-geography/spatial-types-geography.md)

        [rowversion&#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md)

        사용자 정의 형식
    :::column-end:::
    :::column:::
        [geometry&#40;Transact-SQL&#41;](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md)

        [xml&#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md)
    :::column-end:::
:::row-end:::
  
## <a name="notable-supported-data-types"></a>지원되는 주요 데이터 형식  
 메모리 내 OLTP의 대다수 기능은 대부분의 데이터 형식을 지원합니다. 지원되는 몇 가지 주요 데이터 형식은 다음과 같습니다.  
  
|문자열 및 이진 유형|참조 항목|  
|-----------------------------|--------------------------|  
|binary 및 varbinary*|[binary 및 varbinary&#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|char 및 varchar*|[char 및 varchar&#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|nchar 및 nvarchar*|[nchar 및 nvarchar&#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
  
위의 문자열 및 이진 데이터 형식의 경우 SQL Server 2016부터는 다음 사항이 적용됩니다.  
  
- 메모리 최적화 개별 테이블은 `nvarchar(4000)` 등의 긴 열을 여러 개 포함할 수도 있습니다. 이러한 열의 길이로 인해 실제 행 크기가 8060바이트보다 커지더라도 포함이 가능합니다.  
  
- 메모리 최적화 테이블은 `varchar(max)`와 같은 데이터 형식의 이진 열과 최대 길이 문자열을 포함할 수 있습니다.  


### <a name="identify-lobs-and-other-columns-that-are-off-row"></a>LOB 및 기타 행 외부 열 식별

SQL Server 2016부터는 메모리 최적화 테이블이 [행 외부 열을 지원](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)하여, 단일 테이블 행이 8060바이트보다 클 수 있습니다. 다음 Transact-SQL SELECT 문은 메모리 최적화 테이블에 대한 모든 행 외부 열을 보고합니다. 다음 사항에 유의하세요.

- 모든 인덱스 키 열은 행에 저장됩니다.
  - 이제 메모리 최적화 테이블에서 고유하지 않은 인덱스 키에 NULLable 열을 포함할 수 있습니다.
  - 인덱스는 메모리 최적화 테이블에서 UNIQUE로 선언할 수 있습니다.
- 모든 LOB 열은 행 외부에 저장됩니다.
- max_length가 -1이면 LOB(Large Object) 열을 나타냅니다.


```sql
SELECT
        OBJECT_NAME(m.object_id) as [table],
        c.name                   as [column],
        c.max_length
    FROM
             sys.memory_optimized_tables_internal_attributes AS m
        JOIN sys.columns                                     AS c
                ON  m.object_id = c.object_id
                AND m.minor_id  = c.column_id
    WHERE
        m.type = 5;
```


### <a name="other-data-types"></a>기타 데이터 형식


|기타 유형|참조 항목|  
|-----------------|--------------------------|  
|테이블 형식|[메모리 액세스에 최적화된 테이블 변수](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)|  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP에 대한 Transact-SQL 지원](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   
 [메모리 액세스에 최적화된 테이블에서 SQL_VARIANT 구현](../../relational-databases/in-memory-oltp/implementing-sql-variant-in-a-memory-optimized-table.md)  
 [메모리 최적화 테이블의 테이블 및 행 크기](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
  
