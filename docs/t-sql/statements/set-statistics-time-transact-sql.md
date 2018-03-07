---
title: SET STATISTICS TIME (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 523227164984cdabcb65afa3b9213c1cb0d0f18e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="set-statistics-time-transact-sql"></a>SET STATISTICS TIME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  각 문을 구문 분석, 컴파일 및 실행하는 데 필요한 시간(밀리초)을 표시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SET STATISTICS TIME { ON | OFF }  
```  
  
## <a name="remarks"></a>주의  
 SET STATISTICS TIME 옵션을 ON으로 설정하면 문에 대한 시간 통계가 표시됩니다. OFF로 설정하면 시간 통계가 표시되지 않습니다.  
  
 SET STATISTICS TIME 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하도록 설정 하면 활성화 되는 파이버 모드에서 정확한 통계를 제공 하지 못하면는 **경량 풀링** 구성 옵션입니다.  
  
 **cpu** 열에는 **sysprocesses** 테이블은 SET STATISTICS TIME ON으로 쿼리를 실행할 때만 업데이트 됩니다. SET STATISTICS TIME이 OFF 인 경우 **0** 반환 됩니다.  
  
 ON과 OFF 설정은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 Process Info View for Current Activity에 있는 CPU 열에도 영향을 줍니다.  
  
## <a name="permissions"></a>Permissions  
 SET STATISTICS TIME을 사용하려면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있는 적절한 권한이 있어야 합니다. SHOWPLAN 권한이 필요하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 서버 실행, 구문 분석 및 컴파일 시간을 보여 줍니다.  
  
```  
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
  
## <a name="see-also"></a>관련 항목:  
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET STATISTICS IO &#40; Transact SQL &#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)  
  
  
