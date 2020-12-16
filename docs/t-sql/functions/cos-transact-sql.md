---
description: COS(Transact-SQL)
title: COS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COS
- COS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cosine
- COS function
ms.assetid: c9fa8ae1-3373-4f3e-9b97-fa05077c1040
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7f38e99beb7f57fa0b9e63e0bac8f5e86f0cf525
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468274"
---
# <a name="cos-transact-sql"></a>COS(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

지정한 식에서 지정한 각도로 측정된 지정된 각도의 삼각법 코사인을 라디안 단위로 반환하는 수학 함수입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
COS ( float_expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*float_expression*  
**float** 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.
  
## <a name="return-types"></a>반환 형식
**float**
  
## <a name="examples"></a>예제  
이 예제에서는 지정된 각도의 `COS` 값을 반환합니다.
  
```sql
  DECLARE @angle FLOAT;  
SET @angle = 14.78;  
SELECT 'The COS of the angle is: ' + CONVERT(VARCHAR,COS(@angle));  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
The COS of the angle is: -0.599465                        
  
(1 row(s) affected)  
```  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  


이 예제에서는 지정된 각도의 COS 값을 반환합니다.
  
```sql
SELECT COS(14.76) AS cosCalc1, COS(-0.1472738) AS cosCalc2;   
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
cosCalc1  cosCalc2
--------  --------
-0.58     0.99
```
  
## <a name="see-also"></a>참고 항목
[수치 연산 함수&#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)
  
  

