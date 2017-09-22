---
title: '@@NESTLEVEL (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@NESTLEVEL'
- '@@NESTLEVEL_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@NESTLEVEL function'
- nesting stored procedures
- stored procedure nesting levels [SQL Server]
ms.assetid: 8c0b2134-8616-44f6-addc-6583c432fb62
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: d02995ee7093d311cbdc6f4b69430a8bc66a618c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40nestlevel-transact-sql"></a>& #x 40; & #x 40; Nestlevel은 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  로컬 서버의 현재 저장 프로시저 실행의 중첩 수준을 반환합니다(초기값 0).  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@NESTLEVEL  
```  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>주의  
 저장 프로시저가 다른 저장 프로시저를 호출하거나 CLR(공용 언어 런타임) 루틴, 유형 또는 집계를 참조하여 관리 코드를 실행할 때마다 중첩 수준이 증가합니다. 최대값 32를 초과하면 트랜잭션이 종료됩니다.  
  
 @ 때@NESTLEVEL 내에서 실행 되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문자열을 반환 되는 값은 1 + 현재 중첩 수준입니다. @ 때@NESTLEVEL 실행 동적으로 sp_executesql을 사용 하 여 반환 값은 현재 중첩 수준 + 2입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-nestlevel-in-a-procedure"></a>1. 를 사용 하 여@NESTLEVEL 프로시저에서  
 다음 예에서는 다른 프로시저를 호출하는 프로시저와 각각의 `@@NESTLEVEL` 설정을 표시하는 프로시저를 만듭니다.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'usp_OuterProc', N'P')IS NOT NULL  
    DROP PROCEDURE usp_OuterProc;  
GO  
IF OBJECT_ID (N'usp_InnerProc', N'P')IS NOT NULL  
    DROP PROCEDURE usp_InnerProc;  
GO  
CREATE PROCEDURE usp_InnerProc AS   
    SELECT @@NESTLEVEL AS 'Inner Level';  
GO  
CREATE PROCEDURE usp_OuterProc AS   
    SELECT @@NESTLEVEL AS 'Outer Level';  
    EXEC usp_InnerProc;  
GO  
EXECUTE usp_OuterProc;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Outer Level`  
  
 `-----------`  
  
 `1`  
  
 `Inner Level`  
  
 `-----------`  
  
 `2`  
  
### <a name="b-calling-nestlevel"></a>2. 호출@NESTLEVEL  
 다음 예에서는 `SELECT`, `EXEC` 및 `sp`_`executesql`에서 각각 `@@NESTLEVEL`을 호출할 때 반환되는 값의 차이를 보여 줍니다.  
  
```  
CREATE PROC usp_NestLevelValues AS  
    SELECT @@NESTLEVEL AS 'Current Nest Level';  
EXEC ('SELECT @@NESTLEVEL AS OneGreater');   
EXEC sp_executesql N'SELECT @@NESTLEVEL as TwoGreater' ;  
GO  
EXEC usp_NestLevelValues;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Current Nest Level`  
  
 `------------------`  
  
 `1`  
  
 `(1 row(s) affected)`  
  
 `OneGreater`  
  
 `-----------`  
  
 `2`  
  
 `(1 row(s) affected)`  
  
 `TwoGreater`  
  
 `-----------`  
  
 `3`  
  
 `(1 row(s) affected)`  
  
## <a name="see-also"></a>관련 항목:  
 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [저장 프로시저 만들기](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [@@TRANCOUNT&#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  

