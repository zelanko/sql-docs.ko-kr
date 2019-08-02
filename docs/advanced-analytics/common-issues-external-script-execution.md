---
title: 실행 패드 서비스 및 외부 스크립트 실행에 대 한 일반적인 문제
ms.prod: sql
ms.technology: ''
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c90c59f3b59850bb0e2d1cf4cf40eb569e965eba
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715280"
---
# <a name="common-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>SQL Server에서 실행 패드 서비스 및 외부 스크립트 실행에 대 한 일반적인 문제
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 신뢰할 수 있는 실행 패드 서비스는 R 및 Python에 대 한 외부 스크립트 실행을 지원 합니다. 

여러 문제로 인해 구성 문제나 변경 또는 누락 된 네트워크 프로토콜을 포함 하 여 실행 패드를 시작할 수 없습니다. 이 문서에서는 다양 한 문제에 대 한 문제 해결 지침을 제공 합니다. 놓친 경우 [Machine Learning Server 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR)에 질문을 게시할 수 있습니다.

## <a name="determine-whether-launchpad-is-running"></a>실행 패드 실행 여부 확인

1. **서비스** 패널 (services.msc)을 엽니다. 또는 명령줄에서 **sqlservermanager13.msc** 또는 **SQLServerManager14** 를 입력 하 여 [SQL Server 구성 관리자](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)를 엽니다.

2. 실행 패드를 실행 하는 서비스 계정을 적어 둡니다. R 또는 Python을 사용 하도록 설정 된 각 인스턴스에는 실행 패드 서비스의 고유한 인스턴스가 있어야 합니다. 예를 들어 명명 된 인스턴스에 대 한 서비스는 _MSSQLLaunchpad $ InstanceName_과 같을 수 있습니다.

3. 서비스가 중지 된 경우 다시 시작 합니다. 다시 시작할 때 구성에 문제가 있으면 시스템 이벤트 로그에 메시지가 게시 되 고 서비스가 다시 중지 됩니다. 서비스가 중지 된 이유에 대 한 자세한 내용은 시스템 이벤트 로그를 확인 하십시오.

4. RSetup의 내용을 검토 하 고 설치에 오류가 없는지 확인 합니다. 예를 들어 *코드 0으로 종료* 하는 메시지는 서비스를 시작 하지 못했음을 나타냅니다.

5. 다른 오류를 확인 하려면 rlauncher. .log의 내용을 검토 하십시오.

## <a name="check-the-launchpad-service-account"></a>실행 패드 서비스 계정 확인

기본 서비스 계정은 "nt service\$SQL2016" 또는 "nt service\$SQL2017" 일 수 있습니다. 최종 부분은 SQL 인스턴스 이름에 따라 다를 수 있습니다.

실행 패드 서비스 (실행 패드)는 낮은 권한 서비스 계정을 사용 하 여 실행 됩니다. 그러나 R 및 Python을 시작 하 고 데이터베이스 인스턴스와 통신 하려면 실행 패드 서비스 계정에 다음 사용자 권한이 필요 합니다.

- 서비스로 로그온(SeServiceLogonRight)
- 프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)
- 트래버스 검사 무시(SeChangeNotifyPrivilege)
- 프로세스의 메모리 할당량 조정 (SeIncreaseQuotaSizePrivilege)

이러한 사용자 권한에 대 한 자세한 내용은 [windows 서비스 계정 및 권한 구성](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)의 "windows 권한 및 권한" 섹션을 참조 하세요.

> [!TIP]
> SQL Server 진단에 대해 SDP (지원 진단 플랫폼) 도구를 사용 하는 방법을 잘 알고 있는 경우에는 SDP를 사용 하 여 이름이 MachineName_UserRights 인 출력 파일을 검토할 수 있습니다.

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>실행 패드에 대 한 사용자 그룹은 로컬로 로그온 할 수 없습니다.

