---
title: 실행 패드 서비스와 SQL Server의 외부 스크립트 실행을 사용 하 여 일반적인 문제 | Microsoft Docs
ms.prod: sql
ms.technology: mlserver
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 5f770ce536dcbc29245d1b6e853a2548ab1ec744
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51701451"
---
# <a name="common-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>실행 패드 서비스와 SQL Server의 외부 스크립트 실행을 사용 하 여 일반적인 문제
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

 SQL Server 신뢰할 수 있는 실행 패드 서비스는 R 및 Python에 대 한 외부 스크립트 실행을 지원합니다. SP1에서 SQL Server 2016 R Services는 서비스를 제공합니다. SQL Server 2017 나타나며 설치의 일부로 실행 패드 서비스를 포함합니다.

여러 문제는 시작, 구성 문제 또는 변경 내용을 포함 하 여 또는 네트워크 프로토콜을 누락 하에서 실행 패드를 방지할 수 있습니다. 이 문서에서는 다양 한 문제에 대 한 문제 해결 지침을 제공합니다. 모든 하지 못한 것에 대 한 질문을 게시할 수는 [Machine Learning Server 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR)합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services

## <a name="determine-whether-launchpad-is-running"></a>실행 패드 실행 중인지 여부를 결정 합니다.

1. 엽니다는 **Services** 패널 (Services.msc). 또는 명령줄에서 입력 **SQLServerManager13.msc** 하거나 **SQLServerManager14.msc** 열려는 [SQL Server 구성 관리자](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)합니다.

2. 실행 패드에서 실행 되는 서비스 계정을 기록해 둡니다. R 또는 Python이 사용 되는 각 인스턴스에 고유한 인스턴스의 실행 패드 서비스가 있어야 합니다. 예를 들어, 명명 된 인스턴스에 대 한 서비스와 같이 수 있습니다 _MSSQLLaunchpad$ InstanceName_합니다.

3. 서비스를 중지 하면 다시 시작 합니다. 다시 시작 하면, 구성 사용 하 여 문제가 있으면 시스템 이벤트 로그에 메시지를 게시 하 고 서비스 다시 중지 됩니다. 서비스가 중지 되는 이유에 대 한 자세한 내용은 시스템 이벤트 로그를 확인 합니다.

4. RSetup.log의 내용을 검토 및 설치에 오류가 없는지 확인 합니다. 예를 들어, 메시지 *종료 코드 0 사용 하 여* 시작 서비스의 실패를 나타냅니다.

5. 다른 오류를 찾으려면 rlauncher.log의 내용을 검토 합니다.

## <a name="check-the-launchpad-service-account"></a>실행 패드 서비스 계정 확인

기본 서비스 계정은 수 "NT Service\$SQL2016" 또는 "NT Service\$SQL2017" 있습니다. 마지막 부분은 SQL 인스턴스 이름에 따라 달라질 수 있습니다.

실행 패드 서비스 (Launchpad.exe) 낮은 서비스 계정을 사용 하 여 실행 합니다. 그러나 R 및 Python을 시작 하 고 데이터베이스 인스턴스와 통신 하 실행 패드 서비스 계정에 다음 사용자 권한이 필요 합니다.

- 서비스로 로그온(SeServiceLogonRight)
- 프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)
- 트래버스 검사 무시(SeChangeNotifyPrivilege)
- (SeIncreaseQuotaSizePrivilege) 프로세스의 메모리 할당량 조정

이러한 사용자 권한에 대 한 자세한 내용은 "Windows 사용 권한 및 권한" 섹션을 참조 하세요 [구성 하는 Windows 서비스 계정 및 권한](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)합니다.

> [!TIP]
> SQL Server 진단에 대 한 지원 진단 플랫폼 (SDP) 도구를 사용 하 여 잘 알고 있다면 MachineName_UserRights.txt 이름의 출력 파일을 검토 하려면 SDP를 사용할 수 있습니다.

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>실행 패드에 대 한 사용자 그룹에 로컬로 로그온 수 없습니다.

