---
title: NOT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- NOT_TSQL
- NOT
dev_langs:
- TSQL
helpviewer_keywords:
- negating Boolean input
- NOT operator [Transact-SQL]
- expressions [SQL Server], negating
- reversing Boolean expression values
ms.assetid: dc07cc35-20f1-46e6-9995-2938390dc19a
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 30977ed0baff058c838403b436a4da497c5ac4c8
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68121986"
---
# <a name="not-transact-sql"></a>NOT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  부울 입력을 부정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
[ NOT ] boolean_expression  
```  
  
## <a name="arguments"></a>인수  
 *boolean_expression*  
 유효한 부울 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
## <a name="result-types"></a>결과 형식  
 **Boolean**  
  
## <a name="result-value"></a>결과 값  
 NOT은 부울 식의 값을 역으로 표시합니다.  
  
## <a name="remarks"></a>설명  
 NOT을 사용하면 식을 부정합니다.  
  
 다음 표에서는 NOT 연산자를 사용하여 TRUE와 FALSE 값을 비교한 결과를 보여 줍니다.  
  
||NOT|  
|------|---------|  
|**TRUE**|FALSE|  
|**FALSE**|TRUE|  
|**UNKNOWN**|UNKNOWN|  
  
## <a name="examples"></a>예  
 다음 예에서는 표준 가격이 400달러 이하인 은색 자전거를 모두 찾습니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID, Name, Color, StandardCost  
FROM Production.Product  
WHERE ProductNumber LIKE 'BK-%' AND Color = 'Silver' AND NOT StandardCost > 400;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ProductID   Name                     Color         StandardCost
 ---------   -------------------      ------      ------------
 984         Mountain-500 Silver, 40  Silver        308.2179
 985         Mountain-500 Silver, 42  Silver        308.2179
 986         Mountain-500 Silver, 44  Silver        308.2179
 987         Mountain-500 Silver, 48  Silver        308.2179
 988         Mountain-500 Silver, 52  Silver        308.2179
 (6 row(s) affected)
 ```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예제에서는 `SalesOrderNumber`에 대한 결과를 400보다 크거나 같은 `SO6` 및 `ProductKeys`로 시작하는 값으로 제한합니다.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductKey, CustomerKey, OrderDateKey, ShipDateKey  
FROM FactInternetSales  
WHERE SalesOrderNumber LIKE 'SO6%' AND NOT ProductKey < 400;  
```  
  
## <a name="see-also"></a>참고 항목  
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [기본 제공 함수s&#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [연산자&#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE&#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  


