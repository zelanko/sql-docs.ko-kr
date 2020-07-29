---
title: CHECKSUM(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHECKSUM_TSQL
- CHECKSUM
dev_langs:
- TSQL
helpviewer_keywords:
- hash indexes
- CHECKSUM function
- checksum values
ms.assetid: e26d3339-845c-49c2-9d89-243376874c13
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 496c08f2bdf9942349ccdda83c90a97336767203
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87110600"
---
# <a name="checksum-transact-sql"></a>CHECKSUM(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

`CHECKSUM` 함수는 테이블의 행이나 식 목록에 대해 계산한 체크섬 값을 반환합니다. `CHECKSUM`을 사용하여 해시 인덱스를 작성합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
CHECKSUM ( * | expression [ ,...n ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
\*  
이 인수는 체크섬 계산이 모든 테이블 열에 적용됨을 지정합니다. `CHECKSUM`은 비교할 수 없는 데이터 형식인 열이 있는 경우에 오류를 반환합니다. 비교할 수 없는 데이터 형식에는 다음이 포함됩니다.

- **cursor**
- **image**
- **ntext**
- **text**
- **XML**

비교할 수 없는 다른 데이터 형식으로는 앞의 데이터 형식을 기준 형식으로 하는 **sql_variant**가 있습니다.
  
*expression*  
비교할 수 없는 데이터 형식을 제외한 모든 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.
  
## <a name="return-types"></a>반환 형식
 **int**  
  
## <a name="remarks"></a>설명  
`CHECKSUM`은 인수 목록에 대해 체크섬이라고 하는 해시 값을 계산합니다. 이 해시 값을 사용하여 해시 인덱스를 작성합니다. `CHECKSUM` 함수가 열 인수인 경우 결과는 해시 인덱스이며 인덱스는 계산된 `CHECKSUM` 값을 통해 작성됩니다. 이 결과는 열에 대한 등가 검색에 사용할 수 있습니다.
  
`CHECKSUM` 함수는 해시 함수 속성을 만족합니다. 즉 두 식 목록에 적용된 `CHECKSUM`은 두 목록의 해당 요소가 같은 데이터 형식을 갖고 해당하는 요소가 같음(=) 연산자를 사용하여 비교했을 때 동일하면 동일한 값을 반환합니다. 지정된 형식의 Null 값은 `CHECKSUM` 함수에서는 동일한 것으로 비교되게 정의됩니다. 식 목록에 있는 값 중 하나 이상이 변경되면 목록 체크섬도 변경될 수 있습니다. 그러나 이는 보장되지 않습니다. 따라서 값이 변경되었는지 여부를 검색하려면 애플리케이션에서 가끔 누락된 변경을 허용할 수 있는 경우에만 `CHECKSUM`을 사용하는 것이 좋습니다. 그렇지 않으면 `HASHBYTES`를 대신 사용하는 것이 좋습니다. 지정된 MD5 해시 알고리즘을 사용하면 `HASHBYTES`에서 두 개의 다른 입력에 대해 같은 결과를 반환할 가능성이 `CHECKSUM`에 비해 훨씬 낮습니다.
  
식 순서는 계산된 `CHECKSUM` 값에 영향을 미칩니다. `CHECKSUM(*)`에 사용되는 열의 순서는 테이블 또는 뷰 정의에 지정된 열의 순서입니다. 계산 열도 마찬가지입니다.
  
`CHECKSUM` 값은 데이터 정렬에 따라 달라집니다. 같은 값이 다른 데이터 정렬로 저장된 경우 다른 `CHECKSUM` 값이 반환됩니다.
  
`CHECKSUM ()`은 고유한 결과를 보장하지 않습니다.

## <a name="examples"></a>예  
이 예에서는 `CHECKSUM`를 사용하여 해시 인덱스를 작성합니다.
  
해시 인덱스를 구성하기 위해 첫 번째 예에서는 계산된 체크섬 열을 인덱스하려는 테이블에 추가합니다. 그런 다음, 체크섬 열에서 인덱스를 작성합니다. 
  
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
  
이 예에서는 체크섬 인덱스를 해시 인덱스로 사용하는 것을 보여 줍니다. 이렇게 하면 인덱싱할 열이 긴 문자 열일 때 인덱싱 속도를 높일 수 있습니다. 또한 등가 검색에도 체크섬 인덱스를 사용할 수 있습니다.
  
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
  
계산된 열에 인덱스를 만들면 체크섬 열이 만들어지고 `ProductName` 값의 변경 사항이 체크섬 열에 전파됩니다. 또는 인덱싱할 열에 직접 인덱스를 작성할 수 있습니다. 그러나 긴 키 값의 경우 기본 인덱스가 체크섬 인덱스처럼 수행되지 않을 수 있습니다.
  
## <a name="see-also"></a>참고 항목
[CHECKSUM_AGG&#40;Transact-SQL&#41;](../../t-sql/functions/checksum-agg-transact-sql.md)  
[HASHBYTES&#40;Transact-SQL&#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
[BINARY_CHECKSUM&#40;Transact-SQL&#41;](../../t-sql/functions/binary-checksum-transact-sql.md)
  
  
