---
title: xp_cmdshell (거래 -SQL) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/30/2020
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2ce32fc31373077418e77d31ce064d60e23f1b24
ms.sourcegitcommit: fc5b757bb27048a71bb39755648d5cefe25a8bc6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80402688"
---
# <a name="xp_cmdshell-transact-sql"></a>xp_cmdshell(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Windows  명령 셸을 생성하고 실행을 위해 문자열로 전달합니다. 모든 출력은 텍스트 행으로 반환됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_cmdshell { 'command_string' } [ , no_output ]  
```  
  
## <a name="arguments"></a>인수  
 **'** *command_string* **'**  
 운영 체제로 전달할 명령이 포함된 문자열입니다. *command_string* **varchar (8000)** 또는 **nvarchar (4000)이며**기본값은 없습니다. *command_string* 두 개 이상의 이중 따옴표 집합을 포함할 수 없습니다. command_string 참조되는 파일 경로 또는 프로그램 이름에 공백이 있는 경우 단일 인용 부호 쌍이 *필요합니다.* 포함 공백에 문제가 있으면 해결 방법으로 FAT  8.3  파일 이름을 사용하십시오.  
  
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
  
 행은 **nvarchar(255)** 열에 반환됩니다. **no_output** 옵션을 사용하는 경우 다음 만 반환됩니다.  
  
```  
The command(s) completed successfully.  
```  
  
## <a name="remarks"></a>설명  
 **xp_cmdshell** 생성되는 Windows 프로세스는 서비스 계정과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 동일한 보안 권한을 가짐입니다.  
  
 **xp_cmdshell** 동기적으로 작동합니다. 명령 셸 명령이 완료되기 전에는 호출자에게 컨트롤이 반환되지 않습니다.  
  
 **xp_cmdshell** 정책 기반 관리를 사용하거나 **sp_configure**실행하여 활성화 및 비활성화할 수 있습니다. 자세한 내용은 서버 구성 [및 xp_cmdshell 서버](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md) [구성](../../relational-databases/security/surface-area-configuration.md) 옵션을 참조하십시오.  
  
> [!IMPORTANT]
>  **xp_cmdshell** 일괄 처리 내에서 실행되고 오류를 반환하면 일괄 처리가 실패합니다.
  
## <a name="xp_cmdshell-proxy-account"></a>xp_cmdshell  프록시 계정  
 **sysadmin** 고정 서버 역할의 구성원이 아닌 사용자가 호출하는 경우 **xp_cmdshell** **##xp_cmdshell_proxy_account##이라는**자격 증명에 저장된 계정 이름과 암호를 사용하여 Windows에 연결합니다. 이 프록시 자격 증명이 없으면 **xp_cmdshell** 실패합니다.  
  
 sp_xp_cmdshell_proxy_account **실행하여**프록시 계정 자격 증명을 만들 수 있습니다. 이 저장 프로시저는 Windows  사용자 이름과 암호를 인수로 사용합니다. 예를 들어 다음 명령은 Windows  암호가 `SHIPPING\KobeR`인 Windows  도메인 사용자 `sdfh%dkc93vcMt0`에 대한 프록시 자격 증명을 만듭니다.  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'SHIPPING\KobeR','sdfh%dkc93vcMt0';  
```  
  
 자세한 내용은 [sp_xp_cmdshell_proxy_account &#40;거래-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)를 참조하십시오.  
  
## <a name="permissions"></a>사용 권한  
 악의적인 사용자가 xp_cmdshell **사용하여**권한을 높이려고 시도하는 경우가 xp_cmdshell 기본적으로 **비활성화됩니다.** **sp_configure** 또는 **정책 기반 관리를** 사용하여 활성화합니다. 자세한 내용은 [xp_cmdshell 서버 구성 옵션](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)을 참조하세요.  
  
 처음 활성화되면 **xp_cmdshell** CONTROL SERVER 를 실행하려면 권한이 필요하며 **xp_cmdshell** 만든 Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스는 서비스 계정과 동일한 보안 컨텍스트를 가짐을 가시고 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에는 xp_cmdshell 에서 만든 프로세스에서 수행하는 작업에 필요한 것보다 많은 권한이 있는 경우가 **많습니다.** 보안을 강화하려면 **xp_cmdshell** 대한 액세스권한을 높은 권한있는 사용자로 제한해야 합니다.  
  
 관리자가 아닌 사용자가 **xp_cmdshell**사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 수 있도록 허용하고 권한이 낮은 계정의 보안 토큰을 사용하여 자식 프로세스를 만들 수 있도록 하려면 다음 단계를 따르십시오.  
  
1.  프로세스에 필요한 최소한의 권한을 가진 Windows  로컬 사용자 계정 또는 도메인 계정을 만들고 사용자 지정합니다.  
  
2.  **sp_xp_cmdshell_proxy_account** 시스템 프로시저를 사용하여 **xp_cmdshell** 최소 권한 계정을 사용하도록 구성합니다.  
  
    > [!NOTE]  
    >  개체 탐색기에서 서버 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 이름의 **속성을** 마우스 오른쪽 단추로 클릭하여 서버 **프록시 계정** 섹션의 **보안** 탭을 확인하여 이 프록시 계정을 구성할 수도 있습니다.  
  
3.  에서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]마스터 데이터베이스를 사용하여 명령문을 `GRANT exec ON xp_cmdshell TO N'<some_user>';` 실행하여 특정**비ssadmin** 사용자에게 **xp_cmdshell**실행할 수 있는 기능을 제공합니다. 지정된 사용자는 마스터 데이터베이스에 있어야 합니다.  
  
 이제 관리자가 아닌 xp_cmdshell 운영 체제 프로세스를 시작할 수 **있으며** 이러한 프로세스는 구성한 프록시 계정의 사용 권한으로 실행됩니다. CONTROL SERVER 권한(시스템 **관리자** 고정 서버 역할의 구성원)을 가진 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **xp_cmdshell**에서 시작되는 자식 프로세스에 대한 서비스 계정의 권한을 계속 받습니다.  
  
 운영 체제 프로세스를 시작할 때 **xp_cmdshell** 사용하는 Windows 계정을 확인하려면 다음 문을 실행하십시오.  
  
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
  
## <a name="examples"></a>예  
  
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
 다음 예제에서 `xp_cmdshell` 확장 된 저장 프로시저는 반환 상태를 제안합니다. 반환 코드 값은 `@result` 변수에 저장됩니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [Transact-SQL&#41;&#40;일반적인 확장 저장 절차](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_cmdshell 서버 구성 옵션](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)   
 [표면적 구성](../../relational-databases/security/surface-area-configuration.md)   
 [sp_xp_cmdshell_proxy_account &#40;거래 SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)  
  
  
