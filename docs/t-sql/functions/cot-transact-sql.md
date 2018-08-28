---
title: COT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COT_TSQL
- COT
dev_langs:
- TSQL
helpviewer_keywords:
- COT function
- cotangent
ms.assetid: c87a9dac-e398-4125-80c3-7df3c2ce6b63
caps.latest.revision: 31
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f5a42f6e09040457775ef2871eb93acab7d5fd62
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43111858"
---
# <a name="cot-transact-sql"></a>COT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

지정한 **float** 식에서 지정한 각도의 삼각법 코탄젠트를 라디안 단위로 반환하는 수학 함수입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
COT ( float_expression )  
```  
  
## <a name="arguments"></a>인수  
*float_expression*  
**float** 형식 또는 **float**로 암시적으로 변환할 수 있는 형식의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.
  
## <a name="return-types"></a>반환 형식
**float**
  
## <a name="examples"></a>예  
이 예제에서는 특정 각도의 `COT` 값을 반환합니다.
  
```sql
DECLARE @angle float;  
SET @angle = 124.1332;  
SELECT 'The COT of the angle is: ' + CONVERT(varchar,COT(@angle));  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
The COT of the angle is: -0.040312                
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>관련 항목:
[수치 연산 함수&#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)
  
  

