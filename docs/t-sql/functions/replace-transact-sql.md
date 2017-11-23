---
title: REPLACE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- REPLACE_TSQL
- REPLACE
dev_langs: TSQL
helpviewer_keywords:
- first string expression [SQL Server]
- replacing string expression
- third string expressions [SQL Server]
- second string expressions [SQL Server]
- REPLACE function
ms.assetid: 8a7aaaf2-62e3-46c0-8e44-fa22290dd86b
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a50c0b7220eba654df21349e2fd3cd57b9a0d7d3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
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
 문자열은 [식](../../t-sql/language-elements/expressions-transact-sql.md) 를 검색할 수 있습니다. *string_expression* 문자 또는 이진 데이터 형식일 수 있습니다.  
  
 *string_*패턴  
 찾을 부분 문자열입니다. *string_pattern* 문자 또는 이진 데이터 형식일 수 있습니다. *string_pattern* 빈 문자열 (") 될 수 없습니다 하며 페이지에 맞는 최대 바이트 수를 초과 하지 않아야 합니다.  
  
 *string_*교체  
 대체 문자열입니다. *string_replacement* 문자 또는 이진 데이터 형식일 수 있습니다.  
  
## <a name="return-types"></a>반환 형식  
 반환 **nvarchar** 의 입력된 인수 중 하나가 경우는 **nvarchar** 데이터 입력 그렇지 않으면 REPLACE 반환 **varchar**합니다.  
  
 인수 중에 Null이 있으면 NULL을 반환합니다.  
  
 경우 *string_expression* 다른 형식의 **varchar (max)** 또는 **nvarchar (max), REPLACE** 반환 값을 8, 000 바이트에서 자릅니다. 8, 000 바이트 보다 큰 값을 반환 하려면 *string_expression* 큰 값 데이터 형식으로 명시적으로 캐스팅 되어야 합니다.  
  
## <a name="remarks"></a>주의  
 REPLACE는 입력의 데이터 정렬을 기반으로 비교를 수행합니다. 지정된 된 데이터 정렬에서 비교를 수행 하려면 사용할 수 있습니다 [COLLATE](~/t-sql/statements/collations.md) 입력에 명시적 데이터 정렬을 적용할 수 있습니다.  
  
 0x0000 (**char(0)**)은 Windows 데이터 정렬에서 정의 되지 않은 문자 이며 REPLACE에 포함할 수 없습니다.  
  
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

  
## <a name="see-also"></a>관련 항목:  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
