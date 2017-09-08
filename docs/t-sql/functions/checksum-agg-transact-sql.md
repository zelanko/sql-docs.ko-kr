---
title: CHECKSUM_AGG (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b202009c2920dfbcdd068ec3d7ab95de13caa7b4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="checksumagg-transact-sql"></a>CHECKSUM_AGG(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

그룹에서 값의 체크섬을 반환합니다. Null 값은 무시됩니다. 가 올 수 있습니다는 [OVER 절](../../t-sql/queries/select-over-clause-transact-sql.md)합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CHECKSUM_AGG ( [ ALL | DISTINCT ] expression )  
```  
  
## <a name="arguments"></a>인수  
**ALL**  
모든 값에 집계 함수를 적용합니다. 기본값은 ALL입니다.
  
DISTINCT  
CHECKSUM_AGG가 고유한 값의 체크섬을 반환하도록 지정합니다.
  
*expression*  
정수 [식](../../t-sql/language-elements/expressions-transact-sql.md)합니다. 집계 함수와 하위 쿼리는 허용되지 않습니다.
  
## <a name="return-types"></a>반환 형식
모든의 체크섬을 반환 *식* 값으로 **int**합니다.
  
## <a name="remarks"></a>주의  
CHECKSUM_AGG는 테이블에서 변경 사항을 검색하는 데 사용할 수 있습니다.
  
테이블의 행 순서는 CHECKSUM_AGG의 결과에 영향을 주지 않습니다. 또한 CHECKSUM_AGG 함수는 DISTINCT 키워드 및 GROUP BY 절과 함께 사용할 수 있습니다.
  
식 목록에 있는 값을 하나라도 변경하면 일반적으로 목록의 체크섬도 바뀝니다. 그러나 체크섬이 바뀌지 않는 경우도 가끔 있습니다.
  
CHECKSUM_AGG는 다른 집계 함수와 기능이 비슷합니다. 자세한 내용은 참조 [집계 함수 &#40; Transact SQL &#41; ](../../t-sql/functions/aggregate-functions-transact-sql.md).
  
## <a name="examples"></a>예  
다음 예에서는 `CHECKSUM_AGG`를 사용하여 `Quantity` 데이터베이스에 있는 `ProductInventory` 테이블의 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 열에서 변경된 사항을 검색합니다.
  
```sql
--Get the checksum value before the column value is changed.  
SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
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
  
```sql
------------------------  
287  
```  
  
## <a name="see-also"></a>참고 항목
[체크섬 &#40; Transact SQL &#41;](../../t-sql/functions/checksum-transact-sql.md)  
[절 &#40; 조치 Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

