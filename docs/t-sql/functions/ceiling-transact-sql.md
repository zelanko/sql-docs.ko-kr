---
title: CEILING(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CEILING_TSQL
- CEILING
dev_langs:
- TSQL
helpviewer_keywords:
- smallest integer great than or equal to expression
- integers [SQL Server]
- CEILING function [Transact-SQL]
ms.assetid: e736b43a-9457-4781-95a4-4bcf9d4fc46a
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eddc3ca55ebd1eb0fcc87b1346946033e34a9d99
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823296"
---
# <a name="ceiling-transact-sql"></a>CEILING(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

이 함수는 지정한 숫자 식보다 크거나 같은 최소 정수를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
CEILING ( numeric_expression )  
```  
  
## <a name="arguments"></a>인수  
*numeric_expression*  
정밀 숫자 또는 근사 숫자 데이터 형식 범주의 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다. 이 함수에는 **비트** 데이터 형식이 부적합합니다.
  
## <a name="return-types"></a>반환 형식
반환 값은 *numeric_expression*과 같은 형식입니다.
  
## <a name="examples"></a>예  
이 예에서는 CEILING 함수에 대한 양수, 음수 및 0 값 입력을 보여 줍니다.
  
```sql
SELECT CEILING($123.45), CEILING($-123.45), CEILING($0.0);  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
--------- --------- -------------------------   
124.00    -123.00    0.00                       
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목
[시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)
  
  
