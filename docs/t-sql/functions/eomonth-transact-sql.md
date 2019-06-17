---
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e7fd4ca761d87df2a98a8c88ab0848ddff2e4faa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65948848"
---
# <a name="eomonth-transact-sql"></a>EOMONTH(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

이 함수는 선택 사항인 오프셋 옵션을 사용하여 지정한 날짜가 포함된 달의 마지막 날을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
EOMONTH ( start_date [, month_to_add ] )  
```  
  
## <a name="arguments"></a>인수  
*start_date*  
달의 마지막 날을 반환하는 날짜를 지정하는 날짜 식입니다.  
  
*month_to_add*  
*start_date*에 추가할 개월 수를 지정하는 선택적 정수 식입니다.  
  
*month_to_add* 인수가 값을 가지면 `EOMONTH`는 지정한 개월 수를 *start_date*에 추가한 다음, 결과 날짜에 해당하는 달의 마지막 날을 반환합니다. 추가로 인해 유효한 날짜 범위를 벗어날 경우 `EOMONTH`는 오류를 발생시킵니다.  
  
## <a name="return-type"></a>반환 형식  
 **date**  
  
## <a name="remarks"></a>Remarks  
`EOMONTH` 함수는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 서버 이상 버전에 대해서는 원격으로 실행할 수 있습니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이전 버전의 서버에 대해서는 원격으로 실행할 수 없습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-eomonth-with-explicit-datetime-type"></a>1\. 명시적 datetime 형식을 사용하는 EOMONTH  
  
```  
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

### <a name="b-eomonth-with-string-parameter-and-implicit-conversion"></a>2\. 문자열 매개 변수 및 암시적 변환을 사용하는 EOMONTH  
  
```  
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
  
### <a name="c-eomonth-with-and-without-the-monthtoadd-parameter"></a>C. month_to_add 매개 변수를 사용하거나 사용하지 않는 EOMONTH  
  
참고: 이러한 결과 집합에 표시된 값은 실행 날짜를 반환합니다.
        
        12/01/2011
        
        and
        
        12/31/2011

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
  
  

