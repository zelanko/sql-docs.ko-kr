---
title: "일반적인 문제를 SQL Server의 외부 스크립트 실행 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: 2be854d38728670d5f68325da0bcf8136aef53f9
ms.contentlocale: ko-kr
ms.lasthandoff: 10/13/2017

---
# <a name="common-issues-with-external-script-execution-in-sql-server"></a>일반적인 문제를 SQL Server의 외부 스크립트 실행

이 문서에는 알려진된 문제 및 SQL Server에서 R, Python 코드를 실행 된 일반적인 문제 목록이 포함 되어 있습니다.

시작 하기 전에 시스템에 대 한 일부 정보를 수집 하는 것이 좋습니다. 자세한 내용은 참조 [데이터 수집 문제 해결을 위한](data-collection-ml-troubleshooting-process.md)합니다.

또한 초기 설치 또는 구성에 관련 된 일반적인 문제 목록을 검토: [설치 및 업그레이드 FAQ](r/upgrade-and-installation-faq-sql-server-r-services.md)합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스

## <a name="launchpad-issues"></a>실행 패드 문제

SQL Server 신뢰할 수 있는 실행 패드 서비스는 실행 한 외부 스크립트 및 R, Python 또는 기타 외부 런타임와의 통신을 관리합니다. 여러 문제는 시작, 구성 문제 또는 변경 내용을 포함 하 여 또는 네트워크 프로토콜을 누락 하에서 실행 패드를 방해할 수 있습니다.

문제 해결 과정의 일환으로, 다음 질문에 대답 하 여 시작 합니다.

- 실행 패드 항상 실패 않았지만 실행 하려면 또는 작동 하지 않은 것?
- 실행 패드에서 실행 중인 서비스 계정은 무엇입니까?
- 실행 패드 서비스 계정에는 어떤 사용자 권한을 갖고 있습니까?

### <a name="determine-whether-launchpad-is-running"></a>실행 패드 실행 중인지 확인

1. 열기는 **서비스** 패널 (Services.msc). 명령줄에서 입력 또는 **SQLServerManager13.msc** 또는 **SQLServerManager14.msc** 열려는 [SQL Server 구성 관리자](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)합니다.

2. 실행 패드에서 실행 되는 서비스 계정을 기록해 둡니다. R 또는 Python 설정 된 각 인스턴스에 실행 패드 서비스의 자체 인스턴스가 있어야 합니다. 예를 들어 명명 된 인스턴스의 서비스와 같은 수 있습니다 _MSSQLLaunchpad$ InstanceName_합니다.

3. 서비스가 중지 된 경우 다시 시작 합니다. 컴퓨터가 다시 시작에 구성 사용 하 여 모든 문제가 있는지 시스템 이벤트 로그에 메시지가 게시 될 하 고 서비스가 다시 중지 됩니다. 서비스가 중지 된 이유에 대 한 자세한 내용은 시스템 이벤트 로그를 확인 합니다.

4. RSetup.log의 내용을 검토 하 고 설치 프로그램에서 오류가 없는지 확인 합니다. 예를 들어 메시지 *종료 코드 0* 시작 서비스의 실패를 나타냅니다.

5. 다른 오류를 찾으려면 rlauncher.log의 내용을 검토 합니다.

### <a name="check-the-launchpad-service-account"></a>실행 패드 서비스 계정을 확인합니다

기본 서비스 계정 수 "NT Service\$SQL2016" 또는 "NT Service\$SQL2017"입니다. 마지막 부분은 SQL 인스턴스 이름에 따라 달라질 수 있습니다.

실행 패드 서비스 (Launchpad.exe) 서비스를 낮은 권한 계정을 사용 하 여 실행 됩니다. 그러나 R 및 Python을 시작 하 고 데이터베이스 인스턴스와 통신 하는 실행 패드 서비스 계정에 다음 사용자 권한이 필요 합니다.

- 서비스로 로그온(SeServiceLogonRight)
- 프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)
- 트래버스 검사 무시(SeChangeNotifyPrivilege)
- 프로세스 (SeIncreaseQuotaSizePrivilege)에 대 한 메모리 할당량 조정

이러한 사용자 권한에 대 한 내용은 "Windows 사용 권한 및 권한" 섹션을 참조 하십시오. [Windows 구성 서비스 계정 및 권한](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)합니다.