SQL Server Machine Learning 서비스를 설치 하는 동안 Windows 사용자 그룹을 만듭니다 **SQLRUserGroup** 고 다음 SQL Server에 연결 하 고 외부 스크립트 작업을 실행 하려면 실행 패드에 필요한 모든 권한이 포함 된 프로 비전 합니다. 이 사용자 그룹을 사용 하는 경우 Python 스크립트를 실행 하도 사용 됩니다.

그러나 더 제한적인 보안 정책이 적용 되는 조직에서이 그룹에 필요한 권한을 수동으로 제거 되었거나, 또는 정책에 따라 자동으로 취소 될 수 있습니다. 권한을 제거 되었거나, 실행 패드 SQL server에 더 이상 연결할 수 없습니다 하 고 SQL Server 외부 런타임을 호출할 수 없습니다.

문제를 해결하려면 그룹 **SQLRUserGroup**에 시스템 권한 **로컬 로그온 허용**이 있는지 확인합니다.

자세한 내용은 [구성 하는 Windows 서비스 계정 및 권한](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)합니다.

## <a name="permissions-to-run-external-scripts"></a>외부 스크립트를 실행 하는 권한

실행 패드를 올바르게 구성한 경우에 사용자 R 또는 Python 스크립트를 실행할 수 있는 권한이 없는 경우 오류를 반환 합니다.

데이터베이스 관리자는 SQL Server를 설치한 경우 데이터베이스 소유자 인 경우이 권한이 자동으로 부여 됩니다. 그러나 다른 사용자가 일반적으로 더 제한적인 권한을 가집니다. R 스크립트를 실행 하려고 할 경우 실행 패드 오류를 받게 됩니다.

SQL Server Management studio에서 문제를 해결 하려면 보안 관리자가 SQL 로그인 또는 Windows 사용자 계정이 다음 스크립트를 실행 하 여 수정할 수 있습니다.

