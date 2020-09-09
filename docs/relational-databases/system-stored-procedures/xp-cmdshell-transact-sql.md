---
description: xp_cmdshell(Transact-SQL)
title: xp_cmdshell (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_cmdshell
- xp_cmdshell_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: 18935cf4-b320-4954-b6c1-e007fcefe358
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3333e8d26c6f79bc3f99298e2854f05789caac9f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541060"
---
# <a name="xp_cmdshell-transact-sql"></a>xp_cmdshell(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Windows  명령 셸을 생성하고 실행을 위해 문자열로 전달합니다. 모든 출력은 텍스트 행으로 반환됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_cmdshell { 'command_string' } [ , no_output ]  
```  
  
## <a name="arguments"></a>인수  
 **'** *command_string* **'**  
 운영 체제로 전달할 명령이 포함된 문자열입니다. *command_string* 는 **varchar (8000)** 또는 **nvarchar (4000)** 이며 기본값은 없습니다. *command_string* 는 둘 이상의 큰따옴표 집합을 포함할 수 없습니다. *Command_string*에서 참조 되는 파일 경로나 프로그램 이름에 공백이 있는 경우에는 단일 큰따옴표가 필요 합니다. 포함 공백에 문제가 있으면 해결 방법으로 FAT  8.3  파일 이름을 사용하십시오.  
  
 **no_output**  
 출력이 클라이언트에 반환되지 않도록 지정하는 선택적 매개 변수입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 다음 `xp_cmdshell` 문을 실행하면 현재 디렉터리를 나열한 디렉터리를 반환합니다.  
  
```  
EXEC xp_cmdshell 'dir *.exe';  
GO  
```  
  
 행은 **nvarchar (255)** 열로 반환 됩니다. **No_output** 옵션을 사용 하면 다음 항목만 반환 됩니다.  
  
```  
The command(s) completed successfully.  
```  
  
## <a name="remarks"></a>설명  
 **Xp_cmdshell** 로 생성 된 Windows 프로세스는 서비스 계정과 동일한 보안 권한을 갖습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **xp_cmdshell** 동기적으로 작동 합니다. 명령 셸 명령이 완료되기 전에는 호출자에게 컨트롤이 반환되지 않습니다.  
  
 정책 기반 관리를 사용 하거나 **sp_configure**를 실행 하 여 **xp_cmdshell** 를 사용 하거나 사용 하지 않도록 설정할 수 있습니다. 자세한 내용은 [노출 영역 구성](../../relational-databases/security/surface-area-configuration.md) 및 [Xp_cmdshell 서버 구성 옵션](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)을 참조 하세요.  
  
> [!IMPORTANT]
>  일괄 처리 내에서 **xp_cmdshell** 실행 되 고 오류를 반환 하는 경우 일괄 처리가 실패 합니다. 이 동작은 기존 버전과 달라진 동작입니다. 이전 버전의에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 일괄 처리가 계속 실행 됩니다.  
  
## <a name="xp_cmdshell-proxy-account"></a>xp_cmdshell  프록시 계정  
 **Sysadmin** 고정 서버 역할의 멤버가 아닌 사용자가 호출 하는 경우 **xp_cmdshell** **# #xp_cmdshell_proxy_account # #** 이라는 자격 증명에 저장 된 계정 이름과 암호를 사용 하 여 Windows에 연결 합니다. 이 프록시 자격 증명이 없으면 **xp_cmdshell** 실패 합니다.  
  
 프록시 계정 자격 증명은 **sp_xp_cmdshell_proxy_account**를 실행 하 여 만들 수 있습니다. 이 저장 프로시저는 Windows  사용자 이름과 암호를 인수로 사용합니다. 예를 들어 다음 명령은 Windows  암호가 `SHIPPING\KobeR`인 Windows  도메인 사용자 `sdfh%dkc93vcMt0`에 대한 프록시 자격 증명을 만듭니다.  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'SHIPPING\KobeR','sdfh%dkc93vcMt0';  
```  
  
 자세한 내용은 [sp_xp_cmdshell_proxy_account &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)를 참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 악의적인 사용자가 **xp_cmdshell**를 사용 하 여 권한을 상승 하려고 시도 하기 때문에 **xp_cmdshell** 기본적으로 사용 하지 않도록 설정 되어 있습니다. **Sp_configure** 또는 **정책 기반 관리** 를 사용 하 여 사용 하도록 설정 합니다. 자세한 내용은 [xp_cmdshell 서버 구성 옵션](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)을 참조하세요.  
  
 처음 사용 하도록 설정 하면 **xp_cmdshell** 를 실행 하려면 CONTROL SERVER 권한이 필요 하 고 **Xp_cmdshell** 에서 만든 Windows 프로세스는 서비스 계정과 동일한 보안 컨텍스트를 갖습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]서비스 계정에는 **xp_cmdshell**에서 만든 프로세스에서 수행 하는 작업에 필요한 것 보다 많은 권한이 있는 경우가 많습니다. 보안을 강화 하려면 권한이 높은 사용자로 **xp_cmdshell** 에 대 한 액세스를 제한 해야 합니다.  
  
 비관리자가 **xp_cmdshell**를 사용할 수 있도록 하 고에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 권한이 낮은 계정의 보안 토큰을 사용 하 여 자식 프로세스를 만들 수 있도록 허용 하려면 다음 단계를 수행 합니다.  
  
