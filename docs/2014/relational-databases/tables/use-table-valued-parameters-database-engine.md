---
title: 테이블 반환 매개 변수 사용(데이터베이스 엔진) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- DECLARE
- CREATE TYPE
helpviewer_keywords:
- table-valued parameters
- table-valued parameters, about table-valued parameters
- parameters [SQL Server], table-valued
- TVP See table-valued parameters
ms.assetid: 5e95a382-1e01-4c74-81f5-055612c2ad99
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ce96eb2e0cad45e15e03f48bbb27afb5cb61938b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37223213"
---
# <a name="use-table-valued-parameters-database-engine"></a>테이블 반환 매개 변수 사용(데이터베이스 엔진)
  테이블 반환 매개 변수는 사용자 정의 테이블 형식을 사용하여 선언됩니다. 테이블 반환 매개 변수를 사용하면 임시 테이블이나 많은 매개 변수를 만들지 않고도 저장 프로시저 또는 함수와 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이나 루틴에 여러 행의 데이터를 보낼 수 있습니다.  
  
 테이블 반환 매개 변수는 OLE DB 및 ODBC의 매개 변수 배열과 유사하지만 보다 유연하고 [!INCLUDE[tsql](../../includes/tsql-md.md)]과 보다 긴밀하게 통합합니다. 또한 테이블 반환 매개 변수는 집합 기반 작업에 사용할 수 있다는 이점이 있습니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 은 입력 데이터의 복사본을 만들지 않기 위해 참조로 루틴에 테이블 반환 매개 변수를 전달합니다. 테이블 반환 매개 변수를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 루틴을 만들고 실행한 다음 모든 관리 언어의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드, 관리되는 클라이언트 및 기본 클라이언트에서 해당 루틴을 호출할 수 있습니다.  
  
 **항목 내용:**  
  
 [이점](#Benefits)  
  
 [제한 사항](#Restrictions)  
  
 [테이블 반환 매개 변수와 BULK INSERT 작업 비교](#BulkInsert)  
  
 [예제](#Example)  
  
##  <a name="Benefits"></a> 이점  
 테이블 반환 매개 변수의 범위는 다른 매개 변수와 똑같이 저장 프로시저, 함수 또는 동적 [!INCLUDE[tsql](../../includes/tsql-md.md)] 텍스트입니다. 마찬가지로 테이블 형식 변수의 범위는 DECLARE 문을 사용하여 만든 다른 모든 지역 변수의 범위와 같습니다. 동적 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 내에서 테이블 반환 변수를 선언하고 이 변수를 저장 프로시저 및 함수에 테이블 반환 매개 변수로 전달할 수 있습니다.  
  
 테이블 반환 매개 변수는 매개 변수 목록을 전달하는 임시 테이블 또는 다른 방법보다 유연하며 경우에 따라 보다 뛰어난 성능을 제공합니다. 테이블 반환 매개 변수에서 제공하는 이점은 다음과 같습니다.  
  
-   클라이언트의 데이터를 처음 채울 때 잠글 필요가 없습니다.  
  
-   간단한 프로그래밍 모델을 제공합니다.  
  
-   단일 루틴에 복잡한 비즈니스 논리를 포함할 수 있습니다.  
  
-   서버 왕복을 줄입니다.  
  
-   카디널리티가 다른 테이블 구조를 가질 수 있습니다.  
  
-   강력한 형식입니다.  
  
-   클라이언트가 정렬 순서 및 고유 키를 지정할 수 있습니다.  
  
-   저장 프로시저에서 사용 될 때 임시 테이블과 같이 캐시됩니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 테이블-반환 매개 변수는 또한 매개 변수가 있는 쿼리에 대해 캐시됩니다.  
  
##  <a name="Restrictions"></a> 제한 사항  
 테이블 반환 매개 변수에는 다음과 같은 제한 사항이 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 테이블 반환 매개 변수의 열에 대한 통계를 유지 관리하지 않습니다.  
  
-   테이블 반환 매개 변수는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 루틴에 입력 READONLY 매개 변수로 전달되어야 합니다. 루틴 본문의 테이블 반환 매개 변수에 대해서는 UPDATE, DELETE 또는 INSERT와 같은 DML 작업을 수행할 수 없습니다.  
  
-   테이블 반환 매개 변수를 SELECT INTO 또는 INSERT EXEC 문의 대상으로 사용할 수 없습니다. 테이블 반환 매개 변수는 SELECT INTO의 FROM 절 또는 INSERT EXEC 문자열이나 저장 프로시저에 사용할 수 있습니다.  
  
##  <a name="BulkInsert"></a> 테이블 반환 매개 변수와 BULK INSERT 작업 비교  
 테이블 반환 매개 변수를 사용하는 방법은 집합 기반 변수를 사용하는 다른 방법과 유사하지만 큰 데이터 집합의 경우 테이블 반환 매개 변수를 사용하는 것이 훨씬 빠른 경우가 많습니다. 테이블 반환 매개 변수보다 더 많은 시작 비용이 드는 대량 작업과 비교해볼 때 테이블 반환 매개 변수는 1,000개 미만의 행을 삽입할 때 더 효과적입니다.  
  
 다시 사용되는 테이블 반환 매개 변수는 임시 테이블 캐싱을 활용합니다. 이 테이블 캐싱은 이와 동일한 BULK INSERT 작업보다 뛰어난 확장성을 제공합니다. 작은 행 삽입 작업을 사용하는 경우에는 BULK INSERT 작업 또는 테이블 반환 매개 변수 대신 매개 변수 목록 또는 일괄 처리된 문을 사용하여 작은 성능 이점을 얻을 수도 있습니다. 그러나 이러한 메서드는 프로그래밍하기가 다소 불편하고 행이 늘어남에 따라 성능이 빠르게 저하됩니다.  
  
 테이블 반환 매개 변수는 동일한 매개 변수 배열 구현 이상의 성능을 제공합니다.  
  
##  <a name="Example"></a> 예제  
 다음 예에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용하며 테이블 반환 매개 변수 형식을 만들고, 해당 형식을 참조하는 변수를 선언하고, 매개 변수 목록을 채운 다음 저장 프로시저에 값을 전달하는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks2012;  
GO  
  
/* Create a table type. */  
CREATE TYPE LocationTableType AS TABLE   
( LocationName VARCHAR(50)  
, CostRate INT );  
GO  
  
/* Create a procedure to receive data for the table-valued parameter. */  
CREATE PROCEDURE dbo. usp_InsertProductionLocation  
    @TVP LocationTableType READONLY  
    AS   
    SET NOCOUNT ON  
    INSERT INTO AdventureWorks2012.Production.Location  
           (Name  
           ,CostRate  
           ,Availability  
           ,ModifiedDate)  
        SELECT *, 0, GETDATE()  
        FROM  @TVP;  
        GO  
  
/* Declare a variable that references the type. */  
DECLARE @LocationTVP AS LocationTableType;  
  
/* Add data to the table variable. */  
INSERT INTO @LocationTVP (LocationName, CostRate)  
    SELECT Name, 0.00  
    FROM AdventureWorks2012.Person.StateProvince;  
  
/* Pass the table variable data to a stored procedure. */  
EXEC usp_InsertProductionLocation @LocationTVP;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [CREATE TYPE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-type-transact-sql)   
 [DECLARE @local_variable&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)   
 [sys.types&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-types-transact-sql)   
 [sys.parameters&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-parameters-transact-sql)   
 [sys.parameter_type_usages&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql)   
 [CREATE PROCEDURE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)   
 [CREATE FUNCTION&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql)  
  
  