> [!TIP]
> SQL Server 진단에 대 한 지원 진단 플랫폼 (SDP) 도구를 사용 하 여는 잘 알고 있다면 MachineName_UserRights.txt 이름의 출력 파일을 확인 하려면 SDP를 사용할 수 있습니다.

### <a name="review-launchpad-requirements"></a>실행 패드 요구 사항 검토

실행 패드를 방지할 몇 가지 문제 중 하나를 시작할 수 있습니다. 실행 패드 서비스의 시작 및 중지 될 수 있습니다 또는 충돌이 발생 하거나 서비스 연결 제한 시간에 중지 될 수 있습니다. 이러한 경우에는 시스템 일반적으로 변경 되거나 구성 실행 패드를 실행할 수 없습니다.

#### <a name="determine-whether-8dot3-notation-is-enabled"></a>8.3 형식이 표기법을 사용할 수 있는지 여부를 확인합니다

R 통한 호환성을 위해 SQL Server 2016 R Services (In-database)를 사용 하 여 짧은 파일 이름 만들기를 지원 하도록 기능이 설치 되어 있는 드라이브를 필요한 *8.3 형식이 표기법*합니다. 8.3 파일 이름을 라고도 *짧은 파일명*, 긴 파일 이름 대신 또는 Microsoft Windows의 이전 버전과 호환성을 위해 사용 됩니다.

R 설치 하는 볼륨에는 짧은 파일 이름을 지원 하지 않습니다, R에서 SQL Server를 실행 하는 프로세스를 올바른 실행 파일을 찾을 수 수 있습니다 및 실행 패드 시작 되지 않습니다.

문제를 해결 SQL Server를 설치한 및 R Services가 설치 되어 있는 볼륨에 8.3 형식이 표기법을 사용할 수 있습니다. 그런 다음 R Services 구성 파일에서 작업 디렉터리의 짧은 이름을 제공해야 합니다.

1. 8.3 형식이 표기법을 사용 하려면 사용 하 여 fsutil 유틸리티 실행의 *8dot3name* 여기에 설명 된 대로 인수: [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)합니다.

2. 8.3 형식이 표기법을 사용 하도록 설정한 후 RLauncher.config 파일을 열고의 속성을 기록 `WORKING_DIRECTORY`합니다. 이 파일을 확인 하는 방법에 대 한 정보를 참조 하십시오. [기계 학습 문제 해결에 대 한 데이터 수집](data-collection-ml-troubleshooting-process.md)합니다.

3. 사용 하 여 fsutil 유틸리티를 사용 하 여는 *파일* 인수 WORKING_DIRECTORY에 지정 된 폴더에 대 한 짧은 파일 경로를 지정 합니다.

4. WORKING_DIRECTORY 속성에 입력 된 같은 작업 디렉터리를 지정 하려면 구성 파일을 편집 합니다. 또는 다른 작업 디렉터리를 지정 하 고 이미 8.3 형식이 표기법와 호환 되는 기존 경로 선택 수 있습니다.

> [!NOTE] 
> 이 제한은 이후 릴리스에서 제거되었습니다. 이 문제를 발생 하는 경우 다음 중 하나를 설치 합니다.
> * SQL Server 2016 s p 1과 CU1: [SQL Server에 대 한 누적 업데이트 1](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1)합니다.
> * SQL Server 2016 RTM, 누적 업데이트 3 및이 [핫픽스](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3), 요청에서 사용할 수 있습니다.

#### <a name="the-user-group-for-launchpad-cannot-log-on-locally"></a>실행 패드에 대 한 사용자 그룹에 로컬로 로그온 수 없습니다.

기계 학습 서비스를 설치 하는 동안 SQL Server는 Windows 사용자 그룹 만듭니다 **SQLRUserGroup** 다음 SQL Server에 연결 하 고 외부 스크립트 작업을 실행 하려면 실행 패드에 필요한 모든 권한이 포함 된 프로 비전 합니다. 이 사용자 그룹을 사용 하는 경우 Python 스크립트 실행에 사용 됩니다.

그러나 더 제한적인 보안 정책을 적용은 조직에서이 그룹에 필요한 권한을 수동으로 제거 되었을 수, 또는 정책에 의해 자동으로 취소 될 수 있습니다. 권한을 제거 되었거나, 실행 패드 SQL Server에 더 이상 연결할 수 없습니다 및 SQL Server 외부 런타임을 호출할 수 없습니다.

