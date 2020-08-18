---
description: CHECKSUM_AGG(Transact-SQL)
title: CHECKSUM_AGG(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHECKSUM_AGG
- CHECKSUM_AGG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- checksum values
- CHECKSUM_AGG function
- groups [SQL Server], checksum values
ms.assetid: cdede70c-4eb5-4c92-98ab-b07787ab7222
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6190b42e9e52f9f20e9ad645c0169f08dc7694a7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88311129"
---
# <a name="checksum_agg-transact-sql"></a>CHECKSUM_AGG(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

이 함수는 그룹에 있는 값의 체크섬을 반환합니다. `CHECKSUM_AGG`는 Null 값을 무시합니다. [OVER 절](../../t-sql/queries/select-over-clause-transact-sql.md)은 `CHECKSUM_AGG` 다음에 올 수 있습니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CHECKSUM_AGG ( [ ALL | DISTINCT ] expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
**ALL**  
모든 값에 집계 함수를 적용합니다. 기본 인수는 ALL입니다.
  
DISTINCT  
`CHECKSUM_AGG`가 고유한 값의 체크섬을 반환하도록 지정합니다.
  
*expression*  
정수 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. `CHECKSUM_AGG`에서는 집계 함수 또는 하위 쿼리를 사용할 수 없습니다.
  
## <a name="return-types"></a>반환 형식
모든 *expression* 값의 체크섬을 **int**로 반환합니다.
  
## <a name="remarks"></a>설명  
`CHECKSUM_AGG`는 테이블의 변경 내용을 감지할 수 있습니다.
  
`CHECKSUM_AGG` 결과는 테이블의 행 순서 종속되지 않습니다. 또한 `CHECKSUM_AGG` 함수에서는 `DISTINCT` 키워드 및 `GROUP BY` 절을 사용할 수 있습니다.
  
식 목록 값이 바뀌면 목록 체크섬 값 목록도 적절하게 변경됩니다. 그러나 계산된 체크섬은 변경되지 않을 가능성도 일부는 존재합니다.
  
`CHECKSUM_AGG`에는 다른 집계 함수와 유사한 기능이 있습니다. 자세한 내용은 [집계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)를 참조하세요.
  
## <a name="examples"></a>예제  
이 예에서는 `CHECKSUM_AGG`를 사용하여 `Quantity` 데이터베이스에 있는 `ProductInventory` 테이블의 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 열에서 변경된 사항을 검색합니다.
  
```sql
--Get the checksum value before the column value is changed.  

SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
------------------------  
262  
```  
  
```sql
UPDATE Production.ProductInventory   
SET Quantity=125  
WHERE Quantity=100;  
GO  

--Get the checksum of the modified column.  
SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
------------------------  
287  
```  
  
## <a name="see-also"></a>참고 항목
[CHECKSUM&#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)  
[HASHBYTES&#40;Transact-SQL&#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
[BINARY_CHECKSUM  &#40;Transact-SQL&#41;](../../t-sql/functions/binary-checksum-transact-sql.md)
[OVER Clause &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
