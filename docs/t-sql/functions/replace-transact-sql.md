---
title: REPLACE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- REPLACE_TSQL
- REPLACE
dev_langs:
- TSQL
helpviewer_keywords:
- first string expression [SQL Server]
- replacing string expression
- third string expressions [SQL Server]
- second string expressions [SQL Server]
- REPLACE function
ms.assetid: 8a7aaaf2-62e3-46c0-8e44-fa22290dd86b
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 3796514d8397b87db38f13951d0ad9432775db0c
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39456617"
---
# <a name="replace-transact-sql"></a>REPLACE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정된 문자열 값의 모든 항목을 다른 문자열 값으로 바꿉니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
REPLACE ( string_expression , string_pattern , string_replacement )  
```  
  
## <a name="arguments"></a>인수  
 *string_expression*  
 검색할 문자열 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *string_expression*는 문자 또는 이진 데이터 형식일 수 있습니다.  
  
 *string_* pattern  
 찾을 부분 문자열입니다. *string_expression*은 문자 또는 이진 데이터 형식일 수 있습니다. *string_pattern*은 빈 문자열('')일 수 없으며 페이지 크기에 맞는 최대 바이트 수를 초과하지 않아야 합니다.  
  
 *string_* replacement  
 대체 문자열입니다. *string_replacement*는 문자 또는 이진 데이터 형식일 수 있습니다.  
  
## <a name="return-types"></a>반환 형식  
 입력 인수 중 하나의 데이터 형식이 **nvarchar**이면 REPLACE는 **nvarchar**를 반환하고 그렇지 않으면 **varchar**를 반환합니다.  
  
 인수 중에 Null이 있으면 NULL을 반환합니다.  
  
 *string_expression*의 형식이 **varchar(max)** 또는 **nvarchar(max)가 아닌 경우 REPLACE**는 반환 값을 8,000 바이트에서 자릅니다. 8,000바이트를 초과하는 값을 반환하려면 *string_expression*을 큰 값 데이터 형식으로 명시적으로 캐스팅해야 합니다.  
  
## <a name="remarks"></a>Remarks  
 REPLACE는 입력의 데이터 정렬을 기반으로 비교를 수행합니다. 지정된 데이터 정렬에서 비교를 수행하려면 [COLLATE](~/t-sql/statements/collations.md)를 사용하여 입력에 명시적 데이터 정렬을 적용할 수 있습니다.  
  
 0x0000 (**char(0)**)은 Windows 데이터 정렬에서 정의되지 않은 문자이며 REPLACE에 포함할 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `cde`의 `abcdefghi` 문자열을 `xxx`로 대체합니다.  
  
```sql  
SELECT REPLACE('abcdefghicde','cde','xxx');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------  
abxxxfghixxx  
(1 row(s) affected)  
```  
  
 다음 예에서는 `COLLATE` 함수를 사용합니다.  
  
```sql  
SELECT REPLACE('This is a Test'  COLLATE Latin1_General_BIN,  
'Test', 'desk' );  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------  
This is a desk  
(1 row(s) affected)  
```  

  
## <a name="see-also"></a>참고 항목  
 [CONCAT&#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS&#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME&#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REVERSE&#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG&#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE&#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF&#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE&#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
