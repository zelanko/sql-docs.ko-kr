---
description: GOTO(Transact-SQL)
title: GOTO(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GOTO
- GOTO_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- skipping statements
- Transact-SQL statements, skipping
- labels [SQL Server]
- statements [SQL Server], skipping
- GOTO statement
ms.assetid: 589b6f8e-dc80-416f-9e74-48bed5337f58
author: rothja
ms.author: jroth
ms.openlocfilehash: 5e35af299576306b5fd4bcc390c6ccc9d97089db
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467667"
---
# <a name="goto-transact-sql"></a>GOTO(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  실행 흐름을 지정된 레이블로 변경합니다. GOTO 다음에 이어지는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 건너뛰고 지정된 레이블에서 처리를 계속 이어갑니다. GOTO 문과 레이블은 프로시저, 일괄 처리, 문 블록 등 어디에서나 사용할 수 있습니다. GOTO 문은 중첩될 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
Define the label:   
label:   
Alter the execution:  
GOTO label   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *label*  
 GOTO의 대상이 해당 레이블인 경우 처리가 시작되는 지점입니다. 레이블은 [식별자](../../relational-databases/databases/database-identifiers.md) 규칙을 따라야 합니다. 레이블은 GOTO 사용 여부에 관계 없이 주석을 기록하는 방법으로 사용될 수 있습니다.  
  
## <a name="remarks"></a>설명  
 GOTO는 조건부 흐름 제어 문, 문 블록 또는 프로시저 내에서 사용할 수 있지만 일괄 처리 밖에 있는 레이블로 이동할 수 없습니다. GOTO 분기는 GOTO 전후에 정의된 레이블로 이동할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 GOTO 권한은 모든 유효한 사용자에게 기본적으로 부여됩니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `GOTO`를 분기 메커니즘으로 사용하는 방법을 보여 줍니다.  
  
```  
DECLARE @Counter int;  
SET @Counter = 1;  
WHILE @Counter < 10  
BEGIN   
    SELECT @Counter  
    SET @Counter = @Counter + 1  
    IF @Counter = 4 GOTO Branch_One --Jumps to the first branch.  
    IF @Counter = 5 GOTO Branch_Two  --This will never execute.  
END  
Branch_One:  
    SELECT 'Jumping To Branch One.'  
    GOTO Branch_Three; --This will prevent Branch_Two from executing.  
Branch_Two:  
    SELECT 'Jumping To Branch Two.'  
Branch_Three:  
    SELECT 'Jumping To Branch Three.';  
```  
  
## <a name="see-also"></a>참고 항목  
 [흐름 제어 언어 &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [BEGIN...END &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [BREAK&#40;Transact-SQL&#41;](../../t-sql/language-elements/break-transact-sql.md)   
 [CONTINUE&#40;Transact-SQL&#41;](../../t-sql/language-elements/continue-transact-sql.md)   
 [IF...ELSE&#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)   
 [WAITFOR&#40;Transact-SQL&#41;](../../t-sql/language-elements/waitfor-transact-sql.md)   
 [WHILE&#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  
  
  
