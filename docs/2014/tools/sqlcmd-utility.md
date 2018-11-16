---
title: sqlcmd 유틸리티 | Microsoft 문서
ms.custom: ''
ms.date: 11/29/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7fe44b790fbf99811761041f4b81eeb3b48e96da
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51641540"
---
# <a name="sqlcmd-utility"></a>sqlcmd Utility
  합니다 `sqlcmd` 유틸리티를 사용 하면 입력 [!INCLUDE[tsql](../includes/tsql-md.md)] 문, 시스템 프로시저 및 스크립트의 명령 프롬프트에서 파일 **쿼리 편집기** SQLCMD 모드에서 Windows 스크립트 파일에서 또는의 운영 체제 (Cmd.exe) 작업 단계는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 작업입니다. 이 유틸리티는 ODBC를 사용하여 [!INCLUDE[tsql](../includes/tsql-md.md)] 일괄 처리를 실행합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 사용 하는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]실행에서 일반 및 SQLCMD 모드에 대 한 SqlClient **쿼리 편집기**합니다. 명령줄에서 `sqlcmd`를 실행할 경우 `sqlcmd`는 ODBC 드라이버를 사용합니다. 서로 다른 기본 옵션이 적용될 수 있으므로 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] SQLCMD 모드 및 `sqlcmd` 유틸리티에서 동일한 쿼리를 실행할 때 다른 동작이 수행될 수 있습니다.  
  
 현재는 `sqlcmd`를 실행할 때 명령줄 옵션과 값 사이에 공백을 넣을 필요가 없습니다. 하지만 후속 릴리스에서는 명령줄 옵션과 값 사이에 공백을 넣어야 할 수도 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
   sqlcmd  
   -a  
   packet_size  
   -A (dedicated administrator connection)  
-b (terminate batch job if there is an error)  
-cbatch_terminator-C (trust the server certificate)  
-ddb_name-e (echo input)  
-E (use trusted connection)  
-fcodepage | i:codepage[,o:codepage] | o:codepage[,i:codepage]  
-hrows_per_header-Hworkstation_name-iinput_file-I (enable quoted identifiers)  
-k[1 | 2] (remove or replace control characters)  
-Kapplication_intent-llogin_timeout-L[c] (list servers, optional clean output)  
-merror_level-Mmultisubnet_failover-N (encrypt connection)  
-ooutput_file-p[1] (print statistics, optional colon format)  
-Ppassword-q "cmdline query"-Q "cmdline query" (and exit)  
-r[0 | 1] (msgs to stderr)  
-R (use client regional settings)  
-scol_separator-S [protocol:]server[\instance_name][,port]  
-tquery_timeout-u (unicode output file)  
-Ulogin_id-vvar = "value"-Verror_severity_level-wcolumn_width-W (remove trailing spaces)  
-x (disable variable substitution)  
-X[1] (disable commands, startup script, environment variables and optional exit)  
-yvariable_length_type_display_width-Yfixed_length_type_display_width-znew_password -Znew_password (and exit)  
  
