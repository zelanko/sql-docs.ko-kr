---
title: '@@PROCID (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@PROCID'
- '@@PROCID_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- stored procedures [SQL Server], identification numbers
- UDTs [SQL Server], object identifiers
- '@@PROCID function'
- user-defined functions [SQL Server], object identifiers
- triggers [SQL Server], object identifiers
- identification numbers [SQL Server], modules
- IDs [SQL Server], modules
- module object identifiers [SQL Server]
ms.assetid: 0d4882c7-edb8-49b1-a470-2c7497b8998f
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 9288f472601621b3177e3fa978bb2f53324881c8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40procid-transact-sql"></a>& #x 40; & #x 40; PROCID (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 [!INCLUDE[tsql](../../includes/tsql-md.md)] 모듈의 개체 식별자(ID)를 반환합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 모듈은 저장 프로시저, 사용자 정의 함수 또는 트리거일 수 있습니다. @@PROCID CLR 모듈 또는 데이터 처리에에 지정할 수 액세스 공급자입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@PROCID  
```  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="examples"></a>예  
 다음 예에서는 `@@PROCID` 함수에서 입력 매개 변수로 `OBJECT_NAME`를 사용하여 `RAISERROR` 메시지에 있는 저장 프로시저의 이름을 반환합니다.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'usp_FindName', 'P' ) IS NOT NULL   
DROP PROCEDURE usp_FindName;  
GO  
CREATE PROCEDURE usp_FindName  
    @lastname varchar(40) = '%',   
    @firstname varchar(20) = '%'  
AS  
DECLARE @Count int;  
DECLARE @ProcName nvarchar(128);  
SELECT LastName, FirstName  
FROM Person.Person   
WHERE FirstName LIKE @firstname AND LastName LIKE @lastname;  
SET @Count = @@ROWCOUNT;  
SET @ProcName = OBJECT_NAME(@@PROCID);  
RAISERROR ('Stored procedure %s returned %d rows.', 16,10, @ProcName, @Count);  
GO  
EXECUTE dbo.usp_FindName 'P%', 'A%';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [메타 데이터 함수 &#40; Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.objects &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Raiserror&#40; Transact SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  

