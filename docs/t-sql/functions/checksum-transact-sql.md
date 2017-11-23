---
title: "체크섬 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKSUM_TSQL
- CHECKSUM
dev_langs: TSQL
helpviewer_keywords:
- hash indexes
- CHECKSUM function
- checksum values
ms.assetid: e26d3339-845c-49c2-9d89-243376874c13
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: d41736f6ac216de0ecf755cbf7ca73ba34a697b8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="checksum-transact-sql"></a>CHECKSUM(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

테이블의 행이나 식 목록에 대해 계산한 체크섬 값을 반환합니다. CHECKSUM 값은 해시 인덱스를 작성하는 데 사용하기 위한 것입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CHECKSUM ( * | expression [ ,...n ] )  
```  
  
## <a name="arguments"></a>인수  
\*  
테이블의 모든 열에 대해 계산하도록 지정합니다. CHECKSUM은 비교할 수 없는 데이터 형식인 열이 있는 경우에 오류를 반환합니다. 비교할 수 없는 데이터 유형은 **텍스트**, **ntext**, **이미지**, XML, 및 **커서**, 그리고 **sql_variant**기본 형식으로 이러한 형식 중 하나를 사용 합니다.
  
*expression*  
이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 비교할 수 없는 데이터 형식 제외한 모든 형식의 합니다.
  
## <a name="return-types"></a>반환 형식
 **int**  
  
## <a name="remarks"></a>주의  
CHECKSUM은 인수의 목록에 대해 체크섬이라고 하는 해시 값을 계산합니다. 해시 값은 해시 인덱스를 작성하는 데 사용하기 위한 것입니다. CHECKSUM에 대한 인수가 열이고 인덱스가 계산된 CHECKSUM 값을 통해 작성된 경우 결과는 해시 인덱스입니다. 이 결과는 열에 대한 등가 검색에 사용할 수 있습니다.
  
해시 함수의 속성을 충족 하는 체크섬: 식의 두 목록에 대해 적용 되는 CHECKSUM은 두 목록의 해당 요소 동일한 형식이 고 등호 (=) 연산자를 사용 하 여 비교할 때 동일한 경우 같은 값을 반환 합니다. 이러한 정의에 대해 지정한 유형의 Null 값은 비교할 때 동일한 것으로 간주됩니다. 식 목록에 있는 값을 하나라도 변경하면 일반적으로 목록의 체크섬도 바뀝니다. 그러나 체크섬이 바뀌지 않는 경우도 가끔 있습니다. 이 때문에 응용 프로그램에서 변경 내용 누락이 있어서는 안 될 경우 CHECKSUM을 사용하여 값의 변경 여부를 확인하는 것은 좋지 않습니다. 사용 하는 것이 좋습니다 [HashBytes](../../t-sql/functions/hashbytes-transact-sql.md) 대신 합니다. MD5 해시 알고리즘을 지정하면 HashBytes에서 두 개의 다른 입력에 대해 같은 결과를 반환할 가능성이 CHECKSUM보다 훨씬 낮습니다.
  
식의 순서는 CHECKSUM의 결과 값에 영향을 미칩니다. CHECKSUM(*)에 사용되는 열의 순서는 테이블 또는 뷰 정의에 지정된 열의 순서입니다. 계산 열도 마찬가지입니다.
  
CHECKSUM 값은 데이터 정렬에 따라 달라집니다. 같은 값이 다른 데이터 정렬로 저장된 경우 다른 CHECKSUM 값이 반환됩니다.
  
## <a name="examples"></a>예  
다음 예에서는 `CHECKSUM`을 사용하여 해시 인덱스를 작성하는 방법을 보여 줍니다. 해시 인덱스는 인덱스될 테이블에 계산된 체크섬 열을 추가한 다음 체크섬 열에서 인덱스를 만드는 방식으로 작성됩니다.
  
```sql
-- Create a checksum index.  
SET ARITHABORT ON;  
USE AdventureWorks2012;   
GO  
ALTER TABLE Production.Product  
ADD cs_Pname AS CHECKSUM(Name);  
GO  
CREATE INDEX Pname_index ON Production.Product (cs_Pname);  
GO  
```  
  
특히 인덱스될 열이 긴 문자 열인 경우에 인덱싱 속도를 높이기 위해 사용할 수 있습니다. 또한 등가 검색에도 체크섬 인덱스를 사용할 수 있습니다.
  
```sql
/*Use the index in a SELECT query. Add a second search   
condition to catch stray cases where checksums match,   
but the values are not the same.*/  
SELECT *   
FROM Production.Product  
WHERE CHECKSUM(N'Bearing Ball') = cs_Pname  
AND Name = N'Bearing Ball';  
GO  
```  
  
계산 열에 인덱스를 만들면 체크섬 열이 만들어지고 `ProductName` 값의 변경 사항이 체크섬 열에 전파됩니다. 또는 인덱싱된 열에 직접 인덱스를 작성할 수도 있습니다. 그러나 키 값이 긴 경우에는 일반 인덱스가 체크섬 인덱스처럼 수행되지 않을 수 있습니다.
  
## <a name="see-also"></a>참고 항목
[CHECKSUM_AGG &#40; Transact SQL &#41;](../../t-sql/functions/checksum-agg-transact-sql.md)  
[HASHBYTES &#40; Transact SQL &#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
[BINARY_CHECKSUM &#40; Transact SQL &#41;](../../t-sql/functions/binary-checksum-transact-sql.md)
  
  
