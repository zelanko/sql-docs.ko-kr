---
title: "메모리 내 OLTP에 지원되는 데이터 형식 | Microsoft 문서"
ms.custom: 
ms.date: 05/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a928c1f77586198fd0d33cafa445ea406a437c6b
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="supported-data-types-for-in-memory-oltp"></a>메모리 내 OLTP에 지원되는 데이터 형식
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  이 문서에서는 다음 항목의 메모리 내 OLTP 기능에 대해 지원되지 않는 데이터 형식을 소개합니다.  
  
-   메모리 액세스에 최적화된 테이블  
  
-   고유하게 컴파일된 저장 프로시저  
  
## <a name="unsupported-data-types"></a>지원되지 않는 데이터 형식  
 다음 데이터 형식은 지원되지 않습니다.  
  
||||  
|-|-|-|  
|[datetimeoffset&#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)|[geography&#40;Transact-SQL&#41;](../../t-sql/spatial-geography/spatial-types-geography.md)|[geometry&#40;Transact-SQL&#41;](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md)|  
|[hierarchyid&#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)|[rowversion&#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md)|[xml&#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md)|  
|[sql_variant&#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)|사용자 정의 형식|.|  
  
## <a name="notable-supported-data-types"></a>지원되는 주요 데이터 형식  
 메모리 내 OLTP의 대다수 기능은 대부분의 데이터 형식을 지원합니다. 지원되는 몇 가지 주요 데이터 형식은 다음과 같습니다.  
  
|문자열 및 이진 유형|참조 항목|  
|-----------------------------|--------------------------|  
|binary 및 varbinary*|[binary 및 varbinary&#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|char 및 varchar*|[char 및 varchar&#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|nchar 및 nvarchar*|[nchar 및 nvarchar&#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
  
위의 문자열 및 이진 데이터 형식의 경우 SQL Server 2016부터는 다음 사항이 적용됩니다.  
  
- 메모리 액세스에 최적화된 개별 테이블은 `nvarchar(4000)`등의 긴 열을 여러 개 포함할 수도 있습니다. 이러한 열의 길이로 인해 실제 행 크기가 8060바이트보다 커지더라도 포함이 가능합니다.  
  
- 메모리 액세스에 최적화된 테이블은 `varchar(max)`와 같은 데이터 형식의 이진 열과 최대 길이 문자열을 포함할 수 있습니다.  


### <a name="identify-lobs-and-other-columns-that-are-off-row"></a>LOB 및 기타 행 외부 열 식별

다음 Transact-SQL SELECT 문은 메모리 액세스에 최적화된 테이블에 대한 모든 행 외부 열을 보고합니다. 다음을 참고하십시오.

- 모든 인덱스 키 열은 행에 저장됩니다.
  - 이제 메모리 액세스에 최적화된 테이블에서 고유하지 않은 인덱스 키에 NULLable 열을 포함할 수 있습니다.
  - 인덱스는 메모리 액세스에 최적화된 테이블에서 UNIQUE로 선언할 수 있습니다.
- 모든 LOB 열은 행 외부에 저장됩니다.
- max_length가 -1이면 LOB(Large Object) 열을 나타냅니다.


```tsql
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


#### <a name="natively-compiled-modules-support-for-lobs"></a>LOB에 대해 고유하게 컴파일된 모듈 지원


고유하게 컴파일된 모듈에서 기본 프로시저 등의 기본 제공 문자열 함수를 사용할 경우 함수에서 LOB 형식을 사용할 수 있습니다. 예를 들어 기본 프로시저 LTrim 함수는 nvarchar(max) 또는 varbinary(max) 형식의 매개 변수를 입력할 수 있습니다.

또한 이러한 LOB는 고유하게 컴파일된 스칼라 UDF(사용자 정의 함수)의 반환 형식이 될 수 있습니다.


### <a name="other-data-types"></a>기타 데이터 형식


|기타 유형|참조 항목|  
|-----------------|--------------------------|  
|테이블 형식|[메모리 액세스에 최적화된 테이블 변수](http://msdn.microsoft.com/library/bd102e95-53e2-4da6-9b8b-0e4f02d286d3)|  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP에 대한 Transact-SQL 지원](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   
 [메모리 액세스에 최적화된 테이블에서 LOB 열 구현](http://msdn.microsoft.com/en-us/bd8df0a5-12b9-4f4c-887c-2fb78dd79f4e)   
 [메모리 액세스에 최적화된 테이블에서 SQL_VARIANT 구현](../../relational-databases/in-memory-oltp/implementing-sql-variant-in-a-memory-optimized-table.md)  
  
  