-? (usage)  
```  
  
## <a name="command-line-options"></a>명령줄 옵션  
 **로그인 관련 옵션**  
  **-A**  
 DAC(관리자 전용 연결)를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 로그인합니다. 이 연결 유형은 서버 문제를 해결하는 데 사용됩니다. 이 연결은 DAC를 지원하는 서버 컴퓨터에만 사용할 수 있습니다. DAC를 사용할 수 없는 경우 `sqlcmd`는 오류 메시지를 생성하고 종료됩니다. DAC에 대한 자세한 내용은 [데이터베이스 관리자를 위한 진단 연결](../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)을 참조하세요.  
  
 **-C**  
 이 스위치는 클라이언트에서 유효성 검사 없이 암시적으로 서버 인증서를 신뢰하는 데 사용됩니다. 이 옵션은 ADO.NET 옵션 `TRUSTSERVERCERTIFICATE = true`와 동일합니다.  
  
 **-d** *db_name*  
 문제는 `USE` *db_name* 시작 하면 문을 `sqlcmd`합니다. 이 옵션은 `sqlcmd` 스크립팅 변수 SQLCMDDBNAME을 설정합니다. 이 변수는 초기 데이터베이스를 지정합니다. 기본값은 사용자 로그인의 기본 데이터베이스 속성입니다. 데이터베이스가 없을 경우 오류 메시지가 생성되고 `sqlcmd`가 종료됩니다.  
  
 **-l** *login_timeout*  
 서버에 연결을 시도할 때 ODBC 드라이버에 대한 `sqlcmd` 로그인 제한 시간(초)을 지정합니다. 이 옵션은 `sqlcmd` 스크립팅 변수 SQLCMDLOGINTIMEOUT을 설정합니다. 기본 `sqlcmd` 로그인 제한 시간은 8초입니다. 로그인 제한 시간은 0에서 65534 사이의 숫자여야 합니다. 입력한 값이 숫자가 아니거나 이 범위에 속하지 않을 경우 `sqlcmd`는 오류 메시지를 생성합니다. 값을 0으로 설정하면 제한 시간이 없습니다.  
  
 **-E**  
 사용자 이름과 암호를 사용하는 대신 트러스트된 연결을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 로그온합니다. -E를 지정하지 않으면 `sqlcmd`는 기본적으로 트러스트된 연결 옵션을 사용합니다.  
  
 **-E** 옵션은 SQLCMDPASSWORD 등의 가능한 사용자 이름 및 암호 환경 변수 설정을 무시합니다. **-E** 옵션과 함께 **-U** 옵션 또는 **-P** 옵션을 사용하면 오류 메시지가 생성됩니다.  
  
 **-H** *workstation_name*  
 워크스테이션 이름입니다. 이 옵션은 `sqlcmd` 스크립팅 변수 SQLCMDWORKSTATION을 설정합니다. 워크스테이션 이름은 **sys.processes** 카탈로그 뷰의 **hostname** 열에 나열되며 **sp_who** 저장 프로시저를 사용하여 반환할 수 있습니다. 이 옵션을 지정하지 않으면 기본적으로 현재 컴퓨터 이름이 사용됩니다. 이 이름을 사용하여 다른 `sqlcmd` 세션을 식별할 수 있습니다  
  
 **-K** *application_intent*  
 서버에 연결할 때 응용 프로그램 작업 유형을 선언합니다. 현재 **ReadOnly**값만 지원됩니다. **-K**를 지정하지 않으면 sqlcmd 유틸리티가 AlwaysOn 가용성 그룹에 있는 보조 복제본에 연결할 수 없습니다. 자세한 내용은 [활성 보조: 읽기 가능한 보조 복제본](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)합니다.  
  
 `-M` *multisubnet_failover*  
 `-M` 가용성 그룹 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 인스턴스의 가용성 그룹 수신기에 연결할 때는 항상 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 지정하십시오. `-M`은 현재 활성 상태인 서버를 빠르게 검색하여 연결할 수 있도록 제공합니다. `–M`이 지정되지 않은 경우 `-M`이 해제됩니다. 에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../includes/sshadr-md.md)]를 참조 하세요 [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치 &#40;SQL Server&#41;](../database-engine/listeners-client-connectivity-application-failover.md)를 [생성 및 구성의 가용성 그룹 &#40;SQL Server&#41;](../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)하십시오 [장애 조치 클러스터링 및 AlwaysOn 가용성 그룹 &#40;SQL Server&#41;](../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md), 및 [활성 보조: 읽기 가능한 보조 복제본 ](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) .  
  
 **-N**  
 이 스위치는 클라이언트에서 암호화된 연결을 요청하는 데 사용됩니다.  
  
 **-P** *password*  
 사용자가 지정하는 암호입니다. 암호는 대/소문자를 구분합니다. -U 옵션을 사용 하는 경우 및 **-P** 옵션을 사용 하지 않으며 SQLCMDPASSWORD 환경 변수를 설정 하지는 `sqlcmd` 암호를 묻는 메시지를 표시 합니다. 경우는 **-P** 옵션을 사용 하는 암호 없이 명령 프롬프트의 끝 `sqlcmd` 기본 암호 (NULL)을 사용 합니다.  
  
> [!IMPORTANT]  
>  빈 암호를 사용하지 마세요. 강력한 암호를 사용하세요. 자세한 내용은 [Strong Passwords](../relational-databases/security/strong-passwords.md)을 참조하세요.  
  
 암호 프롬프트는 다음과 같이 콘솔에 출력되어 표시됩니다. `Password:`  
  
 사용자 입력은 숨겨지므로 아무 것도 표시되지 않고 커서가 해당 위치에 그대로 남아 있습니다.  
  
 SQLCMDPASSWORD 환경 변수를 사용하면 현재 세션에 대한 기본 암호를 설정할 수 있습니다. 그러므로 암호를 배치 파일로 하드 코딩할 필요가 없습니다.  
  
 다음 예에서는 먼저 명령 프롬프트에서 SQLCMDPASSWORD 변수를 설정하고 `sqlcmd` 유틸리티에 액세스합니다. 명령 프롬프트에서 다음을 입력합니다.  
  
 `SET SQLCMDPASSWORD= p@a$$w0rd`  
  
> [!IMPORTANT]  
>  컴퓨터 모니터에서 누구나 암호를 볼 수 있습니다.  
  
 명령 프롬프트에서 다음을 입력합니다.  
  
 `sqlcmd`  
  
 사용자 이름 및 암호 조합이 잘못된 경우 오류 메시지가 생성됩니다.  
  
> [!NOTE]  
>  OSQLPASSWORD 환경 변수는 이전 버전과의 호환성을 위해 유지되었습니다. SQLCMDPASSWORD 환경 변수는 OSQLPASSWORD 환경 변수; 보다 우선 따라서 `sqlcmd` 하 고 **osql** 사용된 없이 다음 간섭 수 있으며 이전 스크립트는 계속 작동 하는 합니다.  
  
 **-P** 옵션과 함께 **-E** 옵션을 사용하면 오류 메시지가 생성됩니다.  
  
 **-P** 옵션 다음에 둘 이상의 인수를 지정하면 오류 메시지가 생성되고 프로그램이 종료됩니다.  
  
 **-S** [*protocol*:]*server*[**\\***instance_name*][**,***port*]  
 연결할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 지정합니다. `sqlcmd` 스크립팅 변수 SQLCMDSERVER를 설정합니다.  
  
 해당 서버 컴퓨터에 있는 기본 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결하려면 *server_name*을 지정합니다. 지정할 *server_name* [**\\* * * instance_name* ]의 명명된 된 인스턴스에 연결할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 해당 서버 컴퓨터. 서버 컴퓨터를 지정하지 않으면 `sqlcmd`가 로컬 컴퓨터에 있는 기본 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결됩니다. 네트워크의 원격 컴퓨터에서 `sqlcmd`를 실행할 경우에는 이 옵션을 지정해야 합니다.  
  
 *프로토콜* 될 수 있습니다 `tcp` (TCP/IP), `lpc` (공유 메모리) 또는 `np` (명명 된 파이프).  
  
 지정 하지 않는 경우는 *server_name* [**\\* * * instance_name* ] 시작 하면 `sqlcmd`, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 확인 하 고 기본적으로 SQLCMDSERVER 환경 변수를 사용 합니다.  
  
> [!NOTE]  
>  OSQLSERVER 환경 변수는 이전 버전과의 호환성을 위해 유지되었습니다. SQLCMDSERVER 환경 변수는 OSQLSERVER 환경 변수; 보다 우선 따라서 `sqlcmd` 하 고 **osql** 사용된 없이 다음 간섭 수 있으며 이전 스크립트는 계속 작동 하는 합니다.  
  
 **-U** *login_id*  
 사용자 로그인 ID입니다.  
  
> [!NOTE]  
>  OSQLUSER 환경 변수는 이전 버전과의 호환성을 위해 제공됩니다. SQLCMDUSER 환경 변수는 OSQLUSER 환경 변수보다 우선적으로 적용됩니다. 따라서 `sqlcmd` 하 고 **osql** 간섭 없이 나란히 사용할 수 있습니다. 이전 **osql** 스크립트도 계속 사용할 수 있습니다.  
  
 모두를 **-U** 옵션 또는 **-P** 옵션을 지정 하면 `sqlcmd` 사용 하 여 연결 하려고 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 인증 모드입니다. `sqlcmd`를 실행하는 사용자의 Windows 계정을 기반으로 인증이 수행됩니다.  
  
 이 항목의 뒷부분에 설명되어 있는 **-E** 옵션과 함께 **-U** 옵션을 사용하면 오류 메시지가 생성됩니다. **–U** 옵션 다음에 둘 이상의 인수를 지정하면 오류 메시지가 생성되고 프로그램이 종료됩니다.  
  
 **-z** *new_password*  
 암호를 변경합니다.  
  
 `sqlcmd -U someuser -P s0mep@ssword -z a_new_p@a$$w0rd`  
  
 **-Z** *new_password*  
 암호 변경 후 종료합니다.  
  
 `sqlcmd -U someuser -P s0mep@ssword -Z a_new_p@a$$w0rd`  
  
 **입/출력 옵션**  
  **-f** *codepage* | **i:***codepage*[**,o:***codepage*] | **o:***codepage*[**,i:*** codepage*]  
 입력 및 출력 코드 페이지를 지정합니다. 코드 페이지 번호는 설치된 Windows 코드 페이지를 지정하는 숫자 값입니다.  
  
 코드 페이지 변환 규칙은 다음과 같습니다.  
  
-   변환이 필요 없는 유니코드 파일이 입력 파일로 사용된 경우가 아니라면 `sqlcmd`는 지정된 코드 페이지가 없는 경우 입력 파일과 출력 파일에 현재 코드 페이지를 사용합니다.  
  
-   `sqlcmd`는 Big-Endian 및 Little-Endian 유니코드 입력 파일을 모두 자동으로 인식합니다. **-u** 옵션이 지정된 경우 출력은 항상 Little-Endian 유니코드가 됩니다.  
  
-   지정된 출력 파일이 없는 경우 출력 코드 페이지는 콘솔 코드 페이지가 됩니다. 이 경우 출력이 콘솔에 올바르게 표시됩니다.  
  
-   여러 입력 파일이 있는 경우 동일한 코드 페이지를 사용하는 것으로 간주됩니다. 유니코드 및 비유니코드 입력 파일을 함께 사용할 수 있습니다.  
  
 명령 프롬프트에서 `chcp`를 입력하여 Cmd.exe의 코드 페이지를 확인합니다.  
  
 **-i** *input_file*[**,***input_file2*...]  
 SQL 문 또는 저장 프로시저의 일괄 처리가 포함된 파일을 나타냅니다. 순서대로 읽고 처리할 파일을 여러 개 지정할 수 있습니다. 파일 이름 사이에 공백을 넣지 마십시오. 먼저 `sqlcmd`는 지정한 모든 파일이 있는지 확인합니다. 하나 이상의 파일이 없을 경우 `sqlcmd`가 종료됩니다. -i 옵션과 -Q/-q 옵션은 함께 사용할 수 없습니다.  
  
 경로 예는 다음과 같습니다.  
  
 **-i** c:\\< 파일 이름\>  
  
 **-i** \\ \\< 서버\>\\<$ 공유 >\\< 파일 이름\>  
  
 **-i** "C:\Some Folder\\<file name\>"  
  
 공백이 포함된 파일 경로는 따옴표로 묶어야 합니다.  
  
 이 옵션은 두 번 이상 사용할 수 있습니다. **-i***input_file* **-I***I input_file.*  
  
 **-o** *output_file*  
 `sqlcmd`에서 출력을 받는 파일을 나타냅니다.  
  
 **-u** 를 지정하면 *output_file* 이 유니코드 형식으로 저장됩니다. 파일 이름이 잘못된 경우 오류 메시지가 생성되고 `sqlcmd`가 종료됩니다. `sqlcmd`는 여러 `sqlcmd` 프로세스를 같은 파일에 동시에 쓸 수 없습니다. 이 경우 파일 출력이 손상되거나 제대로 수행되지 않습니다. 파일 형식에 대한 자세한 내용은 **-f** 스위치를 참조하세요. 이 파일은 없는 경우 생성됩니다. 이전 `sqlcmd` 세션에서와 이름이 같은 파일은 덮어쓰여집니다. 여기에 지정된 파일은 **stdout** 파일이 아닙니다. **stdout** 파일이 지정된 경우에는 이 파일이 사용되지 않습니다.  
  
 경로 예는 다음과 같습니다.  
  
 **-o** C:\\< filename>  
  
 **-o** \\ \\< 서버\>\\<$ 공유 >\\< 파일 이름\>  
  
 **-o "** C:\Some Folder\\<file name\>"  
  
 공백이 포함된 파일 경로는 따옴표로 묶어야 합니다.  
  
 **-r**[**0** | **1**]  
 오류 메시지 출력을 화면으로 리디렉션합니다(**stderr**). 매개 변수를 지정하지 않거나 **0**을 지정하면 심각도가 11 이상인 오류 메시지만 리디렉션됩니다. **1**을 지정하면 PRINT를 포함하는 모든 오류 메시지 출력이 리디렉션됩니다. -o를 사용할 경우 아무 효과도 없습니다. 기본적으로 메시지는 **stdout**으로 전송됩니다.  
  
 **-R**  
 클라이언트의 로캘을 기반으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 검색한 숫자, 통화, 날짜 및 시간 열을 `sqlcmd`에서 지역화합니다. 기본적으로 이러한 열은 서버의 국가별 설정을 사용하여 표시됩니다.  
  
 **-u**  
 *input_file* 형식에 관계없이 *output_file*이 유니코드 형식으로 저장되도록 지정합니다.  
  
 **쿼리 실행 옵션**  
  **-e**  
 표준 출력 장치에 입력 스크립트를 기록합니다(**stdout**).  
  
 **-I**  
 SET QUOTED_IDENTIFIER 연결 옵션을 ON으로 설정합니다. 기본적으로 OFF로 설정되어 있습니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql)를 참조하세요.  
  
 **-q"** *cmdline query* **"**  
 `sqlcmd`가 시작될 때 쿼리를 실행하지만 쿼리 실행이 완료되더라도 `sqlcmd`를 종료하지 않습니다. 세미콜론으로 구분된 여러 쿼리를 실행할 수 있습니다. 다음 예와 같이 쿼리를 따옴표로 묶습니다.  
  
 명령 프롬프트에서 다음을 입력합니다.  
  
 `sqlcmd -d AdventureWorks2012 -q "SELECT FirstName, LastName FROM Person.Person WHERE LastName LIKE 'Whi%';"`  
  
 `sqlcmd -d AdventureWorks2012 -q "SELECT TOP 5 FirstName FROM Person.Person;SELECT TOP 5 LastName FROM Person.Person;"`  
  
> [!IMPORTANT]  
>  쿼리에 GO 종결자를 사용하지 마십시오.  
  
 이 옵션과 함께 `-b`를 지정하면 `sqlcmd`에 오류가 발생하여 종료됩니다. `-b`에 대해서는 이 항목의 뒷부분에서 설명합니다.  
  
 **-Q"** *cmdline query* **"**  
 `sqlcmd`가 시작될 때 쿼리를 실행한 다음 바로 `sqlcmd`를 종료합니다. 세미콜론으로 구분된 여러 쿼리를 실행할 수 있습니다.  
  
 다음 예와 같이 쿼리를 따옴표로 묶습니다.  
  
 명령 프롬프트에서 다음을 입력합니다.  
  
 `sqlcmd -d AdventureWorks2012 -Q "SELECT FirstName, LastName FROM Person.Person WHERE LastName LIKE 'Whi%';"`  
  
 `sqlcmd -d AdventureWorks2012 -Q "SELECT TOP 5 FirstName FROM Person.Person;SELECT TOP 5 LastName FROM Person.Person;"`  
  
> [!IMPORTANT]  
>  쿼리에 GO 종결자를 사용하지 마십시오.  
  
 이 옵션과 함께 `-b`를 지정하면 `sqlcmd`에 오류가 발생하여 종료됩니다. `-b`에 대해서는 이 항목의 뒷부분에서 설명합니다.  
  
 **-t** *query_timeout*  
 명령 또는 SQL 문 제한 시간(초)을 지정합니다. 이 옵션은 `sqlcmd` 스크립팅 변수 SQLCMDSTATTIMEOUT을 설정합니다. *time_out* 값을 지정하지 않으면 명령이 무기한 실행됩니다. *query**time_out*은 1에서 65534 사이의 숫자여야 합니다. 입력한 값이 숫자가 아니거나 이 범위에 속하지 않을 경우 `sqlcmd`는 오류 메시지를 생성합니다.  
  
> [!NOTE]  
>  실제 제한 시간 값은 지정한 *time_out* 값과 몇 초 정도 차이가 날 수 있습니다.  
  
 **-vvar =**  *value*[ **var =** *value*...]  
 만듭니다는 `sqlcmd`에서 사용할 수 있는 스크립팅 변수는 `sqlcmd` 스크립트입니다. 공백이 포함된 값은 따옴표로 묶습니다. 여러 개 지정할 수 있습니다 ***var***=**"*`values`*"** 값입니다. 지정한 값에 오류가 있을 경우 `sqlcmd`는 오류 메시지를 생성하고 종료됩니다.  
  
 `sqlcmd -v MyVar1=something MyVar2="some thing"`  
  
 `sqlcmd -v MyVar1=something -v MyVar2="some thing"`  
  
 **-x**  
 `sqlcmd`에서 스크립팅 변수를 무시하도록 합니다. 이는 $(*variable_name*) 등의 일반 변수와 형식이 같은 문자열이 포함되어 있을 수 있는 INSERT 문이 스크립트에 많이 포함된 경우에 유용합니다.  
  
 **형식 지정 옵션**  
  **-h** *headers*  
 열 머리글 사이에 출력할 행의 수를 지정합니다. 기본적으로 각 쿼리 결과 집합마다 머리글을 한 번 출력합니다. 이 옵션은 `sqlcmd` 스크립팅 변수 SQLCMDHEADERS를 설정합니다. 머리글을 출력하지 않으려면 **-1** 을 사용합니다. 잘못된 값을 지정할 경우 `sqlcmd`는 오류 메시지를 생성하고 종료됩니다.  
  
 **-k** [**1** | **2**]  
 출력에서 탭이나 줄 바꿈 문자와 같은 모든 제어 문자를 제거합니다. 데이터를 반환할 때 열 서식은 유지됩니다. 1을 지정하면 제어 문자가 단일 공백으로 바뀝니다. 2를 지정하면 연속된 제어 문자가 단일 공백으로 바뀝니다. **-k** 는 **-k1**과 같습니다.  
  
 **-s** *col_separator*  
 열 구분 기호 문자를 지정합니다. 기본값은 공백입니다. 이 옵션은 `sqlcmd` 스크립팅 변수 SQLCMDCOLSEP를 설정합니다. 앰퍼샌드(&)나 세미콜론(;)과 같이 운영 체제에서 특별한 의미를 갖는 문자를 사용하려면 해당 문자를 따옴표(")로 묶습니다. 열 구분 기호로 임의의 8비트 문자를 사용할 수 있습니다.  
  
 **-w** *column_width*  
 출력할 화면 너비를 지정합니다. 이 옵션은 `sqlcmd` 스크립팅 변수 SQLCMDCOLWIDTH를 설정합니다. 열 너비는 8보다 크고 65536보다 작은 숫자여야 합니다. 지정한 열 너비가 이 범위에 속하지 않을 경우 `sqlcmd`는 오류 메시지를 생성합니다. 기본 너비는 80자입니다. 출력 줄이 지정한 열 너비를 초과하면 다음 줄로 넘어갑니다.  
  
 **-W**  
 이 옵션은 열에서 후행 공백을 제거합니다. 다른 응용 프로그램으로 내보낼 데이터를 준비하는 경우 **-s** 옵션과 함께 이 옵션을 사용합니다. **-y** 또는 **-Y** 옵션과 함께 사용할 수 없습니다.  
  
 **-y** *variable_length_type_display_width*  
 `sqlcmd` 스크립팅 변수 SQLCMDMAXVARTYPEWIDTH를 설정합니다. 기본값은 256입니다. 다음과 같은 큰 가변 길이 데이터 형식에 대해 반환되는 문자 수를 제한합니다.  
  
-   `varchar(max)`  
  
-   `nvarchar(max)`  
  
-   `varbinary(max)`  
  
-   `xml`  
  
-   `UDT (user-defined data types)`  
  
-   `text`  
  
-   `ntext`  
  
-   `image`  
  
> [!NOTE]  
>  UDT는 구현에 따라 길이가 고정될 수 있습니다. 길이가 고정된 UDT의 길이가 *display_width*보다 짧으면 반환되는 UDT 값은 영향을 받지 않습니다. 그러나 길이가 *display_width*보다 길면 출력이 잘립니다.  
  
 
> [!IMPORTANT]  
>  **-y 0** 옵션은 반환되는 데이터 크기에 따라 서버와 네트워크 모두에서 심각한 성능 문제를 일으킬 수 있으므로 사용 시 매우 주의해야 합니다.  
  
 **-Y** *fixed_length_type_display_width*  
 `sqlcmd` 스크립팅 변수 SQLCMDMAXFIXEDTYPEWIDTH를 설정합니다. 기본값은 0(무제한)입니다. 다음 데이터 형식에 대해 반환되는 문자 수를 제한합니다.  
  
-   `char(` *n* `)`, 여기서 1 < = n < = 8000  
  
-   `nchar(n` *n* `)`, 여기서 1 < = n < = 4000  
  
-   `varchar(n` *n* `)`, 여기서 1 < = n < = 8000  
  
-   `nvarchar(n` *n* `)`, 여기서 1 < = n < = 4000  
  
-   `varbinary(n` *n* `)`, 여기서 1 < = n < = 4000  
  
-   `variant`  
  
 **오류 보고 옵션**  
  `-b`  
 오류가 발생하면 `sqlcmd`를 끝내고 DOS ERRORLEVEL 값을 반환하도록 지정합니다. **오류 메시지의 심각도가 10보다 큰 경우 DOS ERRORLEVEL 변수로** 1 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이 반환되며 심각도가 10보다 작거나 같은 경우 **0**이 반환됩니다. `-V` 외에도 `-b` 옵션을 설정한 경우 심각도가 `-V`를 사용하여 설정한 값보다 작으면 `sqlcmd`는 오류를 보고하지 않습니다. 명령 프롬프트 배치 파일은 ERRORLEVEL 값을 테스트하고 그에 따라 적절히 오류를 처리할 수 있습니다. `sqlcmd`는 심각도가 10(정보 메시지)인 오류는 보고하지 않습니다.  
  
 `sqlcmd` 스크립트에 잘못된 설명 또는 구문 오류가 포함되었거나 스크립팅 변수가 없을 경우 반환되는 ERRORLEVEL은 1입니다.  
  
 **-m** *error_level*  
 **stdout**에 보낼 오류 메시지를 제어합니다. 심각도가 이 수준보다 크거나 같은 메시지는 보내집니다. 이 값을 **1**로 설정하면 정보 메시지를 포함한 모든 메시지가 보내집니다. **-m** 과 **-1**사이에는 공백이 있으면 안 됩니다. 예를 들어 **-m-1** 은 유효하고 **-m-1** 은 유효하지 않습니다.  
  
 이 옵션은 `sqlcmd` 스크립팅 변수 SQLCMDERRORLEVEL도 설정합니다. 이 변수의 기본값은 0입니다.  
  
 `-V` *error_severity_level*  
 ERRORLEVEL 변수를 설정하는 데 사용되는 심각도를 제어합니다. 심각도가 이 값보다 크거나 같은 오류 메시지는 ERRORLEVEL을 설정합니다. 0보다 작은 값은 0으로 보고됩니다. 배치 파일 및 CMD 파일은 ERRORLEVEL 변수의 값을 테스트하는 데 사용할 수 있습니다.  
  
 **기타 옵션**  
  **-a** *packet_size*  
 다른 크기의 패킷을 요청합니다. 이 옵션은 `sqlcmd` 스크립팅 변수 SQLCMDPACKETSIZE를 설정합니다. *packet_size* 는 512에서 32767 사이의 값이어야 합니다. 기본값은 4096입니다. GO 명령 사이에 SQL 문 수가 많은 스크립트를 실행할 때는 패킷 크기가 클수록 성능이 더 향상됩니다. 더 큰 패킷 크기를 요청할 수 있습니다. 그러나 요청이 거부되면 `sqlcmd`는 서버 기본값을 패킷 크기로 사용합니다.  
  
 **-c** *batch_terminator*  
 일괄 처리 종결자를 지정합니다. 기본적으로 줄에 "GO"만 단독으로 입력하면 명령이 종료되어 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로 보내집니다. 일괄 처리 종결자를 다시 설정할 때는 앞에 백슬래시가 있더라도 [!INCLUDE[tsql](../includes/tsql-md.md)] 예약 키워드 또는 운영 체제와 연관된 특별한 의미를 가진 문자를 사용하지 마십시오.  
  
 **-L**[**c**]  
 로컬로 구성된 서버 컴퓨터와 네트워크상에서 브로드캐스팅하는 서버 컴퓨터의 이름을 표시합니다. 이 매개 변수는 다른 매개 변수와 함께 사용할 수 없습니다. 표시할 수 있는 최대 서버 컴퓨터 수는 3000대입니다. 버퍼 크기 때문에 서버 목록이 잘린 경우 경고 메시지가 표시됩니다.  
  
> [!NOTE]  
>  네트워크에서 브로드캐스팅의 특성으로 인해 `sqlcmd`는 모든 서버로부터 시기 적절한 응답을 받지 못할 수 있습니다. 그러므로 반환되는 서버 목록은 이 옵션을 호출할 때마다 다를 수 있습니다.  
  
 옵션 매개 변수 **c** 를 지정하면 Servers: 머리글 없이 출력이 나타납니다. 그리고 각 서버 줄이 선행 공백 없이 나열됩니다. 이를 정리된 출력이라고 합니다. 정리된 출력은 스크립트 언어의 처리 성능을 향상시킵니다.  
  
 **-p**[**1**]  
 모든 결과 집합에 대한 성능 통계를 출력합니다. 다음은 성능 통계 형식의 예입니다.  
  
 `Network packet size (bytes): n`  
  
 `x xact[s]:`  
  
 `Clock Time (ms.): total       t1  avg       t2 (t3 xacts per sec.)`  
  
 각 항목이 나타내는 의미는 다음과 같습니다.  
  
 `x` = [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 처리되는 트랜잭션 수  
  
 `t1` = 모든 트랜잭션의 총 시간  
  
 `t2` = 단일 트랜잭션의 평균 시간  
  
 `t3` = 초당 평균 트랜잭션 수  
  
 모든 시간은 밀리초 단위입니다.  
  
 선택적 매개 변수 **1** 을 지정할 경우 통계의 출력 형식은 콜론으로 구분된 형식입니다. 이 형식은 스프레드시트로 쉽게 가져오거나 스크립트를 통해 처리할 수 있습니다.  
  
 선택적 매개 변수가 아닌 다른 값 이면 **1**에 오류가 생성 됩니다 및 `sqlcmd` 종료 합니다.  
  
 `-X`[**1**]  
 배치 파일에서 `sqlcmd`를 실행할 때 시스템 보안을 손상시킬 수 있는 명령을 사용할 수 없게 설정합니다. 사용할 수 없게 설정된 명령은 여전히 인식되지만 `sqlcmd`는 경고 메시지를 표시하고 계속 실행됩니다. 경우 선택적 매개 변수 **1** 지정 된 경우 `sqlcmd` 오류 메시지를 생성 하 고 종료 됩니다. `-X` 옵션을 사용하면 다음 명령이 사용할 수 없게 설정됩니다.  
  
-   **ED**  
  
-   **!!** *명령*  
  
 `-X` 옵션을 지정하면 환경 변수가 `sqlcmd`에 전달되지 않습니다. 또한 SQLCMDINI 스크립팅 변수를 사용하여 지정한 시작 스크립트가 실행되지 않습니다. 에 대 한 자세한 내용은 `sqlcmd` 스크립팅 변수를 참조 하세요 [스크립팅 변수와 함께 sqlcmd 사용](../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)합니다.  
  
 **-?**  
 `sqlcmd` 옵션의 구문 요약 정보를 표시합니다.  
  
## <a name="remarks"></a>Remarks  
 옵션은 구문 섹션에 표시된 순서대로 사용하지 않아도 됩니다.  
  
 여러 결과가 반환된 경우 `sqlcmd`는 일괄 처리의 각 결과 집합 사이에 빈 줄을 출력합니다. 또한는 "\<x > 영향을 받는 행" 실행 되는 문에 적용 되지 않는 경우 메시지가 나타나지 않습니다.  
  
 사용 하도록 `sqlcmd` 대화형으로 입력 `sqlcmd` 이 항목의 앞부분에서 설명 하는 옵션 중 하나 이상을 사용 하 여 명령 프롬프트에서. 자세한 내용은 [sqlcmd 유틸리티 사용](../relational-databases/scripting/sqlcmd-use-the-utility.md)을 참조하세요.  
  
> [!NOTE]  
>  옵션 **-L**, **-Q**, **-Z** 하거나 **-i** 발생 `sqlcmd` 실행 후 종료 합니다.  
  
 명령 환경(Cmd.exe)에서 모든 인수 및 확장 변수를 포함한 `sqlcmd` 명령줄의 총 길이는 운영 체제에서 Cmd.exe에 대해 지정한 길이입니다.  
  
## <a name="variable-precedence-low-to-high"></a>변수 우선 순위(낮은 순위에서 높은 순위)  
  
1.  시스템 수준 환경 변수  
  
2.  사용자 수준 환경 변수  
  
3.  명령 셸 (**설정할** X = Y) 실행 하기 전에 명령 프롬프트에서 설정한 `sqlcmd`합니다.  
  
4.  **sqlcmd-v** X=Y  
  
5.  **:Setvar** X Y  
  
> [!NOTE]  
>  환경 변수를 보려면 **제어판**에서 **시스템**을 연 다음 **고급** 탭을 클릭합니다.  
  
## <a name="sqlcmd-scripting-variables"></a>sqlcmd 스크립팅 변수  
  
|변수|관련 스위치|R/W|Default|  
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
|SQLCMDPACKETSIZE|-A|R|"4096"|  
|SQLCMDERRORLEVEL|-M|R/W|0|  
|SQLCMDMAXVARTYPEWIDTH|-y|R/W|"256"|  
|SQLCMDMAXFIXEDTYPEWIDTH|-y|R/W|"0" = 제한 없음|  
|SQLCMDEDITOR||R/W|"edit.com"|  
|SQLCMDINI||R|""|  
  
 SQLCMDUSER, SQLCMDPASSWORD 및 SQLCMDSERVER는 **:Connect**가  
  
 사용될 경우 설정됩니다.  
  
 R은 값이 프로그램 초기화 시 한 번만 설정될 수 있음을 나타냅니다.  
  
 R/W는 값이 **setvar** 명령을 사용하여 수정될 수 있으며 후속 명령이 새 값의 영향을 받을 수 있음을 나타냅니다.  
  
## <a name="sqlcmd-commands"></a>sqlcmd 명령  
 `sqlcmd`에서 [!INCLUDE[tsql](../includes/tsql-md.md)] 문 외에도 다음 명령을 사용할 수 있습니다.  
  
|||  
|-|-|  
|**GO** [*count*]|**:List**|  
|[**:**] **RESET**|**:Error**|  
|[**:**] **ED**|**:Out**|  
|[**:**] **!!**|**:Perftrace**|  
|[**:**] **QUIT**|**:Connect**|  
|[**:**] **EXIT**|**:On Error**|  
|**:r**|**:Help**|  
|**:ServerList**|**:XML** [**ON** &#124; **OFF**]|  
|**:Setvar**|**:Listvar**|  
  
 `sqlcmd` 명령을 사용할 때는 다음 사항에 주의하십시오.  
  
-   GO를 제외하고 모든 `sqlcmd` 명령에는 접두사로 콜론(:)을 붙여야 합니다.  
  
    > [!IMPORTANT]  
    >  **osql** 스크립트와의 호환성을 유지하기 위해 일부 명령은 콜론 없이도 인식됩니다. 이러한 명령은 [**:**]으로 표시됩니다.  
  
-   `sqlcmd` 명령은 줄 시작 부분에 나타난 경우에만 인식됩니다.  
  
-   모든 `sqlcmd` 명령은 대/소문자를 구분하지 않습니다.  
  
-   각 명령을 별도의 줄에 입력해야 합니다. 명령 다음에 [!INCLUDE[tsql](../includes/tsql-md.md)] 문이나 다른 명령을 입력할 수 없습니다.  
  
-   명령은 즉시 실행되며 [!INCLUDE[tsql](../includes/tsql-md.md)] 문처럼 실행 버퍼에 포함되지 않습니다.  
  
 **명령 편집**  
  [**:**] **ED**  
 텍스트 편집기를 시작합니다. 이 편집기를 사용하여 현재 [!INCLUDE[tsql](../includes/tsql-md.md)] 일괄 처리를 편집하거나 마지막으로 실행된 일괄 처리를 편집할 수 있습니다. 마지막으로 실행된 일괄 처리를 편집하려면 마지막 일괄 처리 실행을 마친 후 즉시 **ED** 명령을 입력해야 합니다.  
  
 텍스트 편집기는 SQLCMDEDITOR 환경 변수에 의해 정의됩니다. 기본 편집기는 'Edit'입니다. 편집기를 변경하려면 SQLCMDEDITOR 환경 변수를 설정합니다. 예를 들어 편집기를 [!INCLUDE[msCoName](../includes/msconame-md.md)] 메모장으로 설정하려면 명령 프롬프트에서 다음을 입력합니다.  
  
 `SET SQLCMDEDITOR=notepad`  
  
 [**:**] **RESET**  
 문 캐시를 지웁니다.  
  
 **:List**  
 문 캐시 내용을 출력합니다.  
  
 **변수**  
  **: Setvar** \< **var**> [ **"*`value`*"** ]  
 `sqlcmd` 스크립팅 변수를 정의합니다. 스크립팅 변수의 형식은 다음과 같습니다. `$(VARNAME)`.  
  
 변수 이름은 대/소문자를 구분하지 않습니다.  
  
 스크립팅 변수는 다음과 같은 방법으로 설정할 수 있습니다.  
  
-   명령줄 옵션을 사용하여 암시적으로 설정합니다. 예를 들어 합니다 **-l** 옵션은 SQLCMDLOGINTIMEOUT을 설정 `sqlcmd` 변수입니다.  
  
-   **:Setvar** 명령을 사용하여 명시적으로 설정합니다.  
  
-   `sqlcmd`를 실행하기 전에 환경 변수를 정의하여 설정합니다.  
  
> [!NOTE]  
>  `-X` 옵션은 환경 변수가 `sqlcmd`에 전달되지 않도록 합니다.  
  
 **:Setvar** 명령을 사용하여 정의한 변수와 환경 변수의 이름이 같을 경우 **:Setvar** 명령을 사용하여 정의한 변수가 우선적으로 적용됩니다.  
  
 변수 이름에는 공백 문자를 포함해서는 안 됩니다.  
  
 변수 이름은 $(var) 등의 변수 식과 다른 형식이어야 합니다.  
  
 스크립팅 변수의 문자열 값에 공백이 포함된 경우 값을 따옴표로 묶습니다. 스크립팅 변수 값을 지정하지 않으면 스크립팅 변수가 삭제됩니다.  
  
 **:Listvar**  
 현재 설정되어 있는 스크립팅 변수의 목록을 표시합니다.  
  
> [!NOTE]  
>  설정한 변수를 스크립팅 `sqlcmd`, 및를 사용 하 여 설정 되는 **: Setvar** 명령이 표시 됩니다.  
  
 **출력 명령**  
  **:Error**   
 ***\<***  *filename*  ***>|* STDERR|STDOUT**  
 *file name*에 지정된 파일, **stderr** 또는 **stdout**으로 모든 오류 출력을 리디렉션합니다. 스크립트에서 **Error** 명령이 여러 번 나타날 수 있습니다. 기본적으로 오류 출력은 **stderr**로 전송됩니다.  
  
 *file name*  
 출력을 받을 파일을 만들고 엽니다. 이 파일이 이미 있을 경우 0바이트로 잘립니다. 권한이나 기타 이유로 인해 이 파일을 사용할 수 없을 경우 출력이 전환되지 않으며 마지막으로 지정한 대상이나 기본 대상으로 전송됩니다.  
  
 **STDERR**  
 오류 출력을 **stderr** 스트림으로 전환합니다. 스트림을 리디렉션할 경우 리디렉션된 스트림 대상이 오류 출력을 받습니다.  
  
 **STDOUT**  
 오류 출력을 **stdout** 스트림으로 전환합니다. 스트림을 리디렉션할 경우 리디렉션된 스트림 대상이 오류 출력을 받습니다.  
  
 **:Out \<** *filename* **>**| **STDERR**| **STDOUT**  
 쿼리 결과를 만들어 *file name*에 지정된 파일, **stderr** 또는 **stdout**으로 모두 리디렉션합니다. 기본적으로 출력은 **stdout**으로 전송됩니다. 이 파일이 이미 있을 경우 0바이트로 잘립니다. 스크립트에서 **Out** 명령이 여러 번 나타날 수 있습니다.  
  
 **:Perftrace \<** *filename* **>**| **STDERR**| **STDOUT**  
 성능 추적 정보를 만들어 *file name*에 지정된 파일, **stderr** 또는 **stdout**으로 모두 리디렉션합니다. 기본적으로 성능 추적 출력은 **stdout**으로 전송됩니다. 이 파일이 이미 있을 경우 0바이트로 잘립니다. 스크립트에서 **Perftrace** 명령이 여러 번 나타날 수 있습니다.  
  
 **실행 제어 명령**  
  **: On Error**[ `exit`  |  `ignore`]  
 스크립트나 일괄 처리를 실행하는 동안 오류가 발생할 때 수행할 동작을 설정합니다.  
  
 `exit` 옵션을 사용하면 해당 오류 값이 표시되고 `sqlcmd`가 종료됩니다.  
  
 `ignore` 옵션을 사용하면 `sqlcmd`는 오류를 무시하고 일괄 처리 또는 스크립트를 계속 실행합니다. 기본적으로 오류 메시지가 출력됩니다.  
  
 [**:**] **QUIT**  
 `sqlcmd`를 끝냅니다.  
  
 [**:**] **끝내기**[ **(*`statement`*)** ]  
 `sqlcmd`의 반환 값에 SELECT 문의 결과를 사용할 수 있도록 합니다. 숫자일 경우 마지막 결과 행의 첫째 열은 4바이트 정수(long)로 변환됩니다. MS-DOS는 하위 바이트를 부모 프로세스 또는 운영 체제 오류 수준에 전달합니다. Windows 200x에서는 4바이트 정수 전체를 전달합니다. 구문은 다음과 같습니다.  
  
 `:EXIT(query)`  
  
 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
 `:EXIT(SELECT @@ROWCOUNT)`  
  
 **EXIT** 매개 변수를 배치 파일의 일부로 포함할 수도 있습니다. 예를 들어 명령 프롬프트에서 다음을 입력합니다.  
  
 `sqlcmd -Q "EXIT(SELECT COUNT(*) FROM '%1')"`  
  
 합니다 `sqlcmd` 유틸리티는 괄호 안에 있는 모든 보냅니다 **()** 서버. 시스템의 저장 프로시저가 설정을 선택하고 값을 반환하면 선택 내용만 반환됩니다. 괄호 사이에 아무것도 없는 EXIT **()** 문은 일괄 처리에서 이 문 앞에 나오는 모든 문을 실행한 후에 반환 값 없이 종료됩니다.  
  
 잘못된 쿼리를 지정하면 `sqlcmd`는 값을 반환하지 않고 종료됩니다.  
  
 다음은 EXIT 형식의 목록입니다.  
  
-   :EXIT  
  
 일괄 처리를 실행하지 않고 즉시 종료하며 값을 반환하지 않습니다.  
  
-   :EXIT( )  
  
 일괄 처리를 실행한 다음 종료하며 값을 반환하지 않습니다.  
  
-   :EXIT(query)  
  
 쿼리를 포함하는 일괄 처리를 실행하며 쿼리 결과를 반환한 다음 종료합니다.  
  
 `sqlcmd` 스크립트에 RAISERROR를 사용할 때 상태 127이 발생하면 `sqlcmd`가 종료되고 메시지 ID가 클라이언트에 반환됩니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
 `RAISERROR(50001, 10, 127)`  
  
 이 오류가 발생하면 `sqlcmd` 스크립트가 종료되고 메시지 ID 50001이 클라이언트에 반환됩니다.  
  
 1부터 -99까지의 반환 값은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 예약되어 있으므로 `sqlcmd`는 다음과 같은 추가 반환 값을 정의합니다.  
  
|반환 값|설명|  
|-------------------|-----------------|  
|-100|반환 값을 선택하기 전에 오류가 발생했습니다.|  
|-101|반환 값을 선택할 때 행을 찾을 수 없습니다.|  
|-102|반환 값을 선택할 때 변환 오류가 발생했습니다.|  
  
 **GO** [*count*]  
 GO는 일괄 처리의 끝을 알려 주고 캐시된 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 실행하도록 신호를 보냅니다. *count*값을 지정하면 캐시된 문이 *count* 에 지정한 횟수만큼 단일 일괄 처리로 실행됩니다.  
  
 **기타 명령**  
  **:r \<** *filename* **>**  
 추가 구문 분석 [!INCLUDE[tsql](../includes/tsql-md.md)] 문 및 `sqlcmd` 에서 지정한 파일에서 명령을 **< *`filename`* >** 문 캐시로 합니다.  
  
 파일에 [!INCLUDE[tsql](../includes/tsql-md.md)] 문이 포함되어 있고 뒤에 **GO**가 오지 않을 경우 **:r** 뒤에 오는 줄에 **GO**를 입력해야 합니다.  
  
> [!NOTE]  
>  **\<** *filename* **>** 시작 디렉터리를 기준으로 읽기 `sqlcmd` 실행 되었습니다.  
  
 일괄 처리 종결자가 나타난 후 이 파일이 읽혀지고 실행됩니다. 여러 **:r** 명령을 실행할 수 있습니다. 이 파일에는 모든 유형의 `sqlcmd` 명령이 포함될 수 있으며 그 예로 일괄 처리 종결자 **GO**를 들 수 있습니다.  
  
> [!NOTE]  
>  대화형 모드에서 표시되는 줄 수는 **:r** 명령이 나타날 때마다 1씩 증가합니다. **:r** 명령은 목록 명령의 출력에 나타납니다.  
  
 **:Serverlist**  
 로컬로 구성된 서버와 네트워크상에서 브로드캐스팅하는 서버의 이름을 표시합니다.  
  
 **:Connect**  *server_name*[**\\***instance_name*] [-l *timeout*] [-U *user_name* [-P *password*]]  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결합니다. 또한 현재 연결을 종료합니다.  
  
 제한 시간 옵션은 다음과 같습니다.  
  
|||  
|-|-|  
|0|무기한 대기|  
|n>0|n초 동안 대기|  
  
 SQLCMDSERVER 스크립팅 변수는 현재 활성 연결을 반영합니다.  
  
 *timeout* 을 지정하지 않으면 기본적으로 SQLCMDLOGINTIMEOUT 변수 값이 사용됩니다.  
  
 옵션이나 환경 변수로 *user_name* 만 지정하면 사용자에게 암호를 입력하라는 메시지가 표시됩니다. 이는 SQLCMDUSER 또는 SQLCMDPASSWORD 환경 변수를 설정한 경우 해당되지 않습니다. 옵션이나 환경 변수를 지정하지 않을 경우 로그인하는 데 Windows 인증 모드가 사용됩니다. 예를 들어 통합 보안을 사용하여 `instance1` [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 인스턴스인 `myserver`에 연결하려면 다음을 사용합니다.  
  
 `:connect myserver\instance1`  
  
 스크립팅 변수를 사용하여 `myserver` 의 기본 인스턴스에 연결하려면 다음을 사용합니다.  
  
 `:setvar myusername test`  
  
 `:setvar myservername myserver`  
  
 `:connect $(myservername) $(myusername)`  
  
 [**:**] **!!**  \< *명령*>  
 운영 체제 명령을 실행합니다. 운영 체제 명령을 실행하려면 느낌표 두 개(**!!**)로 줄을 시작하고 운영 체제 명령을 입력합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
 `:!! Dir`  
  
> [!NOTE]  
>  `sqlcmd`를 실행 중인 컴퓨터에서 명령이 실행됩니다.  
  
 **:XML** [**ON** | **OFF**]  
 자세한 내용은 이 항목의 뒷부분에 나오는 "XML 출력 형식"을 참조하십시오.  
  
 **:Help**  
 `sqlcmd` 명령과 각 명령에 대한 간단한 설명을 표시합니다.  
  
### <a name="sqlcmd-file-names"></a>sqlcmd 파일 이름  
 `sqlcmd` 입력된 파일을 사용 하 여 지정할 수는 **-i** 옵션 또는 **: r** 명령입니다. 출력 파일은 **-o** 옵션 또는 **:Error**, **:Out** 및 **:Perftrace** 명령을 사용하여 지정할 수 있습니다. 다음은 이러한 파일 작업에 대한 지침입니다.  
  
-   **: Error**, **: Out** 하 고 **: Perftrace** 별도 사용할지 **< *`filename`* >**. 하는 경우 동일한 **< *`filename`* >** 는 사용 하면 명령의 입력 섞일 수 있습니다.  
  
-   원격 서버에 있는 입력 파일을 로컬 컴퓨터에 있는 `sqlcmd`에서 호출할 경우 이 파일에 :out c:\OutputFile.txt와 같은 드라이브 파일 경로가 포함되어 있으면 출력 파일이 원격 서버가 아닌 로컬 컴퓨터에 생성됩니다.  
  
-   올바른 파일 경로의: c:\\**<*`filename`*>** 하십시오 \\ \\< Server\> \\ <$ 공유 >\\ **< *`filename`* >** 및 "C:\Some 폴더\\  **<  *`file name`*>**". 경로에 공백이 있을 경우 따옴표를 사용합니다.  
  
-   각각의 새 `sqlcmd` 세션은 이름이 같은 기존 파일을 덮어씁니다.  
  
### <a name="informational-messages"></a>정보 메시지  
 `sqlcmd`는 서버에서 보낸 모든 정보 메시지를 출력합니다. 다음 예에서는 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 실행한 후 정보 메시지가 출력됩니다.  
  
 명령 프롬프트에서 다음을 입력합니다.  
  
 `sqlcmd`  
  
 `At the sqlcmd prompt type:`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 Enter 키를 누르면 "데이터베이스 컨텍스트가 'AdventureWorks2012'로 변경되었습니다." 정보 메시지가 출력됩니다.  
  
### <a name="output-format-from-transact-sql-queries"></a>Transact-SQL 쿼리의 출력 형식  
 먼저 `sqlcmd`는 SELECT 목록에서 지정한 열 이름이 포함된 열 머리글을 출력합니다. 열 이름은 SQLCMDCOLSEP 문자로 구분됩니다. 기본적으로 구분 문자는 공백입니다. 열 이름이 열 너비보다 짧은 경우 출력은 다음 열까지 공백으로 채워집니다.  
  
 이 줄 다음에는 대시 문자로 이루어진 구분선이 삽입됩니다. 다음은 출력의 예입니다.  
  
 `sqlcmd`를 시작합니다. `sqlcmd` 명령 프롬프트에서 다음을 입력합니다.  
  
 `USE AdventureWorks2012;`  
  
 `SELECT TOP (2) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 ENTER를 누르면 다음 결과 집합이 반환 됩니다.  
  
 `BusinessEntityID FirstName    LastName`  
  
 `---------------- ------------ ----------`  
  
 `285              Syed         Abbas`  
  
 `293              Catherine    Abel`  
  
 `(2 row(s) affected)`  
  
 `BusinessEntityID` 열의 너비는 4자이지만 보다 긴 열 이름을 포함할 수 있도록 확장되었습니다. 기본적으로 출력은 80자에서 끝납니다. 그러나 **-w** 옵션을 사용하거나 SQLCMDCOLWIDTH 스크립팅 변수를 설정하여 이 값을 변경할 수 있습니다.  
  
