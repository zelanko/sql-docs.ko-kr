---
title: UPPER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UPPER_TSQL
- UPPER
dev_langs:
- TSQL
helpviewer_keywords:
- UPPER function
- characters [SQL Server], lowercase
- converting lowercase to uppercase
- uppercase characters [SQL Server]
- characters [SQL Server], uppercase
- lowercase characters
ms.assetid: 5ced55f7-ac89-4cf2-9465-f63f4dc480db
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d91870e53e5976ba5d52b83f086a57fa552ad1ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927622"
---
# <a name="upper-transact-sql"></a>UPPER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  소문자 데이터를 대문자로 변환한 문자 식을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
UPPER ( character_expression )  
```  
  
## <a name="arguments"></a>인수  
 *character_expression*  
 문자 데이터의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. *character_expression*은 문자나 이진 데이터의 상수, 변수 또는 열일 수 있습니다.  
  
 *character_expression*은 **varchar**로 암시적으로 변환될 수 있는 데이터 형식이어야 합니다. 그렇지 않은 경우 [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md)를 사용하여 *character_expression*을 명시적으로 변환하세요.  
  
## <a name="return-types"></a>반환 형식  
 **varchar** 또는 **nvarchar**  
  
## <a name="examples"></a>예  
 다음 예에서는 `UPPER` 및 `RTRIM` 함수를 사용하여 `dbo.DimEmployee` 테이블에 있는 사람의 성을 반환합니다. 성은 대문자로 변환되고 잘린 다음, 이름 부분과 연결됩니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT UPPER(RTRIM(LastName)) + ', ' + FirstName AS Name  
FROM dbo.DimEmployee  
ORDER BY LastName;  
```  
  
 다음은 결과 집합의 일부입니다.  
  
 ```
Name
------------------------------
ABBAS, Syed
ABERCROMBIE, Kim
ABOLROUS, Hazem
 ```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
 [LOWER&#40;Transact-SQL&#41;](../../t-sql/functions/lower-transact-sql.md)  
  
  

