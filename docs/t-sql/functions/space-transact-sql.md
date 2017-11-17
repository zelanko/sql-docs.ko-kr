---
title: "공간 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SPACE_TSQL
- SPACE
dev_langs:
- TSQL
helpviewer_keywords:
- strings [SQL Server], repeated spaces
- repeated spaces
- SPACE function
ms.assetid: b4fac3b8-2d47-4c11-a6a6-009e5a538f40
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f5de41d3d7619af5f83fa2bee8cd30f980f291b7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="space-transact-sql"></a>SPACE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  반복된 공백 문자열을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SPACE ( integer_expression )  
```  
  
## <a name="arguments"></a>인수  
 *integer_expression*  
 공백 수를 나타내는 양의 정수입니다. 경우 *integer_expression* 가 음수 이면 null 문자열이 반환 됩니다.  
  
 자세한 내용은 참조 [식 &#40; Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
## <a name="return-types"></a>반환 형식  
 **varchar**  
  
## <a name="remarks"></a>주의  
 유니코드 데이터에 공백을 포함하거나 8000개가 넘는 공백을 반환하려면 SPACE 대신 REPLICATE를 사용합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 성을 없애고 쉼표 하나, 공백 두 개 및 `Person`의 `AdventureWorks2012` 테이블에 나열된 사람의 이름을 연결합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT RTRIM(LastName) + ',' + SPACE(2) +  LTRIM(FirstName)  
FROM Person.Person  
ORDER BY LastName, FirstName;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 성을 없애고 쉼표 하나, 공백 두 개 및 `DimCustomer`의 `AdventureWorksPDW2012` 테이블에 나열된 사람의 이름을 연결합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT RTRIM(LastName) + ',' + SPACE(2) +  LTRIM(FirstName)  
FROM dbo.DimCustomer  
ORDER BY LastName, FirstName;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [복제 &#40; Transact SQL &#41;](../../t-sql/functions/replicate-transact-sql.md)   
 [문자열 함수 &#40; Transact SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  