```SQL
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

자세한 내용은 [권한 부여 (Transact SQL](../t-sql/statements/grant-transact-sql.md)합니다.

## <a name="common-launchpad-errors"></a>실행 패드의 일반적인 오류

이 섹션에는 실행 패드를 반환 하는 가장 일반적인 오류 메시지를 나열 합니다.

## <a name="unable-to-launch-runtime-for-r-script"></a>"R 스크립트에 대해 런타임을 시작할 수 없습니다."

(또한 Python 사용)는 R 사용자에 대 한 Windows 그룹 R Services를 실행 하는 인스턴스에 로그온 할 수 없습니다, 하는 경우 다음 오류가 표시 될 수 있습니다.

- R 스크립트를 실행 하려고 할 때 발생 한 오류:

    * *'R' 스크립트에 대해 런타임을 시작할 수 없습니다. 'R' 런타임의 구성을 확인하세요.*

    * *외부 스크립트 오류가 발생했습니다. 런타임을 시작할 수 없습니다.*

- 생성 된 오류는 [!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)] 서비스:

    * *시작 관리자 RLauncher.dll을 초기화하지 못했습니다.*

    * *등록된 시작 관리자 dll이 없습니다!*

    * *NT 서비스 계정에 로그온 할 수 없음을 나타내는 보안 로그*

이 사용자 그룹에 필요한 권한을 부여 하는 방법에 대 한 정보를 참조 하세요 [SQL Server 2016 R Services 설치](install/sql-r-services-windows-install.md)합니다.

> [!NOTE]
> SQL 로그인을 사용하여 원격 워크스테이션에서 R 스크립트를 실행하는 경우에는 이 제한이 적용되지 않습니다.

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>"로그온 실패: 사용자가 요청된 된 로그온 유형을 허가 받지"

기본적으로 [!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)] 계정을 사용 하 여 시작 시: `NT Service\MSSQLLaunchpad`합니다. 계정으로 구성 됩니다 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 필요한 모든 권한이를 설치 합니다.

실행 패드에 다른 계정을 할당 또는 SQL Server 컴퓨터의 정책에 의해 제거 된 경우 계정에 필요한 권한이 없을 하 고이 오류가 발생할 수 있습니다.

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385(0x569) 로그온 실패: 사용자는 이 컴퓨터에서는 요청된 로그온 유형을 허가받지 않았습니다.*

새 서비스 계정에 필요한 권한을 부여 하려면 로컬 보안 정책 응용 프로그램을 사용 하 고 다음 사용 권한을 포함 하는 계정에 대 한 권한을 업데이트.

+ 프로세스의 메모리 할당량 조정(SeIncreaseQuotaPrivilege)
+ 트래버스 검사 무시(SeChangeNotifyPrivilege)
+ 서비스로 로그온(SeServiceLogonRight)
+ 프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>"실행 패드 서비스와 통신할 수 없습니다."

설치 하 고 다음 machine learning을 사용 하도록 설정 하지만 R 또는 Python 스크립트를 실행 하려고 할 때이 오류가 발생 하면 실행 인스턴스에 대 한 실행 패드 서비스 중지 될 수 있습니다.

1. Windows 명령 프롬프트에서 SQL Server 구성 관리자를 엽니다. 자세한 내용은 [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)을 참조하세요.

2. 예를 들어 SQL Server 실행 패드를 마우스 오른쪽 단추로 클릭 하 고 선택한 **속성**합니다.

3. 선택 된 **서비스** 탭 한 다음 서비스가 실행 되 고 있는지를 확인 합니다. 실행 하지 않는 경우 변경 합니다 **시작 모드** 하 **자동**를 선택한 후 **적용**.

4. 기계 학습 스크립트를 실행할 수 있도록 문제를 해결을 일반적으로 서비스를 다시 시작 합니다. 다시 시작에는 문제가 해결 되지 않으면, 경로 및 인수를 확인 합니다 **이진 경로** 속성과 다음을 수행:

    1. 실행 프로그램의.config 파일을 검토 하 고 작업 디렉터리가 올바른지 확인 하십시오.

    2. 에 설명 된 대로 실행 패드에서 사용 되는 Windows 그룹에 SQL Server 인스턴스에 연결할 수 있는지 확인 합니다 [이전 섹션](#bkmk_LaunchpadTS)합니다.

    c. 서비스 속성을 변경 하면 실행 패드 서비스를 다시 시작 합니다.

## <a name="fatal-error-creation-of-tmpfile-failed"></a>"심각한 오류 tmpFile 만들지가 못했습니다."

이 시나리오에서는 machine learning 기능을 성공적으로 설치 및 실행 패드가 실행 중이면 합니다. 몇 가지 간단한 R 또는 Python 코드를 실행 하려고 하지만 실행 패드 다음과 같은 오류로 인해 실패 합니다. 

>*R 스크립트의 런타임과 통신할 수 없습니다. R 런타임의 요구 사항을 확인 하세요.*

동시에, 외부 스크립트 런타임 STDERR 메시지의 일부로 다음 메시지를 작성합니다. 

>*심각한 오류: 실패 한 tmpfile 생성 합니다.*

이 오류는 실행 패드에서 사용 하려고 하는 계정에 데이터베이스에 로그온 할 권한이 없는지를 나타냅니다. 이 경우에는 엄격한 보안 정책을 구현 될 때 발생할 수 있습니다. 이 경우 인지를 확인 하려면 SQL Server 로그를 검토 및 확인 MSSQLSERVER01 계정 로그인 시 거부 되었습니다 여부를 확인 합니다. R 관련 된 로그에 동일한 정보가 제공 됩니다\_서비스나 PYTHON\_서비스입니다. ExtLaunchError.log 찾습니다.

기본적으로 20 개의 계정이 설정 되며 MSSQLSERVER20 통해 MSSQLSERVER01 이름의 Launchpad.exe 프로세스와 연결 합니다. R 또는 Python를 많이 사용 한다면 계정 수를 늘릴 수 있습니다.

이 문제를 해결 하려면 그룹에 있는지 확인 *로컬 로그온 허용* 기계 학습 기능이 있는 설치 및 사용 하도록 설정 된 로컬 인스턴스에 대 한 사용 권한. 일부 환경에서는이 권한 수준에는 네트워크 관리자에서 GPO 예외를 요구할 수 있습니다.

## <a name="not-enough-quota-to-process-this-command"></a>"이이 명령을 처리할 수 할당량이 충분 하지 않습니다"

이 오류는 몇 가지 작업 중 하나를 의미할 수 있습니다.

- 실행 패드 외부 쿼리를 실행 하려면 부족 하 여 외부 사용자가 있을 수 있습니다. 예를 들어, 20 개가 넘는 외부 쿼리를 동시에 실행 중인 20 명의 기본 사용자만 되 고 하나 이상의 쿼리가 실패할 수 있습니다.

- 메모리가 부족 하 여 R 작업을 처리 하는 데 사용할 수 있는 경우 이 오류는 SQL Server 사용 중일 수 컴퓨터 리소스의 최대 70%는 기본 환경에서 가장 자주 발생 합니다. R에서 리소스의 사용을 지원 하기 위해 서버 구성을 수정 하는 방법에 대 한 정보를 참조 하세요 [R 코드 운영 화](r/operationalizing-your-r-code.md)합니다.

## <a name="cant-find-package"></a>"패키지를 찾을 수 없습니다"

SQL Server에서 R 코드를 실행 하 고이 메시지가 있지만 SQL Server 외부 동일한 코드를 실행 했을 때 메시지를 가져오지 않은 경우 패키지를 SQL Server에서 사용 하는 기본 라이브러리 위치에 설치 되지 않았는지를 의미 합니다.

이 오류는 여러 가지 방법으로 발생할 수 있습니다.

- 서버에서 새 패키지를 설치 하지만 R 사용자 라이브러리에 패키지를 설치 하므로 액세스가 거부 되었습니다.

- R Services 설치 및 다음 다른 R 도구 설치 사용자나 라이브러리, Microsoft R Server (독립 실행형)를 Microsoft R Client RStudio를 포함 하 여 설정 및 등입니다.

인스턴스에서 사용 되는 R 패키지 라이브러리의 위치를 확인 하려면 SQL Server Management Studio를 엽니다 (또는 다른 데이터베이스 쿼리 도구)를 인스턴스에 연결 하 고 다음 저장된 프로시저를 실행 하십시오.

```SQL
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>샘플 결과

