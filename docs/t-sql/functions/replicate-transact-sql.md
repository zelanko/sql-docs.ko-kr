---
description: REPLICATE(Transact-SQL)
title: REPLICATE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- REPLICATE_TSQL
- REPLICATE
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], repeating
- REPLICATE function
- repeating character expressions
ms.assetid: 0cd467fb-3f22-471a-892c-0039d9f7fa1a
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d047aa77ca0587a26225f8c0b180d81a8e48fb2d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462454"
---
# <a name="replicate-transact-sql"></a>REPLICATE(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  지정한 횟수만큼 문자열 값을 반복합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
REPLICATE ( string_expression , integer_expression )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *string_expression*  
 문자 또는 이진 데이터 형식의 식입니다.  
  
> [!NOTE]  
> *string_expression* 이 **binary** 형식이라면 REPLICATE는 **varchar** 로의 암시적 변환을 수행하며 따라서 이진 입력을 유지하지 않습니다.  

> [!NOTE]  
> *string_expression* 입력이 **varchar(max)** 또는 **nvarchar(max)** 형식이라면 REPLICATE는 반환 값을 8,000 바이트에서 자릅니다. 8,000바이트를 초과하는 값을 반환하려면 *string_expression* 을 적절한 큰 값 데이터 형식으로 명시적으로 캐스팅해야 합니다.  
  
 *integer_expression*  
 **bigint** 를 포함하는 정수 유형의 식입니다. *integer_expression* 이 음수이면 NULL이 반환됩니다.  
  
## <a name="return-types"></a>반환 형식  
 *string_expression* 과 같은 유형을 반환합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-using-replicate"></a>A. REPLICATE 사용  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 프로덕션 코드 줄 앞에 `0` 문자를 4번 복제합니다.  
  
```sql
SELECT [Name]  
, REPLICATE('0', 4) + [ProductLine] AS 'Line Code'  
FROM [Production].[Product]  
WHERE [ProductLine] = 'T'  
ORDER BY [Name];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Name                                               Line Code  
-------------------------------------------------- ---------  
HL Touring Frame - Blue, 46                        0000T   
HL Touring Frame - Blue, 50                        0000T   
HL Touring Frame - Blue, 54                        0000T   
HL Touring Frame - Blue, 60                        0000T   
HL Touring Frame - Yellow, 46                      0000T   
HL Touring Frame - Yellow, 50                      0000T  
...  
```  
  
### <a name="b-using-replicate-and-datalength"></a>B. REPLICATE 및 DATALENGTH 사용  
 다음 예에서는 숫자 데이터 형식을 문자 또는 유니코드로 변환할 때 지정한 길이까지 0으로 왼쪽을 채웁니다.  
  
```sql
IF EXISTS(SELECT name FROM sys.tables  
      WHERE name = 't1')  
   DROP TABLE t1;  
GO  
CREATE TABLE t1   
(  
 c1 varchar(3),  
 c2 char(3)  
);  
GO  
INSERT INTO t1 VALUES ('2', '2'), ('37', '37'),('597', '597');  
GO  
SELECT REPLICATE('0', 3 - DATALENGTH(c1)) + c1 AS 'Varchar Column',  
       REPLICATE('0', 3 - DATALENGTH(c2)) + c2 AS 'Char Column'  
FROM t1;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Varchar Column        Char Column  
--------------------  ------------  
002                   2    
037                   37   
597                   597  
  
(3 row(s) affected)  
  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-replicate"></a>C: REPLICATE 사용  
 다음 예에서는 `ItemCode` 값 앞의 `0` 문자를 4번 복제합니다.  
  
```sql
-- Uses AdventureWorks  
  
SELECT EnglishProductName AS Name,  
   ProductAlternateKey AS ItemCode,  
   REPLICATE('0', 4) + ProductAlternateKey AS FullItemCode  
FROM dbo.DimProduct  
ORDER BY Name;  
```  
  
 다음은 결과 집합의 첫 번째 행입니다.  
  
 ```
Name                     ItemCode       FullItemCode
------------------------ -------------- ---------------
Adjustable Race          AR-5381        0000AR-5381
All-Purpose Bike Stand   ST-1401        0000ST-1401
AWC Logo Cap             CA-1098        0000CA-1098
AWC Logo Cap             CA-1098        0000CA-1098
AWC Logo Cap             CA-1098        0000CA-1098
BB Ball Bearing          BE-2349        0000BE-2349
 ```  
  
## <a name="see-also"></a>참고 항목  
 [SPACE&#40;Transact-SQL&#41;](../../t-sql/functions/space-transact-sql.md)  
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [문자열 함수&#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