문제를 해결하려면 그룹 **SQLRUserGroup**에 시스템 권한 **로컬 로그온 허용**이 있는지 확인합니다.

자세한 내용은 참조 [Windows 구성 서비스 계정 및 권한](https://msdn.microsoft.com/library/ms143504.aspx#Windows)합니다.

#### <a name="improper-setup-leading-to-mismatched-dlls"></a>앞에 일치 하지 않는 Dll에 잘못 설치

다른 기능을 서버에 패치를 데이터베이스 엔진을 설치 하 고 다음 원본 미디어를 사용 하 여 나중에 기계 학습 기능을 추가 하는 경우에 잘못 된 버전의 기계 학습 구성 요소를 설치할 수 있습니다. 실행 패드에서 버전 불일치를 발견 하면 종료 하 고 덤프 파일을 만듭니다.

이 문제를 방지 하려면 서버 인스턴스와 동일한 패치 수준에 새로운 기능을 설치 해야 합니다.

**업그레이드 하는 잘못 된 방법입니다.**

1. R 서비스 없이 SQL Server 2016을 설치 합니다.
2. SQL Server 2016 누적 업데이트 2를 업그레이드 합니다.
3. RTM 미디어를 사용 하 여 R Services (In-database)를 설치 합니다.

**업그레이드 하는 올바른 방법입니다.**

1. R 서비스 없이 SQL Server 2016을 설치 합니다.
2. SQL Server 2016 원하는 패치 수준으로 업그레이드 합니다. 예를 들어 서비스 팩 1 및 누적 업데이트 2를 설치 합니다.
3. 정확한 패치 수준에 기능을 추가 하려면 s p 1과 c u 2 설치 프로그램을 다시 실행 하 고 R Services (In-database)를 선택 합니다. 

#### <a name="check-whether-a-user-has-rights-to-run-external-scripts"></a>사용자에 외부 스크립트 실행에 대 한 권한이 있는지 확인 하십시오.

실행 패드를 올바르게 구성 된 경우에 사용자에 Python 또는 R 스크립트를 실행할 수 있는 권한이 없는 경우 오류가 반환 됩니다.

데이터베이스 소유자는 데이터베이스 관리자는 SQL Server를 설치한 경우이 사용 권한은 자동으로 부여 됩니다. 그러나 다른 사용자가 일반적으로 더 제한 된 사용 권한. R 스크립트를 실행 하려고 할 경우 실행 패드 오류를 받게 합니다.

SQL Server Management Studio에서 문제를 해결 하려면 보안 관리자가 SQL 로그인 또는 Windows 사용자 계정을 다음 스크립트를 실행 하 여 수정할 수 있습니다.

```SQL
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

자세한 내용은 참조 [GRANT (TRANSACT-SQL](../t-sql/statements/grant-transact-sql.md)합니다.

### <a name="common-launchpad-errors"></a>실행 패드의 일반적인 오류

이 섹션에는 실행 패드 반환 하는 가장 일반적인 오류 메시지가 나열 됩니다.

#### <a name="error-unable-to-launch-runtime-for-r-script"></a>오류: *R 스크립트에 대해 런타임을 시작할 수 없습니다.*

R 사용자 (Python에도 사용)에 대 한 Windows 그룹 R 서비스를 실행 하는 인스턴스에 로그온 할 수 없습니다, 경우에 다음과 같은 오류가 나타날 수 있습니다.

- R 스크립트를 실행 하려고 할 때 발생 한 오류:

    * *'R' 스크립트에 대해 런타임을 시작할 수 없습니다. 'R' 런타임의 구성을 확인하세요.*

    * *외부 스크립트 오류가 발생했습니다. 런타임을 시작할 수 없습니다.*

- 생성 된 오류는 [!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)] 서비스:

    * *시작 관리자 RLauncher.dll을 초기화하지 못했습니다.*

    * *등록된 시작 관리자 dll이 없습니다!*

    * *NT 서비스 계정에 로그온 할 수 없음을 나타내는 보안 로그*

이 사용자 그룹에 필요한 권한을 부여 하는 방법에 대 한 정보를 참조 하십시오. [SQL Server R Services 설치](r/set-up-sql-server-r-services-in-database.md)합니다.

> [!NOTE]
> SQL 로그인을 사용하여 원격 워크스테이션에서 R 스크립트를 실행하는 경우에는 이 제한이 적용되지 않습니다.

#### <a name="error-logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>오류: *로그온 실패: 사용자가 요청한 로그온 유형을 부여 되지*

기본적으로 [!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)] 시작 다음 계정을 사용 하 여: `NT Service\MSSQLLaunchpad`합니다. 계정을 구성 하 여 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 필요한 권한이 모두에 설치 합니다.

실행 패드에 다른 계정에 할당 하거나 오른쪽 SQL Server 컴퓨터에 적용 된 정책에 의해 제거는 계정에 필요한 권한이 없을 수 있습니다 및이 오류가 표시 될 수 있습니다.

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385(0x569) 로그온 실패: 사용자는 이 컴퓨터에서는 요청된 로그온 유형을 허가받지 않았습니다.*

새 서비스 계정에 필요한 권한을 부여할 로컬 보안 정책 응용 프로그램을 사용 하 고 다음 사용 권한을 포함 하는 계정에 대 한 권한을 업데이트 합니다.

+ 프로세스의 메모리 할당량 조정(SeIncreaseQuotaPrivilege)
+ 트래버스 검사 무시(SeChangeNotifyPrivilege)
+ 서비스로 로그온(SeServiceLogonRight)
+ 프로세스 수준 토큰 바꾸기(SeAssignPrimaryTokenPrivilege)

#### <a name="error-unable-to-communicate-with-the-launchpad-service"></a>오류: *실행 패드 서비스와 통신할 수 없습니다.*

설치 하 고 다음 기계 학습을 사용 하지만 R, Python 스크립트를 실행 하려고 할 때이 오류가 발생할 경우 실행 중인 인스턴스에 대 한 실행 패드 서비스 중지 되었을 수 있습니다.

1. Windows 명령 프롬프트에서 SQL Server 구성 관리자를 엽니다. 자세한 내용은 [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager)을 참조하세요.

2. 인스턴스에 대 한 SQL Server 실행 패드를 마우스 오른쪽 단추로 클릭 한 다음 선택 **속성**합니다.

3. 선택 된 **서비스** 탭을 선택한 다음 서비스가 실행 되 고 있는지를 확인 합니다. 실행 되지 않는 경우 변경 된 **시작 모드** 를 **자동**, 선택한 후 **적용**합니다.

4. 일반적으로 서비스를 다시 시작 컴퓨터 학습 스크립트 실행 될 수 있도록 하며 문제를 해결 합니다. 경로 인수에 기록해 둡니다 다시 시작이 문제를 해결 하지 않는 경우는 **이진 경로** 속성을 선택한 다음을 수행 합니다.

    a. 실행 프로그램의.config 파일을 검토 하 고 작업 디렉터리가 올바른지 확인 하십시오.

    b. 에 설명 된 대로 Windows 그룹 실행 패드에서 사용 되는 SQL Server 인스턴스에 연결할 수 있는지를 확인는 [이전 섹션](#bkmk_LaunchpadTS)합니다.

    c. 서비스 속성을 변경 하는 경우에 실행 패드 서비스 다시 시작 합니다.

#### <a name="error-fatal-error-creation-of-tmpfile-failed"></a>오류: *tmpFile 심각한 오류 만들지 못했습니다.*

이 시나리오에서는 컴퓨터 학습 기능을 성공적으로 설치한 및 실행 패드를 실행 합니다. 몇 가지 간단한 Python 또는 R 코드를 실행 하려고 하지만 다음과 같은 오류가 발생 하 여 실행 패드에 실패 합니다. 

>*R 스크립트의 런타임과 통신할 수 없습니다. R 런타임의 요구 사항을 확인 하십시오.*

같은 시간에 외부 스크립트 런타임 STDERR 메시지의 일부로 다음과 같은 메시지를 기록 합니다. 

>*심각한 오류: 실패 tmpfile 생성 합니다.*

이 오류는 실행 패드를 사용 하려고 하는 계정에 데이터베이스에 로그온 할 수 있는 없는지를 나타냅니다. 엄격한 보안 정책이 구현 되는 경우에 이러한 상황이 발생할 수 있습니다. 이 경우 인지를 확인 하려면 SQL Server 로그를 검토 하 고 확인은 MSSQLSERVER01 계정에 로그인 할 때 액세스가 거부 되었습니다 있는지 여부를 확인 하려면. R 관련 된 로그에 동일한 정보가 제공 됩니다\_서비스 또는 PYTHON\_서비스입니다. ExtLaunchError.log 찾습니다.

기본적으로 20 계정은 설정 이므로 MSSQLSERVER20 통해은 MSSQLSERVER01 이름의 Launchpad.exe 프로세스에 연결 된입니다. R 또는 Python를 많이 사용 하는 경우 계정의 수를 늘릴 수 있습니다.

이 문제를 해결 하려면 그룹에 있는지를 확인 *로컬 로그온 허용* 컴퓨터 학습 기능 여기서 설치 및 사용 하도록 설정 된 로컬 인스턴스에 대 한 사용 권한. 이 권한 수준은 일부 환경에서는 네트워크 관리자에 게 GPO 예외가 필요할 수 있습니다.

## <a name="r-script-issues"></a>R 스크립트 문제

이 섹션에는 R 스크립트 실행 및 R 스크립트 오류에 관련 된 몇 가지 일반적인 문제를 포함 합니다. 목록 않으므로 포괄적는 여러 R 패키지 및 오류는 동일한 R 패키지의 버전 간에 다를 수 있습니다. R 스크립트 오류를 게시 하는 것이 좋습니다는 [Microsoft R Server 포럼](https://social.msdn.microsoft.com/Forums/home?category=MicrosoftR)를 지 원하는 기계 학습 R Services (In-database) 컴퓨터 Microsoft R, Python 및 Microsoft R 클라이언트와 서비스 학습에 사용 되는 구성 요소 서버입니다.

### <a name="multiple-r-instances-on-the-same-computer"></a>동일한 컴퓨터에서 여러 R 인스턴스

다양 한 버전의 동일한 R 패키지의 여러 복사본 뿐만 아니라 동일한 컴퓨터에는 R의 여러 배포판 직접 찾기 쉬울 수 있습니다. 예를 들어 컴퓨터 학습 서버 (독립 실행형)와 컴퓨터 학습 Services (In-database)를 설치 하는 경우 설치 관리자가 서로 다른 버전의 R 라이브러리를 만듭니다. 

이러한 중복 확실 하지 않은 사용 하는 라이브러리를 명령줄에서 스크립트를 실행 하려고 할 때 문제가 됩니다. 또는 잘못 된 라이브러리에 패키지를 설치 하 고 SQL Server에서 패키지를 찾을 수 없는 이유 나중 궁금할 수 있습니다.

+ R 라이브러리 및 SQL Server 인스턴스를 사용 하기 위한 문제 해 결과 같은 제한 된 경우를 제외 하 고 설치 된 도구는 직접 사용 하거나 새 패키지를 설치 하지 마세요. 
+ R 명령줄 도구를 사용 해야 하는 경우 설치할 수 있습니다 [Microsoft R Client](https://docs.microsoft.com/r-server/r-client/what-is-microsoft-r-client)합니다. 
+ SQL Server R 패키지의 데이터베이스에서 관리 기능을 제공 합니다. 이것이 사용자 간에 공유할 수 있는 R 패키지 라이브러리를 만드는 가장 쉬운 방법입니다. 자세한 내용은 참조 [SQL Server에 대 한 R 패키지 관리](r/r-package-management-for-sql-server-r-services.md)합니다.

### <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>SQL 계산 컨텍스트에서 R을 실행 하는 동안 작업 영역을 선택 취소 하지 마십시오.

가질 수 있습니다는 R 콘솔에서 작업할 때 작업 영역을 선택 취소 하는 것은 일반적인, 계산 컨텍스트는 SQL에서 의도 하지 않은 결과입니다.

`revoScriptConnection`SQL Server에서 호출 되는 R 세션에 대 한 정보를 포함 하는 R 작업 영역에서 개체가입니다. 그러나 R 코드의 작업 영역을 선택 취소 하는 명령을 포함 하는 경우 (예: `rm(list=ls())`), 세션 및 기타 개체는 R 작업 영역에 대 한 모든 정보의 선택도 취소 됩니다.

이 문제를 해결 SQL Server에서 R을 실행 하는 동안 변수 및 기타 개체를 무분별 하 게 삭제를 하지 마십시오. 사용 하 여 특정 변수를 삭제할 수는 **제거** 함수:

```R
remove('name1', 'name2', ...)
```

여러 변수를 삭제 하는, 경우에 임시 변수의 이름이 목록에 저장 한 다음 목록에 주기적 가비지 컬렉션을 수행 하는 것이 좋습니다.

### <a name="implied-authentication-for-remote-execution-via-odbc"></a>ODBC 통해 원격 실행에 대 한 묵시적된 인증

에 연결 하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] R을 실행할 컴퓨터를 사용 하 여 명령을 **RevoScaleR** 함수를 서버에 데이터를 기록 하는 ODBC 호출을 사용 하는 경우 오류가 발생할 수 있습니다. 이 오류는 Windows 인증을 사용 하는 경우에 발생 합니다.

원인은 R Services 용으로 작성 된 작업자 계정은 서버에 연결할 수 있는 권한이 없는 것입니다. 따라서 사용자 대신 ODBC 호출을 실행할 수 없습니다. SQL 로그인이 있는 자격 증명 전달 되기 때문에 명시적으로 R 클라이언트로부터 SQL Server 인스턴스 및 ODBC SQL 로그인이 있는 문제가 발생 하지 않습니다. 그러나 SQL 로그인을 사용 하 여 이기도 Windows 인증을 사용 하 여 보다 덜 안전 합니다.

사용자가 시작한 원격으로 SQL Server 스크립트에서 안전 하 게 전달 될 Windows 자격 증명을 사용 하도록 설정 하려면 자격 증명을 에뮬레이트할 해야 합니다. 이 프로세스 라고 _암시 된 인증이_합니다. 이 작업을 하려면 SQL Server 컴퓨터에 R, Python 스크립트를 실행 하는 작업자 계정이 올바른 사용 권한이 있어야 합니다.

1. 열기 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] R 코드를 실행 하려면 인스턴스의 관리자 권한으로 합니다.

2. 다음 스크립트를 실행합니다. 기본적으로 변경한 경우 사용자 그룹 이름 및 컴퓨터 및 인스턴스 이름을 편집 해야 합니다.

    ```SQL
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

### <a name="the-r-script-works-outside-of-t-sql-but-not-in-a-stored-procedure"></a>T-SQL 외부 있지만 저장된 프로시저에 없는 작동 하는 R 스크립트

저장된 프로시저에서 R 코드를 배치 하기 전에 외부 IDE에서 또는 rterm이 또는 관리자 권한 같은 R 도구 중 하나에서 R 코드를 실행 하 것이 좋습니다. 이 메서드를 사용 하 여 테스트 하 고 오른쪽에서 반환 되는 자세한 오류 메시지를 사용 하 여 코드를 디버깅 합니다.

그러나 경우에 따라 저장된 프로시저에서 실행 하거나 계산 컨텍스트는 SQL Server에서 외부 IDE 또는 유틸리티에서 완벽 하 게 작동 하는 코드 실패할 수 있습니다. 이런 경우가 발생 하는 경우 패키지 SQL Server에서 작동 하지 않는 가정할 수 전에 찾아봐야 할 문제는 여러 가지 사항이 있습니다.

1. 실행 패드 실행 중인지 여부를 확인 합니다.

2. 입력된 데이터 또는 출력 데이터 호환 되지 않거나 지원 되지 않는 데이터 형식 열이 포함 되어 있는지 여부를 확인 하려면 메시지를 검토 합니다. 예를 들어 SQL 데이터베이스에 대 한 쿼리 Guid 또는 지원 되지 않습니다는 RowGUIDs 자주 반환 합니다. 자세한 내용은 참조 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)합니다.

