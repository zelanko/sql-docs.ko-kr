---
description: EOMONTH(Transact-SQL)
title: EOMONTH(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EOMONTH
- EOMONTH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EOMONTH function
ms.assetid: 1d060d8e-3297-4244-afef-57df2f8f92e2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ebf85e3455d0024cfc6e7e850b20678717257849
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462514"
---
# <a name="eomonth-transact-sql"></a>EOMONTH(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 함수는 선택 사항인 오프셋 옵션을 사용하여 지정한 날짜가 포함된 달의 마지막 날을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
EOMONTH ( start_date [, month_to_add ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*start_date*  
달의 마지막 날을 반환하는 날짜를 지정하는 날짜 식입니다.  
  
*month_to_add*  
*start_date* 에 추가할 개월 수를 지정하는 선택적 정수 식입니다.  
  
*month_to_add* 인수가 값을 가지면 `EOMONTH`는 지정한 개월 수를 *start_date* 에 추가한 다음, 결과 날짜에 해당하는 달의 마지막 날을 반환합니다. 추가로 인해 유효한 날짜 범위를 벗어날 경우 `EOMONTH`는 오류를 발생시킵니다.  
  
## <a name="return-type"></a>반환 형식  
 **date**  
  
## <a name="remarks"></a>설명  
`EOMONTH` 함수는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 서버 이상 버전에 대해서는 원격으로 실행할 수 있습니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이전 버전의 서버에 대해서는 원격으로 실행할 수 없습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-eomonth-with-explicit-datetime-type"></a>A. 명시적 datetime 형식을 사용하는 EOMONTH  
  
```sql 
DECLARE @date DATETIME = '12/1/2011';  
SELECT EOMONTH ( @date ) AS Result;  
GO  
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
2011-12-31  
  
(1 row(s) affected)  
```  

### <a name="b-eomonth-with-string-parameter-and-implicit-conversion"></a>B. 문자열 매개 변수 및 암시적 변환을 사용하는 EOMONTH  
  
```sql
DECLARE @date VARCHAR(255) = '12/1/2011';  
SELECT EOMONTH ( @date ) AS Result;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
2011-12-31  
  
(1 row(s) affected)  
```  
  
### <a name="c-eomonth-with-and-without-the-month_to_add-parameter"></a>C. month_to_add 매개 변수를 사용하거나 사용하지 않는 EOMONTH  
  
이러한 결과 집합에 표시된 값은 `12/01/2011`과 `12/31/2011` 사이의 실행 날짜(두 날짜 포함)를 반영합니다.

```sql  
DECLARE @date DATETIME = GETDATE();  
SELECT EOMONTH ( @date ) AS 'This Month';  
SELECT EOMONTH ( @date, 1 ) AS 'Next Month';  
SELECT EOMONTH ( @date, -1 ) AS 'Last Month';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
This Month  
-----------------------  
2011-12-31  
  
(1 row(s) affected)  
  
Next Month  
-----------------------  
2012-01-31  
  
(1 row(s) affected)  
  
Last Month  
-----------------------  
2011-11-30  
  
(1 row(s) affected)  
```
