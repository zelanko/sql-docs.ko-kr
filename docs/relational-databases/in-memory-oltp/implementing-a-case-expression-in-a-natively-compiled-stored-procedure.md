---
title: 고유하게 컴파일된 저장 프로시저의 CASE 식
description: 고유하게 컴파일된 T-SQL 모듈은 일부 버전의 SQL Server에서 CASE 식을 지원합니다. 이 예제에서는 쿼리에 CASE 식을 구현합니다.
ms.custom: seo-dt-2019
ms.date: 11/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2f82db01-da7e-4a7d-8bc0-48b245e6f768
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 10dac4fb1068e42d296c5091da5e7c9ff6d96eec
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460456"
---
# <a name="implementing-a-case-expression-in-a-natively-compiled-stored-procedure"></a>고유하게 컴파일된 저장 프로시저에서 CASE 식 구현
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**적용 대상:** [!INCLUDE[ssSDSFull_md](../../includes/sssdsfull-md.md)] 및 SQL Server [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 이상

CASE 식은 고유하게 컴파일된 T-SQL 모듈에서 지원됩니다. 다음 예제에서는 쿼리에서 CASE 식을 사용하는 방법을 보여 줍니다. 

``` 
-- Query using a CASE expression in a natively compiled stored procedure.
CREATE PROCEDURE dbo.usp_SOHOnlineOrderResult  
   WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
   AS BEGIN ATOMIC WITH  (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE=N'us_english')  
   SELECT   
      SalesOrderID,   
      CASE (OnlineOrderFlag)   
      WHEN 1 THEN N'Order placed online by customer'  
      ELSE N'Order placed by sales person'  
      END  
   FROM Sales.SalesOrderHeader_inmem
END  
GO  
  
EXEC dbo.usp_SOHOnlineOrderResult  
GO  
``` 

**적용 대상:** [!INCLUDE[ssSQL14-md](../../includes/ssSQL14-md.md)] 및 SQL Server [!INCLUDE[ssSQL15-md](../../includes/ssSQL15-md.md)] 이상

  CASE 식은 고유하게 컴파일된 T-SQL 모듈에서 지원되지 *않습니다*. 다음 예제에서는 고유하게 컴파일된 저장 프로시저에서 CASE 식의 기능을 구현하는 방법을 보여 줍니다.  
  
 코드 샘플은 테이블 변수를 사용하여 단일 결과 집합을 생성합니다. 이것은 제한된 수의 행을 처리하는 경우 데이터 행의 추가 복사본을 만들어야 하기 때문에 적절합니다.  
  
 이 방법의 성능을 테스트해야 합니다.  
  
```  
-- original query  
SELECT   
   SalesOrderID,   
   CASE (OnlineOrderFlag)   
   WHEN 1 THEN N'Order placed online by customer'  
   ELSE N'Order placed by sales person'  
   END  
FROM Sales.SalesOrderHeader_inmem  
  
--  workaround for CASE in natively compiled stored procedures  
--  use a table for the single resultset  
CREATE TYPE dbo.SOHOnlineOrderResult AS TABLE  
(  
   SalesOrderID uniqueidentifier not null index ix_SalesOrderID,  
     OrderFlag nvarchar(100) not null  
) with (memory_optimized=on)  
go  
  
-- natively compiled stored procedure that includes the query  
CREATE PROCEDURE dbo.usp_SOHOnlineOrderResult  
   WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
   AS BEGIN ATOMIC WITH  
      (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE=N'us_english')  
  
   -- table variable for creating the single resultset  
   DECLARE @result dbo.SOHOnlineOrderResult  
  
   -- CASE OnlineOrderFlag=1  
   INSERT @result   
   SELECT SalesOrderID, N'Order placed online by customer'  
      FROM Sales.SalesOrderHeader_inmem  
      WHERE OnlineOrderFlag=1  
  
   -- ELSE  
   INSERT @result   
   SELECT SalesOrderID, N'Order placed by sales person'  
      FROM Sales.SalesOrderHeader_inmem  
      WHERE OnlineOrderFlag!=1  
  
   -- return single resultset  
   SELECT SalesOrderID, OrderFlag FROM @result  
END  
GO  
  
EXEC dbo.usp_SOHOnlineOrderResult  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [고유하게 컴파일된 저장 프로시저의 마이그레이션 문제](./a-guide-to-query-processing-for-memory-optimized-tables.md)   
 [메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