### <a name="xml-output-format"></a>XML 출력 형식  
 FOR XML 절의 결과로 나오는 XML 출력은 연속 스트림에서 형식이 지정되지 않은 출력입니다.  
  
 XML 출력을 원하는 경우에는 `:XML ON`명령을 사용합니다.  
  
> [!NOTE]  
>  `sqlcmd`는 일반 형식으로 오류 메시지를 반환합니다. 오류 메시지는 XML 형식으로 XML 텍스트 스트림에도 출력됩니다. `:XML ON`을 사용할 경우 `sqlcmd`에서는 정보 메시지를 표시하지 않습니다.  
  
 XML 모드를 해제하려면 `:XML OFF`명령을 사용합니다.  
  
 XML OFF 명령은 `sqlcmd`를 다시 행 기반 출력으로 전환하기 때문에 GO 명령이 나타난 다음에 XML OFF 명령을 실행해야 합니다.  
  
 스트리밍된 XML 데이터와 행 집합 데이터를 혼합할 수 없습니다. XML 스트림을 출력하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 실행하기 전에 XML ON 명령을 실행하지 않은 경우 출력이 잘못됩니다. XML ON 명령을 실행한 경우 일반 행 집합을 출력하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 실행할 수 없습니다.  
  
> [!NOTE]  
>  **:XML** 명령은 SET STATISTICS XML 문을 지원하지 않습니다.  
  
