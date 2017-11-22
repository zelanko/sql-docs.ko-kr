---
title: "= (대입 연산자) (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- operators [Transact-SQL], assignment
- assignment operators [Transact-SQL]
- headings [SQL Server columns]
- relationships [SQL Server], assignment operators
- column headings [SQL Server]
ms.assetid: c3040db6-21d6-40ac-a783-82c98ec006cc
caps.latest.revision: "29"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 51f9aef3b4ef22dc63e36524627589b3f3c0c4cf
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="-assignment-operator-transact-sql"></a>= (대입 연산자) (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  등호(=)가 유일한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 대입 연산자입니다. 다음 예에서는 `@MyCounter` 변수가 만들어진 다음 대입 연산자가 `@MyCounter`를 식에서 반환된 값으로 설정합니다.  
  
```  
DECLARE @MyCounter INT;  
SET @MyCounter = 1;  
```  
  
 대입 연산자는 열 머리글과 열에 대한 값을 정의하는 식 사이의 관계를 설정하는 데도 사용할 수 있습니다. 다음 예에서는 열 머리글 `FirstColumnHeading` 및 `SecondColumnHeading`를 표시합니다. 문자열 `xyz`는 모든 행의 `FirstColumnHeading` 열 머리글에 표시됩니다. 그런 다음 `Product` 테이블의 각 제품 ID가 `SecondColumnHeading` 열 머리글에 나열됩니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstColumnHeading = 'xyz',  
       SecondColumnHeading = ProductID  
FROM Production.Product;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [복합 연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
