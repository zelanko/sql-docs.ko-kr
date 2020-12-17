---
title: sqlcmd 유틸리티
description: sqlcmd 유틸리티를 사용하면 다양한 모드를 사용해 Transact-SQL 문, 시스템 프로시저 및 스크립트 파일을 입력할 수 있습니다. 이 유틸리티는 ODBC를 사용하여 Transact-SQL 일괄 처리를 실행합니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- statements [SQL Server], command prompt
- QUIT command
- Transact-SQL statements, command prompt
- EXIT command
- sqlcmd commands
- ED command
- sqlcmd utility
- command prompt utilities [SQL Server], sqlcmd
- '!! command'
- stored procedures [SQL Server], command prompt
- system stored procedures [SQL Server], command prompt
- sqlcmd utility, about sqlcmd utility
- scripts [SQL Server], command prompt
- RESET command
- GO command
ms.assetid: e1728707-5215-4c04-8320-e36f161b834a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 09/11/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017'
ms.openlocfilehash: fcd184e195ce8c81e16ca4ceaaab03a1f156a812
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471834"
---
# <a name="sqlcmd-utility"></a>sqlcmd 유틸리티

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

> SQL Server 2014 이하는 [sqlcmd 유틸리티](/previous-versions/sql/2014/tools/sqlcmd-utility?view=sql-server-2014&preserve-view=true)를 참조하세요.
>
> Linux에서 sqlcmd를 사용하는 방법은 [Linux에 sqlcmd 및 bcp 설치](../linux/sql-server-linux-setup-tools.md)를 참조하세요.

 **sqlcmd** 유틸리티를 사용하면 다양한 모드를 통해 Transact-SQL 문, 시스템 프로시저 및 스크립트 파일을 입력할 수 있습니다.

- 명령 프롬프트에서 다음을 수행합니다.
- **쿼리 편집기** 의 SQLCMD 모드에서.
- Windows 스크립트 파일에서.
- SQL Server 에이전트 작업의 운영 체제(Cmd.exe) 작업 단계에서.

이 유틸리티는 ODBC를 사용하여 Transact-SQL 일괄 처리를 실행합니다.

## <a name="download-the-latest-version-of-sqlcmd-utility"></a>최신 버전의 sqlcmd 유틸리티 다운로드

