---
title: ERROR_MESSAGE (Transact SQL) | Microsoft Docs
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
- ERROR_MESSAGE_TSQL
- ERROR_MESSAGE
dev_langs:
- TSQL
helpviewer_keywords:
- ERROR_MESSAGE function
- errors [SQL Server], text of
- messages [SQL Server], text of
- TRY...CATCH [SQL Server]
- CATCH block
ms.assetid: f32877a6-5f17-418c-a32c-5a1a344b3c45
caps.latest.revision: 53
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: ad4e69ea267af2a9575558737e17e79bbdad684f
ms.contentlocale: ko-kr
ms.lasthandoff: 10/17/2017

---
# <a name="errormessage-transact-sql"></a>ERROR_MESSAGE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  TRY...CATCH 구문의 CATCH 블록을 실행시키는 오류의 메시지 텍스트를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ERROR_MESSAGE ( )   
```  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar(4000)**  
  
## <a name="return-value"></a>반환 값  
 CATCH 블록에서 호출된 경우 CATCH 블록을 실행시키는 오류 메시지의 전체 텍스트를 반환합니다. 이 텍스트는 길이, 개체 이름 또는 시간과 같은 대체 가능한 매개 변수에 제공된 값을 포함합니다.  
  
 CATCH 블록 범위 밖에서 호출된 경우 NULL을 반환합니다.  
  
## <a name="remarks"></a>주의  
 ERROR_MESSAGE는 CATCH 블록 범위 내의 아무 위치에서나 호출할 수 있습니다.  
  
 ERROR_MESSAGE는 CATCH 블록 범위 내에서 실행 횟수 또는 실행 위치에 상관없이 오류 메시지를 반환합니다. 이 같은 함수와 대조 @@ERROR만의 반환 하는 오류 번호는 오류를 발생 시키는 것 바로 다음 문으로 또는 첫 번째 문은 catch 블록입니다.  
  
 중첩된 CATCH 블록에서 ERROR_MESSAGE는 참조하는 CATCH 블록의 범위에 한정된 오류 메시지를 반환합니다. 예를 들어 외부 TRY...CATCH 구문의 CATCH 블록에는 중첩된 TRY...CATCH 구문이 있을 수 있습니다. 중첩된 CATCH 블록에서 ERROR_MESSAGE는 중첩된 CATCH 블록을 호출한 오류 메시지를 반환합니다. ERROR_MESSAGE가 외부 CATCH 블록에서 실행되는 경우 해당 CATCH 블록을 호출한 오류 메시지를 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-errormessage-in-a-catch-block"></a>1. CATCH 블록에서 ERROR_MESSAGE 사용  
 다음 코드 예에서는 0으로 나누기 오류를 생성하는 `SELECT` 문을 보여 줍니다. 오류 메시지가 반환됩니다.  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errormessage-in-a-catch-block-with-other-error-handling-tools"></a>2. 다른 오류 처리 도구로 CATCH 블록에서 ERROR_MESSAGE 사용  
 다음 코드 예에서는 0으로 나누기 오류를 생성하는 `SELECT` 문을 보여 줍니다. 오류 메시지와 함께 오류와 관련된 정보가 반환됩니다.  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errormessage-in-a-catch-block-with-other-error-handling-tools"></a>3. 다른 오류 처리 도구로 CATCH 블록에서 ERROR_MESSAGE 사용  
 다음 코드 예에서는 0으로 나누기 오류를 생성하는 `SELECT` 문을 보여 줍니다. 오류 메시지와 함께 오류와 관련된 정보가 반환됩니다.  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  


