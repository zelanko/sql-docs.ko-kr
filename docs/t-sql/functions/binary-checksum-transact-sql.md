---
title: BINARY_CHECKSUM (Transact SQL) | Microsoft Docs
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
- BINARY_CHECKSUM
- BINARY_CHECKSUM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- BINARY_CHECKSUM function
- binary [SQL Server], checksum values
ms.assetid: 07fece4d-58e3-446e-a3b5-92fe24d2d1fb
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b84847f3efe7224c6fa0ad945b03f3afbc1381b9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="binarychecksum--transact-sql"></a>BINARY_CHECKSUM (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

테이블 행이나 식 목록에 대해 계산한 이진 체크섬 값을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
BINARY_CHECKSUM ( * | expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>인수  
*\**  
테이블의 모든 열에 대해 계산하도록 지정합니다. BINARY_CHECKSUM은 계산에서 비교할 수 없는 데이터 형식의 열을 무시합니다. 비교할 수 없는 데이터 형식에는 **텍스트**, **ntext**, **이미지**, **커서**, **xml**, 및 비교할 수 없는 공용 언어 런타임 (CLR) 사용자 정의 형식입니다.
  
*expression*  
이 [식](../../t-sql/language-elements/expressions-transact-sql.md) 모든 종류의 합니다. BINARY_CHECKSUM은 계산에서 비교할 수 없는 데이터 형식의 식을 무시합니다.
  
## <a name="remarks"></a>주의  
테이블의 행에 대해 계산한 BINARY_CHECKSUM(*)은 이후에 행을 수정하지 않은 경우 같은 값을 반환합니다. Binary_checksum은 해시 함수의 속성을 만족: binary_checksum은 식의 두 목록에 대해 적용 된 두 목록의 해당 요소가 유형이 동일 하 고 등호 (=) 연산자를 사용 하 여 비교할 때 동일한 경우 같은 값을 반환 합니다. 이러한 정의에 대해 지정한 유형의 Null 값은 비교할 때 동일한 것으로 간주됩니다. 식 목록에 있는 값을 하나라도 변경하면 일반적으로 목록의 체크섬도 바뀝니다. 그러나 체크섬이 바뀌지 않는 경우도 가끔 있습니다. 이러한 이유로 권장 하지는 않습니다 BINARY_CHECKSUM를 사용 하 여 응용 프로그램 변경 누락을 허용할 수 있는 경우가 아니면 값 변경 되었는지 여부를 검색 합니다. HashBytes를 대신 사용 하십시오. MD5 해시 알고리즘을 지정 하면 HashBytes 두 개의 서로 다른 입력에 대 한 동일한 결과 반환할 가능성이 BINARY_CHECKSUM 보다 훨씬 낮습니다.
  
BINARY_CHECKSUM은 식 목록에 대해 적용할 수 있으며 지정된 목록에 대해 같은 값을 반환합니다. 식의 두 목록에 대해 적용되는 BINARY_CHECKSUM은 두 목록의 해당 요소가 유형 및 바이트 표현에서 동일할 경우 같은 값을 반환합니다. 이러한 정의에서 지정된 유형의 Null 값은 바이트 표현이 동일한 것으로 간주됩니다.
  
BINARY_CHECKSUM과 CHECKSUM는 비슷한 함수: 목록 식에 대해 체크섬 값을 계산에 사용할 수 있으며 식의 순서는 결과 값에 영향을 줍니다. BINARY_CHECKSUM(*)에 사용되는 열의 순서는 테이블이나 뷰 정의에 지정된 열의 순서입니다. 여기에는 계산 열이 포함됩니다.
  
CHECKSUM과 BINARY_CHECKSUM은 문자열 데이터 형식에 대해 서로 다른 값을 반환하는데 로캘로 인해 표현이 서로 다른 문자열이 동일하게 비교될 수 있습니다. 문자열 데이터 형식은 **char**, **varchar**, **nchar**, **nvarchar**, 또는 **sql_variant** (하는 경우는 기본 형식이 **sql_variant** string 데이터 형식). 예를 들어 "McCavity" 문자열과 "Mccavity" 문자열에 대한 BINARY_CHECKSUM 값은 서로 다릅니다. 그러나 대소문자를 구분하지 않는 서버에서는 CHECKSUM이 이러한 문자열에 대해 같은 체크섬 값을 반환하므로 CHECKSUM 값을 BINARY_CHECKSUM 값과 비교하면 안 됩니다.
 
Binary_checksum은 최대 8, 000 자 형식의 지원 **varbinary (max)** 및 형식의 255 자까지 **nvarchar (max)**합니다.
  
## <a name="examples"></a>예  
다음 예에서는 `BINARY_CHECKSUM`을 사용하여 테이블 행의 변경 내용을 검색합니다.
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE myTable (column1 int, column2 varchar(256));  
GO  
INSERT INTO myTable VALUES (1, 'test');  
GO  
SELECT BINARY_CHECKSUM(*) from myTable;  
GO  
UPDATE myTable set column2 = 'TEST';  
GO  
SELECT BINARY_CHECKSUM(*) from myTable;  
GO  
```  
  
## <a name="see-also"></a>참고 항목
[집계 함수 &#40; Transact SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[체크섬 &#40; Transact SQL &#41;](../../t-sql/functions/checksum-transact-sql.md)  
[CHECKSUM_AGG &#40; Transact SQL &#41;](../../t-sql/functions/checksum-agg-transact-sql.md)
  
  

