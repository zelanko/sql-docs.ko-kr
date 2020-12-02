---
description: SET STATISTICS TIME(Transact-SQL)
title: SET STATISTICS TIME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET_STATISTICS_TIME_TSQL
- SET STATISTICS TIME
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], statement processing
- time [SQL Server], statement processing statistics
- SET STATISTICS TIME statement
- STATISTICS TIME option
- statements [SQL Server], statistical information
- parsing [SQL Server], SET STATISTICS TIME statement
- compile times [SQL Server]
- execution processing time [SQL Server]
ms.assetid: eec2e1cd-a29d-4cf3-a271-be9d61506f15
author: markingmyname
ms.author: maghan
ms.openlocfilehash: abde67780d0eff93a791a2b48654ba712dea6859
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "89539812"
---
# <a name="set-statistics-time-transact-sql"></a>SET STATISTICS TIME(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  각 문을 구문 분석, 컴파일 및 실행하는 데 필요한 시간(밀리초)을 표시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
SET STATISTICS TIME { ON | OFF }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>설명
 SET STATISTICS TIME 옵션을 ON으로 설정하면 문에 대한 시간 통계가 표시됩니다. OFF로 설정하면 시간 통계가 표시되지 않습니다.  
  
 SET STATISTICS TIME 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
 **lightweight pooling** 구성 옵션을 설정하면 활성화되는 파이버 모드에서는 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 정확한 통계를 제공할 수 없습니다.  
  
 SET STATISTICS TIME을 ON으로 설정해 쿼리를 실행하면 **sysprocesses** 테이블의 **cpu** 열만 업데이트됩니다. SET STATISTICS TIME이 OFF인 경우에는 **0** 이 반환됩니다.  
  
 ON과 OFF 설정은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 Process Info View for Current Activity에 있는 CPU 열에도 영향을 줍니다.  
  
## <a name="permissions"></a>사용 권한  
 SET STATISTICS TIME을 사용하려면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있는 적절한 권한이 있어야 합니다. SHOWPLAN 권한이 필요하지 않습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 서버 실행, 구문 분석 및 컴파일 시간을 보여 줍니다.  
  
```sql
USE AdventureWorks2012;  
GO         
SET STATISTICS TIME ON;  
GO  
SELECT ProductID, StartDate, EndDate, StandardCost   
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET STATISTICS TIME OFF;  
GO  
```  
  
 결과 집합은 다음과 같습니다.  
  
```  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
  
(269 row(s) affected)  
  
SQL Server Execution Times:  
   CPU time = 0 ms,  elapsed time = 2 ms.  
SQL Server parse and compile time:   
   CPU time = 0 ms, elapsed time = 1 ms.  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET STATISTICS IO &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  