Machine Learning Services를 설치 하는 동안 Windows 사용자 그룹 **SQLRUserGroup** SQL Server 만든 다음 실행 패드에 SQL Server 연결 하 여 외부 스크립트 작업을 실행 하는 데 필요한 모든 권한으로 프로 비전 합니다. 이 사용자 그룹을 사용 하는 경우 Python 스크립트를 실행 하는 데도 사용 됩니다.

그러나 더 제한적인 보안 정책이 적용 되는 조직에서는이 그룹에 필요한 권한이 수동으로 제거 되었거나 정책에 의해 자동으로 취소 될 수 있습니다. 권한이 제거 된 경우 실행 패드는 더 이상 SQL Server에 연결할 수 없으며, SQL Server 외부 런타임을 호출할 수 없습니다.

문제를 해결하려면 그룹 **SQLRUserGroup**에 시스템 권한 **로컬 로그온 허용**이 있는지 확인합니다.

자세한 내용은 [Windows 서비스 계정 및 권한 구성](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.

## <a name="permissions-to-run-external-scripts"></a>외부 스크립트를 실행할 수 있는 권한

실행 패드를 올바르게 구성 했더라도 사용자에 게 R 또는 Python 스크립트를 실행할 수 있는 권한이 없는 경우 오류가 반환 됩니다.

데이터베이스 관리자 권한으로 SQL Server를 설치 했거나 사용자가 데이터베이스 소유자 인 경우이 권한이 자동으로 부여 됩니다. 그러나 다른 사용자에 게는 일반적으로 보다 제한적인 사용 권한이 있습니다. R 스크립트를 실행 하려고 하면 실행 패드 오류가 발생 합니다.

문제를 해결 하기 위해 SQL Server Management Studio 보안 관리자는 다음 스크립트를 실행 하 여 SQL 로그인 또는 Windows 사용자 계정을 수정할 수 있습니다.

```sql
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

자세한 내용은 [GRANT (transact-sql](../t-sql/statements/grant-transact-sql.md)을 참조 하세요.

## <a name="common-launchpad-errors"></a>일반적인 실행 패드 오류

이 섹션에서는 실행 패드에서 반환 하는 가장 일반적인 오류 메시지를 나열 합니다.

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="unable-to-launch-runtime-for-r-script"></a>"R 스크립트에 대해 런타임을 시작할 수 없습니다."

R 사용자에 대 한 Windows 그룹 (Python에도 사용 됨)이 R Services를 실행 하는 인스턴스에 로그온 할 수 없는 경우 다음과 같은 오류가 표시 될 수 있습니다.

- R 스크립트를 실행 하려고 할 때 생성 되는 오류:

    * *'R' 스크립트에 대해 런타임을 시작할 수 없습니다. 'R' 런타임의 구성을 확인하세요.*

    * *외부 스크립트 오류가 발생했습니다. 런타임을 시작할 수 없습니다.*

- [!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)] 서비스에서 생성 된 오류:

    * *시작 관리자 RLauncher.dll을 초기화하지 못했습니다.*

    * *등록된 시작 관리자 dll이 없습니다!*

    * *계정 NT 서비스에서 로그온 할 수 없음을 나타내는 보안 로그*

이 사용자 그룹에 필요한 권한을 부여 하는 방법에 대 한 자세한 내용은 [Install SQL Server R Services](install/sql-r-services-windows-install.md)를 참조 하세요.

> [!NOTE]
> SQL 로그인을 사용하여 원격 워크스테이션에서 R 스크립트를 실행하는 경우에는 이 제한이 적용되지 않습니다.
::: moniker-end

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>"로그온 실패: 사용자에 게 요청 된 로그온 유형이 부여 되지 않았습니다."

기본적으로는 [!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)] `NT Service\MSSQLLaunchpad`시작 시 다음 계정을 사용 합니다. 이 계정은 설치 프로그램에서 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 필요한 모든 권한을 갖도록 구성 됩니다.

실행 패드에 다른 계정을 할당 하거나 SQL Server 컴퓨터의 정책에 의해 권한이 제거 된 경우 계정에 필요한 권한이 없을 수 있으며 다음 오류가 표시 될 수 있습니다.

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385(0x569) 로그온 실패: 사용자는 이 컴퓨터에서는 요청된 로그온 유형을 허가받지 않았습니다.*

새 서비스 계정에 필요한 사용 권한을 부여 하려면 로컬 보안 정책 응용 프로그램을 사용 하 고 다음 사용 권한을 포함 하도록 계정에 대 한 사용 권한을 업데이트 합니다.

+ 프로세스의 메모리 할당량 조정(SeIncreaseQuotaPrivilege)
+ 트래버스 검사 무시(SeChangeNotifyPrivilege)
+ 서비스로 로그온(SeServiceLogonRight)
+ 프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>"실행 패드 서비스와 통신할 수 없습니다."

을 설치 하 고 machine learning을 사용 하도록 설정 했지만 R 또는 Python 스크립트를 실행 하려고 할 때이 오류가 발생 하는 경우 인스턴스에 대 한 실행 패드 서비스가 실행 중지 되었을 수 있습니다.

1. Windows 명령 프롬프트에서 SQL Server 구성 관리자를 엽니다. 자세한 내용은 [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)을 참조하세요.

2. 인스턴스에 대 한 SQL Server 실행 패드를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 선택 합니다.

3. **서비스** 탭을 선택 하 고 서비스가 실행 중인지 확인 합니다. 실행 되 고 있지 않으면 **시작 모드** 를 **자동**으로 변경 하 고 **적용**을 선택 합니다.

4. 서비스를 다시 시작 하면 일반적으로 문제를 해결 하 여 machine learning 스크립트를 실행할 수 있습니다. 다시 시작 해도 문제가 해결 되지 않으면 **이진 경로** 속성의 경로와 인수를 확인 하 고 다음을 수행 합니다.

    a. 시작 관리자의 .config 파일을 검토 하 고 작업 디렉터리가 올바른지 확인 합니다.

    b. 실행 패드에서 사용 되는 Windows 그룹이 SQL Server 인스턴스에 연결할 수 있는지 확인 합니다.

    c. 서비스 속성을 변경 하는 경우 실행 패드 서비스를 다시 시작 합니다.

## <a name="fatal-error-creation-of-tmpfile-failed"></a>"TmpFile의 심각한 오류를 만들지 못했습니다."

이 시나리오에서는 machine learning 기능을 성공적으로 설치 하 고 실행 패드를 실행 합니다. 몇 가지 간단한 R 또는 Python 코드를 실행 하려고 하지만 실행 패드는 다음과 같은 오류와 함께 실패 합니다. 

>*R 스크립트에 대 한 런타임과 통신할 수 없습니다. R 런타임의 요구 사항을 확인 하세요.*

동시에 외부 스크립트 런타임은 STDERR 메시지의 일부로 다음 메시지를 기록 합니다. 

>*심각한 오류: tmpfile를 만들지 못했습니다.*

이 오류는 실행 패드에서 사용 하려고 하는 계정에 데이터베이스에 로그온 할 수 있는 권한이 없음을 나타냅니다. 엄격한 보안 정책을 구현할 때 이러한 상황이 발생할 수 있습니다. 이 경우에 해당 하는지 확인 하려면 SQL Server 로그를 검토 하 고 로그인 시 MSSQLSERVER01 계정이 거부 되었는지 확인 하십시오. R\_services 또는 PYTHON\_서비스와 관련 된 로그에 동일한 정보가 제공 됩니다. ExtLaunchError .log를 찾습니다.

기본적으로 20 개의 계정이 설정 되 고 실행 패드 프로세스와 연결 되며 이름이 MSSQLSERVER01에서 MSSQLSERVER20로 설정 됩니다. R 또는 Python을 과도 하 게 사용 하는 경우 계정 수를 늘릴 수 있습니다.

이 문제를 해결 하려면 그룹에 machine learning 기능이 설치 되 고 사용 하도록 설정 된 로컬 인스턴스에 대 한 *로컬 로그온 허용* 권한이 있는지 확인 합니다. 일부 환경에서는이 권한 수준에서 네트워크 관리자의 GPO 예외가 필요할 수 있습니다.

## <a name="not-enough-quota-to-process-this-command"></a>"이 명령을 처리 하기에 충분 한 할당량이 없습니다."

이 오류는 다음과 같은 여러 가지 중 하나를 의미할 수 있습니다.

- 실행 패드에 외부 사용자가 외부 쿼리를 실행 하는 데 충분 하지 않을 수 있습니다. 예를 들어 20 개가 넘는 외부 쿼리를 동시에 실행 하는 경우 20 개의 기본 사용자만 있는 경우 하나 이상의 쿼리가 실패할 수 있습니다.

- R 태스크를 처리 하는 데 사용할 수 있는 메모리가 부족 합니다. 이 오류는 기본 환경에서 가장 자주 발생 합니다 .이 경우 SQL Server는 컴퓨터 리소스의 최대 70%까지 사용할 수 있습니다. R에서 더 많은 리소스 사용을 지원 하도록 서버 구성을 수정 하는 방법에 대 한 자세한 내용은 [r 코드 운영 화](r/operationalizing-your-r-code.md)을 참조 하세요.

## <a name="cant-find-package"></a>"패키지를 찾을 수 없음"

SQL Server에서 R 코드를 실행 하 고이 메시지를 가져오지만 SQL Server 외부에서 동일한 코드를 실행할 때 메시지를 가져오지 못한 경우 SQL Server에서 사용 하는 기본 라이브러리 위치에 패키지가 설치 되지 않았음을 의미 합니다.

이 오류는 다음과 같은 여러 가지 방법으로 발생할 수 있습니다.

- 서버에 새 패키지를 설치 했지만 액세스가 거부 되었으므로 R은 사용자 라이브러리에 패키지를 설치 했습니다.

- R Services를 설치한 후 Microsoft R Server (독립 실행형), Microsoft R Client, RStudio 등을 비롯 한 다른 R 도구나 라이브러리 집합을 설치 했습니다.

인스턴스에 사용 되는 R 패키지 라이브러리의 위치를 확인 하려면 SQL Server Management Studio (또는 다른 데이터베이스 쿼리 도구)를 열고 인스턴스에 연결한 후 다음 저장 프로시저를 실행 합니다.

```sql
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>샘플 결과

*STDOUT message(s) from external script:*

*[1] "C:\\프로그램 파일\\Microsoft SQL Server\\MSSQL13. SQL2016\\R_SERVICES "*

*[1] "C:/Program Files/Microsoft SQL Server/MSSQL13.SQL2016/R_SERVICES/library"*

이 문제를 해결 하려면 패키지를 SQL Server 인스턴스 라이브러리에 다시 설치 해야 합니다.

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
>[!NOTE]
>SQL Server 2016의 인스턴스를 업그레이드 하 여 최신 버전의 Microsoft R을 사용 하는 경우 기본 라이브러리 위치는 다릅니다. 자세한 내용은 [SqlBindR을 사용 하 여 R Services 인스턴스 업그레이드](install/upgrade-r-and-python.md)를 참조 하세요.
::: moniker-end

::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"
## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>Dll이 일치 하지 않아 실행 패드 종료

다른 기능을 사용 하 여 데이터베이스 엔진을 설치 하는 경우 서버를 패치 한 후 나중에 원본 미디어를 사용 하 여 Machine Learning 기능을 추가 하면 잘못 된 버전의 Machine Learning 구성 요소가 설치 될 수 있습니다. 실행 패드에서 버전이 일치 하지 않는 것을 감지 하면 종료 하 고 덤프 파일을 만듭니다.

이 문제를 방지 하려면 서버 인스턴스와 동일한 패치 수준에서 새 기능을 설치 해야 합니다.

**잘못 된 업그레이드 방법:**

1. R Services 없이 SQL Server 2016을 설치 합니다.
2. SQL Server 2016 누적 업데이트 2로 업그레이드 합니다.
3. RTM 미디어를 사용 하 여 R Services (데이터베이스 내)를 설치 합니다.

**올바른 업그레이드 방법:**

1. R Services 없이 SQL Server 2016을 설치 합니다.
2. SQL Server 2016을 원하는 패치 수준으로 업그레이드 합니다. 예를 들어 서비스 팩 1을 설치 하 고 누적 업데이트 2를 설치 합니다.
3. 올바른 패치 수준에서 기능을 추가 하려면 s p 1을 실행 하 고 설치 프로그램을 다시 CU2 하 고 R Services (데이터베이스 내)를 선택 합니다. 

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>8\.3 표기법이 필요한 경우 실행 패드를 시작 하지 못함

> [!NOTE] 
> 이전 시스템에서는 8.3 표기법 요구 사항이 있을 경우 실행 패드를 시작할 수 없습니다. 이후 릴리스에서는이 요구 사항이 제거 되었습니다. SQL Server 2016 R Services 고객은 다음 중 하나를 설치 해야 합니다.
> * SQL Server 2016 SP1 및 CU1: [SQL Server에 대 한 누적 업데이트 1](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1).
> * SQL Server 2016 RTM, 누적 업데이트 3 및이 [핫픽스](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3)를 요청 시 사용할 수 있습니다.

R과의 호환성을 위해 SQL Server 2016 R Services (데이터베이스 내)에는 *8.3 표기법*을 사용 하 여 짧은 파일 이름 생성을 지원 하기 위해 기능이 설치 된 드라이브가 필요 합니다. 8\.3 파일 이름은 *짧은 파일 이름이*라고도 하며, 이전 버전의 Microsoft Windows와의 호환성을 위해 또는 긴 파일 이름 대신 사용 됩니다.

R을 설치 하는 볼륨에서 짧은 파일 이름을 지원 하지 않는 경우 SQL Server에서 R을 시작 하는 프로세스가 올바른 실행 파일을 찾지 못할 수 있으며 실행 패드는 시작 되지 않습니다.

이 문제를 해결 하기 위해 SQL Server가 설치 되 고 R Services가 설치 된 볼륨에서 8.3 표기법을 사용 하도록 설정할 수 있습니다. 그런 다음 R Services 구성 파일에서 작업 디렉터리의 짧은 이름을 제공해야 합니다.

1. 8dot3 표기법을 사용 하려면 [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)에 설명 된 대로 *8dot3name* 인수를 사용 하 여 fsutil 유틸리티를 실행 합니다.

2. 8\.3 표기법을 사용 하도록 설정한 후에는 RLauncher 파일을 열고의 `WORKING_DIRECTORY`속성을 기록해 둡니다. 이 파일을 찾는 방법에 대 한 자세한 내용은 [Machine Learning 문제 해결을 위한 데이터 수집](data-collection-ml-troubleshooting-process.md)을 참조 하세요.

3. *File* 인수와 함께 fsutil 유틸리티를 사용 하 여 WORKING_DIRECTORY에 지정 된 폴더에 대 한 짧은 파일 경로를 지정 합니다.

4. 구성 파일을 편집 하 여 WORKING_DIRECTORY 속성에 입력 한 것과 동일한 작업 디렉터리를 지정 합니다. 또는 다른 작업 디렉터리를 지정 하 고 이미 8.3 표기법과 호환 되는 기존 경로를 선택할 수 있습니다.
::: moniker-end

## <a name="next-steps"></a>다음 단계

[Machine Learning Services 문제 해결 및 알려진 문제](machine-learning-troubleshooting-faq.md)

[기계 학습 문제 해결을 위한 데이터 수집](data-collection-ml-troubleshooting-process.md)

[업그레이드 및 설치 FAQ](r/upgrade-and-installation-faq-sql-server-r-services.md)

[데이터베이스 엔진 연결 문제 해결](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