3. SQL Server 계산 컨텍스트에서 대 한 모든 매개 변수 지원 되는지 여부를 확인 하려면 개별 R 함수에 대 한 도움말 페이지를 검토 합니다. ScaleR 도움말에 대 한 인라인 R 도움말 명령을 사용 하거나 참조 [패키지 참조](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)합니다.

### <a name="you-get-different-results-from-the-same-script-when-running-in-sql-compared-to-other-environments"></a>다른 환경에 비해 SQL에서 실행할 때는 같은 스크립트에서 다른 결과 얻을

R 스크립트 여러 가지 이유로 SQL Server 컨텍스트에서 서로 다른 값을 반환할 수 있습니다.

- 데이터는 SQL Server와 오른쪽 간에 전달 될 때 일부 데이터 형식에 암시적 형식 변환은 자동으로 수행 됩니다. 자세한 내용은 참조 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)합니다.

- 비트는 요소 인지 확인 합니다. 예를 들어 32 비트 및 64 비트 부동 지점 라이브러리에 대 한 수치 연산의 결과의 차이 종종 됩니다.

- Nan 작업에서 생성 된 여부를 결정 합니다. 결과 무효화 될 수 있습니다.

- 0에 가까운 숫자의 역을 수행할 때 방법 차이로 증폭 수 있습니다.

