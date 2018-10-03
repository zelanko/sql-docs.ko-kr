---
title: 시도 사용 하 여... 고유 하 게 컴파일된 저장된 프로시저의 catch | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f730e70c-4f92-411d-9984-289e241e43ee
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7ea148b3a17f11ce0993beff82dfb38701af251f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075233"
---
# <a name="using-trycatch-in-natively-compiled-stored-procedures"></a>고유하게 컴파일된 저장 프로시저에서 Try..Catch 사용
  고유하게 컴파일된 저장 프로시저 내부에서 try..catch 블록을 사용할 수 있습니다. 다음과 같은 구문이 지원됩니다.  
  
-   ERROR_LINE  
  
-   ERROR_MESSAGE  
  
-   ERROR_NUMBER  
  
-   ERROR_PROCEDURE  
  
-   ERROR_SEVERITY  
  
-   ERROR_STATE  
  
```tsql  
CREATE PROCEDURE test_try_catch  
with native_compilation, schemabinding, execute as owner   
as  
begin atomic with (transaction isolation level = snapshot, language = N'us_english')  
  
  BEGIN TRY  
    -- generate error  
    declare @i int = 1,  
    @j int = 0  
    select @i/@j  
  END TRY  
  BEGIN CATCH  
    -- Execute error retrieval routine.  
    SELECT  
    ERROR_SEVERITY() AS ErrorSeverity  
    ,ERROR_STATE() AS ErrorState  
    ,ERROR_PROCEDURE() AS ErrorProcedure  
    ,ERROR_LINE() AS ErrorLine  
    ,ERROR_MESSAGE() AS ErrorMessage  
  END CATCH  
end  
go  
  
exec test_try_catch  
go  
```  
  
## <a name="see-also"></a>관련 항목  
 [고유하게 컴파일된 저장 프로시저](../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
