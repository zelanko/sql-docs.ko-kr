---
title: RETURN (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RETURN_TSQL
- RETURN
dev_langs:
- TSQL
helpviewer_keywords:
- unconditionally exiting program
- stored procedures [SQL Server], exiting
- batches [SQL Server], exiting
- statement blocks [SQL Server]
- queries [SQL Server], exiting
- exiting queries [SQL Server]
- exiting procedures [SQL Server]
- RETURN statement
ms.assetid: 1d9c8247-fd89-4544-be9c-01c95b745db0
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c4c3db821e25a671872035e1a584bf5e4205657d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="return-transact-sql"></a>RETURN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  쿼리나 프로시저를 무조건 종료합니다. RETURN은 즉각적이고 완전하며 프로시저, 일괄 처리, 문 블록에서 아무 때나 종료하는 데 사용할 수 있습니다. RETURN 다음에 있는 문은 실행되지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
RETURN [ integer_expression ]   
```  
  
## <a name="arguments"></a>인수  
 *integer_expression*  
 반환되는 정수 값입니다. 저장 프로시저는 호출 프로시저나 응용 프로그램에 정수 값을 반환할 수 있습니다.  
  
## <a name="return-types"></a>반환 형식  
 필요에 따라 반환 **int**합니다.  
  
> [!NOTE]  
>  달리 설명하지 않는 한 모든 시스템 저장 프로시저는 0 값을 반환합니다. 이 값은 성공을 나타내며 0 이외의 값은 실패를 나타냅니다.  
  
## <a name="remarks"></a>주의  
 저장 프로시저와 함께 사용할 경우 RETURN은 null 값을 반환할 수 없습니다. 프로시저에서 Null 값을 반환하려는 경우(예: @status가 NULL일 때 RETURN @status 사용) 경고 메시지가 생성되고 값 0이 반환됩니다.  
  
 현재 프로시저를 실행한 일괄 처리나 프로시저에 있는 후속 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 반환 상태 값을 포함시킬 수 있지만 `EXECUTE @return_status = <procedure_name>` 형식으로 입력해야 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-returning-from-a-procedure"></a>1. 프로시저에서 반환  
 다음 예에서는 `findjobs`를 실행할 때 매개 변수로 사용자 이름을 지정하지 않은 경우 `RETURN`으로 사용자의 화면에 메시지를 보낸 다음 프로시저를 종료하는 방법을 보여 줍니다. 사용자 이름을 지정하면 현재 데이터베이스에서 이 사용자가 만든 모든 개체 이름을 해당 시스템 테이블에서 가져옵니다.  
  
```  
CREATE PROCEDURE findjobs @nm sysname = NULL  
AS   
IF @nm IS NULL  
    BEGIN  
        PRINT 'You must give a user name'  
        RETURN  
    END  
ELSE  
    BEGIN  
        SELECT o.name, o.id, o.uid  
        FROM sysobjects o INNER JOIN master..syslogins l  
            ON o.uid = l.sid  
        WHERE l.name = @nm  
    END;  
```  
  
### <a name="b-returning-status-codes"></a>2. 상태 코드 반환  
 다음 예에서는 지정된 연락처 ID의 주를 확인하는 방법을 보여 줍니다. 주가 워싱턴(`WA`)인 경우 `1`이 반환됩니다. 그 외 다른 조건(`2` 또는 `WA`가 `StateProvince` 이외의 값)인 경우 `ContactID`가 반환됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE PROCEDURE checkstate @param varchar(11)  
AS  
IF (SELECT StateProvince FROM Person.vAdditionalContactInfo WHERE ContactID = @param) = 'WA'  
    RETURN 1  
ELSE  
    RETURN 2;  
GO  
```  
  
 다음 예는 `checkstate` 실행의 반환 상태를 보여 줍니다. 첫 번째 예는 워싱턴의 연락처를 두 번째 예는 워싱턴에 없는 연락처를 세 번째는 유효하지 않은 연락처를 보여 줍니다. `@return_status` 지역 변수를 선언해야 이를 사용할 수 있습니다.  
  
```  
DECLARE @return_status int;  
EXEC @return_status = checkstate '2';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status 
  
 ------------- 
  
 1
 ```  
  
 다른 연락처를 지정하여 쿼리를 다시 실행합니다.  
  
```  
DECLARE @return_status int;  
EXEC @return_status = checkstate '6';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status  
 -------------  
  
 2
 ```  
  
 또 다른 연락처를 지정하여 쿼리를 다시 실행합니다.  
  
```  
DECLARE @return_status int  
EXEC @return_status = checkstate '12345678901';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status  
 -------------  
  
 2
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)   
 [THROW&#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)  
  
  