## <a name="sqlcmd-best-practices"></a>sqlcmd를 위한 최선의 구현 방법  
 보안 및 효율성을 극대화하려면 다음 방법을 사용하십시오.  
  
-   통합 보안을 사용합니다.  
  
-   자동화된 환경에서 `-X`를 사용합니다.  
  
-   적절한 NTFS 파일 시스템 권한을 사용하여 입력 및 출력 파일을 보호합니다.  
  
-   성능을 향상시키려면 여러 세션 대신 한 번의 `sqlcmd` 세션에서 가능한 한 많은 작업을 수행합니다.  
  
-   일괄 처리 또는 쿼리를 실행하는 데 걸리는 예상 시간보다 높은 제한 시간 값을 일괄 처리 또는 쿼리 실행에 대해 설정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sqlcmd 유틸리티 시작](../relational-databases/scripting/sqlcmd-start-the-utility.md)   
 [sqlcmd를 사용하여 Transact-SQL 스크립트 파일 실행](../relational-databases/scripting/sqlcmd-run-transact-sql-script-files.md)   
 [sqlcmd 유틸리티 사용](../relational-databases/scripting/sqlcmd-use-the-utility.md)   
 [스크립팅 변수와 함께 sqlcmd 사용](../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)   
 [sqlcmd를 사용하여 데이터베이스 엔진에 연결](../relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md)   
 [쿼리 편집기로 SQLCMD 스크립트 편집](../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)   
 [작업 단계 관리](../ssms/agent/manage-job-steps.md)   
 [CmdExec 작업 단계 만들기](../ssms/agent/create-a-cmdexec-job-step.md)  
  
  
