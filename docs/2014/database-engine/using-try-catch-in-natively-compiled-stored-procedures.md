---
title: Try .를 사용 합니다. 고유 하 게 컴파일된 저장 프로시저에서 Catch | Microsoft Docs
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
ms.openlocfilehash: fa7115be43361e25f5ad2b082a92929298ce8bef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62842481"
---
# <a name="using-trycatch-in-natively-compiled-stored-procedures"></a>고유하게 컴파일된 저장 프로시저에서 Try..Catch 사용
  고유하게 컴파일된 저장 프로시저 내부에서 try..catch 블록을 사용할 수 있습니다. 다음과 같은 구문이 지원됩니다.  
  
-   ERROR_LINE  
  
-   ERROR_MESSAGE  
  
-   ERROR_NUMBER  
  
-   ERROR_PROCEDURE  
  
-   ERROR_SEVERITY  
  
-   ERROR_STATE  
  
```sql  
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
  
## <a name="see-also"></a>참고 항목  
 [고유하게 컴파일된 저장 프로시저](../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
