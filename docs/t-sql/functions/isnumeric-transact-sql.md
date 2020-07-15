---
title: ISNUMERIC(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ISNUMERIC
- ISNUMERIC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], valid numeric type
- numeric data
- ISNUMERIC function
- verifying valid numeric type
- valid numeric type [SQL Server]
- checking valid numeric type
ms.assetid: 7aa816de-529a-4f6c-a99f-4d5a9ef599eb
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 813d2b8be0797e510728e9d61f9e2bb965931e29
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012836"
---
# <a name="isnumeric-transact-sql"></a>ISNUMERIC(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  식이 유효한 숫자 유형인지 여부를 지정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
``` 
ISNUMERIC ( expression )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 평가해야 하는 [식](../../t-sql/language-elements/expressions-transact-sql.md)입니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>설명  
 ISNUMERIC은 입력 식이 올바른 숫자 데이터 형식으로 평가되면 1을 반환하고 그렇지 않으면 0을 반환합니다. 올바른 [숫자 데이터 형식](../../t-sql/data-types/numeric-types.md)은 다음과 같습니다.  

| 영역 | 숫자 데이터 형식 |
|-|-|
| [정확한 수치](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md) | **bigint**, **int**, **smallint**, **tinyint**, **bit** |
| [고정 전체 자릿수](../../t-sql/data-types/decimal-and-numeric-transact-sql.md) | **decimal**, **numeric** |
| [근사치](../../t-sql/data-types/float-and-real-transact-sql.md) | **float**, **real** |
| [통화 값](../../t-sql/data-types/money-and-smallmoney-transact-sql.md) | **money**, **smallmoney** |

> [!NOTE]  
> ISNUMERIC은 더하기(+), 빼기(-)와 같은 숫자가 아닌 일부 문자 및 달러 기호($)와 같은 올바른 통화 기호에 대해 1을 반환합니다. 통화 기호의 전체 목록은 [money 및 smallmoney &#40;Transact-SQL&#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)을 참조하세요.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `ISNUMERIC`을 사용하여 숫자 값이 아닌 모든 우편 번호를 반환합니다.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT City, PostalCode  
FROM Person.Address   
WHERE ISNUMERIC(PostalCode) <> 1;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 `ISNUMERIC`을 사용하여 숫자 값이 아닌 모든 우편 번호를 반환합니다.  
  
```sql
USE master;  
GO  
SELECT name, ISNUMERIC(name) AS IsNameANumber, database_id, ISNUMERIC(database_id) AS IsIdANumber   
FROM sys.databases;  
GO  
```  
  
## <a name="see-also"></a>참고 항목

- [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)
- [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)
- [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