*STDOUT message(s) from external script:*

*[1] "c:\\프로그램 파일\\Microsoft SQL Server\\MSSQL13. SQL2016\\R_SERVICES "*

*[1] "c: / Program Files/Microsoft SQL Server/MSSQL13. 라이브러리 "SQL2016/R_SERVICES*

문제를 해결 하려면 SQL Server 인스턴스 라이브러리에 패키지 다시 설치 해야 합니다.

>[!NOTE]
>최신 버전의 Microsoft R을 사용 하려면 SQL Server 2016의 인스턴스를 업그레이드 한 경우에 기본 라이브러리 위치를 다릅니다. 자세한 내용은 [R services 인스턴스를 업그레이드 하려면 사용 하 여 SqlBindR](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>실행 패드가 일치 하지 않는 Dll 인해 종료

다른 기능을 서버에 패치를 사용 하 여 데이터베이스 엔진을 설치 하 고 다음 원본 미디어를 사용 하 여 나중에 Machine Learning 기능을 추가 하는 경우에 잘못 된 버전의 Machine Learning 구성 요소를 설치할 수 있습니다. 버전 불일치를 발견 하는 실행 패드를 종료 하 고 덤프 파일을 만듭니다.

이 문제를 방지 하려면 서버 인스턴스와 동일한 패치 수준에서 새 기능을 설치 해야 합니다.

**업그레이드에 잘못 된 방법.**

1. R Services 없이 SQL Server 2016을 설치 합니다.
2. SQL Server 2016 용 누적 업데이트 2를 업그레이드 합니다.
3. RTM 미디어를 사용 하 여 R Services (In-database)를 설치 합니다.

**업그레이드 하는 올바른 방법:**

1. R Services 없이 SQL Server 2016을 설치 합니다.
2. 원하는 패치 수준으로 SQL Server 2016을 업그레이드 합니다. 예를 들어, 서비스 팩 1 및 누적 업데이트 2를 설치 합니다.
3. 정확한 패치 수준에서 기능을 추가할 SP1 CU2 설치를 다시 실행 하 고 R Services (In-database)를 선택 합니다. 

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>실행 패드 8dot3 표기법 필요한 경우 시작 실패

> [!NOTE] 
> 이전 시스템에서 실행 패드는 8dot3 표기법 요구 사항이 있는 경우 시작에 실패할 수 있습니다. 이 요구 사항은 이후 릴리스에서 제거 되었습니다. SQL Server 2016 R Services 고객은 다음 중 하나를 설치 해야 합니다.
> * SQL Server 2016 SP1 및 CU1: [SQL Server 용 누적 업데이트 1](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1)합니다.
> * SQL Server 2016 RTM, 누적 업데이트 3 및이 [핫픽스](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3), 요청 시 사용할 수 있는 합니다.

R 사용 하 여 호환성을 위해 SQL Server 2016 R Services (In-database)를 사용 하 여 짧은 파일 이름을 생성을 지원 하도록 기능이 설치 되어 있는 드라이브를 필요한 *8dot3 표기법*합니다. 8.3 파일 이름을 라고는 *약식 파일 이름을*, 또는 긴 파일 이름에는 대 안으로 Microsoft Windows의 이전 버전과 호환성을 위해 사용 됩니다.

R 설치 하는 볼륨에서 짧은 파일 이름을 지원 하지 않습니다, 경우에 SQL Server에서 R을 시작 하는 프로세스를 올바른 실행 파일을 찾을 수 되지 않을 수 있으며 실행 패드 시작 되지 않습니다.

대 안으로 SQL Server를 설치한 및 R Services가 설치 된 볼륨에서 8dot3 표기법을 사용할 수 있습니다. 그런 다음 R Services 구성 파일에서 작업 디렉터리의 짧은 이름을 제공해야 합니다.

1. 8dot3 표기법을 사용 하도록 설정 하려면 함께 fsutil 유틸리티를 실행 합니다 *8dot3name* 여기에 설명 된 대로 인수: [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)합니다.

2. 8dot3 표기법을 사용 하는 후 RLauncher.config 파일을 열고의 속성을 `WORKING_DIRECTORY`입니다. 이 파일을 찾는 방법에 대 한 자세한 내용은 [기계 학습 문제 해결에 대 한 데이터 수집](data-collection-ml-troubleshooting-process.md)합니다.

3. 함께 fsutil 유틸리티를 사용 합니다 *파일* WORKING_DIRECTORY에 지정 된 폴더에 대 한 짧은 파일 경로 지정 하는 인수입니다.

4. WORKING_DIRECTORY 속성에 입력 하는 동일한 작업 디렉터리를 지정 하도록 구성 파일을 편집 합니다. 또는 다른 작업 디렉터리를 지정 수 있으며 8dot3 표기법을 사용 하 여 호환 이미 있는 기존 경로 선택할 수 있습니다.


## <a name="next-steps"></a>다음 단계

[Machine Learning Services 문제 해결 및 알려진된 문제](machine-learning-troubleshooting-faq.md)

[기계 학습 문제 해결에 대 한 데이터 수집](data-collection-ml-troubleshooting-process.md)

[업그레이드 및 설치 FAQ](r/upgrade-and-installation-faq-sql-server-r-services.md)

[데이터베이스 엔진 연결 문제 해결](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
