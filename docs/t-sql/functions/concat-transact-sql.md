---
title: CONCAT (Transact SQL) | Microsoft Docs
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
- CONCAT
- CONCAT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT function
ms.assetid: fce5a8d4-283b-4c47-95e5-4946402550d5
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 046278bb3016b39df8039a1450a58b177d2bc180
ms.contentlocale: ko-kr
ms.lasthandoff: 10/17/2017

---
# <a name="concat-transact-sql"></a>CONCAT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

둘 이상의 문자열 값을 연결한 결과인 문자열을 반환합니다. (연결 중를 분리 하면 값을 추가 하려면 참조 [CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md).)
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CONCAT ( string_value1, string_value2 [, string_valueN ] )  
```  
  
## <a name="arguments"></a>인수  
*string_value*  
다른 값에 연결할 문자열 값입니다.
  
## <a name="return-types"></a>반환 형식
입력에 따라 문자열 또는 길이가 반환됩니다.
  
## <a name="remarks"></a>주의  
**CONCAT** 가변 개수의 문자열 인수를 사용 하 고 단일 문자열로 연결 합니다. 최소 두 개의 입력 값이 필요하며, 그렇지 않은 경우 오류가 발생합니다. 모든 인수는 문자열 형식으로 암시적으로 변환된 다음 연결됩니다. Null 값은 암시적으로 빈 문자열로 변환됩니다. 모든 인수가 null, 빈 문자열 형식의 경우 **varchar**(1)이 반환 됩니다. 문자열에 대한 암시적 변환은 데이터 형식 변환에 대한 기존 규칙을 따릅니다. 데이터 형식 변환에 대 한 자세한 내용은 참조 하십시오. [CAST 및 convert&#40; Transact SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
반환 형식은 인수의 형식에 따라 달라집니다. 아래 표에서는 매핑을 보여 줍니다.
  
|입력 형식|출력 형식 및 길이|  
|---|---|
|인수가 SQL-CLR 시스템 형식, SQL-CLR UDT 또는 `nvarchar(max)`인 경우|**nvarchar(max)**|  
|그렇지 않고 인수가 있으면 **varbinary (max)** 또는 **varchar (max)**|**varchar (max)** 매개 변수 중 하나가 아닌 경우는 **nvarchar** 의 길이입니다. 따라서 다음 결과가 이면 **nvarchar (max)**합니다.|  
|그렇지 않고 인수가 있으면 **nvarchar**(< = 4000)|**nvarchar**(< = 4000)|  
|그렇지 않은 다른 모든 경우|**varchar**(< = 8000) 매개 변수 중 하나가 임의 길이의 nvarchar가 아닌 경우. 따라서 다음 결과가 이면 **nvarchar (max)**합니다.|  
  
인수가 < = 4000 **nvarchar**, 또는 < = 8000 **varchar**, 암시적 변환은 결과의 길이 영향을 줄 수 있습니다. 다른 데이터 형식은 암시적으로 문자열로 변환될 경우 다른 길이를 가집니다. 예를 들어는 **int** (14)의 문자열 길이는 12, 동안는 **float** 길이 32입니다. 따라서 두 정수를 연결한 결과는 길이가 24자 이상입니다.
  
지원되는 큰 개체(LOB) 형식의 입력 인수가 없는 경우에는 형식에 관계없이 모든 반환 형식이 8000자로 잘립니다. 이 잘림은 공간을 유지하고 계획 생성의 효율성을 지원합니다.
  
CONCAT 함수 버전이 있는 연결된 된 서버에서 원격으로 실행할 수 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상. 오래 된 연결 된 서버에는 CONCAT 작업이 수행 되도록 로컬로 연결된 된 서버에서 비 연결 된 값이 반환 후 합니다.
  
## <a name="examples"></a>예  
  
### <a name="a-using-concat"></a>1. CONCAT 사용  
  
```sql
SELECT CONCAT ( 'Happy ', 'Birthday ', 11, '/', '25' ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
-------------------------  
Happy Birthday 11/25  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-concat-with-null-values"></a>2. NULL 값이 있는 CONCAT 사용  
  
```sql
CREATE TABLE #temp (  
    emp_name nvarchar(200) NOT NULL,  
    emp_middlename nvarchar(200) NULL,  
    emp_lastname nvarchar(200) NOT NULL  
);  
INSERT INTO #temp VALUES( 'Name', NULL, 'Lastname' );  
SELECT CONCAT( emp_name, emp_middlename, emp_lastname ) AS Result  
FROM #temp;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
------------------  
NameLastname  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목
[문자열 함수 (Transact SQL)](../../t-sql/functions/string-functions-transact-sql.md)  
[CONCAT_WS (Transact SQL)](../../t-sql/functions/concat-ws-transact-sql.md)   
  



