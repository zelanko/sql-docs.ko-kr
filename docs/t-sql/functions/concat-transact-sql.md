---
title: CONCAT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 63b257076b2568b66a13e1e9f973e490f01dc861
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39454237"
---
# <a name="concat-transact-sql"></a>CONCAT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

이 함수는 둘 이상의 문자열 값을 종단 간 방식으로 연결하거나 조인한 결과 문자열을 반환합니다. (연결 중 구분 값을 추가하려면 [CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md)를 참조하세요.)
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CONCAT ( string_value1, string_value2 [, string_valueN ] )  
```  
  
## <a name="arguments"></a>인수  
*string_value*  
다른 값에 연결할 문자열 값입니다. `CONCAT` 함수에는 둘 이상의 *string_value* 인수와 254개 이하의 *string_value*  인수가 필요합니다.
  
## <a name="return-types"></a>반환 형식  
*string_value*  
길이와 형식이 입력에 따라 달라지는 문자열 값입니다.
  
## <a name="remarks"></a>Remarks  
`CONCAT`는 가변 개수의 문자열 인수를 가져와서 단일 문자열로 연결(또는 조인)합니다. 둘 이상의 입력 값이 필요하며, 그렇지 않은 경우 `CONCAT`에서 오류가 발생합니다. `CONCAT`는 병합하기 전에 모든 인수를 문자열 형식으로 암시적으로 변환합니다. `CONCAT`는 null 값을 빈 문자열로 암시적으로 변환합니다. `CONCAT`에서 모두 **NULL** 값인 인수를 받으면 **varchar**(1) 형식의 빈 문자열을 반환합니다. 문자열에 대한 암시적 변환은 데이터 형식 변환에 대한 기존 규칙을 따릅니다. 데이터 형식 변환에 대한 자세한 내용은 [CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)를 참조하세요.
  
반환 형식은 인수의 형식에 따라 달라집니다. 아래 표에서는 매핑을 보여 줍니다.
  
|입력 형식|출력 형식 및 길이|  
|---|---|
|1. 인수가<br><br />SQL-CLR 시스템 종류,<br><br />SQL-CLR UDT인 경우<br><br />로 구분하거나 여러<br><br />`nvarchar(max)`|**nvarchar(max)**|  
|2. 그렇지 않고 인수가<br><br />**varbinary(max)**<br><br />로 구분하거나 여러<br><br />**varchar(max)**|**varchar(max)** - 매개 변수 중 하나가 임의 길이의 **nvarchar**가 아닌 경우. 이 경우 `CONCAT`는 **nvarchar(max)** 형식의 결과를 반환합니다.|  
|3. 그렇지 않고 인수가 최대 4,000자의 **nvarchar** 형식인 경우<br><br />( **nvarchar**(<= 4000) )|**nvarchar**(<= 4000)|  
|4. 다른 모든 경우|매개 변수 중 하나가 임의 길이의 nvarcha가 아닌 경우 **varchar**(<= 8000)(최대 8,000자의 **varchar**) 이 경우 `CONCAT`는 **nvarchar(max)** 형식의 결과를 반환합니다.|  
  
`CONCAT`에서 길이가 4,000자 이하인 **nvarchar** 또는 길이가 8,000자 이하인 **varchar** 입력 인수를 받으면, 암시적 변환이 결과의 길이에 영향을 줄 수 있습니다. 다른 데이터 형식은 문자열로 암시적으로 변환되는 경우 길이가 달라집니다. 예를 들어 **int** (14)의 문자열 길이는 12자이고, **float**의 길이는 32자입니다. 따라서 두 개의 정수를 연결하면 길이가 24 이상인 결과가 반환됩니다.
  
지원되는 LOB(Large Object) 형식의 입력 인수가 없는 경우 반환 형식에 관계없이 모든 반환 형식이 8,000자 길이로 잘립니다. 이 잘림은 공간을 유지하고 계획 생성 효율성을 지원합니다.
  
CONCAT 함수는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 버전 이상의 연결된 서버에서 원격으로 실행할 수 있습니다. 이전 버전의 연결된 서버인 경우 연결된 서버에서 연결되지 않은 값을 반환한 후에 CONCAT 작업이 로컬로 수행됩니다.
  
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
  
## <a name="see-also"></a>관련 항목:
 [CONCAT_WS&#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)   
 [FORMATMESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME&#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE&#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE&#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG&#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE&#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF&#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE&#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  


