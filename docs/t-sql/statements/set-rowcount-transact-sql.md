---
description: SET ROWCOUNT (Transact-SQL)
title: SET ROWCOUNT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET_ROWCOUNT_TSQL
- ROWCOUNT_TSQL
- SET ROWCOUNT
- ROWCOUNT
dev_langs:
- TSQL
helpviewer_keywords:
- row return limitations [SQL Server]
- SET ROWCOUNT statement
- number of rows affected by statement
- ROWCOUNT option
- counting rows
- stopping queries
- limiting rows returned
- queries [SQL Server], stopping
ms.assetid: c6966fb7-6421-47ef-98f3-82351f2f6bdc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aaf1d91677429b6870ff42684d302528e5df3376
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471844"
---
# <a name="set-rowcount-transact-sql"></a>SET ROWCOUNT (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  지정한 행 수가 반환된 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 쿼리 처리를 중지하도록 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
SET ROWCOUNT { number | @number_var }   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *number* | @*number_var*  
 특정 쿼리를 중지하기 전에 처리된 행의 수(정수)입니다.  
  
## <a name="remarks"></a>설명  
  
> [!IMPORTANT]  
>  SQL Server의 다음 버전에서는 SET ROWCOUNT 옵션을 사용해도 DELETE, INSERT 및 UPDATE 문에 영향을 주지 않습니다. 새 개발 작업에서는 DELETE, INSERT 및 UPDATE 문에 SET ROWCOUNT 옵션을 사용하지 않도록 하고 현재 이 옵션을 사용하는 애플리케이션은 수정하세요. 유사한 동작의 경우 TOP 구문을 사용합니다. 자세한 내용은 [TOP&#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)을 참조하세요.  
  
 모든 행이 반환될 수 있도록 이 옵션을 해제하려면 SET ROWCOUNT 0을 지정하세요.  
  
 SET ROWCOUNT 옵션을 설정하면 대부분의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 지정한 행 수에 영향을 받게 될 때 처리를 중지합니다. 여기에는 트리거가 포함됩니다. ROWCOUNT 옵션은 동적 커서에는 영향을 주지 않지만 키 집합 및 INSENSITIVE 커서의 행 집합을 제한합니다. 이 옵션을 사용할 때는 주의해야 합니다.  
  
 SET ROWCOUNT 옵션은 행 개수가 더 작은 값일 경우 SELECT 문의 TOP 키워드보다 우선 적용됩니다.  
  
 SET ROWCOUNT 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
 SET ROWCOUNT는 지정한 행 수 이후에는 처리를 중지합니다. 다음 예에서는 500개 이상의 행이 `Quantity`보다 작은 `300` 조건과 일치합니다. 그러나 SET ROWCOUNT를 적용한 후 일부 행이 반환되지 않은 것을 알 수 있습니다.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT count(*) AS Count  
FROM Production.ProductInventory  
WHERE Quantity < 300;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Count 
 ----------- 
 537 
 
 (1 row(s) affected)
 ```  
  
 이제 `ROWCOUNT`를 `4`로 설정하고 모든 행을 반환하여 4개의 행만 반환되는지 확인합니다.  
  
```sql
SET ROWCOUNT 4;  
SELECT *  
FROM Production.ProductInventory  
WHERE Quantity < 300;  
GO  
  
-- (4 row(s) affected)
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 SET ROWCOUNT는 지정한 행 수 이후에는 처리를 중지합니다. 다음 예에서는 20개를 초과한 행이 `AccountType = 'Assets'`의 기준을 충족한다는 것에 유의하십시오. 그러나 SET ROWCOUNT를 적용한 후 일부 행이 반환되지 않은 것을 알 수 있습니다.  
  
```sql
-- Uses AdventureWorks  
  
SET ROWCOUNT 5;  
SELECT * FROM [dbo].[DimAccount]  
WHERE AccountType = 'Assets';  
```  
  
 모든 행을 반환하려면 ROWCOUNT를 0으로 설정합니다.  
  
```sql
-- Uses AdventureWorks  
  
SET ROWCOUNT 0;  
SELECT * FROM [dbo].[DimAccount]  
WHERE AccountType = 'Assets';  
```  
  
## <a name="see-also"></a>관련 항목  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