1.  프로세스에 필요한 최소한의 권한을 가진 Windows  로컬 사용자 계정 또는 도메인 계정을 만들고 사용자 지정합니다.  
  
2.  **Sp_xp_cmdshell_proxy_account** 시스템 프로시저를 사용 하 여 최소 권한 계정을 사용 하도록 **xp_cmdshell** 를 구성 합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]개체 탐색기에서 서버 이름의 **속성** 을 마우스 오른쪽 단추로 클릭 하 고 **서버 프록시 계정** 섹션의 **보안** 탭을 확인 하 여을 사용 하 여이 프록시 계정을 구성할 수도 있습니다.  
  
3.  에서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] master 데이터베이스를 사용 하 여 `GRANT exec ON xp_cmdshell TO N'<some_user>';` 특정**sysadmin** 이 아닌 사용자에 게 **xp_cmdshell**실행 기능을 제공 하는 문을 실행 합니다. 지정한 사용자가 master 데이터베이스에 있어야 합니다.  
  
 이제 관리자가 아닌 사용자가 **xp_cmdshell** 를 사용 하 여 운영 체제 프로세스를 시작할 수 있으며, 이러한 프로세스는 구성한 프록시 계정의 권한으로 실행 됩니다. CONTROL SERVER 권한이 있는 사용자 ( **sysadmin** 고정 서버 역할의 멤버)는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **xp_cmdshell**에 의해 시작 되는 자식 프로세스에 대 한 서비스 계정의 사용 권한을 계속 받습니다.  
  
 운영 체제 프로세스를 시작할 때 **xp_cmdshell** 에서 사용 되는 Windows 계정을 확인 하려면 다음 문을 실행 합니다.  
  
```  
xp_cmdshell 'whoami.exe'  
  
```  
  
 다른 로그인의 보안 컨텍스트를 확인하려면 다음을 실행합니다.  
  
```  
EXECUTE AS LOGIN = '<other_login>' ;  
GO  
xp_cmdshell 'whoami.exe' ;  
REVERT ;  
  
```  
  
## <a name="examples"></a>예제  
  
### <a name="a-returning-a-list-of-executable-files"></a>A. 실행 파일의 목록 반환  
 다음 예에서는 디렉터리 명령을 실행하는 `xp_cmdshell` 확장 저장 프로시저를 보여 줍니다.  
  
```  
EXEC master..xp_cmdshell 'dir *.exe'  
```  
  
### <a name="b-returning-no-output"></a>B. 출력 반환 안 함  
 다음 예에서는 `xp_cmdshell`을 사용하여 클라이언트에게 출력을 반환하지 않고 명령 문자열을 실행하는 것을 보여 줍니다.  
  
```  
USE master;  
  
EXEC xp_cmdshell 'copy c:\SQLbcks\AdvWorks.bck  
    \\server2\backups\SQLbcks', NO_OUTPUT;  
GO  
```  
  
### <a name="c-using-return-status"></a>C. 반환 상태 사용  
 다음 예에서는 `xp_cmdshell` 확장 저장 프로시저도 반환 상태를 제안 합니다. 반환 코드 값은 `@result` 변수에 저장됩니다.  
  
```  
DECLARE @result int;  
EXEC @result = xp_cmdshell 'dir *.exe';  
IF (@result = 0)  
   PRINT 'Success'  
ELSE  
   PRINT 'Failure';  
```  
  
### <a name="d-writing-variable-contents-to-a-file"></a>D. 파일에 변수 내용 기록  
 다음 예에서는 `@var` 변수의 내용을 현재 서버 디렉터리에 있는 `var_out.txt`라는 파일에 기록합니다.  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'Hello world';  
SET @cmd = 'echo ' + @var + ' > var_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
### <a name="e-capturing-the-result-of-a-command-to-a-file"></a>E. 명령 결과를 파일로 캡처  
 다음 예에서는 현재 디렉터리의 내용을 현재 서버 디렉터리에 있는 `dir_out.txt`라는 파일에 기록합니다.  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'dir/p';  
SET @cmd = @var + ' > dir_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;일반 확장 저장 프로시저 &#40;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_cmdshell 서버 구성 옵션](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)   
 [노출 영역 구성](../../relational-databases/security/surface-area-configuration.md)   
 [Transact-sql&#41;sp_xp_cmdshell_proxy_account &#40;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)  
  
  
