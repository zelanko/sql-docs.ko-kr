---
title: CREATE SYNONYM (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_SYNONYM_TSQL
- SYNONYM_TSQL
- SYNONYM
- CREATE SYNONYM
dev_langs: TSQL
helpviewer_keywords:
- alternate names [SQL Server]
- names [SQL Server], synonyms
- CREATE SYNONYM statement
- synonyms [SQL Server], creating
ms.assetid: 41313809-e970-449c-bc35-85da2ef96e48
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5dd9893a3832a2fc1bd40d56b119096718b2cf42
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="create-synonym-transact-sql"></a>CREATE SYNONYM(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  새 동의어를 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- SQL Server Syntax  
  
CREATE SYNONYM [ schema_name_1. ] synonym_name FOR <object>  
  
<object> :: =  
{  
    [ server_name.[ database_name ] . [ schema_name_2 ]. object_name   
  | database_name . [ schema_name_2 ].| schema_name_2. ] object_name  
}  
```  
  
```  
-- Azure SQL Database Syntax  
  
CREATE SYNONYM [ schema_name_1. ] synonym_name FOR < object >  
  
< object > :: =  
{  
    [database_name. [ schema_name_2 ].| schema_name_2. ] object_name  
}  
```  
  
## <a name="arguments"></a>인수  
 *schema_name_1*  
 동의어가 생성되는 스키마를 지정합니다. 경우 *스키마* 를 지정 하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 현재 사용자의 기본 스키마를 사용 합니다.  
  
 *synonym_name*  
 새 동의어의 이름입니다.  
  
 *server_name*  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 기준 개체가 있는 서버의 이름입니다.  
  
 *database_name*  
 기준 개체가 있는 데이터베이스의 이름입니다. 경우 *database_name* 를 지정 하지 않으면 현재 데이터베이스의 이름이 사용 됩니다.  
  
 *schema_name_2*  
 기준 개체의 스키마 이름입니다. 경우 *schema_name* 지정 하지 않으면 현재 사용자의 기본 스키마가 사용 합니다.  
  
 *object_name*  
 동의어가 참조하는 기준 개체의 이름입니다.  
  
 database_name이 현재 데이터베이스이거나 database_name이 tempdb이고 object_name이 #으로 시작하는 경우 Microsoft Azure SQL Database는 세 부분으로 구성된 이름 형식 database_name.[schema_name].object_name을 지원합니다.  
  
## <a name="remarks"></a>주의  
 동의어를 만들 때 기준 개체가 존재해야 할 필요는 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 기준 개체의 존재 여부를 런타임에 검사합니다.  
  
 다음과 같은 유형의 개체에 대해 동의어를 만들 수 있습니다.  
  
|||  
|-|-|  
|어셈블리(CLR) 저장 프로시저|어셈블리(CLR) 테이블 반환 함수|  
|어셈블리(CLR) 스칼라 함수|어셈블리 집계(CLR) 집계 함수|  
|복제 필터 프로시저|확장 저장 프로시저|  
|SQL 스칼라 함수|SQL 테이블 반환 함수|  
|SQL 인라인 테이블 반환 함수|SQL 저장 프로시저|  
|보기|테이블<sup>1</sup> (사용자 정의 됨)|  
  
 <sup>1 로컬 및 전역 임시 테이블이 포함 됩니다.</sup>  
  
 함수 기본 개체의 네 부분으로 된 이름은 지원되지 않습니다.  
  
 동의어는 동적 SQL에서 생성, 삭제 및 참조할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 지정된 스키마에서 동의어를 만들려면 사용자에게 CREATE SYNONYM 권한이 있어야 하며 스키마를 소유하거나 ALTER SCHEMA 권한이 있어야 합니다.  
  
 CREATE SYNONYM 권한은 부여할 수 있는 권한입니다.  
  
> [!NOTE]  
>  기준 개체에 대한 모든 권한 확인은 런타임까지 지연되므로 CREATE SYNONYM 문을 성공적으로 컴파일하기 위해 기준 개체에 대한 권한이 필요하지는 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-synonym-for-a-local-object"></a>1. 로컬 개체의 동의어 만들기  
 다음 예에서는 먼저 `Product` 데이터베이스의 기준 개체인 `AdventureWorks2012`에 대한 동의어를 만든 다음 동의어를 사용하여 쿼리합니다.  
  
```  
-- Create a synonym for the Product table in AdventureWorks2012.  
CREATE SYNONYM MyProduct  
FOR AdventureWorks2012.Production.Product;  
GO  
  
-- Query the Product table by using the synonym.  
SELECT ProductID, Name   
FROM MyProduct  
WHERE ProductID < 5;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ----------------------- 
 ProductID   Name 
 ----------- -------------------------- 
 1           Adjustable Race 
 2           Bearing Ball 
 3           BB Ball Bearing 
 4           Headset Ball Bearings 

 (4 row(s) affected)
``` 
  
### <a name="b-creating-a-synonym-to-remote-object"></a>2. 원격 개체의 동의어 만들기  
 다음 예에서 기준 개체인 `Contact`는 원격 서버인 `Server_Remote`에 있습니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
EXEC sp_addlinkedserver Server_Remote;  
GO  
USE tempdb;  
GO  
CREATE SYNONYM MyEmployee FOR Server_Remote.AdventureWorks2012.HumanResources.Employee;  
GO  
```  
  
### <a name="c-creating-a-synonym-for-a-user-defined-function"></a>3. 사용자 정의 함수의 동의어 만들기  
 다음 예제에서는 주문 총계를 정확하게 12단위로 늘리는 `dbo.OrderDozen`라는 함수를 만듭니다. 그런 다음 `dbo.CorrectOrder` 함수에 대해 동의어 `dbo.OrderDozen`를 만듭니다.  
  
```  
-- Creating the dbo.OrderDozen function  
CREATE FUNCTION dbo.OrderDozen (@OrderAmt int)  
RETURNS int  
WITH EXECUTE AS CALLER  
AS  
BEGIN  
IF @OrderAmt % 12 <> 0  
BEGIN  
    SET @OrderAmt +=  12 - (@OrderAmt % 12)  
END  
RETURN(@OrderAmt);  
END;  
GO  
  
-- Using the dbo.OrderDozen function  
DECLARE @Amt int;  
SET @Amt = 15;  
SELECT @Amt AS OriginalOrder, dbo.OrderDozen(@Amt) AS ModifiedOrder;  
  
-- Create a synonym dbo.CorrectOrder for the dbo.OrderDozen function.  
CREATE SYNONYM dbo.CorrectOrder  
FOR dbo.OrderDozen;  
GO  
  
-- Using the dbo.CorrectOrder synonym.  
DECLARE @Amt int;  
SET @Amt = 15;  
SELECT @Amt AS OriginalOrder, dbo.CorrectOrder(@Amt) AS ModifiedOrder;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [DROP synonym&#40; Transact SQL &#41;](../../t-sql/statements/drop-synonym-transact-sql.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
