---
title: xp_cmdshell (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_cmdshell
- xp_cmdshell_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: 18935cf4-b320-4954-b6c1-e007fcefe358
caps.latest.revision: 26
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4474d6bcd0c24c00ae4c0b6297d11cdbe76ff55b
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39102381"
---
# <a name="xpcmdshell-transact-sql"></a>xp_cmdshell(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Windows  명령 셸을 생성하고 실행을 위해 문자열로 전달합니다. 모든 출력은 텍스트 행으로 반환됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_cmdshell { 'command_string' } [ , no_output ]  
```  
  
## <a name="arguments"></a>인수  
 **'** *command_string* **'**  
 운영 체제로 전달할 명령이 포함된 문자열입니다. *command_string* 됩니다 **varchar(8000)** 하거나 **nvarchar(4000)**, 기본값은 없습니다. *command_string* 큰따옴표 하나 이상의 집합을 포함할 수 없습니다. 단일 쌍의 따옴표가 필요한 경우 공백을 파일 경로에 있는 프로그램에서 참조 하는 이름이 나 *command_string*합니다. 포함 공백에 문제가 있으면 해결 방법으로 FAT  8.3  파일 이름을 사용하십시오.  
  
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
  
 행을 반환 되는 **nvarchar(255)** 열입니다. 경우는 **no_output** 옵션을 사용 하면 다음만 반환 됩니다.  
  
```  
The command(s) completed successfully.  
```  
  
## <a name="remarks"></a>Remarks  
 Windows 프로세스에 의해 생성 된 **xp_cmdshell** 와 같은 보안 권한이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정입니다.  
  
 **xp_cmdshell** 동기적으로 작동 합니다. 명령 셸 명령이 완료되기 전에는 호출자에게 컨트롤이 반환되지 않습니다.  
  
 **xp_cmdshell** 사용 될 수 있고 정책 기반 관리를 사용 하 여 또는 실행 하 여 사용 하지 않도록 **sp_configure**합니다. 자세한 내용은 [노출 영역 구성](../../relational-databases/security/surface-area-configuration.md) 하 고 [xp_cmdshell 서버 구성 옵션](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)합니다.  
  
> [!IMPORTANT]  
>  하는 경우 **xp_cmdshell** 일괄 처리 내에서 실행 되 고 오류를 반환 합니다. 일괄 처리 하지 못합니다. 이 동작은 기존 버전과 달라진 동작입니다. 이전 버전의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 일괄 처리가 계속 실행 합니다.  
  
## <a name="xpcmdshell-proxy-account"></a>xp_cmdshell  프록시 계정  
 멤버가 아닌 사용자가 호출 되는 경우는 **sysadmin** 고정 서버 역할 **xp_cmdshell** 계정 이름 및 명명 된 자격 증명에 저장 된 암호를 사용 하 여 Windows를 연결할 **# # xp_cmdshell_proxy_account # #** 합니다. 프록시 자격 증명이 없으면 **xp_cmdshell** 실패 합니다.  
  
 프록시 계정 자격 증명을 실행 하 여 만들 수 있습니다 **sp_xp_cmdshell_proxy_account**합니다. 이 저장 프로시저는 Windows  사용자 이름과 암호를 인수로 사용합니다. 예를 들어 다음 명령은 Windows  암호가 `SHIPPING\KobeR`인 Windows  도메인 사용자 `sdfh%dkc93vcMt0`에 대한 프록시 자격 증명을 만듭니다.  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'SHIPPING\KobeR','sdfh%dkc93vcMt0';  
```  
  
 자세한 내용은 [sp_xp_cmdshell_proxy_account &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 악의적인 사용자가 사용 하 여 해당 권한을 승격할 경우에 따라 시도 하기 때문에 **xp_cmdshell**하십시오 **xp_cmdshell** 기본적으로 비활성화 됩니다. 사용 하 여 **sp_configure** 하거나 **정책 기반 관리** 사용 하도록 설정 합니다. 자세한 내용은 [xp_cmdshell 서버 구성 옵션](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)을 참조하세요.  
  
 먼저 사용 하도록 설정 하면 **xp_cmdshell** 에서 만든 Windows 프로세스 및 실행 하려면 CONTROL SERVER 권한이 필요 **xp_cmdshell** 와 같은 보안 컨텍스트에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정입니다. 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에서 만든 프로세스에서 수행 된 작업에 필요한 것 보다 많은 권한을 같으며 **xp_cmdshell**합니다. 보안을 강화 하기에 대 한 액세스 **xp_cmdshell** 높은 권한이 가진된 사용자로 제한 해야 합니다.  
  
 비관리자 사용을 허용 하도록 **xp_cmdshell**, 허용 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자식 프로세스 낮은 계정의 보안 토큰을 만들려면 다음이 단계를 수행 합니다.  
  
1.  프로세스에 필요한 최소한의 권한을 가진 Windows  로컬 사용자 계정 또는 도메인 계정을 만들고 사용자 지정합니다.  
  
2.  사용 하 여는 **sp_xp_cmdshell_proxy_account** 시스템 구성 하는 절차 **xp_cmdshell** 해당 최소 권한 계정을 사용 하도록 합니다.  
  
    > [!NOTE]  
    >  사용 하 여이 프록시 계정을 구성할 수도 있습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 마우스 오른쪽 단추로 클릭 하 여 **속성** 서버에서 개체 탐색기에서 이름을 지정 하 고에 **보안** 탭을 **서버 프록시 계정** 섹션입니다.  
  
3.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], 실행 master 데이터베이스를 사용 하는 `GRANT exec ON xp_cmdshell TO '<somelogin>'` 아닌 특정 있도록 문을**sysadmin** 사용자 실행 하는 기능은 **xp_cmdshell**. 지정된 로그인은 master 데이터베이스에서 사용자에게 매핑해야 합니다.  
  
 이제 관리자가 아닌 운영 체제 프로세스를 시작할 수 있습니다 **xp_cmdshell** 구성한 프록시 계정의 권한으로 실행 하는 프로세스 및 합니다. CONTROL SERVER 권한이 있는 사용자 (의 멤버는 **sysadmin** 고정된 서버 역할)의 사용 권한의 받을 계속 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에서 실행 되는 자식 프로세스에 대 한 **xp_cmdshell** .  
  
 사용 중인 Windows 계정에 결정할 **xp_cmdshell** 운영 체제 프로세스를 시작할 때 다음 문을 실행 합니다.  
  
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
  
### <a name="a-returning-a-list-of-executable-files"></a>1. 실행 파일의 목록 반환  
 다음 예에서는 디렉터리 명령을 실행하는 `xp_cmdshell` 확장 저장 프로시저를 보여 줍니다.  
  
```  
EXEC master..xp_cmdshell 'dir *.exe''  
```  
  
### <a name="b-returning-no-output"></a>2. 출력 반환 안 함  
 다음 예에서는 `xp_cmdshell`을 사용하여 클라이언트에게 출력을 반환하지 않고 명령 문자열을 실행하는 것을 보여 줍니다.  
  
```  
USE master;  
  
EXEC xp_cmdshell 'copy c:\SQLbcks\AdvWorks.bck  
    \\server2\backups\SQLbcks, NO_OUTPUT';  
GO  
```  
  
### <a name="c-using-return-status"></a>3. 반환 상태 사용  
 다음 예제에서는 `xp_cmdshell` 확장된 저장된 프로시저도 반환 상태를 제안 합니다. 반환 코드 값은 `@result` 변수에 저장됩니다.  
  
```  
DECLARE @result int;  
EXEC @result = xp_cmdshell 'dir *.exe';  
IF (@result = 0)  
   PRINT 'Success'  
ELSE  
   PRINT 'Failure';  
```  
  
### <a name="d-writing-variable-contents-to-a-file"></a>4. 파일에 변수 내용 기록  
 다음 예에서는 `@var` 변수의 내용을 현재 서버 디렉터리에 있는 `var_out.txt`라는 파일에 기록합니다.  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'Hello world';  
SET @cmd = 'echo ' + @var + ' > var_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
### <a name="e-capturing-the-result-of-a-command-to-a-file"></a>5. 명령 결과를 파일로 캡처  
 다음 예에서는 현재 디렉터리의 내용을 현재 서버 디렉터리에 있는 `dir_out.txt`라는 파일에 기록합니다.  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'dir/p';  
SET @cmd = @var + ' > dir_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
## <a name="see-also"></a>관련 항목  
 [일반 확장 저장된 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_cmdshell 서버 구성 옵션](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)   
 [노출 영역 구성](../../relational-databases/security/surface-area-configuration.md)   
 [sp_xp_cmdshell_proxy_account &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)  
  
  
