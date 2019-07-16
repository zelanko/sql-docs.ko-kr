---
title: 추가 확장 저장 프로시저를 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], adding
- adding extended stored procedures
- collations [SQL Server], extended stored procedures
ms.assetid: 10f1bb74-3b43-4efd-b7ab-7a85a8600a50
author: rothja
ms.author: jroth
ms.openlocfilehash: bba543dbf89cb1dd3c0eb8a456a54c3c31c51d02
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903405"
---
# <a name="adding-an-extended-stored-procedure-to-sql-server"></a>SQL Server에 확장 저장 프로시저 추가
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 확장 저장 프로시저 함수가 포함된 DLL은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 확장으로 사용됩니다. DLL을 설치 하려면 표준을 포함 하는 것과 같은 디렉터리에 파일 복사 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DLL 파일 (C:\Program Files\Microsoft SQL Server\MSSQL12.0. *x*\MSSQL\Binn 기본적으로).  
  
 확장 저장 프로시저 DLL을 서버에 복사한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자가 DLL의 각 확장 저장 프로시저 함수를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 등록해야 합니다. 이 작업은 sp_addextendedproc 시스템 저장 프로시저를 사용하여 수행합니다.  
  
> [!IMPORTANT]  
>  시스템 관리자는 확장 저장 프로시저를 서버에 추가하고 다른 사용자에게 실행 권한을 부여하기 전에 각 확장 저장 프로시저를 철저히 검토하여 유해한 악성 코드가 포함되지는 않았는지를 확인해야 합니다.  모든 사용자 입력에 대해 유효성을 검사합니다. 유효성 검사를 수행하기 전에는 사용자 입력을 연결하지 마십시오. 유효성 검사가 수행되지 않은 사용자 입력으로부터 생성된 명령은 실행하지 마세요.  
  
 sp_addextendedproc의 첫 번째 매개 변수는 함수 이름을 지정하고 두 번째 매개 변수는 해당 함수가 있는 DLL의 이름을 지정합니다. DLL의 전체 경로를 지정하는 것이 좋습니다.  
  
> [!IMPORTANT]  
>  SQL Server 2005 이상으로 업그레이드하면 전체 경로에 등록되지 않은 기존 DLL은 작동하지 않습니다. 이 문제를 해결하려면 sp_dropextendedproc를 사용하여 DLL의 등록을 취소한 다음 전체 경로를 지정하여 sp_addextendedproc로 DLL을 다시 등록합니다.  
  
 `sp_addextendedproc`에 지정된 함수 이름은 DLL의 함수 이름과 대/소문자를 포함하여 정확히 일치해야 합니다. 예를 들어 다음 명령은 `xp_hello,`이라는 dll에 있는 `xp_hello.dll` 함수를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 확장 저장 프로시저로 등록합니다.  
  
```  
sp_addextendedproc 'xp_hello', 'c:\Program Files\Microsoft SQL Server\MSSQL13.0.MSSQLSERVER\MSSQL\Binn\xp_hello.dll';  
```  
  
 `sp_addextendedproc`에 지정된 함수 이름이 DLL의 함수 이름과 정확히 일치하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 새 이름이 등록되지만 해당 이름을 사용할 수 없습니다. 예를 들어 있지만 `xp_Hello` 로 등록 된를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 확장 저장된 프로시저에 있는 `xp_hello.dll`, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하는 경우 DLL의 함수를 찾을 수 없습니다 `xp_Hello` 나중에 함수를 호출 하 여 합니다.  
  
```  
--Register the function (xp_hello) with an initial upper case  
sp_addextendedproc 'xp_Hello', 'c:\xp_hello.dll';  
  
--Use the newly registered name to call the function  
DECLARE @txt varchar(33);  
EXEC xp_Hello @txt OUTPUT;  
  
--This is the error message  
Server: Msg 17750, Level 16, State 1, Procedure xp_Hello, Line 1  
Could not load the DLL xp_hello.dll, or one of the DLLs it references. Reason: 127(The specified procedure could not be found.).  
```  
  
 `sp_addextendedproc`에 지정한 함수 이름이 DLL의 함수 이름과 정확히 일치하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 데이터 정렬에서 대/소문자를 구분하지 않는 경우 사용자는 이름의 대/소문자를 임의로 조합하여 확장 저장 프로시저를 호출할 수 있습니다.  
  
```  
--Register the function (xp_hello)  
sp_addextendedproc 'xp_hello', 'c:\xp_hello.dll';  
  
--The following will succeed in calling xp_hello  
DECLARE @txt varchar(33);  
EXEC xp_Hello @txt OUTPUT;  
  
DECLARE @txt varchar(33);  
EXEC xp_HelLO @txt OUTPUT;  
  
DECLARE @txt varchar(33);  
EXEC xp_HELLO @txt OUTPUT;  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 데이터 정렬에서 대/소문자를 구분하는 경우에는 프로시저가 DLL의 함수 이름 및 데이터 정렬과 정확히 일치하도록 등록되었더라도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 대/소문자를 다르게 하여 프로시저를 호출하면 확장 저장 프로시저를 호출할 수 없습니다.  
  
```  
--Register the function (xp_hello)  
sp_addextendedproc 'xp_hello', 'c:\xp_hello.dll';  
  
--The following will result in an error  
DECLARE @txt varchar(33);  
EXEC xp_HELLO @txt OUTPUT;  
  
--This is the error  
Server: Msg 2812, Level 16, State 62, Line 1  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 중지한 후 다시 시작할 필요는 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_addextendedproc &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
