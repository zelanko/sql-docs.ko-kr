---
title: FLOOR(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FLOOR_TSQL
- FLOOR
dev_langs:
- TSQL
helpviewer_keywords:
- integers [SQL Server]
- largest integers
- FLOOR function [Transact-SQL]
ms.assetid: 4f26c784-9240-491f-b854-754be3fccae4
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2e366876c5b71f410f05b7ed4483347b1f754686
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74249805"
---
# <a name="floor-transact-sql"></a>FLOOR(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정된 숫자 식보다 작거나 같은 최대 정수를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
FLOOR ( numeric_expression )  
```  
  
## <a name="arguments"></a>인수  
 *numeric_expression*  
 **bit** 데이터 형식을 제외한 정확한 수치 또는 근사치 데이터 형식 범주의 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 *numeric_expression*과 같은 유형을 반환합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `FLOOR` 함수의 인수로 양수, 음수 및 통화 값을 넣고 계산합니다.  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR($123.45);  
```  
  
 결과는 *numeric_expression*과 동일한 데이터 형식으로 계산된 값의 정수 부분입니다.  
  
```  
---------      ---------     -----------  
123            -124          123.0000     
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 양수, 음수 및 `FLOOR` 함수 값을 보여줍니다.  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR($123.45);  
```  
  
 결과는 *numeric_expression*과 동일한 데이터 형식으로 계산된 값의 정수 부분입니다.  
  
 ```
 -----   ---------    -----------  
  
 123     -124         123
 ```  
  
## <a name="see-also"></a>참고 항목  
 [수치 연산 함수&#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  