- 누적 된 반올림 오류 등의 작업 하는 0이 아닌 0 보다 작은 값으로 발생할 수 있습니다.

### <a name="error-not-enough-quota-to-process-this-command"></a>오류: *이 명령을 처리할 수 할당량이 충분 하지 않습니다*

이 오류 중 하나를 의미 합니다.

- 실행 패드 부족 하 여 외부 사용자가 외부 쿼리를 실행 하도록 할 수 있습니다. 예를 들어 20 개 이상의 외부 쿼리를 동시에 실행 중인 경우 20 기본 사용자만는 하나 이상의 쿼리가 실패할 수 있습니다.

- 메모리가 부족 하 여은 R 작업을 처리할 수 있습니다. 이 오류를 SQL Server 사용 중일 수는 컴퓨터의 리소스의 최대 70%는 기본 환경에서 가장 자주 발생 합니다. R 리소스 큰 사용을 지원 하기 위해 서버 구성을 수정 하는 방법에 대 한 정보를 참조 하십시오. [작업에서 R 코드 활용](r/operationalizing-your-r-code.md)합니다.

### <a name="error-cant-find-package"></a>오류: *패키지를 찾을 수 없습니다*

SQL Server에서 R 코드를 실행 하 고이 메시지가 하지만 SQL Server 외부 동일한 코드를 실행 한 경우 메시지를 발생 하지 않는 경우 패키지가 SQL Server에서 사용 되는 기본 라이브러리 위치에 설치 되지 않은 의미 합니다.

