---
title: 시퀀스 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 12/30/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SEQUENCES
- SEQUENCES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SEQUENCES view
- INFORMATION_SCHEMA.SEQUENCES view
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5ad17bb63dc60accb220799d62a81e625f20d5c7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716614"
---
# <a name="sequences-transact-sql"></a>시퀀스 (Transact-sql)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

현재 데이터베이스에서 현재 사용자가 액세스할 수 있는 각 시퀀스에 대해 하나의 행을 반환 합니다.

이러한 뷰에서 정보를 검색 하려면 **INFORMATION_SCHEMA**의 정규화 된 이름을 지정_view_name_합니다.

|열 이름|데이터 형식|Description|
|-----------------|---------------|-----------------|
|**SEQUENCE_CATALOG**|**nvarchar(128)**|시퀀스 한정자|
|**SEQUENCE_SCHEMA**|**nvarchar (** 128) * *|시퀀스를 포함 하는 스키마의 이름입니다.|
|**SEQUENCE_NAME**|**nvarchar(128)**|시퀀스 이름|
|**DATA_TYPE**|**nvarchar (** 128 **)**|Sequence 데이터 형식입니다.|
|**NUMERIC_PRECISION**|**tinyint**|시퀀스의 전체 자릿수입니다.|
|**NUMERIC_PRECISION_RADIX**|**smallint**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 전체 자릿수 기수입니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|
|**NUMERIC_SCALE**|**int**|근사 숫자 데이터, 정확한 숫자 데이터, 정수 데이터 또는 통화 데이터의 소수 자릿수입니다. 다른 데이터 형식에 대해서는 NULL이 반환됩니다.|
|**START_VALUE**|**int**|시퀀스 개체가 반환할 첫 번째 값입니다.|
|**MINIMUM_VALUE**|**int**|시퀀스 개체의 범위입니다. 새 시퀀스 개체의 기본 최소값은 해당 시퀀스 개체의 데이터 형식에 대한 최소값입니다. tinyint 형식에 대해서는 0이고 다른 모든 데이터 형식에 대해서는 음수입니다.|
|**MAXIMUM_VALUE**|**int**|시퀀스 개체의 범위입니다. 새 시퀀스 개체의 기본 최대값은 해당 시퀀스 개체의 데이터 형식에 대한 최대값입니다.|
|**씩**|**int**|각각의 NEXT VALUE FOR 함수 호출에 대해 시퀀스 개체의 값을 증가시키거나 감소시키는(음수인 경우) 데 사용되는 값입니다. 증가값이 음수이면 시퀀스 개체가 내림차순이고, 그렇지 않으면 오름차순입니다. 증가값은 0일 수 없습니다. 새 시퀀스 개체의 기본 증가분은 1입니다.
|**CYCLE_OPTION**|**int**|시퀀스 개체를 최소값 또는 최대값(내림차순 시퀀스 개체의 경우)에서 다시 시작해야 하는지, 아니면 최소값 또는 최대값을 초과하는 경우 예외를 발생시켜야 하는지를 지정하는 속성입니다. 새 시퀀스 개체의 기본 순환 옵션은 NO CYCLE입니다.
|**DECLARED_DATA_TYPE**|**int**|사용자 정의 데이터 형식에 대 한 데이터 형식입니다.|
|**DECLARED_DATA_PRECISION**|**int**|사용자 정의 데이터 형식의 전체 자릿수입니다.|
|**DECLARED_NUJMERIC_SCALE**|**int**|사용자 정의 데이터 형식의 소수 자릿수입니다.|

**예** 다음 예에서는 테스트 데이터베이스의 스키마에 대 한 정보를 반환 합니다.

```sql
SELECT * FROM test.INFORMATION_SCHEMA.SEQUENCES;
```

## <a name="see-also"></a>참고 항목

- [Transact-sql&#41;&#40;정보 스키마 뷰](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)
- [sys.sequences&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)