**[![sqlcmd for x64 다운로드](../ssdt/media/download.png) SQL Server용 Microsoft 명령줄 유틸리티 15(x64) 다운로드(2.6MB)](https://go.microsoft.com/fwlink/?linkid=2142258)**
<br>**[![sqlcmd for x86 다운로드](../ssdt/media/download.png) SQL Server용 Microsoft 명령줄 유틸리티 15(x86) 다운로드(2.3MB)](https://go.microsoft.com/fwlink/?linkid=2142257)**

명령줄 도구는 일반 공급(GA)이지만 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]의 설치 프로그램 패키지로 릴리스됩니다.

**버전 정보**

릴리스 번호: 15.0.2<br>
빌드 번호: 15.0.2000.5<br>
릴리스 날짜: 2020년 9월 11일

최신 버전의 SQLCMD는 Azure AD 인증을 지원하며, 여기에는 SQL Database, Azure Synapse Analytics, Always Encrypted 기능에 대한 MFA(Multi-Factor Authentication) 지원이 포함됩니다.
최신 BCP는 Azure AD 인증을 지원하며, 여기에는 SQL Database 및 Azure Synapse Analytics에 대한 MFA(Multi-Factor Authentication) 지원이 포함됩니다.

**시스템 요구 사항** Windows 10 , Windows 7, Windows 8, Windows 8.1, Windows Server 2008~2019.

이 구성 요소에는 [Windows Installer 4.5](https://www.microsoft.com/download/details.aspx?id=8483) 및 [Microsoft ODBC Driver 17 for SQL Server](https://aka.ms/downloadmsodbcsql)가 둘 다 필요합니다.
 
SQLCMD 버전을 확인하려면 `sqlcmd -?` 명령을 실행하여 15.0.2000.5 버전 이상을 사용하는지 확인합니다.

> [!NOTE]
> Always Encrypted(`-g`) 및 Azure Active Directory 인증(`-G`)을 지원하려면 버전 13.1 이상이 필요합니다. (컴퓨터에 설치된 sqlcmd.exe 버전이 여러 개일 수 있습니다. 올바른 버전을 사용해야 합니다. 버전을 확인하려면 `sqlcmd -?`를 실행하세요.)

기본적으로 미리 설치된 Azure Cloud Shell에서 sqlcmd 유틸리티를 사용해 볼 수 있습니다. [![Cloud Shell 시작](https://shell.azure.com/images/launchcloudshell.png "Cloud Shell 시작")](https://shell.azure.com)

SSMS에서 sqlcmd 문을 실행하려면 위쪽 탐색 쿼리 메뉴 드롭다운에서 SQLCMD 모드를 선택합니다.  

> [!IMPORTANT]
> [!INCLUDE[ssManStudioFull_md](../includes/ssmanstudiofull-md.md)](SSMS)에서는 **쿼리 편집기** 의 일반 및 SQLCMD 모드에서 실행하기 위해 Microsoft [!INCLUDE[dnprdnshort_md](../includes/dnprdnshort-md.md)] SqlClient를 사용합니다. 명령줄에서 **sqlcmd** 를 실행할 경우 **sqlcmd** 는 ODBC 드라이버를 사용합니다. 서로 다른 기본 옵션이 적용될 수 있으므로 [!INCLUDE[ssManStudioFull_md](../includes/ssmanstudiofull-md.md)] SQLCMD 모드 및 **sqlcmd** 유틸리티에서 동일한 쿼리를 실행할 때 다른 동작이 수행될 수 있습니다.  
>

현재는 **sqlcmd** 를 실행할 때 명령줄 옵션과 값 사이에 공백을 넣을 필요가 없습니다. 하지만 후속 릴리스에서는 명령줄 옵션과 값 사이에 공백을 넣어야 할 수도 있습니다.  

 다른 항목: 

- [sqlcmd 유틸리티 시작](../ssms/scripting/sqlcmd-start-the-utility.md)
- [sqlcmd 유틸리티 사용](../ssms/scripting/sqlcmd-use-the-utility.md)
  
## <a name="syntax"></a>구문

```cmd
sqlcmd
   -a packet_size
   -A (dedicated administrator connection)
   -b (terminate batch job if there is an error)
   -c batch_terminator
   -C (trust the server certificate)
   -d db_name
   -D
   -e (echo input)
   -E (use trusted connection)
   -f codepage | i:codepage[,o:codepage] | o:codepage[,i:codepage]
   -g (enable column encryption)
   -G (use Azure Active Directory for authentication)
   -h rows_per_header
   -H workstation_name
   -i input_file
   -I (enable quoted identifiers)
   -j (Print raw error messages)
   -k[1 | 2] (remove or replace control characters)  
   -K application_intent  
   -l login_timeout  
   -L[c] (list servers, optional clean output)  
   -m error_level  
   -M multisubnet_failover  
   -N (encrypt connection)  
   -o output_file  
   -p[1] (print statistics, optional colon format)  
   -P password  
   -q "cmdline query"  
   -Q "cmdline query" (and exit)  
   -r[0 | 1] (msgs to stderr)  
   -R (use client regional settings)  
   -s col_separator  
   -S [protocol:]server[instance_name][,port]  
   -t query_timeout  
   -u (unicode output file)  
   -U login_id  
   -v var = "value"
   -V error_severity_level
   -w column_width
   -W (remove trailing spaces)
   -x (disable variable substitution)
   -X[1] (disable commands, startup script, environment variables, optional exit)
   -y variable_length_type_display_width
   -Y fixed_length_type_display_width
   -z new_password
   -Z new_password (and exit)
   -? (usage)
```
  
## <a name="command-line-options"></a>명령줄 옵션

**로그인 관련 옵션**

**-A**  
DAC(관리자 전용 연결)를 사용하여 SQL Server에 로그인합니다. 이 연결 유형은 서버 문제를 해결하는 데 사용됩니다. 이 연결은 DAC를 지원하는 서버 컴퓨터에서만 작동합니다. DAC를 사용할 수 없는 경우 **sqlcmd** 는 오류 메시지를 생성하고 종료됩니다. DAC에 대한 자세한 내용은 [데이터베이스 관리자를 위한 진단 연결](../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)을 참조하세요. -A 옵션은 -G 옵션과 함께 지원되지 않습니다. -A를 사용하여 SQL Database에 연결하는 경우 SQL Server 관리자여야 합니다. Azure Active Directory 관리자는 DAC를 사용할 수 없습니다.

**-C**  
이 스위치는 클라이언트에서 유효성 검사 없이 암시적으로 서버 인증서를 신뢰하는 데 사용됩니다. 이 옵션은 ADO.NET 옵션 `TRUSTSERVERCERTIFICATE = true`와 동일합니다.  

**-d** _db_name_  
**sqlcmd** 를 시작할 때 `USE` *db_name* 문을 실행합니다. 이 옵션은 **sqlcmd** 스크립팅 변수 SQLCMDDBNAME을 설정합니다. 이 매개 변수는 초기 데이터베이스를 지정합니다. 기본값은 사용자 로그인의 기본 데이터베이스 속성입니다. 데이터베이스가 없을 경우 오류 메시지가 생성되고 **sqlcmd** 가 종료됩니다.  

**-D**  
-S에 제공된 서버 이름을 호스트 이름이 아닌 DSN으로 해석합니다. 자세한 내용은 [sqlcmd를 사용하여 연결](../connect/odbc/linux-mac/connecting-with-sqlcmd.md)에서 _sqlcmd 및 bcp에서 DSN 지원_ 을 참조하세요.

> [!NOTE]
> -D 옵션은 Linux 및 MacOS 클라이언트에서만 사용할 수 있습니다. Windows 클라이언트에서 이전에 now-obsolete 옵션으로 불렸던 이 옵션은 이제 제거되었으며 무시됩니다.

**-l** _login_timeout_  
서버에 연결을 시도할 때 ODBC 드라이버에 대한 **sqlcmd** 로그인 시간 제한(초)을 지정합니다. 이 옵션은 **sqlcmd** 스크립팅 변수 SQLCMDLOGINTIMEOUT을 설정합니다. 기본 **sqlcmd** 로그인 제한 시간은 8초입니다. **-G** 옵션을 사용하여 SQL Database 또는 Azure Synapse Analytics에 연결하고 Azure Active Directory를 통해 인증하는 경우 최소 30초의 시간 제한 값이 권장됩니다. 로그인 제한 시간은 0에서 65534 사이의 숫자여야 합니다. 입력한 값이 숫자가 아니거나 이 범위에 속하지 않을 경우 **sqlcmd** 는 오류 메시지를 생성합니다. 값을 0으로 설정하면 제한 시간이 없습니다.

**-E**  
사용자 이름과 암호를 사용하는 대신 트러스트된 연결을 사용하여 SQL Server에 로그인합니다. **-E** 를 지정하지 않으면 **sqlcmd** 는 기본적으로 트러스트된 연결 옵션을 사용합니다.  

**-E** 옵션은 SQLCMDPASSWORD 등의 가능한 사용자 이름 및 암호 환경 변수 설정을 무시합니다. **-E** 옵션과 함께 **-U** 옵션 또는 **-P** 옵션을 사용하면 오류 메시지가 생성됩니다.  

**-g**  
열 암호화 설정을 `Enabled`로 설정합니다. 자세한 내용은 [Always Encrypted](../relational-databases/security/encryption/always-encrypted-database-engine.md)를 참조하세요. Windows 인증서 저장소에 저장된 마스터 키만 지원됩니다. -g 스위치를 사용하려면 적어도 **sqlcmd** 버전 [13.1](https://go.microsoft.com/fwlink/?LinkID=825643)이 필요합니다. 사용 중인 버전을 확인하려면 `sqlcmd -?`를 실행하세요.

**-G**  
이 스위치는 SQL Database 또는 Azure Synapse Analytics에 연결할 때 클라이언트에서 Azure Active Directory 인증을 통해 사용자가 인증되도록 지정하는 데 사용됩니다. 이 옵션은 **sqlcmd** 스크립팅 변수 SQLCMDUSEAAD = true를 설정합니다. -G 스위치를 사용하려면 적어도 **sqlcmd** 버전 [13.1](https://go.microsoft.com/fwlink/?LinkID=825643)이 필요합니다. 사용 중인 버전을 확인하려면 `sqlcmd -?`를 실행하세요. 자세한 내용은 [Azure Active Directory 인증을 사용하여 SQL Database 또는 Azure Synapse Analytics에 연결](/azure/azure-sql/database/authentication-aad-overview)을 참조하세요. -A 옵션은-G 옵션과 함께 지원되지 않습니다.

> [!IMPORTANT]
> `-G` 옵션은 Azure SQL Database 및 Azure Data Warehouse에만 적용됩니다.
> AAD 대화형 인증은 현재 Linux 또는 macOS에서 지원되지 않습니다. AAD 통합 인증을 사용하려면 [Microsoft ODBC Driver 17 for SQL Server](https://aka.ms/downloadmsodbcsql) 버전 17.6.1 이상과 올바르게 구성된 Kerberos 환경이 필요합니다.

- **Azure Active Directory 사용자 이름 및 암호:** 

    Azure Active Directory의 사용자 이름과 암호를 사용하려는 경우 **-G** 옵션을 제공하고 **-U** 및 **-P** 옵션도 제공하여 사용자 이름 및 암호를 사용할 수 있습니다.

    ```cmd
    Sqlcmd -S testsrv.database.windows.net -d Target_DB_or_DW -U bob@contoso.com -P MyAADPassword -G
    ```

    -G 매개 변수는 백 엔드에서 다음 연결 문자열을 생성합니다. 

    ```cmd
     SERVER = Target_DB_or_DW.testsrv.database.windows.net;UID= bob@contoso.com;PWD=MyAADPassword;AUTHENTICATION = ActiveDirectoryPassword 
    ```

- **Azure Active Directory 통합**

   Azure Active Directory 통합 인증을 위해 사용자 이름이나 암호 없이 **-G** 옵션을 제공합니다.
   *AAD 통합 인증은 현재 Linux 또는 macOS에서 지원되지 않습니다*.

    ```cmd
    Sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -G
    ```

    그러면 백 엔드에서 다음 연결 문자열이 생성됩니다. 

    ```cmd
    SERVER = Target_DB_or_DW.testsrv.database.windows.net Authentication = ActiveDirectoryIntegrated; Trusted_Connection=NO
    ```

    > [!NOTE]
    > `-E` 옵션(Trusted_Connection)은 `-G` 옵션과 함께 사용할 수 없습니다.

- **Azure Active Directory 대화형**

    Azure SQL Database 및 Azure Synapse Analytics에 대한 Azure AD 대화형 인증을 통해 사용자는 다단계 인증을 지원하는 대화형 방법을 사용할 수 있습니다. 자세한 내용은 [Active Directory 대화형 인증](../ssdt/azure-active-directory.md#active-directory-interactive-authentication)을 참조하세요. 

   Azure AD 대화형에는 **sqlcmd** [버전 15.0.1000.34](#download-the-latest-version-of-sqlcmd-utility) 이상과 [ODBC 버전 17.2 이상](https://aka.ms/downloadmsodbcsql)이 필요합니다.  

   대화형 인증을 사용 설정하려면 암호 없이 사용자 이름(-U)으로만 -G 옵션을 제공해야 합니다.

   다음 예제에서는 사용자가 AAD 계정에 해당할 경우 Azure AD 대화형 모드(사용자 이름 표시)를 사용하여 데이터를 내보냅니다. 이는 이전 섹션 *Azure Active Directory 사용자 이름 및 암호* 에 사용된 예제와 동일합니다.  

   대화형 모드에서는 암호를 수동으로 입력해야 하며, 다단계 인증이 사용 설정된 계정의 경우에는 구성된 MFA 인증 메서드를 완료해야 합니다.

   ```cmd
   sqlcmd -S testsrv.database.windows.net -d Target_DB_or_DW -G -U alice@aadtest.onmicrosoft.com
   ```

   이전 명령은 백 엔드에서 다음 연결 문자열을 생성합니다.  

   ```cmd
   SERVER = Target_DB_or_DW.testsrv.database.windows.net;UID=alice@aadtest.onmicrosoft.com; AUTHENTICATION = ActiveDirectoryInteractive   
   ```

   Azure AD 사용자가 Windows 계정을 사용하는 도메인 페더레이션된 사용자인 경우에는 명령줄에 필요한 사용자 이름에 도메인 계정이 포함됩니다(예: joe@contoso.com인 경우 아래 참조).

   ```cmd
   sqlcmd -S testsrv.database.windows.net -d Target_DB_or_DW -G -U joe@contoso.com  
   ```

   특정 Azure AD에 있는 게스트 사용자가 sqlcmd 명령을 실행할 데이터베이스 권한이 있는 SQL Database 내의 그룹에 포함되는 경우, 이들의 게스트 사용자 별칭이 사용됩니다(예: *keith0@adventureworks.com* ).

  >[!IMPORTANT]
  >SQLCMD를 사용하여 `-G` 및 `-U` 옵션을 사용하는 경우 알려진 문제가 있습니다. `-G` 옵션 앞에 `-U` 옵션을 배치하면 인증이 실패할 수 있습니다. 항상 `-G` 옵션부터 시작하고 그 다음에 `-U` 옵션을 사용합니다.

**-H** _workstation_name_  
 워크스테이션 이름입니다. 이 옵션은 **sqlcmd** 스크립팅 변수 SQLCMDWORKSTATION을 설정합니다. 워크스테이션 이름은 **sys.sysprocesses** 카탈로그 뷰의 **hostname** 열에 나열되거나 **sp_who** 저장 프로시저를 사용하여 반환할 수 있습니다. 이 옵션을 지정하지 않으면 기본적으로 현재 컴퓨터 이름이 사용됩니다. 이 이름을 사용하여 

**sqlcmd** 세션을 식별할 수 있습니다.  

**-j** 화면에 원시 오류 메시지를 출력합니다.
  
 **-K** _application_intent_  
 서버에 연결할 때 애플리케이션 작업 유형을 선언합니다. 현재 **ReadOnly** 값만 지원됩니다. **-K** 를 지정하지 않으면 sqlcmd 유틸리티가 Always On 가용성 그룹에 있는 보조 복제본에 연결할 수 없습니다. 자세한 내용은 [활성 보조 복제본: 읽기 가능한 보조 복제본(Always On 가용성 그룹)](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)을 참조하세요.  
  
**-M** _multisubnet_failover_  
 SQL Server 가용성 그룹 또는 SQL Server 장애 조치(failover) 클러스터 인스턴스의 가용성 그룹 수신기에 연결할 때는 항상 **-M** 을 지정합니다. **-M** 은 현재 활성 상태인 서버를 빠르게 검색하여 연결할 수 있도록 제공합니다. **–M** 이 지정되지 않으면 **-M** 이 해제되어 있습니다. [수신기, 클라이언트 연결 및 애플리케이션 장애 조치(Failover)](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)에 대한 자세한 내용은 [가용성 그룹의 생성 및 구성 &#40;SQL Server&#41;](../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md), [장애 조치(Failover) 클러스터링 및 Always On 가용성 그룹(SQL Server)](../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md) 및 [활성 보조 복제본: 읽기 가능한 보조 복제본(Always On 가용성 그룹)](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)을 참조하세요.
  
 **-N**  
 이 스위치는 클라이언트에서 암호화된 연결을 요청하는 데 사용됩니다.  
  
 **-P** _password_  
 사용자가 지정하는 암호입니다. 암호는 대소문자를 구분합니다. -U 옵션을 사용하고 **-P** 옵션을 사용하지 않으며 SQLCMDPASSWORD 환경 변수를 설정하지 않을 경우 **sqlcmd** 는 암호를 묻는 메시지를 표시합니다. Null 암호를 사용하지 않는 것이 좋지만, 매개 변수 값에 연속된 큰따옴표 쌍을 사용하여 null 암호를 지정할 수 있습니다.

- **-P ""**

강력한 암호를 사용하는 것이 좋습니다.

#### <a name="use-a-strong-password"></a>[**강력한 암호를 사용하세요.**](../relational-databases/security/strong-passwords.md)

 암호 프롬프트는 다음과 같이 콘솔에 출력되어 표시됩니다. `Password:`  
  
 사용자 입력은 숨겨지므로 아무 것도 표시되지 않고 커서가 해당 위치에 그대로 남아 있습니다.  
  
 SQLCMDPASSWORD 환경 변수를 사용하면 현재 세션에 대한 기본 암호를 설정할 수 있습니다. 그러므로 암호를 배치 파일로 하드 코딩할 필요가 없습니다.  
  
 다음 예에서는 먼저 명령 프롬프트에서 SQLCMDPASSWORD 변수를 설정하고 **sqlcmd** 유틸리티에 액세스합니다. 명령 프롬프트에 다음을 입력합니다.  
  
 `SET SQLCMDPASSWORD= p@a$$w0rd`  
 명령 프롬프트에서 다음을 입력합니다.  
  
 `sqlcmd`  
  
 사용자 이름 및 암호 조합이 잘못된 경우 오류 메시지가 생성됩니다.  
  
**참고!**  OSQLPASSWORD 환경 변수는 이전 버전과의 호환성을 위해 유지되었습니다. SQLCMDPASSWORD 환경 변수는 OSQLPASSWORD 환경 변수보다 우선적으로 적용됩니다. 이제 OSQLPASSWORD가 더 이상 공유되지 않으므로 **sqlcmd** 와 **osql** 을 간섭 없이 나란히 사용할 수 있습니다. 이전 스크립트는 계속 작동합니다.  
  
 **-P** 옵션과 함께 **-E** 옵션을 사용하면 오류 메시지가 생성됩니다.  
  
 **-P** 옵션 다음에 둘 이상의 인수를 지정하면 오류 메시지가 생성되고 프로그램이 종료됩니다.  
  
 **-S** [*protocol*:]*server*[ **\\** _instance\_name_][ **,** _port_]  
 연결할 SQL Server 인스턴스를 지정합니다. **sqlcmd** 스크립팅 변수 SQLCMDSERVER를 설정합니다.  
  
 해당 서버 컴퓨터에 있는 기본 SQL Server 인스턴스에 연결하려면 *server_name* 을 지정합니다. 해당 서버 컴퓨터에 있는 명명된 SQL Server 인스턴스에 연결하려면 *server_name* [ **\\** _instance\_name_ ]을 지정합니다. 서버 컴퓨터를 지정하지 않으면 **sqlcmd** 가 로컬 컴퓨터에 있는 기본 SQL Server 인스턴스에 연결됩니다. 네트워크의 원격 컴퓨터에서 **sqlcmd** 를 실행할 경우에는 이 옵션을 지정해야 합니다.  
  
 *protocol* 은 **tcp** (TCP/IP), **lpc** (공유 메모리) 또는 **np** (명명된 파이프)일 수 있습니다.  
  
 **sqlcmd** 를 시작할 때 *server_name* [ **\\** _instance\_name_ ]을 지정하지 않으면 SQL Server에서 SQLCMDSERVER 환경 변수를 확인하고 사용합니다.  
  
> [!NOTE]  
>  OSQLSERVER 환경 변수는 이전 버전과의 호환성을 위해 유지되었습니다. SQLCMDSERVER 환경 변수는 OSQLSERVER 환경 변수보다 우선 적용됩니다. 따라서 **sqlcmd** 와 **osql** 을 문제 없이 함께 사용할 수 있으며 이전 스크립트를 계속 사용할 수 있습니다.  
  
 **-U** _login_id_  
 로그인 이름 또는 포함된 데이터베이스 사용자 이름입니다. 포함된 데이터베이스 사용자의 경우 데이터베이스 이름 옵션(-d)을 제공해야 합니다.  
  
> [!NOTE]  
>  OSQLUSER 환경 변수는 이전 버전과의 호환성을 위해 제공됩니다. SQLCMDUSER 환경 변수는 OSQLUSER 환경 변수보다 우선적으로 적용됩니다. 따라서 **sqlcmd** 와 **osql** 을 문제 없이 함께 사용할 수 있으며 이전 **osql** 스크립트도 계속 사용할 수 있습니다.  
  
 **-U** 옵션과 **-P** 옵션을 모두 지정하지 않으면 **sqlcmd** 는 Microsoft Windows 인증 모드를 사용하여 연결을 시도합니다. **sqlcmd** 를 실행하는 사용자의 Windows 계정을 기반으로 인증이 수행됩니다.  
  
 이 항목의 뒷부분에 설명되어 있는 **-E** 옵션과 함께 **-U** 옵션을 사용하면 오류 메시지가 생성됩니다. **–U** 옵션 다음에 둘 이상의 인수를 지정하면 오류 메시지가 생성되고 프로그램이 종료됩니다.  
  
 **-z** _new_password_  
 암호를 변경합니다.  
  
 `sqlcmd -U someuser -P s0mep@ssword -z a_new_p@a$$w0rd`  
  
 **-Z** _new_password_  
 암호 변경 후 종료합니다.  
  
 `sqlcmd -U someuser -P s0mep@ssword -Z a_new_p@a$$w0rd`  
  
 **입/출력 옵션**  
  **-f** _codepage_ | **i:** _codepage_[ **,o:** _codepage_] | **o:** _codepage_[ **,i:** _codepage_]  
 입력 및 출력 코드 페이지를 지정합니다. 코드 페이지 번호는 설치된 Windows 코드 페이지를 지정하는 숫자 값입니다.  
  
 코드 페이지 변환 규칙은 다음과 같습니다.  
  
- 변환이 필요 없는 유니코드 파일이 입력 파일로 사용된 경우가 아니라면 **sqlcmd** 는 지정된 코드 페이지가 없는 경우 입력 파일과 출력 파일에 현재 코드 페이지를 사용합니다.  
  
- **sqlcmd** 는 Big-Endian 및 Little-Endian 유니코드 입력 파일을 모두 자동으로 인식합니다. **-u** 옵션이 지정된 경우 출력은 항상 Little-Endian 유니코드가 됩니다.  
  
- 지정된 출력 파일이 없는 경우 출력 코드 페이지는 콘솔 코드 페이지가 됩니다. 이 방식을 사용하면 출력이 콘솔에 올바르게 표시됩니다.  
  
- 여러 입력 파일이 있는 경우 동일한 코드 페이지를 사용하는 것으로 간주됩니다. 유니코드 및 비유니코드 입력 파일을 함께 사용할 수 있습니다.  
  
 명령 프롬프트에서 **chcp** 를 입력하여 Cmd.exe의 코드 페이지를 확인합니다.  
  
 **-i** _input_file_[ **,** _input\_file2_...]  
 SQL 문 또는 저장 프로시저의 일괄 처리가 포함된 파일을 나타냅니다. 순서대로 읽고 처리할 파일을 여러 개 지정할 수 있습니다. 파일 이름 사이에 공백을 넣지 마십시오. 먼저 **sqlcmd** 는 지정한 모든 파일이 있는지 확인합니다. 하나 이상의 파일이 없을 경우 **sqlcmd** 가 종료됩니다. -i 옵션과 -Q/-q 옵션은 함께 사용할 수 없습니다.  
  
 경로 예는 다음과 같습니다.  

```cmd
-i C:\<filename>  
-i \\<Server>\<Share$>\<filename>  
-i "C:\Some Folder\<file name>"  
```
  
 공백이 포함된 파일 경로는 따옴표로 묶어야 합니다.  
  
 이 옵션은 다음과 같이 두 번 이상 사용할 수 있습니다. **-i**_input\_file_ **-I**_I input_file._  
  
 **-o** _output_file_  
 **sqlcmd** 에서 출력을 받는 파일을 식별합니다.  
  
 **-u** 를 지정하면 *output_file* 이 유니코드 형식으로 저장됩니다. 파일 이름이 잘못된 경우 오류 메시지가 생성되고 **sqlcmd** 가 종료됩니다. **sqlcmd** 는 여러 **sqlcmd** 프로세스를 같은 파일에 동시에 쓸 수 없습니다. 이 경우 파일 출력이 손상되거나 제대로 수행되지 않습니다. **-f** 스위치는 파일 형식과도 관련이 있습니다. 이 파일은 존재하지 않는 경우 만들어집니다. 이전 **sqlcmd** 세션에서와 이름이 같은 파일은 덮어쓰여집니다. 여기에 지정된 파일은 **stdout** 파일이 아닙니다. **stdout** 파일이 지정된 경우에는 이 파일이 사용되지 않습니다.  
  
 경로 예는 다음과 같습니다.  

```cmd
-o C:< filename>  
-o \\<Server>\<Share$>\<filename>  
-o "C:\Some Folder\<file name>"  
 ```
 공백이 포함된 파일 경로는 따옴표로 묶어야 합니다.  
  
 **-r**[**0** | **1**]  
 오류 메시지 출력을 화면으로 리디렉션합니다(**stderr**). 매개 변수를 지정하지 않거나 **0** 을 지정하면 심각도가 11 이상인 오류 메시지만 리디렉션됩니다. **1** 을 지정하면 PRINT를 포함하는 모든 오류 메시지 출력이 리디렉션됩니다. -o를 사용할 경우 아무 효과도 없습니다. 기본적으로 메시지는 **stdout** 으로 전송됩니다.  
  
 **-R**  
 클라이언트의 로캘을 기반으로 SQL Server에서 검색된 숫자, 통화, 날짜 및 시간 열을 **sqlcmd** 에서 지역화합니다. 기본적으로 이러한 열은 서버의 국가별 설정을 사용하여 표시됩니다.  
  
 **-u**  
 *input_file* 형식에 관계없이 *output_file* 이 유니코드 형식으로 저장되도록 지정합니다.  
  
 **쿼리 실행 옵션**  
  **-e**  
 표준 출력 디바이스에 입력 스크립트를 기록합니다(**stdout**).  
  
 **-I**  
 SET QUOTED_IDENTIFIER 연결 옵션을 ON으로 설정합니다. 기본적으로 OFF로 설정되어 있습니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](~/t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.  
  
 **-q "** _cmdline query_ **"**  
 **sqlcmd** 가 시작될 때 쿼리를 실행하지만 쿼리 실행이 완료되더라도 **sqlcmd** 가 종료되지는 않습니다. 세미콜론으로 구분된 여러 쿼리를 실행할 수 있습니다. 다음 예와 같이 쿼리를 따옴표로 묶습니다.  
  
 명령 프롬프트에 다음을 입력합니다.  
  
 `sqlcmd -d AdventureWorks2012 -q "SELECT FirstName, LastName FROM Person.Person WHERE LastName LIKE 'Whi%';"`  
  
 `sqlcmd -d AdventureWorks2012 -q "SELECT TOP 5 FirstName FROM Person.Person;SELECT TOP 5 LastName FROM Person.Person;"`  
  
> [!IMPORTANT]  
>  쿼리에 GO 종결자를 사용하지 마십시오.  
  
 이 옵션과 함께 **-b** 를 지정하면 오류가 발생하여 **sqlcmd** 가 종료됩니다. **-b** 에 대해서는 이 문서의 뒷부분에서 설명합니다.  
  
 **-Q "** _cmdline query_ **"**  
 **sqlcmd** 가 시작될 때 쿼리를 실행한 다음 바로 **sqlcmd** 를 종료합니다. 세미콜론으로 구분된 여러 쿼리를 실행할 수 있습니다.  
  
 다음 예와 같이 쿼리를 따옴표로 묶습니다.  
  
 명령 프롬프트에 다음을 입력합니다.  
  
 `sqlcmd -d AdventureWorks2012 -Q "SELECT FirstName, LastName FROM Person.Person WHERE LastName LIKE 'Whi%';"`  
  
 `sqlcmd -d AdventureWorks2012 -Q "SELECT TOP 5 FirstName FROM Person.Person;SELECT TOP 5 LastName FROM Person.Person;"`  
  
> [!IMPORTANT]  
>  쿼리에 GO 종결자를 사용하지 마십시오.  
  
 이 옵션과 함께 **-b** 를 지정하면 오류가 발생하여 **sqlcmd** 가 종료됩니다. **-b** 에 대해서는 이 문서의 뒷부분에서 설명합니다.  
  
 **-t** _query_timeout_  
 명령 또는 SQL 문 제한 시간(초)을 지정합니다. 이 옵션은 **sqlcmd** 스크립팅 변수 SQLCMDSTATTIMEOUT을 설정합니다. *time_out* 값을 지정하지 않으면 명령이 무기한 실행됩니다. *query**time_out* 은 1에서 65534 사이의 숫자여야 합니다. 입력한 값이 숫자가 아니거나 이 범위에 속하지 않을 경우 **sqlcmd** 는 오류 메시지를 생성합니다.  
  
> [!NOTE]  
>  실제 제한 시간 값은 지정한 *time_out* 값과 몇 초 정도 차이가 날 수 있습니다.  
  
 **-vvar =**  _value_[ **var =** _value_...]  
 **sqlcmd** 스크립트에서 사용할 수 있는 **sqlcmd** 스크립팅 변수를 만듭니다. 공백이 포함된 값은 따옴표로 묶습니다. 여러 _**var**_= **"** _values_ **"** 값을 지정할 수 있습니다. 지정한 값에 오류가 있을 경우 **sqlcmd** 는 오류 메시지를 생성하고 종료됩니다.  
  
 `sqlcmd -v MyVar1=something MyVar2="some thing"`  
  
 `sqlcmd -v MyVar1=something -v MyVar2="some thing"`  
  
 **-x**  
 **sqlcmd** 에서 스크립팅 변수를 무시하도록 합니다. 이 매개 변수는 $(*variable_name*) 등의 일반 변수와 형식이 같은 문자열이 포함되어 있을 수 있는 INSERT 문이 스크립트에 많이 포함된 경우에 유용합니다.  
  
 **형식 지정 옵션**  
  **-h** _headers_  
 열 머리글 사이에 출력할 행의 수를 지정합니다. 기본적으로 각 쿼리 결과 집합마다 머리글을 한 번 출력합니다. 이 옵션은 **sqlcmd** 스크립팅 변수 SQLCMDHEADERS를 설정합니다. 머리글을 출력하지 않으려면 **-1** 을 사용합니다. 잘못된 값을 지정할 경우 **sqlcmd** 는 오류 메시지를 생성하고 종료됩니다.  
  
 **-k** [**1** | **2**]  
 출력에서 탭이나 줄 바꿈 문자와 같은 모든 제어 문자를 제거합니다. 이 매개 변수는 데이터를 반환할 때 열 서식은 유지됩니다. 1을 지정하면 제어 문자가 단일 공백으로 바뀝니다. 2를 지정하면 연속된 제어 문자가 단일 공백으로 바뀝니다. **-k** 는 **-k1** 과 같습니다.  
  
 **-s** _col_separator_  
 열 구분 기호 문자를 지정합니다. 기본값은 공백입니다. 이 옵션은 **sqlcmd** 스크립팅 변수 SQLCMDCOLSEP를 설정합니다. 앰퍼샌드(&)나 세미콜론(;)과 같이 운영 체제에서 특별한 의미를 갖는 문자를 사용하려면 해당 문자를 따옴표(")로 묶습니다. 열 구분 기호로 임의의 8비트 문자를 사용할 수 있습니다.  
  
 **-w** _column_width_  
 출력할 화면 너비를 지정합니다. 이 옵션은 **sqlcmd** 스크립팅 변수 SQLCMDCOLWIDTH를 설정합니다. 열 너비는 8보다 크고 65536보다 작은 숫자여야 합니다. 지정한 열 너비가 이 범위에 속하지 않을 경우 **sqlcmd** 는 오류 메시지를 생성합니다. 기본 너비는 80자입니다. 출력 줄이 지정한 열 너비를 초과하면 다음 줄로 넘어갑니다.  
  
 **-W**  
 이 옵션은 열에서 후행 공백을 제거합니다. 다른 애플리케이션으로 내보낼 데이터를 준비하는 경우 **-s** 옵션과 함께 이 옵션을 사용합니다. **-y** 또는 **-Y** 옵션과 함께 사용할 수 없습니다.  
  
 **-y** _variable_length_type_display_width_  
 **sqlcmd** 스크립팅 변수 `SQLCMDMAXVARTYPEWIDTH`를 설정합니다. 기본값은 256입니다. 다음과 같은 큰 가변 길이 데이터 형식에 대해 반환되는 문자 수를 제한합니다.  
  
- **varchar(max)**  
  
- **nvarchar(max)**  
  
- **varbinary(max)**  
  
- **xml**  
  
- **UDT(사용자 정의 데이터 형식)**  
  
- **text**  
  
- **ntext**  
  
- **image**  
  
> [!NOTE]  
>  UDT는 구현에 따라 길이가 고정될 수 있습니다. 길이가 고정된 UDT의 길이가 *display_width* 보다 짧으면 반환되는 UDT 값은 영향을 받지 않습니다. 그러나 길이가 *display_width* 보다 길면 출력이 잘립니다.  
   
  
> [!IMPORTANT]  
>  **-y 0** 옵션은 반환되는 데이터 크기에 따라 서버와 네트워크 모두에서 심각한 성능 문제를 일으킬 수 있으므로 사용 시 매우 주의해야 합니다.  
  
 **-Y** _fixed_length_type_display_width_  
 **sqlcmd** 스크립팅 변수 `SQLCMDMAXFIXEDTYPEWIDTH`를 설정합니다. 기본값은 0(무제한)입니다. 다음 데이터 형식에 대해 반환되는 문자 수를 제한합니다.  
  
- **char(** _n_ **)** , 여기서 n의 범위는 1<=n<=8000  
  
- **nchar(n** _n_ **)** , 여기서 n의 범위는 1<=n<=4000  
  
- **varchar(n** _n_ **)** , 여기서 n의 범위는 1<=n<=8000  
  
- **nvarchar(n** _n_ **)** , 여기서 n의 범위는 1<=n<=4000  
  
- **varbinary(n** _n_ **)** , 여기서 n의 범위는 1<=n\<=4000  
  
- **variant**  
  
 **오류 보고 옵션**  
  **-b**  
 오류가 발생하면 **sqlcmd** 가 종료되고 DOS ERRORLEVEL 값을 반환하도록 지정합니다. SQL Server 오류 메시지의 심각도가 10보다 큰 경우 DOS ERRORLEVEL 변수로 **1** 이 반환되며 그렇지 않은 경우 **0** 이 반환됩니다. **-b** 외에도 **-V** 옵션을 설정한 경우 심각도가 **-V** 를 사용하여 설정한 값보다 작으면 **sqlcmd** 에서 오류를 보고하지 않습니다. 명령 프롬프트 배치 파일은 ERRORLEVEL 값을 테스트하고 그에 따라 적절히 오류를 처리할 수 있습니다. **sqlcmd** 는 심각도가 10(정보 메시지)인 오류는 보고하지 않습니다.  
  
 **sqlcmd** 스크립트에 잘못된 설명 또는 구문 오류가 포함되었거나 스크립팅 변수가 없을 경우 반환되는 ERRORLEVEL은 1입니다.  
  
 **-m** _error_level_  
 **stdout** 에 보낼 오류 메시지를 제어합니다. 심각도가 이 수준보다 크거나 같은 메시지는 보내집니다. 이 값을 **1** 로 설정하면 정보 메시지를 포함한 모든 메시지가 보내집니다. **-m** 과 **-1** 사이에는 공백이 있으면 안 됩니다. 예를 들어 **-m-1** 은 유효하고 **-m-1** 은 유효하지 않습니다.  
  
 이 옵션은 **sqlcmd** 스크립팅 변수 SQLCMDERRORLEVEL도 설정합니다. 이 변수의 기본값은 0입니다.  
  
 **-V** _error_severity_level_  
 ERRORLEVEL 변수를 설정하는 데 사용되는 심각도를 제어합니다. 심각도가 이 값보다 크거나 같은 오류 메시지는 ERRORLEVEL을 설정합니다. 0보다 작은 값은 0으로 보고됩니다. 배치 파일 및 CMD 파일은 ERRORLEVEL 변수의 값을 테스트하는 데 사용할 수 있습니다.  
  
 **기타 옵션**  
  **-a** _packet_size_  
 다른 크기의 패킷을 요청합니다. 이 옵션은 **sqlcmd** 스크립팅 변수 SQLCMDPACKETSIZE를 설정합니다. *packet_size* 는 512에서 32767 사이의 값이어야 합니다. 기본값은 4096입니다. GO 명령 사이에 SQL 문 수가 많은 스크립트를 실행할 때는 패킷 크기가 클수록 성능이 더 향상됩니다. 더 큰 패킷 크기를 요청할 수 있습니다. 그러나 요청이 거부되면 **sqlcmd** 는 서버 기본값을 패킷 크기로 사용합니다.  
  
 **-c** _batch_terminator_  
 일괄 처리 종결자를 지정합니다. 기본적으로 줄에 "GO"만 단독으로 입력하면 명령이 종료되어 SQL Server로 보내집니다. 일괄 처리 종결자를 다시 설정할 때는 앞에 백슬래시가 있더라도 Transact-SQL 예약 키워드 또는 운영 체제와 연관된 특별한 의미를 가진 문자를 사용하지 마십시오.  
  
 **-L**[**c**]  
 로컬로 구성된 서버 컴퓨터와 네트워크상에서 브로드캐스팅하는 서버 컴퓨터의 이름을 표시합니다. 이 매개 변수는 다른 매개 변수와 함께 사용할 수 없습니다. 표시할 수 있는 최대 서버 컴퓨터 수는 3000대입니다. 버퍼 크기 때문에 서버 목록이 잘린 경우 경고 메시지가 표시됩니다.  
  
> [!NOTE]  
>  네트워크에서 브로드캐스팅의 특성으로 인해 **sqlcmd** 는 모든 서버로부터 시기 적절한 응답을 받지 못할 수 있습니다. 그러므로 반환되는 서버 목록은 이 옵션을 호출할 때마다 다를 수 있습니다.  
  
 옵션 매개 변수 **c** 를 지정하면 **Servers:** 머리글 없이 출력이 나타납니다. 그리고 각 서버 줄이 선행 공백 없이 나열됩니다. 이 프레젠테이션을 정리된 출력이라고 합니다. 정리된 출력은 스크립트 언어의 처리 성능을 향상시킵니다.  
  
 **-p**[**1**]  
 모든 결과 집합에 대한 성능 통계를 출력합니다. 다음 표시는 성능 통계 형식의 예입니다.  
  
 `Network packet size (bytes): n`  
  
 `x xact[s]:`  
  
 `Clock Time (ms.): total       t1  avg       t2 (t3 xacts per sec.)`  
  
 위치:  
  
 `x` = SQL Server에서 처리되는 트랜잭션 수  
  
 `t1` = 모든 트랜잭션의 총 시간  
  
 `t2` = 단일 트랜잭션의 평균 시간  
  
 `t3` = 초당 평균 트랜잭션 수  
  
 모든 시간은 밀리초 단위입니다.  
  
 선택적 매개 변수 **1** 을 지정할 경우 통계의 출력 형식은 콜론으로 구분된 형식입니다. 이 형식은 스프레드시트로 쉽게 가져오거나 스크립트를 통해 처리할 수 있습니다.  
  
 이 선택적 매개 변수의 값이 **1** 이 아닌 경우 오류가 생성되고 **sqlcmd** 가 종료됩니다.  
  
 **-X**[**1**]  
 배치 파일에서 **sqlcmd** 를 실행할 때 시스템 보안을 손상시킬 수 있는 명령을 사용할 수 없게 설정합니다. 사용할 수 없게 설정된 명령은 여전히 인식되지만 **sqlcmd** 는 경고 메시지를 표시하고 계속 실행됩니다. 선택적 매개 변수 **1** 을 지정하면 **sqlcmd** 는 오류 메시지를 생성하고 종료됩니다. **-X** 옵션을 사용하면 다음 명령이 사용할 수 없게 설정됩니다.  
  
- **ED**  
  
- **!!** _command_  
  
 **-X** 옵션을 지정하면 환경 변수가 **sqlcmd** 에 전달되지 않습니다. 또한 SQLCMDINI 스크립팅 변수를 사용하여 지정한 시작 스크립트가 실행되지 않습니다. **sqlcmd** 스크립팅 변수에 대한 자세한 내용은 [스크립팅 변수와 함께 sqlcmd 사용](~/relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)을 참조하세요.  
  
 **-?**  
 **sqlcmd** 버전과 **sqlcmd** 옵션의 구문 요약 정보를 표시합니다.  
  
## <a name="remarks"></a>설명

옵션은 구문 섹션에 표시된 순서대로 사용하지 않아도 됩니다.

여러 결과가 반환된 경우 **sqlcmd** 는 일괄 처리의 각 결과 집합 사이에 빈 줄을 출력합니다. 또한, 실행되는 문에 적용되지 않을 때는 `<x> rows affected` 메시지가 나타나지 않습니다.

대화형으로 **sqlcmd** 를 사용하려면 명령 프롬프트에 이 문서의 위에서 설명한 하나 이상의 옵션과 함께 **sqlcmd** 를 입력합니다. 자세한 내용은 [sqlcmd 유틸리티 사용](~/relational-databases/scripting/sqlcmd-use-the-utility.md)을 참조하세요.

> [!NOTE]  
>  **-L**, **-Q**, **-Z** 또는 **-i** 옵션으로 인해 **sqlcmd** 는 실행 후 종료됩니다.
  
 명령 환경(Cmd.exe)에서 모든 인수 및 확장 변수를 포함한 **sqlcmd** 명령줄의 총 길이는 운영 체제에서 Cmd.exe에 대해 지정한 길이입니다.
  
## <a name="variable-precedence-low-to-high"></a>변수 우선 순위(낮은 순위에서 높은 순위)
  
1.  시스템 수준 환경 변수
  
2.  사용자 수준 환경 변수  
  
3.  **sqlcmd** 를 실행하기 전에 명령 프롬프트에서 설정한 명령 셸( **SET** X=Y)  
  
4.  **sqlcmd-v** X=Y  
  
5.  **:Setvar** X Y  
  
> [!NOTE]  
>  환경 변수를 보려면 **제어판** 에서 **시스템** 을 연 다음 **고급** 탭을 클릭합니다.  
  
## <a name="sqlcmd-scripting-variables"></a>sqlcmd 스크립팅 변수  
  
|변수|관련 스위치|R/W|기본값|  
|--------------|--------------------|----------|-------------|  
|SQLCMDUSER|-U|R|""|  
|SQLCMDPASSWORD|-P|--|""|  
|SQLCMDSERVER|-S|R|"DefaultLocalInstance"|  
|SQLCMDWORKSTATION|-H|R|"ComputerName"|  
|SQLCMDDBNAME|-d|R|""|  
|SQLCMDLOGINTIMEOUT|-l|R/W|"8"(초)|  
|SQLCMDSTATTIMEOUT|-t|R/W|"0" = 무기한 대기|  
|SQLCMDHEADERS|-H|R/W|"0"|  
|SQLCMDCOLSEP|-S|R/W|" "|  
|SQLCMDCOLWIDTH|-w|R/W|"0"|  
|SQLCMDPACKETSIZE|지정하지 않을 경우|R|"4096"|  
|SQLCMDERRORLEVEL|-M|R/W|0|  
|SQLCMDMAXVARTYPEWIDTH|-y|R/W|"256"|  
|SQLCMDMAXFIXEDTYPEWIDTH|-y|R/W|"0" = 제한 없음|  
|SQLCMDEDITOR||R/W|"edit.com"|  
|SQLCMDINI||R|""|
|SQLCMDUSEAAD  | -G | R/W | "" |  
  
 SQLCMDUSER, SQLCMDPASSWORD 및 SQLCMDSERVER는 **:Connect** 가 사용될 때 설정됩니다.  
  
 R은 값이 프로그램 초기화 시 한 번만 설정될 수 있음을 나타냅니다.  
  
 R/W는 값이 **setvar** 명령을 사용하여 수정될 수 있으며 후속 명령이 새 값의 영향을 받을 수 있음을 나타냅니다.  
  
## <a name="sqlcmd-commands"></a>sqlcmd 명령  
 **sqlcmd** 에서 Transact-SQL 문 외에도 다음 명령을 사용할 수 있습니다.  
  
|||  
|-|-|  
|**GO** [*count*]|**:List**|  
|[ **:** ] **RESET**|**:Error**|  
|[ **:** ] **ED**|**:Out**|  
|[**:**] **!!**|**:Perftrace**|  
|[ **:** ] **QUIT**|**:Connect**|  
|[ **:** ] **EXIT**|**:On Error**|  
|**:r**|**:Help**|  
|**:ServerList**|**:XML** [**ON** &#124; **OFF**]|  
|**:Setvar**|**:Listvar**|  
  
 **sqlcmd** 명령을 사용할 때는 다음 사항에 주의하세요.  
  
- GO를 제외한 모든 **sqlcmd** 명령에는 접두사로 콜론(:)을 붙여야 합니다.  
  
    > [!IMPORTANT]  
    >  **osql** 스크립트와의 호환성을 유지하기 위해 일부 명령은 콜론 없이, [ **:** ] 형식으로 표시되어 인식됩니다.
  
- **sqlcmd** 명령은 줄 시작 부분에 나타난 경우에만 인식됩니다.  
  
- 모든 **sqlcmd** 명령은 대/소문자를 구분하지 않습니다.  
  
- 각 명령을 별도의 줄에 입력해야 합니다. 명령 다음에 Transact-SQL 문이나 다른 명령을 입력할 수 없습니다.  
  
- 명령은 즉시 실행되며 Transact-SQL 문처럼 실행 버퍼에 포함되지 않습니다.  
  
 **명령 편집**  
  [ **:** ] **ED**  
 텍스트 편집기를 시작합니다. 이 편집기를 사용하여 현재 Transact-SQL 일괄 처리를 편집하거나 마지막으로 실행된 일괄 처리를 편집할 수 있습니다. 마지막으로 실행된 일괄 처리를 편집하려면 마지막 일괄 처리 실행을 마친 후 즉시 **ED** 명령을 입력해야 합니다.  
  
 텍스트 편집기는 SQLCMDEDITOR 환경 변수에 의해 정의됩니다. 기본 편집기는 'Edit'입니다. 편집기를 변경하려면 SQLCMDEDITOR 환경 변수를 설정합니다. 예를 들어 편집기를 Microsoft 메모장으로 설정하려면 명령 프롬프트에서 다음을 입력합니다.  
  
 `SET SQLCMDEDITOR=notepad`  
  
 [ **:** ] **RESET**  
 문 캐시를 지웁니다.  
  
 **:List**  
 문 캐시 내용을 출력합니다.  
  
 **변수**  
  **:Setvar** \<**var**> [ **"** _value_ **"** ]  
 **sqlcmd** 스크립팅 변수를 정의합니다. 스크립팅 변수의 형식은 다음과 같습니다. `$(VARNAME)`.  
  
 변수 이름은 대/소문자를 구분하지 않습니다.  
  
 스크립팅 변수는 다음과 같은 방법으로 설정할 수 있습니다.  
  
- 명령줄 옵션을 사용하여 암시적으로 설정합니다. 예를 들어 **-l** 옵션은 SQLCMDLOGINTIMEOUT **sqlcmd** 변수를 설정합니다.  
  
- **:Setvar** 명령을 사용하여 명시적으로 설정합니다.  
  
- **sqlcmd** 를 실행하기 전에 환경 변수를 정의하여 설정합니다.  
  
> [!NOTE]  
>  **-X** 옵션은 환경 변수가 **sqlcmd** 에 전달되지 않도록 합니다.  
  
 **:Setvar** 명령을 사용하여 정의한 변수와 환경 변수의 이름이 같을 경우 **:Setvar** 명령을 사용하여 정의한 변수가 우선적으로 적용됩니다.  
  
 변수 이름에는 공백 문자를 포함해서는 안 됩니다.  
  
 변수 이름은 $(var) 등의 변수 식과 다른 형식이어야 합니다.  
  
 스크립팅 변수의 문자열 값에 공백이 포함된 경우 값을 따옴표로 묶습니다. 스크립팅 변수 값을 지정하지 않으면 스크립팅 변수가 삭제됩니다.  
  
 **:Listvar**  
 현재 설정되어 있는 스크립팅 변수의 목록을 표시합니다.  
  
> [!NOTE]  
>  **sqlcmd** 에서 설정한 스크립팅 변수와 **:Setvar** 명령을 사용하여 설정한 스크립팅 변수만 표시됩니다.  
  
 **출력 명령**  
  **:Error**   
 _**\<**_  _filename_  **_>|_ STDERR|STDOUT**  
 *file name* 에 지정된 파일, **stderr** 또는 **stdout** 으로 모든 오류 출력을 리디렉션합니다. 스크립트에서 **Error** 명령이 여러 번 나타날 수 있습니다. 기본적으로 오류 출력은 **stderr** 로 전송됩니다.  
  
 *file name*  
 출력을 받을 파일을 만들고 엽니다. 이 파일이 이미 있을 경우 0바이트로 잘립니다. 권한이나 기타 이유로 인해 이 파일을 사용할 수 없을 경우 출력이 전환되지 않으며 마지막으로 지정한 대상이나 기본 대상으로 전송됩니다.  
  
 **STDERR**  
 오류 출력을 **stderr** 스트림으로 전환합니다. 스트림을 리디렉션할 경우 리디렉션된 스트림 대상이 오류 출력을 받습니다.  
  
 **STDOUT**  
 오류 출력을 **stdout** 스트림으로 전환합니다. 스트림을 리디렉션할 경우 리디렉션된 스트림 대상이 오류 출력을 받습니다.  
  
 **:Out \<** _filename_ **>** | **STDERR**| **STDOUT**  
 쿼리 결과를 만들어 *file name* 에 지정된 파일, **stderr** 또는 **stdout** 으로 모두 리디렉션합니다. 기본적으로 출력은 **stdout** 으로 전송됩니다. 이 파일이 이미 있을 경우 0바이트로 잘립니다. 스크립트에서 **Out** 명령이 여러 번 나타날 수 있습니다.  
  
 **:Perftrace \<** _filename_ **>** | **STDERR**| **STDOUT**  
 성능 추적 정보를 만들어 *file name* 에 지정된 파일, **stderr** 또는 **stdout** 으로 모두 리디렉션합니다. 기본적으로 성능 추적 출력은 **stdout** 으로 전송됩니다. 이 파일이 이미 있을 경우 0바이트로 잘립니다. 스크립트에서 **Perftrace** 명령이 여러 번 나타날 수 있습니다.  
  
 **실행 제어 명령**  
  **:On Error**[ **exit** | **ignore**]  
 스크립트나 일괄 처리를 실행하는 동안 오류가 발생할 때 수행할 동작을 설정합니다.  
  
 **exit** 옵션을 사용하면 해당 오류 값이 표시되고 **sqlcmd** 가 종료됩니다.  
  
 **ignore** 옵션을 사용하면 **sqlcmd** 는 오류를 무시하고 일괄 처리 또는 스크립트를 계속 실행합니다. 기본적으로 오류 메시지가 출력됩니다.  
  
 [ **:** ] **QUIT**  
 **sqlcmd** 가 종료되도록 합니다.  
  
 [ **:** ] **EXIT**[ **(** _statement_ **)** ]  
 SELECT 문의 결과를 **sqlcmd** 의 반환 값으로 사용할 수 있도록 합니다. 숫자일 경우 마지막 결과 행의 첫째 열은 4바이트 정수(long)로 변환됩니다. MS-DOS, Linux 및 Mac은 하위 바이트를 부모 프로세스 또는 운영 체제 오류 수준에 전달합니다. Windows 200x에서는 4바이트 정수 전체를 전달합니다. 구문은 다음과 같습니다.  
  
 `:EXIT(query)`  
  
 다음은 그 예입니다.  
  
 `:EXIT(SELECT @@ROWCOUNT)`  
  
 **EXIT** 매개 변수를 배치 파일의 일부로 포함할 수도 있습니다. 예를 들어 명령 프롬프트에서 다음을 입력합니다.  
  
 `sqlcmd -Q "EXIT(SELECT COUNT(*) FROM '%1')"`  
  
 **sqlcmd** 유틸리티는 괄호 **()** 안의 모든 항목을 서버로 보냅니다. 시스템의 저장 프로시저가 설정을 선택하고 값을 반환하면 선택 내용만 반환됩니다. 괄호 사이에 아무것도 없는 EXIT **()** 문은 일괄 처리에서 이 문 앞에 나오는 모든 문을 실행한 후에 반환 값 없이 종료됩니다.  
  
 잘못된 쿼리를 지정하면 **sqlcmd** 는 값을 반환하지 않고 종료됩니다.  
  
 다음은 EXIT 형식의 목록입니다.  
  
- :EXIT  
  
 일괄 처리를 실행하지 않고 즉시 종료하며 값을 반환하지 않습니다.  
  
- :EXIT( )  
  
 일괄 처리를 실행한 다음 종료하며 값을 반환하지 않습니다.  
  
- :EXIT(query)  
  
 쿼리를 포함하는 일괄 처리를 실행하며 쿼리 결과를 반환한 다음 종료합니다.  
  
 **sqlcmd** 스크립트에 RAISERROR를 사용할 때 상태 127이 발생하면 **sqlcmd** 가 종료되고 메시지 ID가 클라이언트에 반환됩니다. 다음은 그 예입니다.  
  
 `RAISERROR(50001, 10, 127)`  
  
 이 오류가 발생하면 **sqlcmd** 스크립트가 종료되고 메시지 ID 50001이 클라이언트에 반환됩니다.  
  
 -1부터 -99까지의 반환 값은 SQL Server에 예약되어 있으므로 **sqlcmd** 는 다음과 같은 추가 반환 값을 정의합니다.  
  
|반환 값|Description|  
|-------------------|-----------------|  
|-100|반환 값을 선택하기 전에 오류가 발생했습니다.|  
|-101|반환 값을 선택할 때 행을 찾을 수 없습니다.|  
|-102|반환 값을 선택할 때 변환 오류가 발생했습니다.|  
  
 **GO** [*count*]  
 GO는 일괄 처리의 끝을 알려 주고 캐시된 Transact-SQL 문을 실행하도록 신호를 보냅니다. 일괄 처리는 별개의 일괄 처리로 여러 번 실행됩니다. 단일 일괄 처리에서 변수를 두 번 이상 선언할 수 없습니다.
  
 **기타 명령**  
  **:r \<** _filename_ **>**  
 **\<**_filename_**>** 으로 지정된 파일의 추가 Transact-SQL 문 및 **sqlcmd** 명령을 명령문 캐시로 구문 분석합니다.  
  
 파일에 Transact-SQL 문이 포함되어 있고 뒤에 **GO** 가 오지 않을 경우 **:r** 뒤에 오는 줄에 **GO** 를 입력해야 합니다.  
  
> [!NOTE]  
>  **\<** _filename_ **>** 은 **sqlcmd** 를 실행한 시작 디렉터리를 기준으로 상대적으로 읽혀집니다.  
  
 일괄 처리 종결자가 나타난 후 이 파일이 읽혀지고 실행됩니다. 여러 **:r** 명령을 실행할 수 있습니다. 이 파일에는 모든 유형의 **sqlcmd** 명령이 포함될 수 있으며 그 예로 일괄 처리 종결자 **GO** 를 들 수 있습니다.  
  
> [!NOTE]  
>  대화형 모드에서 표시되는 줄 수는 `:r` 명령이 나타날 때마다 1씩 증가합니다. `:r` 명령은 목록 명령의 출력에 나타납니다.  
  
 **:Serverlist**  
 로컬로 구성된 서버와 네트워크상에서 브로드캐스팅하는 서버의 이름을 표시합니다.  
  
 **:Connect**  _server_name_[ **\\** _instance\_name_] [-l *timeout*] [-U *user_name* [-P *password*]]  
 SQL Server 인스턴스에 연결합니다. 또한 현재 연결을 종료합니다.  
  
 제한 시간 옵션은 다음과 같습니다.  
  
|값|동작|  
|-|-|  
|0|무기한 대기|  
|n>0|n초 동안 대기|  
  
 SQLCMDSERVER 스크립팅 변수는 현재 활성 연결을 반영합니다.  
  
 *timeout* 을 지정하지 않으면 기본적으로 SQLCMDLOGINTIMEOUT 변수 값이 사용됩니다.  
  
 옵션이나 환경 변수로 *user_name* 만 지정하면 사용자에게 암호를 입력하라는 메시지가 표시됩니다. SQLCMDUSER 또는 SQLCMDPASSWORD 환경 변수를 설정한 경우 사용자에게 메시지가 표시되지 않습니다. 옵션이나 환경 변수를 지정하지 않을 경우 로그인하는 데 Windows 인증 모드가 사용됩니다. 예를 들어 통합 보안을 사용하여 SQL Server `myserver`의 인스턴스인 `instance1`에 연결하려면 다음 명령을 사용합니다.  
  
 `:connect myserver\instance1`  
  
 스크립팅 변수를 사용하여 `myserver` 의 기본 인스턴스에 연결하려면 다음을 사용합니다.  
  
 `:setvar myusername test`  
  
 `:setvar myservername myserver`  
  
 `:connect $(myservername) $(myusername)`  
  
 [ **:** ] **!!** < *명령*>  
 운영 체제 명령을 실행합니다. 운영 체제 명령을 실행하려면 느낌표 두 개( **!!** )로 줄을 시작하고 운영 체제 명령을 입력합니다. 다음은 그 예입니다.  
  
 `:!! Dir`  
  
> [!NOTE]  
>  **sqlcmd** 를 실행 중인 컴퓨터에서 명령이 실행됩니다.  
  
 **:XML** [**ON** | **OFF**]  
 자세한 내용은 이 문서의 [XML 출력 형식](#OutputXML) 및 [JSON 출력 형식](#OutputJSON)을 참조하세요.  
  
 **:Help**  
 **sqlcmd** 명령과 각 명령에 대한 간단한 설명을 표시합니다.  
  
### <a name="sqlcmd-file-names"></a>sqlcmd 파일 이름  
 **sqlcmd** 입력 파일은 **-i** 옵션 또는 **:r** 명령을 사용하여 지정할 수 있습니다. 출력 파일은 **-o** 옵션 또는 **:Error**, **:Out** 및 **:Perftrace** 명령을 사용하여 지정할 수 있습니다. 다음은 이러한 파일 작업에 대한 지침입니다.  
  
- **:Error**, **:Out** 및 **:Perftrace** 는 별도의 **\<**_filename_**>** 을 사용해야 합니다. 동일한 **\<**_filename_**>** 을 사용하면 명령의 입력이 섞일 수 있습니다.  
  
- 원격 서버에 있는 입력 파일을 로컬 컴퓨터에 있는 **sqlcmd** 에서 호출할 경우 이 파일에 :Out c:\OutputFile.txt와 같은 드라이브 파일 경로가 포함되어 있으면 출력 파일이 원격 서버가 아닌 로컬 컴퓨터에 생성됩니다.  
  
- 올바른 파일 경로의 예는 `C:\<filename>`, `\\<Server>\<Share$>\<filename>` 및 `"C:\Some Folder\<file name>"`입니다. 경로에 공백이 있을 경우 따옴표를 사용합니다.  
  
- 각각의 새 **sqlcmd** 세션은 이름이 같은 기존 파일을 덮어씁니다.  
  
### <a name="informational-messages"></a>정보 메시지

**sqlcmd** 는 서버에서 보낸 모든 정보 메시지를 출력합니다. 다음 예에서는 Transact-SQL 문을 실행한 후 정보 메시지가 출력됩니다.
  
명령 프롬프트에서 다음 명령을 입력합니다.

`sqlcmd`
  
sqlcmd 프롬프트에서 다음을 입력합니다.

`USE AdventureWorks2012;`

`GO`

Enter 키를 누르면 다음 정보 메시지가 출력됩니다. "Changed database context to 'AdventureWorks2012'."  
  
### <a name="output-format-from-transact-sql-queries"></a>Transact-SQL 쿼리의 출력 형식  
 먼저 **sqlcmd** 는 SELECT 목록에서 지정한 열 이름이 포함된 열 머리글을 출력합니다. 열 이름은 SQLCMDCOLSEP 문자로 구분됩니다. 기본적으로 구분 문자는 공백입니다. 열 이름이 열 너비보다 짧은 경우 출력은 다음 열까지 공백으로 채워집니다.  
  
 이 줄 다음에는 대시 문자로 이루어진 구분선이 삽입됩니다. 다음은 출력의 예입니다.  
  
 **sqlcmd** 를 시작합니다. **sqlcmd** 명령 프롬프트에서 다음 쿼리를 입력합니다.  
  
 `USE AdventureWorks2012;`  
  
 `SELECT TOP (2) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 Enter 키를 누르면 다음 결과 집합이 반환됩니다.  
  
 `BusinessEntityID FirstName    LastName`  
  
 `---------------- ------------ ----------`  
  
 `285              Syed         Abbas`  
  
 `293              Catherine    Abel`  
  
 `(2 row(s) affected)`  
  
 `BusinessEntityID` 열의 너비는 4자이지만 보다 긴 열 이름을 포함할 수 있도록 확장되었습니다. 기본적으로 출력은 80자에서 끝납니다. 그러나 **-w** 옵션을 사용하거나 SQLCMDCOLWIDTH 스크립팅 변수를 설정하여 이 값을 변경할 수 있습니다.  
  
###  <a name="xml-output-format"></a><a name="OutputXML"></a> XML 출력 형식  
 FOR XML 절의 결과로 나오는 XML 출력은 연속 스트림에서 형식이 지정되지 않은 출력입니다.  
  
 XML 출력을 원하는 경우에는 `:XML ON`명령을 사용합니다.  
  
> [!NOTE]  
>  **sqlcmd** 는 일반 형식으로 오류 메시지를 반환합니다. 오류 메시지는 XML 형식으로 XML 텍스트 스트림에도 출력됩니다. `:XML ON`을 사용할 경우 **sqlcmd** 에서는 정보 메시지를 표시하지 않습니다.  
  
 XML 모드를 해제하려면 `:XML OFF`명령을 사용합니다.  
  
 XML OFF 명령은 **sqlcmd** 를 다시 행 기반 출력으로 전환하기 때문에 GO 명령은 XML OFF 명령이 실행된 후에 나타나야 합니다.  
  
 스트리밍된 XML 데이터와 행 집합 데이터를 혼합할 수 없습니다. XML 스트림을 출력하는 Transact-SQL 문을 실행하기 전에 XML ON 명령을 실행하지 않은 경우 출력이 잘못됩니다. XML ON 명령을 실행한 경우 일반 행 집합을 출력하는 Transact-SQL 문을 실행할 수 없습니다.  
  
> [!NOTE]  
>  `:XML` 명령은 SET STATISTICS XML 문을 지원하지 않습니다.  
  
###  <a name="json-output-format"></a><a name="OutputJSON"></a> JSON 출력 형식  
 JSON 출력을 원하는 경우에는 다음 명령을 사용합니다. `:XML ON` 그렇지 않으면 출력에 열 이름과 JSON 텍스트가 모두 포함됩니다. 이 출력은 유효한 JSON이 아닙니다.  
  
 XML 모드를 해제하려면 `:XML OFF`명령을 사용합니다.  
  
 자세한 내용은 이 문서의 [XML 출력 형식](#OutputXML)을 참조하세요.  

### <a name="using-azure-active-directory-authentication"></a>Azure Active Directory 인증 사용

Azure Active Directory 인증 사용 예제:

```cmd
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  -l 30
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -G -U bob@contoso.com -P MyAADPassword -l 30
```
  
## <a name="sqlcmd-best-practices"></a>sqlcmd를 위한 최선의 구현 방법

보안 및 효율성을 극대화하려면 다음 방법을 사용하십시오.  

- 통합 보안을 사용합니다.  

- 자동화된 환경에서 **-X** 를 사용합니다.  

- 적절한 NTFS 파일 시스템 권한을 사용하여 입력 및 출력 파일을 보호합니다.

- 성능을 향상시키려면 여러 세션 대신 한 번의 **sqlcmd** 세션에서 가능한 한 많은 작업을 수행합니다.

- 일괄 처리 또는 쿼리를 실행하는 데 걸리는 예상 시간보다 높은 제한 시간 값을 일괄 처리 또는 쿼리 실행에 대해 설정합니다.

## <a name="next-steps"></a>다음 단계

- [sqlcmd 유틸리티 시작](~/relational-databases/scripting/sqlcmd-start-the-utility.md)
- [sqlcmd를 사용하여 Transact-SQL 스크립트 파일 실행](~/relational-databases/scripting/sqlcmd-run-transact-sql-script-files.md)
- [sqlcmd 유틸리티 사용](~/relational-databases/scripting/sqlcmd-use-the-utility.md)
- [스크립팅 변수와 함께 sqlcmd 사용](~/relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)
- [sqlcmd를 사용하여 데이터베이스 엔진에 연결](~/relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md)
- [쿼리 편집기로 SQLCMD 스크립트 편집](~/relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)
- [작업 단계 관리](~/ssms/agent/manage-job-steps.md)   
- [CmdExec 작업 단계 만들기](~/ssms/agent/create-a-cmdexec-job-step.md)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
