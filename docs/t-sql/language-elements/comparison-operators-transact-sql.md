---
title: 비교 연산자(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], testing
- operators [Transact-SQL], comparison
- testing expressions
- Boolean data type
- Boolean expressions
- comparing expressions
- comparison operators [SQL Server]
ms.assetid: b0cc68ef-3029-484c-a917-0c15dcbc230d
author: rothja
ms.author: jroth
ms.openlocfilehash: a1cc6427e01055a3aa97f8f79f9270dc22579255
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140263"
---
# <a name="comparison-operators-transact-sql"></a>비교 연산자(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  비교 연산자는 두 식이 동일한지 여부를 테스트합니다. 비교 연산자는 **text**, **ntext** 또는 **image** 데이터 형식의 식을 제외한 모든 식에 사용할 수 있습니다. 다음 표에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 비교 연산자를 나열합니다.  
  
|연산자|의미|  
|--------------|-------------|  
|[=(같음)](../../t-sql/language-elements/equals-transact-sql.md)|같음|  
|[>(보다 큼)](../../t-sql/language-elements/greater-than-transact-sql.md)|보다 큼|  
|[<(보다 작음)](../../t-sql/language-elements/less-than-transact-sql.md)|보다 작음|  
|[>=(크거나 같음)](../../t-sql/language-elements/greater-than-or-equal-to-transact-sql.md)|크거나 같음|  
|[<=(작거나 같음)](../../t-sql/language-elements/less-than-or-equal-to-transact-sql.md)|작거나 같음|  
|[<>(같지 않음)](../../t-sql/language-elements/not-equal-to-transact-sql-traditional.md)|같지 않음|  
|[\!=(같지 않음)](../../t-sql/language-elements/not-equal-to-transact-sql-exclamation.md)|같지 않음(ISO 표준이 아님)|  
|[\!<(보다 작지 않음)](../../t-sql/language-elements/not-less-than-transact-sql.md)|보다 작지 않음(ISO 표준이 아님)|  
|[\!>(보다 크지 않음)](../../t-sql/language-elements/not-greater-than-transact-sql.md)|보다 크지 않음(ISO 표준이 아님)|  
  
## <a name="boolean-data-type"></a>부울 데이터 형식  
 비교 연산자의 결과는 **Boolean** 데이터 형식입니다. 이 결과에는 TRUE, FALSE 및 UNKNOWN이라는 세 가지 값이 있습니다. **Boolean** 데이터 형식을 반환하는 식을 부울 식이라고 합니다.  
  
 **Boolean** 데이터 형식은 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식과 달리 테이블 열이나 변수의 데이터 형식으로 지정될 수 없으며 결과 집합으로 반환될 수 없습니다.  
  
 SET ANSI_NULLS가 ON이면 한두 개의 NULL 식이 있는 연산자가 UNKNOWN을 반환합니다. SET ANSI_NULLS가 OFF이면 같음(=) 및 같지 않음(<>) 연산자를 제외하고 동일한 규칙이 적용됩니다. SET ANSI_NULLS가 OFF이면 이러한 연산자는 다른 모든 NULL과 동등한 알려진 값으로 NULL을 처리하고 TRUE 또는 FALSE(UNKNOWN은 절대 아님)만 반환합니다.  
  
 **Boolean** 데이터 형식의 식은 WHERE 절에서 검색 조건에 적합한 행을 필터링하는 데 사용되며 IF와 WHILE 등의 흐름 제어 언어 문에서 사용됩니다. 예를 들면 다음과 같습니다.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @MyProduct int;  
SET @MyProduct = 750;  
IF (@MyProduct <> 0)  
   SELECT ProductID, Name, ProductNumber  
   FROM Production.Product  
   WHERE ProductID = @MyProduct;  
```  
  
## <a name="see-also"></a>참고 항목  
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
