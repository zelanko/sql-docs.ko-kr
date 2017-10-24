---
title: '@@ERROR (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@ERROR'
- '@@ERROR_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@ERROR function'
- errors [SQL Server], Transact-SQL
- error numbers [SQL Server]
ms.assetid: c8b43477-b6c0-49bf-a608-394a0b6cc7a2
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1ef3f7b2f0b051fd79dd59325af7900aefff95a9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40error-transact-sql"></a>&#x40;&#x40; 오류 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  최근에 실행된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 오류 번호를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@ERROR  
```  
  
## <a name="return-types"></a>반환 형식  
 integer  
  
## <a name="remarks"></a>주의  
 이전 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 오류가 발생하지 않으면 0이 반환됩니다.  
  
 이전 문에 오류가 발생하면 오류 번호가 반환됩니다. 오류가 sys.messages 카탈로그 뷰의 오류 중 하나가 다음 경우@ERROR 해당 오류에 대 한 sys.messages.message_id 열의 값을에서 포함 합니다. 연결 된 텍스트를 볼 수는 @@ERROR sys.messages에 오류 번호입니다.  
  
 때문에 @@ERROR 의 선택을 취소 하 고 실행 된 각 문에서 다시 설정, 확인 하는 문 바로 다음을 확인 또는 나중에 확인할 수 있는 지역 변수에 저장 합니다.  
  
 TRY...CATCH 구문을 사용하여 오류를 처리하세요. TRY... CATCH 구성 지원 추가 시스템 함수 (ERROR_LINE, ERROR_MESSAGE, ERROR_PROCEDURE, ERROR_SEVERITY 및 ERROR_STATE) 보다 많은 오류 정보를 반환 하는 또한 @@ERROR 합니다. TRY...CATCH는 오류가 발생된 문 바로 다음 문의 오류 번호만 반환하도록 제한되지 않은 ERROR_NUMBER 함수도 지원합니다. 자세한 내용은 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)를 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-error-to-detect-a-specific-error"></a>1. 를 사용 하 여 @@ERROR 에 특정 오류 검색  
 다음 예에서는 `@@ERROR`를 사용하여 `UPDATE` 문에서 CHECK 제약 조건 위반(오류 #547)을 확인합니다.  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.EmployeePayHistory  
    SET PayFrequency = 4  
    WHERE BusinessEntityID = 1;  
IF @@ERROR = 547  
    PRINT N'A check constraint violation occurred.';  
GO  
```  
  
### <a name="b-using-error-to-conditionally-exit-a-procedure"></a>2. 를 사용 하 여 @@ERROR 를 조건부로 프로시저 종료  
 다음 예제에서는 `IF...ELSE` 테스트 합니다 `@@ERROR` 후는 `INSERT` 저장된 프로시저의 문. `@@ERROR` 변수의 값은 호출하는 프로그램으로 보내진 반환 코드를 결정하고 프로시저의 성공 여부를 나타냅니다.  
  
```  
USE AdventureWorks2012;  
GO  
-- Drop the procedure if it already exists.  
IF OBJECT_ID(N'HumanResources.usp_DeleteCandidate', N'P') IS NOT NULL  
    DROP PROCEDURE HumanResources.usp_DeleteCandidate;  
GO  
-- Create the procedure.  
CREATE PROCEDURE HumanResources.usp_DeleteCandidate   
    (  
    @CandidateID INT  
    )  
AS  
-- Execute the DELETE statement.  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = @CandidateID;  
-- Test the error value.  
IF @@ERROR <> 0   
    BEGIN  
        -- Return 99 to the calling program to indicate failure.  
        PRINT N'An error occurred deleting the candidate information.';  
        RETURN 99;  
    END  
ELSE  
    BEGIN  
        -- Return 0 to the calling program to indicate success.  
        PRINT N'The job candidate has been deleted.';  
        RETURN 0;  
    END;  
GO  
```  
  
### <a name="c-using-error-with-rowcount"></a>3. 를 사용 하 여 @@ERROR 와 @@ROWCOUNT   
 다음 예에서는 `@@ERROR`를 `@@ROWCOUNT`와 함께 사용하여 `UPDATE` 문 작업의 유효성을 검사합니다. `@@ERROR`의 값을 확인하여 오류 표시가 있는지 검사하고 `@@ROWCOUNT`를 사용하여 업데이트가 테이블의 행에 제대로 적용되었는지 확인합니다.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Purchasing.usp_ChangePurchaseOrderHeader',N'P')IS NOT NULL  
    DROP PROCEDURE Purchasing.usp_ChangePurchaseOrderHeader;  
GO  
CREATE PROCEDURE Purchasing.usp_ChangePurchaseOrderHeader  
    (  
    @PurchaseOrderID INT  
    ,@BusinessEntityID INT  
   )  
AS  
-- Declare variables used in error checking.  
DECLARE @ErrorVar INT;  
DECLARE @RowCountVar INT;  
  
-- Execute the UPDATE statement.  
UPDATE PurchaseOrderHeader   
    SET BusinessEntityID = @BusinessEntityID   
    WHERE PurchaseOrderID = @PurchaseOrderID;  
  
-- Save the @@ERROR and @@ROWCOUNT values in local   
-- variables before they are cleared.  
SELECT @ErrorVar = @@ERROR  
    ,@RowCountVar = @@ROWCOUNT;  
  
-- Check for errors. If an invalid @BusinessEntityID was specified,  
-- the UPDATE statement returns a foreign key violation error #547.  
IF @ErrorVar <> 0  
    BEGIN  
        IF @ErrorVar = 547  
            BEGIN  
                PRINT N'ERROR: Invalid ID specified for new employee.';  
                 RETURN 1;  
            END  
        ELSE  
            BEGIN  
                PRINT N'ERROR: error '  
                    + RTRIM(CAST(@ErrorVar AS NVARCHAR(10)))  
                    + N' occurred.';  
                RETURN 2;  
            END  
    END  
  
-- Check the row count. @RowCountVar is set to 0   
-- if an invalid @PurchaseOrderID was specified.  
IF @RowCountVar = 0  
    BEGIN  
        PRINT 'Warning: The BusinessEntityID specified is not valid';  
        RETURN 1;  
    END  
ELSE  
    BEGIN  
        PRINT 'Purchase order updated with the new employee';  
        RETURN 0;  
    END;  
GO  
```  

  
## <a name="see-also"></a>관련 항목:  
 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE&#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER&#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE&#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY&#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [Error_state &#40; Transact SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [@@ROWCOUNT&#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [sys.messages &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  


