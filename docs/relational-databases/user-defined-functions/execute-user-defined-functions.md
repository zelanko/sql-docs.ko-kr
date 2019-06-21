---
title: 사용자 정의 함수 실행 | Microsoft 문서
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- invoking user-defined functions
- user-defined functions [SQL Server], executing
ms.assetid: 0de7744d-9b73-463f-ae80-e31a020004b5
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 74a14c0f28b7353a4d09eb531678450f0b26f3fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63034742"
---
# <a name="execute-user-defined-functions"></a>사용자 정의 함수 실행
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Transact-SQL을 사용하여 사용자 정의 함수 실행
  

> **참고:** 사용자 정의 함수에 대한 자세한 내용은 [사용자 정의 함수](user-defined-functions.md) 및 [Create Function (Transact SQL)](../../t-sql/statements/create-function-transact-sql.md) 항목을 참고하세요. 
  
 
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
 Transact-SQL에서 *value* 또는 @*parameter_name*=*value*를 사용하여 매개 변수를 제공할 수 있습니다. 를 사용하여 제공할 수 있습니다. 매개 변수는 트랜잭션의 일부가 아니므로 나중에 롤백되는 트랜잭션에서 매개 변수가 변경된 경우 해당 매개 변수의 값은 이전 값으로 되돌아가지 않습니다. 호출자에게 반환되는 값은 항상 모듈이 반환되는 시점의 값입니다.  
  
###  <a name="Security"></a> 보안  
  
 [EXECUTE](../../t-sql/language-elements/execute-transact-sql.md) 문을 실행하는 데에는 사용 권한이 필요하지 않습니다. 그러나 EXECUTE 문자열 내에서 참조되는 보안 개체에 대해서는 사용 권한이 **필요합니다** . 예를 들어 문자열에 [INSERT](../../t-sql/statements/insert-transact-sql.md) 문이 있는 경우 EXECUTE 문의 호출자에게는 대상 테이블에 대한 INSERT 권한이 있어야 합니다. EXECUTE 문이 모듈 내에 포함된 경우에도 EXECUTE 문이 실행될 때는 사용 권한 검사가 수행됩니다. 자세한 내용은 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)를 참조하세요.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
### <a name="example"></a>예제 
  
이 예제에서는 대부분의 `ufnGetSalesOrderStatusText` 버전에서 사용할 수 있는 `AdventureWorks`스칼라 반환 함수를 사용합니다.  이 함수는 지정된 정수에서 판매 상태 텍스트 값을 반환하는 데 사용됩니다.  **\@Status** 매개 변수에 1-7 정수를 전달하여 예제를 변경합니다.
  
~~~tsql
USE [AdventureWorks2016CTP3]
GO  

-- Declare a variable to return the results of the function. 
DECLARE @ret nvarchar(15);   

-- Execute the function while passing a value to the @status parameter
EXEC @ret = dbo.ufnGetSalesOrderStatusText 
    @Status = 5; 

-- View the returned value.  The Execute and Select statements must be executed at the same time.  
SELECT N'Order Status: ' + @ret; 

-- Result:
-- Order Status: Shipped
~~~
  
  
  
