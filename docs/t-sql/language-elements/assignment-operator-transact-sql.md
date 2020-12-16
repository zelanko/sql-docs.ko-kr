---
description: = (할당 연산자)(Transact-SQL)
title: = (할당 연산자)(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 86e9675dd5a11869c73f8f7dc77c12589cd38e1f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468044"
---
# <a name="-assignment-operator-transact-sql"></a>= (할당 연산자)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  등호(=)가 유일한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 대입 연산자입니다. 다음 예에서는 `@MyCounter` 변수가 만들어진 다음 대입 연산자가 `@MyCounter`를 식에서 반환된 값으로 설정합니다.  
  
```sql  
DECLARE @MyCounter INT;  
SET @MyCounter = 1;  
```  
  
 대입 연산자는 열 머리글과 열에 대한 값을 정의하는 식 사이의 관계를 설정하는 데도 사용할 수 있습니다. 다음 예에서는 열 머리글 `FirstColumnHeading` 및 `SecondColumnHeading`를 표시합니다. 문자열 `xyz`는 모든 행의 `FirstColumnHeading` 열 머리글에 표시됩니다. 그런 다음 `Product` 테이블의 각 제품 ID가 `SecondColumnHeading` 열 머리글에 나열됩니다.  
  
```sql  
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
  
  
