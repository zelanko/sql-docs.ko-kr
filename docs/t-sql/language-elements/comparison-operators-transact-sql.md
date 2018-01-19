---
title: "비교 연산자 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- expressions [SQL Server], testing
- operators [Transact-SQL], comparison
- testing expressions
- Boolean data type
- Boolean expressions
- comparing expressions
- comparison operators [SQL Server]
ms.assetid: b0cc68ef-3029-484c-a917-0c15dcbc230d
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 7c36efad752eb830b44415add3d279a4a3ecf3ab
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="comparison-operators-transact-sql"></a>비교 연산자(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  비교 연산자는 두 식이 동일한지 여부를 테스트합니다. 비교 연산자의 식 제외한 모든 식에서 사용할 수 있습니다는 **텍스트**, **ntext**, 또는 **이미지** 데이터 형식입니다. 다음 표에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 비교 연산자를 나열합니다.  
  
|연산자|의미|  
|--------------|-------------|  
|[=(같음)](../../t-sql/language-elements/equals-transact-sql.md)|같음|  
|[>(보다 큼)](../../t-sql/language-elements/greater-than-transact-sql.md)|보다 큼|  
|[<(보다 작음)](../../t-sql/language-elements/less-than-transact-sql.md)|보다 작음|  
|[>=(크거나 같음)](../../t-sql/language-elements/greater-than-or-equal-to-transact-sql.md)|크거나 같음|  
|[<=(작거나 같음)](../../t-sql/language-elements/less-than-or-equal-to-transact-sql.md)|작거나 같음|  
|[<>(같지 않음)](../../t-sql/language-elements/not-equal-to-transact-sql-traditional.md)|같지 않음|  
|[\!= (같지 않음)](../../t-sql/language-elements/not-equal-to-transact-sql-exclamation.md)|같지 않음(ISO 표준이 아님)|  
|[\!< (보다 작지 않음)](../../t-sql/language-elements/not-less-than-transact-sql.md)|보다 작지 않음(ISO 표준이 아님)|  
|[\!> (보다 크지 않음)](../../t-sql/language-elements/not-greater-than-transact-sql.md)|보다 크지 않음(ISO 표준이 아님)|  
  
## <a name="boolean-data-type"></a>부울 데이터 형식  
 비교 연산자의 결과는 **부울** 데이터 형식입니다. 이 결과: TRUE, FALSE 및 UNKNOWN입니다. 반환 하는 식은 **부울** 데이터 형식이 부울 식 이라고 합니다.  
  
 다른 달리 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에는 **부울** 데이터 형식 테이블 열 또는 변수, 데이터 형식으로 지정할 수 없습니다 및 결과 집합에 반환 될 수 없습니다.  
  
 SET ANSI_NULLS가 ON이면 한두 개의 NULL 식이 있는 연산자가 UNKNOWN을 반환합니다. SET ANSI_NULLS가 OFF인 경우에도 같은 규칙이 적용됩니다. 단, 등호(=) 연산자는 두 식이 모두 NULL인 경우에 TRUE를 반환합니다. 예를 들어 NULL = NULL은 SET ANSI_NULLS가 OFF인 경우에 TRUE를 반환합니다.  
  
 가 있는 식 **부울** 데이터 형식은 및 한 정하는 검색 조건에 대 한 흐름 제어 언어 문에서 등 IF와 WHILE, 예를 들어 행을 필터링 할 WHERE 절에 사용 됩니다.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @MyProduct int;  
SET @MyProduct = 750;  
IF (@MyProduct <> 0)  
   SELECT ProductID, Name, ProductNumber  
   FROM Production.Product  
   WHERE ProductID = @MyProduct;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
