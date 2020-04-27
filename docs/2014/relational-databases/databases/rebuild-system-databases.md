---
title: 시스템 데이터베이스 다시 빌드 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], rebuilding
- REBUILDDATABASE parameter
- rebuilding databases, master
- system databases [SQL Server], rebuilding
ms.assetid: af457ecd-523e-4809-9652-bdf2e81bd876
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b58378e8ba2193a186fb58e3e784bf9bc3cb4d4c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62871280"
---
# <a name="rebuild-system-databases"></a>시스템 데이터베이스 다시 작성
  [master](master-database.md), [model](model-database.md), [msdb](msdb-database.md)또는 [resource](resource-database.md) 시스템 데이터베이스의 손상 문제를 수정하거나 기본 서버 수준 데이터 정렬을 변경하려면 시스템 데이터베이스를 다시 작성해야 합니다. 이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 시스템 데이터베이스를 다시 작성하는 단계별 지침을 제공합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [필수 구성 요소](#Prerequisites)  
  
-   **절차:**  
  
     [시스템 데이터베이스 다시 작성](#RebuildProcedure)  
  
     [리소스 데이터베이스 다시 작성](#Resource)  
  
     [새 msdb 데이터베이스 만들기](#CreateMSDB)  
  
-   **후속 작업:**  
  
     [다시 작성 오류 문제 해결](#Troubleshoot)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
 master, model, msdb 및 tempdb 시스템 데이터베이스를 다시 작성하면 해당 데이터베이스가 삭제된 후 원래 위치에 다시 만들어집니다. REBUILD 문에 새로운 데이터 정렬이 지정되면 해당 데이터 정렬 설정을 사용하여 시스템 데이터베이스가 만들어집니다. 이러한 데이터베이스에 사용자들이 변경한 내용은 손실됩니다. 예를 들어, master 데이터베이스에 사용자 정의 개체가 있거나, msdb에 예약된 작업이 있거나 model 데이터베이스에서 기본 데이터베이스 설정을 변경했을 수 있습니다.  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
 시스템 데이터베이스를 다시 작성하기 전에 다음 태스크를 수행하면 시스템 데이터베이스를 현재 설정으로 복원할 수 있습니다.  
  
1.  서버 차원의 모든 구성 값을 기록합니다.  
  
    ```  
    SELECT * FROM sys.configurations;  
    ```  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 현재 데이터 정렬에 적용된 모든 서비스 팩과 핫픽스를 기록합니다. 시스템 데이터베이스를 다시 작성한 후 이러한 업데이트를 다시 적용해야 합니다.  
  
    ```  
    SELECT  
    SERVERPROPERTY('ProductVersion ') AS ProductVersion,  
    SERVERPROPERTY('ProductLevel') AS ProductLevel,  
    SERVERPROPERTY('ResourceVersion') AS ResourceVersion,  
    SERVERPROPERTY('ResourceLastUpdateDateTime') AS ResourceLastUpdateDateTime,  
    SERVERPROPERTY('Collation') AS Collation;  
    ```  
  
3.  시스템 데이터베이스의 모든 데이터와 로그 파일의 현재 위치를 기록합니다. 시스템 데이터베이스를 다시 작성하면 모든 시스템 데이터베이스가 원래 위치에 설치됩니다. 시스템 데이터베이스 데이터나 로그 파일을 다른 위치로 이동한 경우 해당 파일을 다시 이동해야 합니다.  
  
    ```  
    SELECT name, physical_name AS current_file_location  
    FROM sys.master_files  
    WHERE database_id IN (DB_ID('master'), DB_ID('model'), DB_ID('msdb'), DB_ID('tempdb'));  
    ```  
  
4.  master, model, msdb 데이터베이스의 현재 백업을 찾습니다.  
  
5.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 복제 배포자로 구성된 경우 배포 데이터베이스의 현재 백업을 찾습니다.  
  
6.  시스템 데이터베이스를 다시 작성할 수 있는 권한이 있는지 확인합니다. 이 작업을 수행하려면 `sysadmin` 고정 서버 역할의 멤버여야 합니다. 자세한 내용은 [서버 수준 역할](../security/authentication-access/server-level-roles.md)을 참조하세요.  
  
7.  master, model, msdb 데이터와 로그 템플릿 파일의 복사본이 로컬 서버에 있는지 확인합니다. 템플릿 파일의 기본 위치는 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn\Templates입니다. 이러한 파일은 다시 작성 프로세스 중에 사용되므로 성공적으로 설치를 수행하려면 반드시 있어야 합니다. 이러한 파일이 없으면 설치 시 복구 기능을 실행하거나 설치 미디어에서 해당 파일을 직접 복사하세요. 설치 미디어에서 이러한 파일을 찾으려면 해당 플랫폼 디렉터리(x86 또는 x64)로 이동한 후 setup\sql_engine_core_inst_msi\Pfiles\SqlServr\MSSQL.X\MSSQL\Binn\Templates로 이동합니다.  
  
##  <a name="rebuild-system-databases"></a><a name="RebuildProcedure"></a> 시스템 데이터베이스 다시 작성  
 다음은 master, model, msdb 및 tempdb 시스템 데이터베이스를 다시 작성하는 절차입니다. 다시 작성할 시스템 데이터베이스를 지정할 수 없습니다. 클러스터형 인스턴스의 경우 액티브 노드에서 이 절차를 수행해야 하고, 이 절차를 수행하기 전에 해당 클러스터 애플리케이션 그룹의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스를 오프라인으로 설정해야 합니다.  
  
 리소스 데이터베이스는 이 절차를 통해 다시 작성할 수 없습니다. 이 항목 뒷부분에 나오는 "리소스 데이터베이스 다시 작성 절차" 섹션을 참조하세요.  
  
#### <a name="to-rebuild-system-databases-for-an-instance-of-sql-server"></a>SQL Server 2008 인스턴스의 시스템 데이터베이스를 다시 작성하려면  
  
1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 미디어를 디스크 드라이브에 넣거나, 명령 프롬프트에서 로컬 서버의 setup.exe 파일이 있는 디렉터리로 변경합니다. 서버의 기본 위치는 C:\Program Files\Microsoft SQL Server\120\Setup Bootstrap\Release입니다.  
  
2.  명령 프롬프트 창에서 다음 명령을 입력합니다. 대괄호([])는 옵션 매개 변수를 나타내는 데 사용되며, 입력하지는 않습니다. Windows 운영 체제에서 UAC(사용자 계정 컨트롤)를 사용할 경우 설치를 실행하려면 승격된 권한이 필요합니다. 명령 프롬프트에서 관리자 권한으로 실행합니다.  
  
     `Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName /SQLSYSADMINACCOUNTS=accounts [ /SAPWD= StrongPassword ] [ /SQLCOLLATION=CollationName]`  
  
    |매개 변수 이름|설명|  
    |--------------------|-----------------|  
    |/QUIET 또는 /Q|설치 프로그램이 사용자 인터페이스 없이 실행되도록 지정합니다.|  
    |/ACTION=REBUILDDATABASE|설치 시 시스템 데이터베이스를 다시 작성하도록 지정합니다.|  
    |/INSTANCENAME =*instancename*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 이름입니다. 기본 인스턴스의 경우 MSSQLSERVER를 입력합니다.|  
    |/SQLSYSADMINACCOUNTS=*accounts*|`sysadmin` 고정 서버 역할에 추가할 Windows 그룹이나 개별 계정을 지정합니다. 둘 이상의 계정을 지정할 경우 각 계정 이름을 공백으로 구분합니다. 예를 들면 **BUILTIN\Administrators MyDomain\MyUser**와 같이 입력합니다. 계정 이름에 공백이 포함되어 있는 계정을 지정할 때는 계정을 큰따옴표로 묶습니다. 예를 들어 다음과 같이 입력합니다. `NT AUTHORITY\SYSTEM`|  
    |[ /SAPWD=*StrongPassword* ]|`sa` 계정에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 암호를 지정 합니다. 해당 인스턴스에서 혼합 인증([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 인증) 모드를 사용할 경우 이 매개 변수가 필요합니다.<br /><br /> ** \* \* 보안 \* 정보** `sa` 계정은 잘 알려진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정 이므로 악의적인 사용자의 대상이 되는 경우가 많습니다. `sa` 로그인에 대해 강력한 암호를 사용하도록 합니다.<br /><br /> Windows 인증 모드에 이 매개 변수를 지정하지 마세요.|  
    |[ /SQLCOLLATION=*CollationName* ]|서버 수준 데이터 정렬을 새로 지정합니다. 이 매개 변수는 선택 사항입니다. 지정하지 않으면 서버의 현재 데이터 정렬이 사용됩니다.<br /><br /> ** \* 중요 \* \* ** 서버 수준 데이터 정렬을 변경 해도 기존 사용자 데이터베이스의 데이터 정렬은 변경 되지 않습니다. 새로 만드는 모든 사용자 데이터베이스는 기본적으로 새로운 데이터 정렬을 사용하게 됩니다.<br /><br /> 자세한 내용은 [서버 데이터 정렬 설정 또는 변경](../collations/set-or-change-the-server-collation.md)을 참조하세요.|  
  
3.  시스템 데이터베이스를 다시 작성하는 작업이 완료되면 아무런 메시지 없이 명령 프롬프트로 돌아갑니다. Summary.txt 로그 파일을 검토하여 프로세스가 성공적으로 완료되었는지 확인합니다. 이 파일은 C:\Program Files\Microsoft SQL Server\120\Setup Bootstrap\Logs에 있습니다.  
  
## <a name="post-rebuild-tasks"></a>다시 작성 후 수행할 태스크  
 데이터베이스를 다시 작성한 후에는 다음과 같은 추가 태스크를 수행해야 할 수 있습니다.  
  
-   master, model 및 msdb 데이터베이스의 최근 전체 백업을 복원합니다. 자세한 내용은 [시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)를 참조하세요.  
  
    > [!IMPORTANT]  
    >  서버 데이터 정렬을 변경했을 경우 시스템 데이터베이스를 복원하지 마세요. 시스템 데이터베이스를 복원하면 새로운 데이터 정렬이 이전 데이터 정렬 설정으로 바뀝니다.  
  
     백업을 사용할 수 없거나 복원된 백업이 최신 백업이 아닌 경우 누락된 항목을 다시 만듭니다. 예를 들어 사용자 데이터베이스, 백업 디바이스, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인, 끝점 등에 대한 모든 누락 항목을 다시 만듭니다. 항목을 다시 만드는 가장 좋은 방법은 해당 항목을 만들었던 원래 스크립트를 실행하는 것입니다.  
  
> [!IMPORTANT]  
>  스크립트에 보안을 설정해 무단으로 내용을 변경할 수 없도록 하는 것이 좋습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 복제 배포자로 구성된 경우 배포 데이터베이스를 복원해야 합니다. 자세한 내용은 [복제된 데이터베이스 백업 및 복원](../replication/administration/back-up-and-restore-replicated-databases.md)을 참조하세요.  
  
-   시스템 데이터베이스를 앞에서 기록해 둔 위치로 이동합니다. 자세한 내용은 [시스템 데이터베이스 이동](system-databases.md)을 참조하세요.  
  
-   서버 차원의 구성 값이 앞에서 기록해 둔 값과 일치하는지 확인합니다.  
  
##  <a name="rebuild-the-resource-database"></a><a name="Resource"></a> 리소스 데이터베이스 다시 작성  
 다음은 리소스 시스템 데이터베이스를 다시 작성하는 절차입니다. 리소스 데이터베이스를 다시 작성하면 모든 서비스 팩과 핫픽스 업데이트가 손실되므로 다시 적용해야 합니다.  
  
#### <a name="to-rebuild-the-resource-system-database"></a>리소스 시스템 데이터베이스를 다시 작성하려면  
  
1.  배포 미디어에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 프로그램(setup.exe)을 실행합니다.  
  
2.  왼쪽의 탐색 영역에서 **유지 관리**를 클릭한 다음 **복구**를 클릭합니다.  
  
3.  시스템에 사전 요구 사항가 설치되어 있고 컴퓨터가 설치 유효성 검사 규칙을 통과하는지 확인하기 위해 설치 지원 규칙 및 파일 루틴이 실행됩니다. 계속하려면 **확인** 또는 **설치** 를 클릭합니다.  
  
4.  인스턴스 선택 페이지에서 복구할 인스턴스를 선택한 후 **다음**을 클릭합니다.  
  
5.  작업이 유효한지 검사하는 복구 규칙이 실행됩니다. 계속하려면 **다음**을 클릭합니다.  
  
6.  **복구 준비** 페이지에서 **복구**를 클릭합니다. 완료 페이지에서 작업이 완료되었음을 알려 줍니다.  
  
##  <a name="create-a-new-msdb-database"></a><a name="CreateMSDB"></a>새 msdb 데이터베이스 만들기  
 `msdb` 데이터베이스가 손상 된 경우 `msdb` 데이터베이스 백업이 없는 **경우에는** 인스턴스를 사용 하 여 새 `msdb` 를 만들 수 있습니다.  
  
> [!WARNING]  
>  사용 된 `msdb` **msdb** 스크립트를 사용 하 여 데이터베이스를 다시 작성 하면 작업, `msdb` 경고, 운영자, 유지 관리 계획, 백업 기록, 정책 기반 관리 설정, 데이터베이스 메일, 성능 데이터 웨어하우스 등과 같은에 저장 된 모든 정보가 제거 됩니다.  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에이전트, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssRS](../../includes/ssrs.md)]를 포함하는 [!INCLUDE[ssIS](../../includes/ssis-md.md)]에 연결된 서비스 및 데이터 저장소와 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하는 애플리케이션을 모두 중지합니다.  
  
2.  다음 명령을 사용하여 명령줄에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 시작합니다. `NET START MSSQLSERVER /T3608`  
  
     자세한 내용은 [시작, 중지, 일시 중지, 다시 시작, 데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)를 참조 하세요.  
  
3.  다른 명령줄 창에서 다음 명령을 실행 하 `msdb` 여 데이터베이스를 분리 하 고 * \<servername>* 를 인스턴스로 바꿉니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`SQLCMD -E -S<servername> -dmaster -Q"EXEC sp_detach_db msdb"`  
  
4.  Windows 탐색기를 사용 하 여 데이터베이스 `msdb` 파일의 이름을 바꿉니다. 기본적으로 이러한 데이터베이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 데이터 하위 폴더에 있습니다.  
  
5.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 서비스를 중지하고 다시 시작합니다.  
  
6.  명령줄 창에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 시작하고 다음 명령을 실행합니다. `SQLCMD -E -S<servername> -i"C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Install\instmsdb.sql" -o" C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Install\instmsdb.out"`  
  
     * \<Servername>* 를 인스턴스로 바꿉니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 파일 시스템 경로를 사용합니다.  
  
7.  Windows 메모장을 사용하여 **instmsdb.out** 파일을 열고 오류 출력을 확인합니다.  
  
8.  인스턴스에 이미 설치된 서비스 팩 또는 핫픽스를 모두 다시 적용합니다.  
  
9. 작업, 경고 등의 `msdb` 데이터베이스에 저장 된 사용자 콘텐츠를 다시 만듭니다.  
  
10. `msdb` 데이터베이스를 백업합니다.  
  
##  <a name="troubleshoot-rebuild-errors"></a><a name="Troubleshoot"></a> 다시 작성 오류 문제 해결  
 구문 및 기타 런타임 오류는 명령 프롬프트 창에 표시됩니다. 설치 문에 다음과 같은 구문 오류가 없는지 확인합니다.  
  
-   각 매개 변수 이름 앞에 슬래시(/)가 있어야 합니다.  
  
-   매개 변수 이름과 매개 변수 값 사이에 등호(=)가 있어야 합니다.  
  
-   매개 변수 이름과 등호 사이에 공백이 없어야 합니다.  
  
-   구문에 지정되지 않은 쉼표(,)나 기타 문자가 없어야 합니다.  
  
 다시 작성 작업이 완료되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그를 검토하여 오류가 없는지 확인합니다. 로그의 기본 위치는 C:\Program Files\Microsoft SQL Server\120\Setup Bootstrap\Logs입니다. 다시 작성 프로세스의 결과가 들어 있는 로그 파일을 찾으려면 명령 프롬프트에서 Logs 폴더로 이동한 후 `findstr /s RebuildDatabase summary*.*`를 입력합니다. 이렇게 검색하면 시스템 데이터베이스 다시 작성의 결과가 들어 있는 모든 로그 파일이 나타납니다. 로그 파일을 열고 검토하여 관련된 오류 메시지가 없는지 확인합니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 데이터베이스](system-databases.md)  
  
  
