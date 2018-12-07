---
title: BINARY_CHECKSUM(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ca0c77ccf18d47f14c7f9eb286158bb8d4642ddf
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/29/2018
ms.locfileid: "52617763"
---
# <a name="binarychecksum--transact-sql"></a>BINARY_CHECKSUM(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

테이블 행이나 식 목록에 대해 계산한 이진 체크섬 값을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
BINARY_CHECKSUM ( * | expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>인수  
*\**  
모든 테이블 열이 계산에 포함되도록 지정합니다. BINARY_CHECKSUM은 계산에서 비교할 수 없는 데이터 형식의 열을 무시합니다. 비교할 수 없는 데이터 형식에는 다음이 포함됩니다.  
* **cursor**  
* **image**  
* **ntext**  
* **text**  
* **xml**  

그리고 비교할 수 없는 CLR(공용 언어 런타임) 사용자 정의 형식도 포함됩니다.
  
*expression*  
모든 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. BINARY_CHECKSUM은 계산에서 비교할 수 없는 데이터 형식의 식을 무시합니다.

## <a name="return-types"></a>반환 형식  
 **int**
  
## <a name="remarks"></a>Remarks  
테이블의 행에 대해 계산한 BINARY_CHECKSUM(*)은 이후에 행을 수정하지 않은 경우 같은 값을 반환합니다. BINARY_CHECKSUM은 해시 함수의 속성을 만족시킵니다. 식의 두 목록에 대해 적용되는 BINARY_CHECKSUM은 두 목록의 해당 요소가 동일한 형식이고 등호(=) 연산자를 사용하여 비교할 때 동일한 경우 같은 값을 반환합니다. 이러한 정의에서는 지정된 유형의 Null 값은 동일한 값으로 비교됩니다. 식 목록에 있는 값 중 하나 이상이 변경되면 식 체크섬도 변경될 수 있습니다. 그러나 이는 보장되지 않습니다. 따라서 값이 변경되었는지 여부를 검색하려면 응용 프로그램에서 가끔 누락된 변경을 허용할 수 있는 경우에만 BINARY_CHECKSUM을 사용하는 것이 좋습니다. 그렇지 않으면 HashBytes를 대신 사용하는 것이 좋습니다. 지정된 MD5 해시 알고리즘을 사용하면 HashBytes에서 두 가지 입력에 대해 같은 결과를 반환할 가능성이 BINARY_CHECKSUM에 비해 훨씬 낮습니다.
  
BINARY_CHECKSUM은 식 목록에 대해 작동할 수 있으며 지정된 목록에 대해 같은 값을 반환합니다. 식의 두 목록에 대해 적용되는 BINARY_CHECKSUM은 두 목록의 해당 요소가 유형 및 바이트 표현에서 동일할 경우 같은 값을 반환합니다. 이러한 정의에서 지정된 유형의 Null 값은 바이트 표현이 동일한 것으로 간주됩니다.
  
BINARY_CHECKSUM 및 CHECKSUM은 유사한 함수입니다. 식 목록에 대해 체크섬 값을 계산하는 데 사용할 수 있고 식 순서가 결과 값에 영향을 미칩니다. BINARY_CHECKSUM(*)에 사용되는 열의 순서는 테이블이나 뷰 정의에 지정된 열의 순서입니다. 계산 열도 마찬가지입니다.
  
BINARY_CHECKSUM 및 CHECKSUM은 문자열 데이터 형식에 대해 서로 다른 값을 반환합니다. 여기서 로캘은 표현이 서로 다른 문자열을 동일하게 비교할 수 있습니다. 문자열 데이터 형식은  

* **char**  
* **nchar**  
* **nvarchar**  
* **varchar**  

로 구분하거나 여러  

* **sql_variant**(**sql_variant**의 기본 형식이 문자열 데이터 형식인 경우)입니다.  
  
예를 들어 "McCavity" 및 "Mccavity" 문자열에는 서로 다른 BINARY_CHECKSUM 값이 있습니다. 그러나 대소문자를 구분하지 않는 서버의 경우 CHECKSUM은 해당 문자열에 대해 같은 체크섬 값을 반환합니다. CHECKSUM 값과 BINARY_CHECKSUM 값의 비교는 피해야 합니다.
 
BINARY_CHECKSUM은 길이 제한 없는 **varbinary(max)** 형식과 최대 255자의 **nvarchar(max)** 형식을 지원합니다.
  
## <a name="examples"></a>예  
이 예에서는 `BINARY_CHECKSUM`을 사용하여 테이블 행의 변경 내용을 검색합니다.
  
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
  
## <a name="see-also"></a>관련 항목:
[집계 함수&#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[CHECKSUM&#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)  
[CHECKSUM_AGG&#40;Transact-SQL&#41;](../../t-sql/functions/checksum-agg-transact-sql.md)
  
  
