---
title: ERROR_PROCEDURE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ERROR_PROCEDURE_TSQL
- ERROR_PROCEDURE
dev_langs:
- TSQL
helpviewer_keywords:
- ERROR_PROCEDURE function
- messages [SQL Server], trigger where occurred
- errors [SQL Server], stored procedure where occurred
- TRY...CATCH [SQL Server]
- CATCH block
- messages [SQL Server], stored procedure where occurred
- errors [SQL Server], trigger where occurred
ms.assetid: b81edbf0-856a-498f-ba87-48ff1426d980
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 459119eb08117ed52a455fdfb80fe3f393a410fa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47807110"
---
# <a name="errorprocedure-transact-sql"></a>ERROR_PROCEDURE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

이 함수는 해당 오류가 TRY...CATCH 구문의 CATCH 블록이 실행되게 하는 경우 오류가 발생한 저장 프로시저나 트리거의 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ERROR_PROCEDURE ( )  
```  
  
## <a name="return-types"></a>반환 형식  
**nvarchar(128)**  
  
## <a name="return-value"></a>반환 값  
오류가 발생한 저장 프로시저 CATCH 블록에서 호출된 경우 `ERROR_PROCEDURE`는 해당 저장 프로시저 이름을 반환합니다.  
  
`ERROR_PROCEDURE`는 오류가 저장 프로시저나 트리거 내에서 발생하지 않은 경우 NULL을 반환합니다.  
  
`ERROR_PROCEDURE`는 CATCH 블록 범위 밖에서 호출된 경우 NULL을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
`ERROR_PROCEDURE`는 CATCH 블록 범위 내의 어떤 위치에서나 호출을 지원합니다.  
  
`ERROR_PROCEDURE`는 `CATCH` 블록 범위 내에서 실행 위치나 실행 횟수에 관계 없이 오류가 발생하는 저장 프로시저 또는 트리거의 이름을 반환합니다. 이것은 오류가 발생한 명령문 바로 다음 명령문에 오류 번호만 반환하는 @@ERROR 같은 함수와 대조적입니다.  
  
중첩된 `CATCH` 블록에서 `ERROR_PROCEDURE`는 해당 `CATCH` 블록을 참조한 `CATCH` 블록의 범위에 관련된 오류를 반환합니다. 예를 들어 외부 TRY...CATCH 구문의 `CATCH` 블록에는 내부 `TRY...CATCH` 구문이 있을 수 있습니다. 해당 내부 `CATCH` 블록 내에서 `ERROR_PROCEDURE`는 내부 `CATCH` 블록을 호출한 오류의 번호를 반환합니다. `ERROR_PROCEDURE`가 외부 `CATCH` 블록에서 실행되는 경우 해당 외부 `CATCH` 블록을 호출한 오류의 번호를 반환합니다.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]
  
### <a name="a-using-errorprocedure-in-a-catch-block"></a>1. CATCH 블록에서 ERROR_PROCEDURE 사용  
이 예에서는 0으로 나누기 오류를 생성하는 저장 프로시저를 보여 줍니다. `ERROR_PROCEDURE`는 오류가 발생한 저장 프로시저의 이름을 반환합니다.  
  
```  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_PROCEDURE() AS ErrorProcedure;  
END CATCH;  
GO  

-----------

(0 row(s) affected)

ErrorProcedure
--------------------
usp_ExampleProc

(1 row(s) affected)

```  
  
### <a name="b-using-errorprocedure-in-a-catch-block-with-other-error-handling-tools"></a>2. CATCH 블록에서 다른 오류 처리 도구와 함께 ERROR_PROCEDURE 사용  
이 예에서는 0으로 나누기 오류를 생성하는 저장 프로시저를 보여 줍니다. 오류가 발생한 저장 프로시저의 이름과 함께 저장 프로시저는 오류에 대한 정보를 반환합니다.  
  
```  
  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_MESSAGE() AS ErrorMessage,  
        ERROR_LINE() AS ErrorLine;  
        END CATCH;  
GO  

-----------

(0 row(s) affected)

ErrorNumber ErrorSeverity ErrorState  ErrorProcedure   ErrorMessage                       ErrorLine
----------- ------------- ----------- ---------------- ---------------------------------- -----------
8134        16            1           usp_ExampleProc  Divide by zero error encountered.  6

(1 row(s) affected)

```  
  
## <a name="see-also"></a>참고 항목  
 [sys.messages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH&#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE&#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE&#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER&#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_SEVERITY&#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR&#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  

