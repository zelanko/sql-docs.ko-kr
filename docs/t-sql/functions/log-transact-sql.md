---
title: LOG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- LOG
- LOG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- float expressions
- logarithm of expression
- LOG function
ms.assetid: f7c39511-cd84-4362-93ba-0d93655217ee
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1d3cbf58a3a85d84daf5b0f83006a7cdcb24b589
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73982253"
---
# <a name="log-transact-sql"></a>LOG(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  **에서 지정된** float[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 식의 자연 로그를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server  
  
LOG ( float_expression [, base ] )  
```  
  
```  
-- Syntax for Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
LOG ( float_expression )  
```  
  
## <a name="arguments"></a>인수  
 *float_expression*  
 [float](../../t-sql/language-elements/expressions-transact-sql.md) 형식 또는 **float**로 암시적으로 변환되는 형식의 **식**입니다.  
  
 *base*  
 로그 밑을 설정하는 선택적 정수 인수입니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상
  
## <a name="return-types"></a>반환 형식  
 **float**  
  
## <a name="remarks"></a>설명  
 기본적으로 **LOG()** 는 자연 로그를 반환합니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터는 선택적 *베이스* 매개 변수를 사용하여 로그 밑을 다른 값으로 변경할 수 있습니다.  
  
 자연 로그는 밑이 **e**인 로그입니다. 여기서 **e**는 대략 2.718281828과 같은 무리 상수입니다.  
  
 한 수의 지수에 대한 자연 로그는 그 수 자체입니다. LOG( EXP( *n* ) ) = *n*. 한 수의 자연 로그에 대한 지수는 그 수 자체입니다. EXP( LOG( *n* ) ) = *n*.  
  
## <a name="examples"></a>예  
  
### <a name="a-calculating-the-logarithm-for-a-number"></a>A. 수의 로그를 계산합니다.  
 다음 예에서는 지정된 `LOG`float**식의**를 계산하는 방법을 보여 줍니다.  
  
```  
DECLARE @var float = 10;  
SELECT 'The LOG of the variable is: ' + CONVERT(varchar, LOG(@var));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------------------------  
The LOG of the variable is: 2.30259  
  
(1 row(s) affected)  
```  
  
### <a name="b-calculating-the-logarithm-of-the-exponent-of-a-number"></a>B. 수의 지수에 대한 로그를 계산합니다.  
 다음 예에서는 수의 지수에 대한 `LOG`를 계산합니다.  
  
```  
SELECT LOG (EXP (10));  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------------------------  
10  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-calculating-the-logarithm-for-a-number"></a>C. 수의 로그를 계산합니다.  
 다음 예에서는 지정된 `LOG`float**식의**를 계산하는 방법을 보여 줍니다.  
  
```  
SELECT LOG(10);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ----------------`  
  
 2.30
 ```  
  
## <a name="see-also"></a>참고 항목  
 [수치 연산 함수&#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [EXP &#40;Transact-SQL&#41;](../../t-sql/functions/exp-transact-sql.md)   
 [LOG10&#40;Transact-SQL&#41;](../../t-sql/functions/log10-transact-sql.md)  
  
  