이 오류는 여러 가지 방법으로 발생할 수 있습니다.

- 서버에 새 패키지를 설치 하지만 R 사용자 라이브러리에 패키지를 설치 하므로 액세스가 거부 되었습니다.

- R 서비스를 설치 하 고 다른 R 도구를 설치 또는 Microsoft R Server (독립 실행형), Microsoft R Client RStudio를 비롯 한 라이브러리의 설정 했으며 등

인스턴스에서 사용 되는 R 패키지 라이브러리의 위치를 확인 하려면 SQL Server Management Studio를 엽니다 (또는 다른 데이터베이스 쿼리 도구)는 인스턴스에 연결 하 고 다음 저장된 프로시저를 실행 하십시오.

```SQL
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>샘플 결과

*STDOUT message(s) from external script:*

*[1] "c:\\프로그램 파일\\Microsoft SQL Server\\MSSQL13 합니다. SQL2016\\R_SERVICES "*

*[1] "c: / Program 파일/Microsoft SQL Server/MSSQL13 합니다. SQL2016/R_SERVICES/라이브러리 "*

문제를 해결 하려면 SQL Server 인스턴스 라이브러리에 패키지를 다시 설치 해야 합니다.

>[!NOTE]
>Microsoft R의 최신 버전을 사용 하도록 SQL Server 2016의 인스턴스를 업그레이드 한 경우에 기본 라이브러리 위치 차이가 있습니다. 자세한 내용은 참조 [R Services의 인스턴스를 업그레이드 하려면 사용 하 여 SqlBindR](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

## <a name="next-steps"></a>다음 단계

[컴퓨터 학습 서비스 문제 해결 및 알려진된 문제](machine-learning-troubleshooting-faq.md)

[기계 학습 문제 해결에 대 한 데이터 수집](data-collection-ml-troubleshooting-process.md)

[업그레이드 및 설치 FAQ](r/upgrade-and-installation-faq-sql-server-r-services.md)

[데이터베이스 엔진 연결 문제 해결](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)

