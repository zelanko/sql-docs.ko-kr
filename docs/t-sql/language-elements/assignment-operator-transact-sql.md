---
title: = (할당 연산자)(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], assignment
- assignment operators [Transact-SQL]
- headings [SQL Server columns]
- relationships [SQL Server], assignment operators
- column headings [SQL Server]
ms.assetid: c3040db6-21d6-40ac-a783-82c98ec006cc
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 51e8c7fb8f85eabe4f4e8fd30da6c95bf548e60f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33057490"
---
# <a name="-assignment-operator-transact-sql"></a>= (할당 연산자)(Transact-SQL)
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
  
## <a name="see-also"></a>참고 항목  
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [복합 연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
