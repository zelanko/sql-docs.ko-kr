---
title: SOUNDEX(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SOUNDEX
- SOUNDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SOUNDEX function
- comparing string data
- strings [SQL Server], similarity
- strings [SQL Server], comparing
- SOUNDEX values
ms.assetid: 8f1ed34e-8467-4512-a211-e0f43dee6584
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e4e9d630691eed9d727df5074508210c95ab7345
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65947725"
---
# <a name="soundex-transact-sql"></a>SOUNDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  두 문자열의 유사성을 평가하기 위한 4자의 SOUNDEX 코드를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SOUNDEX ( character_expression )  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 문자 데이터의 영숫자 [expression](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *character_expression*은 상수, 변수 또는 열일 수 있습니다.  
  
## <a name="return-types"></a>반환 형식  
 **varchar**  
  
## <a name="remarks"></a>Remarks  
 SOUNDEX는 문자열을 말할 때 어떻게 들리는지에 따라 영숫자 문자열을 4자의 코드로 변환합니다. 코드의 첫 번째 문자는 *character_expression*의 첫 번째 문자이며 대문자로 변환됩니다. 코드의 두 번째부터 네 번째 문자까지의 문자는 식의 문자를 나타내는 숫자입니다. 문자 A, E, I, O, U, H, W 및 Y는 문자열의 첫 문자가 아닌 경우 무시됩니다. 4자로 된 코드를 생성하기 위해 필요한 경우 끝에 0이 추가됩니다. SOUNDEX 코드에 대한 자세한 내용은 [Soundex 인덱싱 시스템](https://www.archives.gov/research/census/soundex.html)을 참조하세요.  
  
 다른 문자열의 SOUNDEX 코드는 문자열을 말할 때 얼마나 비슷한지 확인하기 위해 비교할 수 있습니다. DIFFERENCE 함수는 두 개의 문자열에서 SOUNDEX를 수행하고 이러한 문자열에 대해 SOUNDEX 코드가 얼마나 유사한지 나타내는 정수를 반환합니다.  
  
 SOUNDEX는 데이터 정렬을 인식합니다. 문자열 함수는 중첩될 수 있습니다.  
  
## <a name="soundex-compatibility"></a>SOUNDEX 호환성  
 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 SOUNDEX 함수는 SOUNDEX 규칙의 하위 집합을 적용했습니다. 데이터베이스 호환성 수준 110 이상에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 더 자세한 규칙 집합을 적용합니다.  
  
 호환성 수준 110 이상으로 업그레이드한 후 SOUNDEX 함수를 사용하는 인덱스, 힙 또는 CHECK 제약 조건을 다시 작성해야 할 수 있습니다.  
  
-   SOUNDEX로 정의된 지속형 계산 열이 포함된 힙은 `ALTER TABLE <table> REBUILD` 문을 실행하여 힙을 다시 작성한 후에만 쿼리할 수 있습니다.  
  
-   업그레이드를 수행하면 SOUNDEX를 사용하여 정의된 CHECK 제약 조건이 비활성화됩니다. 이 제약 조건을 활성화하려면 `ALTER TABLE <table> WITH CHECK CHECK CONSTRAINT ALL` 문을 실행하세요.  
  
-   SOUNDEX로 정의된 지속형 계산 열이 포함된 인덱스(인덱싱된 뷰 포함)는 `ALTER INDEX ALL ON <object> REBUILD` 문을 실행하여 인덱스를 다시 작성한 후에만 쿼리할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 SOUNDEX 함수 및 관련된 DIFFERENCE 함수를 보여 줍니다. 첫 번째 예에서는 모든 자음에 대해 표준 `SOUNDEX` 값이 반환됩니다. `SOUNDEX` 및 `Smith`에 대해 `Smythe`를 반환하면 모든 모음, 문자 `y`, 이중 문자 및 문자 `h`가 포함되지 않으므로 똑같은 결과가 반환됩니다.  
  
```  
-- Using SOUNDEX  
SELECT SOUNDEX ('Smith'), SOUNDEX ('Smythe');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Latin1_General 데이터 정렬에 유효합니다.  
  
```  
  
----- -----   
S530  S530    
  
(1 row(s) affected)  
```  
  
 `DIFFERENCE` 함수는 `SOUNDEX` 패턴 결과의 차이를 비교합니다. 다음 예에서는 모음만 다른 두 문자열을 보여 줍니다. 반환되는 차이는 `4`(가능한 최저 차이)입니다.  
  
```  
-- Using DIFFERENCE  
SELECT DIFFERENCE('Smithers', 'Smythers');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Latin1_General 데이터 정렬에 유효합니다.  
  
```  
-----------   
4             
  
(1 row(s) affected)  
```  
  
 다음 예에서는 문자열의 자음이 다르므로 반환되는 차이는 `2`이며 더 많은 차이가 납니다.  
  
```  
SELECT DIFFERENCE('Anothers', 'Brothers');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Latin1_General 데이터 정렬에 유효합니다.  
  
```  
-----------   
2             
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목  
 [DIFFERENCE &#40;Transact-SQL&#41;](../../t-sql/functions/difference-transact-sql.md)   
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  

