---
title: Python 및 R에 대 한 알려진 문제
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/23/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d56e3109c0820b800bbd72c9cc86bed9b7a09eea
ms.sourcegitcommit: 823d7bdfa01beee3cf984749a8c17888d4c04964
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/26/2019
ms.locfileid: "70030299"
---
# <a name="known-issues-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services의 알려진 문제
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 [SQL Server Machine Learning Services](what-is-sql-server-machine-learning.md) 및 [SQL Server 2016 R Services](r/sql-server-r-services.md)에서 옵션으로 제공 되는 기계 학습 구성 요소에 대 한 알려진 문제 또는 제한 사항을 설명 합니다.

## <a name="setup-and-configuration-issues"></a>설정 및 구성 문제

초기 설정 및 구성과 관련 된 프로세스 및 일반적인 질문에 대 한 설명은 [업그레이드 및 설치 FAQ](r/upgrade-and-installation-faq-sql-server-r-services.md)를 참조 하세요. 여기에는 업그레이드, 함께 설치 및 새 R 또는 Python 구성 요소 설치에 대 한 정보가 포함 되어 있습니다.

### <a name="1-inconsistent-results-in-mkl-computations-due-to-missing-environment-variable"></a>1. 환경 변수가 누락 되어 MKL 계산 결과가 일치 하지 않습니다.

**적용 대상:** R_SERVER 이진 파일 9.0, 9.1, 9.2 또는 9.3.

R_SERVER는 Intel MKL (Math Kernel Library)을 사용 합니다. MKL을 포함 하는 계산의 경우 시스템에 환경 변수가 없는 경우 일관성 없는 결과가 발생할 수 있습니다. 

환경 변수 `'MKL_CBWR'=AUTO` 를 설정 하 여 R_SERVER에서 조건부 숫자 재현 가능성를 확인 합니다. 자세한 내용은 [CNR (조건부 숫자 재현 가능성) 소개](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)를 참조 하세요.

**해결 방법**

1. 제어판에서 **시스템 및 보안** > **시스템** > **고급 시스템 설정** > **환경 변수**를 클릭 합니다.

2. 새 사용자 또는 시스템 변수를 만듭니다. 

  + 변수 이름을 ' MKL_CBWR '로 설정 합니다.
  + ' 변수 값 '을 ' 자동 '으로 설정 합니다.

3. R_SERVER를 다시 시작 합니다. SQL Server에서 SQL Server 실행 패드 서비스를 다시 시작할 수 있습니다.

> [!NOTE]
> Linux에서 SQL Server 2019 미리 보기를 실행 하는 경우 사용자 홈 디렉터리에서 *bash_profile* 를 편집 하거나 만든 다음 줄 `export MKL_CBWR="AUTO"`을 추가 합니다. Bash 명령 프롬프트에서 `source .bash_profile`을 입력하여 이 파일을 실행합니다. R 명령 프롬프트에서 `Sys.getenv()` 를 입력 하 여 R_SERVER를 다시 시작 합니다.

### <a name="2-r-script-runtime-error-sql-server-2017-cu5-cu7-regression"></a>2. R 스크립트 런타임 오류 (SQL Server 2017 CU5-CU7 회귀)

SQL Server 2017의 경우 누적 업데이트 5부터 7까지 rlauncher 파일에 임시 디렉터리 파일 경로에 공백이 포함 된 회귀가 있습니다 **.** 이 회귀는 CU8에서 수정 되었습니다.

R 스크립트를 실행할 때 표시 되는 오류 메시지는 다음과 같습니다.

> *' R ' 스크립트의 런타임과 통신할 수 없습니다. ' R ' 런타임의 요구 사항을 확인 하세요.*
>
> 외부 스크립트의 STDERR 메시지: 
>
> *심각한 오류: ' R_TempDir '을 만들 수 없습니다.*

**해결 방법**

CU8를 사용할 수 있게 되 면 적용 합니다. 또는 관리자 권한 명령 프롬프트 에서 설치 프로그램을 사용 하 여 **registerrext.exe** 를 다시 만들 수 있습니다. 

```cmd
<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /uninstall /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>

<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /install /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>
```

다음 예에서는 기본 인스턴스 "MSSQL14"를 사용 하는 명령을 보여 줍니다. "C:\Program Files\Microsoft SQL Server\"에 설치 된 MSSQLSERVER:

```cmd
"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /uninstall /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER

"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /install /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER
```

### <a name="3-unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>3. 도메인 컨트롤러에 SQL Server machine learning 기능을 설치할 수 없습니다.

SQL Server 2016 R Services 또는 SQL Server Machine Learning Services를 도메인 컨트롤러에 설치 하려고 하면 설치에 실패 하 고 다음 오류가 발생 합니다.

> *기능의 설치 프로세스 중에 오류가 발생 했습니다.*
> 
> *Id가 인 그룹을 찾을 수 없습니다.*
> 
> *구성 요소 오류 코드: 0x80131509*

도메인 컨트롤러에서 서비스는 machine learning을 실행 하는 데 필요한 20 개의 로컬 계정을 만들 수 없기 때문에 오류가 발생 합니다. 일반적으로 도메인 컨트롤러에 SQL Server를 설치 하지 않는 것이 좋습니다. 자세한 내용은 [지원 공지 2032911](https://support.microsoft.com/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont)을 참조 하세요.

### <a name="4-install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>4. 최신 서비스 릴리스를 설치 하 여 Microsoft R Client와의 호환성 확인

최신 버전의 Microsoft R Client를 설치 하 고이를 사용 하 여 원격 계산 컨텍스트에서 SQL Server R을 실행 하는 경우 다음과 같은 오류가 발생할 수 있습니다.

> *컴퓨터에서 버전 4.x. x. x. x. x. x. x. x. x. x. x.x. Microsoft R Server와 호환 되지 않는 버전의 Microsoft R Client를 실행 하 고 호환되는 버전을 다운로드하여 설치하세요.*

2016 SQL Server 클라이언트의 R 라이브러리가 서버의 R 라이브러리와 정확히 일치 해야 합니다. R Server 9.0.1 이후 릴리스에서는 제한 사항이 제거 되었습니다. 그러나이 오류가 발생 하는 경우 클라이언트와 서버에서 사용 하는 R 라이브러리의 버전을 확인 하 고 필요한 경우 클라이언트를 서버 버전과 일치 하도록 업데이트 합니다.

SQL Server R Services와 함께 설치 되는 R 버전은 SQL Server 서비스 릴리스가 설치 될 때마다 업데이트 됩니다. 항상 최신 버전의 R 구성 요소를 유지 하려면 모든 서비스 팩을 설치 해야 합니다.

Microsoft R Client 9.0.0와의 호환성을 보장 하려면이 [지원 문서](https://support.microsoft.com/kb/3210262)에 설명 된 업데이트를 설치 합니다.

R 패키지와 관련 된 문제를 방지 하려면 [다음 섹션](#bkmk_sqlbindr)에 설명 된 대로 최신 수명 주기 지원 정책을 사용 하도록 서비스 계약을 변경 하 여 서버에 설치 된 r 라이브러리 버전을 업그레이드할 수도 있습니다. 이렇게 하면 SQL Server와 함께 설치 되는 R 버전이 machine Learning Server (이전의 Microsoft R Server)의 업데이트에 사용 되는 것과 동일한 일정에 따라 업데이트 됩니다.

**적용 대상:** SQL Server 2016 R Services, R Server 버전 9.0.0 또는 이전 버전

### <a name="5-r-components-missing-from-cu3-setup"></a>5. CU3 설치 프로그램에서 R 구성 요소가 누락 됨

SQL Server에 포함 되어야 하는 R 설치 파일 없이 제한 된 수의 Azure virtual machines가 프로 비전 되었습니다. 이 문제는 2018-01-05에서 2018-01-23 까지의 기간에 프로 비전 된 가상 컴퓨터에 적용 됩니다. 2018-01-05에서 2018-01-23의 기간 동안 SQL Server 2017에 대 한 CU3 업데이트를 적용 한 경우에도이 문제가 온-프레미스 설치에 영향을 줄 수 있습니다.

올바른 버전의 R 설치 파일을 포함 하는 서비스 릴리스가 제공 됩니다.

+ [SQL Server 2017에 대 한 누적 업데이트 패키지 3 KB4052987](https://www.microsoft.com/download/details.aspx?id=56128).

구성 요소를 설치 하 고 SQL Server 2017 CU3를 복구 하려면 CU3를 제거 하 고 업데이트 된 버전을 다시 설치 해야 합니다.

1. R 설치 관리자를 포함 하는 업데이트 된 CU3 설치 파일을 다운로드 합니다.
2. CU3을 제거 합니다. 제어판에서 **업데이트 제거**를 검색 하 고 "SQL Server 2017 (KB4052987) (64 비트)의 핫픽스 3015을 선택 합니다. 제거 단계를 진행 합니다.
3. 방금 다운로드 `SQLServer2017-KB4052987-x64.exe`한 KB4052987에 대 한 업데이트를 두 번 클릭 하 여 CU3 업데이트를 다시 설치 합니다. 설치 지침을 따릅니다.

### <a name="6-unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>6. SQL Server 2017 CTP 2.0 이상 버전의 오프 라인 설치에서 Python 구성 요소를 설치할 수 없습니다.

인터넷에 액세스할 수 없는 컴퓨터에 SQL Server 2017의 시험판 버전을 설치 하는 경우 다운로드 한 Python 구성 요소의 위치를 묻는 페이지가 표시 되지 않을 수 있습니다. 이러한 인스턴스에서는 Python 구성 요소가 아닌 Machine Learning Services 기능을 설치할 수 있습니다.

이 문제는 릴리스 버전에서 해결 되었습니다. 또한 R 구성 요소에는 이러한 제한이 적용 되지 않습니다.

**적용 대상:** Python과 SQL Server 2017

### <a name="bkmk_sqlbindr"></a>을 사용 하 여 클라이언트에서 이전 버전의 SQL Server R Services에 연결 하는 경우 호환 되지 않는 버전의 경고[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

SQL Server 2016 계산 컨텍스트에서 R 코드를 실행 하면 다음과 같은 오류가 표시 될 수 있습니다.

> *컴퓨터에서 Microsoft R Server 버전 8.0.3과 호환되지 않는 Microsoft R Client 버전 9.0.0을 실행 중입니다. 호환되는 버전을 다운로드하여 설치하세요.*

다음 두 문 중 하나가 true 인 경우이 메시지가 표시 됩니다.

+ 용 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]설치 마법사를 사용 하 여 클라이언트 컴퓨터에 R Server (독립 실행형)를 설치 했습니다.
+ [별도의 Windows installer](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)를 사용 하 여 Microsoft R Server를 설치 했습니다.

서버와 클라이언트가 동일한 버전을 사용 하는지 확인 하려면 Microsoft R Server 9.0 이상 릴리스에서 지원 되는 _바인딩을_사용 하 여 SQL Server 2016 인스턴스의 R 구성 요소를 업그레이드 해야 합니다. 해당 버전의 R Services에 대 한 업그레이드 지원을 사용할 수 있는지 확인 하려면 [SqlBindR .exe를 사용 하 여 r services 인스턴스 업그레이드](install/upgrade-r-and-python.md)를 참조 하세요.

**적용 대상:** SQL Server 2016 R Services, R Server 버전 9.0.0 또는 이전 버전

### <a name="7-setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>7. SQL Server 2016 서비스 릴리스 설치 프로그램에서 최신 버전의 R 구성 요소를 설치하지 못할 수 있음

인터넷에 연결 되지 않은 컴퓨터에 누적 업데이트를 설치 하거나 SQL Server 2016에 대 한 Service Pack를 설치 하는 경우 다운로드 한 CAB 파일을 사용 하 여 R 구성 요소를 업데이트할 수 있는 프롬프트가 설치 마법사에 표시 되지 않을 수 있습니다. 일반적으로이 오류는 여러 구성 요소가 데이터베이스 엔진과 함께 설치 된 경우에 발생 합니다.

해결 방법으로, 명령줄을 사용 하 여 서비스 릴리스를 설치 하 고 CU1 업데이트를 `MRCACHEDIRECTORY` 설치 하는이 예제에 표시 된 대로 인수를 지정할 수 있습니다.

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

최신 설치 관리자를 다운로드 하려면 [인터넷에 액세스 하지 않고 machine learning 구성 요소 설치](install/sql-ml-component-install-without-internet-access.md)를 참조 하세요.

**적용 대상:** SQL Server 2016 R Services, R Server 버전 9.0.0 또는 이전 버전

### <a name="8-launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>8. 버전이 R 버전과 다른 경우 실행 패드 서비스를 시작 하지 못함

데이터베이스 엔진과 별도로 SQL Server R Services를 설치 하 고 빌드 버전이 다른 경우 시스템 이벤트 로그에 다음과 같은 오류가 표시 될 수 있습니다.

> *다음 오류 때문에 SQL Server 실행 패드 서비스를 시작 하지 못했습니다. 서비스가 시작 또는 제어 요청에 시기 적절 하 게 응답 하지 않았습니다.*

예를 들어 릴리스 버전을 사용 하 여 데이터베이스 엔진을 설치 하 고, 패치를 적용 하 여 데이터베이스 엔진을 업그레이드 한 다음, 릴리스 버전을 사용 하 여 R Services 기능을 추가 하는 경우이 오류가 발생할 수 있습니다.

이 문제를 방지 하려면 파일 관리자와 같은 유틸리티를 사용 하 여 실행 패드의 버전을 sqldk와 같은 SQL 이진 파일과 비교 합니다. 모든 구성 요소의 버전 번호는 동일 해야 합니다. 하나의 구성 요소를 업그레이드하는 경우 설치된 다른 모든 구성 요소에 동일한 업그레이드를 적용해야 합니다.

인스턴스의 `Binn` 폴더에서 실행 패드를 찾습니다. 예를 들어 SQL Server 2016의 기본 설치에서 경로는 일 `C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`수 있습니다. 

### <a name="9-remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>9. 원격 계산 컨텍스트는 Azure virtual machines에서 실행 되는 SQL Server 인스턴스의 방화벽에 의해 차단 됩니다.

Microsoft Azure 가상 컴퓨터 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 에를 설치한 경우 가상 컴퓨터의 작업 영역을 사용 해야 하는 계산 컨텍스트를 사용 하지 못할 수 있습니다. 이는 기본적으로 Azure 가상 컴퓨터의 방화벽에 로컬 R 사용자 계정에 대 한 네트워크 액세스를 차단 하는 규칙이 포함 되어 있기 때문입니다.

해결 방법으로, Azure VM에서 **고급 보안이 포함 된 Windows 방화벽**을 열고 **아웃 바운드 규칙**을 선택한 후 다음 규칙을 사용 하지 않도록 설정 합니다. **SQL Server 인스턴스 MSSQLSERVER의 R 로컬 사용자 계정에 대 한 네트워크 액세스를 차단**합니다. 규칙을 사용 하도록 설정 된 상태로 둘 수도 있지만 보안 속성은 보안을 **허용**하도록 변경 합니다.

### <a name="10-implied-authentication-in-sqlexpress"></a>10. SQLEXPRESS의 암시적 인증

Windows 통합 인증을 사용 하 여 원격 데이터 과학 워크스테이션에서 R 작업을 실행 하는 경우 SQL Server는 *암시적 인증* 을 사용 하 여 스크립트에 필요할 수 있는 로컬 ODBC 호출을 생성 합니다. 그러나 SQL Server Express Edition의 RTM 빌드에서는 이 기능이 작동하지 않았습니다.

이 문제를 해결하려면 이후 서비스 릴리스로 업그레이드하는 것이 좋습니다.

업그레이드가 불가능 한 경우에는 SQL 로그인을 사용 하 여 포함 된 ODBC 호출이 필요할 수 있는 원격 R 작업을 실행할 수 있습니다.

**적용 대상:** SQL Server 2016 R Services Express Edition

### <a name="11-performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>11. SQL Server에서 사용 하는 라이브러리가 다른 도구에서 호출 되는 경우의 성능 제한

RGui와 같은 외부 응용 프로그램에서 SQL Server 용으로 설치 된 기계 학습 라이브러리를 호출할 수 있습니다. 이렇게 하면 새 패키지를 설치 하거나 매우 짧은 코드 샘플에서 임시 테스트를 실행 하는 등의 특정 작업을 수행할 수 있는 가장 편리한 방법이 될 수 있습니다. 그러나 SQL Server 외부에서는 성능이 제한 될 수 있습니다. 

예를 들어 SQL Server의 Enterprise Edition을 사용 하는 경우에도 R 코드를 외부 도구를 사용 하 여 실행할 때 R은 단일 스레드 모드로 실행 됩니다. SQL Server의 성능 이점을 얻으려면 SQL Server 연결을 시작 하 고 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 를 사용 하 여 외부 스크립트 런타임을 호출 합니다.

일반적으로 외부 도구의 SQL Server에서 사용 하는 기계 학습 라이브러리를 호출 하지 마세요. R 또는 Python 코드를 디버깅 해야 하는 경우에는 일반적으로 SQL Server 외부에서 수행 하는 것이 더 쉽습니다. SQL Server에 있는 동일한 라이브러리를 얻으려면 Microsoft R Client, [SQL Server 2017 Machine Learning Server (독립 실행형)](install/sql-machine-learning-standalone-windows-install.md)또는 [SQL Server 2016 R 서버 (독립 실행형)](install/sql-r-standalone-windows-install.md)를 설치할 수 있습니다.

### <a name="12-sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>12. SQL Server Data Tools는 외부 스크립트에 필요한 사용 권한을 지원 하지 않습니다.

Visual Studio 또는 SQL Server Data Tools를 사용 하 여 데이터베이스 프로젝트를 게시할 때 외부 스크립트 실행에 대 한 권한이 있는 보안 주체가 있으면 다음과 같은 오류가 발생할 수 있습니다.

> *TSQL 모델: 데이터베이스를 리버스 엔지니어링 하는 동안 오류가 발생 했습니다. 사용 권한을 인식할 수 없으며 가져오지 못했습니다.*

현재 DACPAC 모델은 R Services 또는 Machine Learning Services에서 사용 하는 사용 권한을 지원 하지 않습니다. 예를 들어 모든 외부 스크립트를 부여 하거나 외부 스크립트를 실행할 수 있습니다. 이 문제는 향후 릴리스에서 해결될 예정입니다.

이 문제를 해결 하려면 배포 후 스크립트에서 추가 GRANT 문을 실행 합니다.

### <a name="13-external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>13. 리소스 거 버 넌 스 기본값으로 인해 외부 스크립트 실행이 제한 됩니다.

Enterprise Edition에서 리소스 풀을 사용하여 외부 스크립트 프로세스를 관리할 수 있습니다. 일부 초기 릴리스 빌드에서는 R 프로세스에 할당 될 수 있는 최대 메모리가 20% 였습니다. 따라서 서버에 32 GB의 RAM이 있는 경우 R 실행 파일 (RTerm .exe 및 BxlServer .exe)은 단일 요청에 최대 6.4 GB를 사용할 수 있습니다.

리소스 제한 사항이 발생 하는 경우 현재 기본값을 확인 합니다. 20%가 충분 하지 않은 경우이 값을 변경 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 하는 방법에 대 한 설명서를 참조 하세요.

**적용 대상:** SQL Server 2016 R Services, Enterprise Edition

## <a name="r-script-execution-issues"></a>R 스크립트 실행 문제

이 섹션에는 SQL Server에서 R을 실행 하는 것과 관련 된 알려진 문제 뿐만 아니라 Microsoft에서 게시 한 R 라이브러리 및 도구와 관련 된 몇 가지 문제 (RevoScaleR 포함)가 포함 되어 있습니다.

R 솔루션에 영향을 줄 수 있는 알려진 추가 문제는 [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues) 사이트를 참조 하십시오.

### <a name="1-access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>1. 기본 위치가 아닌 위치에 있는 SQL Server에서 R 스크립트를 실행할 때 액세스 거부 경고

SQL Server 인스턴스가 `Program Files` 폴더 외부와 같이 기본이 아닌 위치에 설치 된 경우에는 패키지를 설치 하는 스크립트를 실행 하려고 할 때 ACCESS_DENIED 경고가 발생 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

> *위치 `normalizePath(path.expand(path), winslash, mustWork)` : 경로 [2] = "~ externallibraries/R/8/1": 액세스가 거부 되었습니다.*

그 이유는 R 함수가 경로를 읽으려고 시도 하 고 기본 제공 사용자 그룹 **SQLRUserGroup**에 읽기 권한이 없는 경우 실패 하는 것입니다. 발생 한 경고는 현재 R 스크립트의 실행을 차단 하지 않지만 사용자가 다른 R 스크립트를 실행할 때마다 경고가 반복적으로 되풀이 될 수 있습니다.

SQL Server를 기본 위치에 설치한 경우 모든 Windows 사용자에 게 `Program Files` 폴더에 대 한 읽기 권한이 있으므로이 오류가 발생 하지 않습니다.

이 문제 ia는 예정 된 서비스 릴리스에서 해결 되었습니다. 이 문제를 해결 하려면의 `ExternalLibraries`모든 부모 폴더에 대 한 읽기 권한이 있는 **SQLRUserGroup**그룹을 제공 합니다.

### <a name="2-serialization-error-between-old-and-new-versions-of-revoscaler"></a>2. 이전 버전 및 새 버전의 RevoScaleR 간에 Serialization 오류가 발생 했습니다.

Serialize 된 형식을 사용 하 여 모델을 원격 SQL Server 인스턴스에 전달 하면 다음과 같은 오류가 발생할 수 있습니다. 

> *Memdecompress 풀기 (데이터, 유형 = 압축 풀기)에서 오류가 발생 했습니다. memDecompress 풀기 (2)에서 내부 오류-3입니다.*

이 오류는 직렬화 함수 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)의 최신 버전을 사용 하 여 모델을 저장 했지만 모델을 deserialize 하는 SQL Server 인스턴스에 SQL SERVER 2017 CU2 이전 버전에서 RevoScaleR api의 이전 버전이 있는 경우에 발생 합니다.

해결 방법으로 SQL Server 2017 인스턴스를 CU3 이상으로 업그레이드할 수 있습니다.

API 버전이 동일 하거나 이전 직렬화 함수를 사용 하 여 저장 된 모델을 최신 버전의 serialization API를 사용 하는 서버로 이동 하는 경우에는 오류가 표시 되지 않습니다.

즉, serialization 및 deserialization 작업에 동일한 버전의 RevoScaleR를 사용 합니다.

### <a name="3-real-time-scoring-does-not-correctly-handle-the-_learningrate_-parameter-in-tree-and-forest-models"></a>3. 실시간 점수 매기기는 트리 및 포리스트 모델에서 _learningRate_ 매개 변수를 올바르게 처리 하지 않습니다.

의사 결정 트리 또는 의사 결정 포리스트 방법을 사용 하 여 모델을 만들고 학습 률을 지정 하는 경우를 사용 하는 것 `sp_rxpredict` 과 비교 하 `PREDICT` 여 또는 SQL 함수 `rxPredict`를 사용할 때 일관 되지 않은 결과가 나타날 수 있습니다.

원인은 직렬화 된 모델을 처리 하 고 `learningRate` 매개 변수로 제한 되는 API의 오류입니다 (예: [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)).

이 문제는 예정 된 서비스 릴리스에서 해결 될 예정입니다.

### <a name="4-limitations-on-processor-affinity-for-r-jobs"></a>4. R 작업에 대한 프로세서 선호도 제한

SQL Server 2016의 초기 릴리스 빌드에서는 첫 번째 k 그룹의 Cpu에 대해서만 프로세서 선호도를 설정할 수 있습니다. 예를 들어 서버가 두 개의 k 그룹이 있는 2 소켓 컴퓨터 이면 첫 번째 k 그룹의 프로세서만 R 프로세스에 사용 됩니다. R 스크립트 작업에 대 한 리소스 관리를 구성 하는 경우에도 동일한 제한이 적용 됩니다.

이 문제는 SQL Server 2016 서비스 팩 1에서 해결되었습니다. 최신 서비스 릴리스로 업그레이드 하는 것이 좋습니다.

**적용 대상:** SQL Server 2016 R Services RTM 버전

### <a name="5-changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>5. SQL Server 컴퓨팅 컨텍스트에서 데이터를 읽는 경우 열 형식을 변경할 수 없음

컴퓨팅 컨텍스트가 SQL Server 인스턴스로 설정된 경우 _colClasses_ 인수(또는 다른 유사한 인수)를 사용하여 R 코드에서 열의 데이터 형식을 변경할 수 없습니다.

예를 들어 CRSDepTimeStr 열이 정수가 아닌 경우 다음 문에서 오류가 발생합니다.

```R
data <- RxSqlServerData(
  sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall", 
  connectionString = connectionString, 
  colClasses = c(CRSDepTimeStr = "integer"))
```

이 문제를 해결 하려면 CAST 또는 CONVERT를 사용 하 고 올바른 데이터 형식을 사용 하 여 데이터를 R로 제공 하도록 SQL 쿼리를 다시 작성 하면 됩니다. 일반적으로 R 코드에서 데이터를 변경 하는 대신 SQL을 사용 하 여 데이터 작업을 하는 경우 성능이 향상 됩니다.

**적용 대상:** SQL Server 2016 R Services

### <a name="6-limits-on-size-of-serialized-models"></a>6. 직렬화 된 모델 크기 제한

모델을 SQL Server 테이블에 저장 하는 경우 모델을 직렬화 하 고 이진 형식으로 저장 해야 합니다. 이론적으로이 메서드를 사용 하 여 저장할 수 있는 모델의 최대 크기는 SQL Server에서 varbinary 열의 최대 크기인 2gb입니다.

더 큰 모델을 사용 해야 하는 경우 다음 해결 방법을 사용할 수 있습니다.

+ 모델 크기를 줄이기 위한 단계를 수행 합니다. 일부 오픈 소스 R 패키지에는 모델 개체에 대 한 많은 정보가 포함 되어 있으며이 정보 중 상당수는 배포를 위해 제거할 수 있습니다. 
+ 기능 선택을 사용 하 여 불필요 한 열을 제거 합니다.
+ 오픈 소스 알고리즘을 사용 하는 경우 MicrosoftML 또는 RevoScaleR에서 해당 하는 알고리즘을 사용 하 여 유사한 구현을 고려 합니다. 이러한 패키지는 배포 시나리오에 맞게 최적화 되었습니다.
+ 모델을 합리적으로 만들고 이전 단계를 사용 하 여 크기를 줄인 후에는 기본 R의 [Memcompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress) 함수를 사용 하 여 모델을 SQL Server 전달 하기 전에 모델 크기를 줄일 수 있는지 여부를 확인 합니다. 이 옵션은 모델이 2gb 제한에 근접 한 경우에 가장 적합 합니다.
+ 큰 모델의 경우 varbinary 열을 사용 하지 않고 SQL Server [FileTable](../relational-databases/blob/filetables-sql-server.md) 기능을 사용 하 여 모델을 저장할 수 있습니다.

    Filetable를 사용 하려면 Filetable에 저장 된 데이터가 SQL Server의 Filestream 파일 시스템 드라이버에 의해 관리 되 고 기본 방화벽 규칙이 네트워크 파일 액세스를 차단 하기 때문에 방화벽 예외를 추가 해야 합니다. 자세한 내용은 [FileTable에 대 한 필수 구성 요소 사용](../relational-databases/blob/enable-the-prerequisites-for-filetable.md)을 참조 하세요.

    FileTable을 사용 하도록 설정한 후 모델을 쓰려면 FileTable API를 사용 하 여 SQL에서 경로를 가져온 다음 코드에서 해당 위치에 모델을 씁니다. 모델을 읽어야 하는 경우 SQL에서 경로를 가져온 다음 스크립트의 경로를 사용 하 여 모델을 호출 합니다. 자세한 내용은 [파일 입/출력 api를 사용 하 여 Filetable 액세스](../relational-databases/blob/access-filetables-with-file-input-output-apis.md)를 참조 하세요.

### <a name="7-avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>7. 계산 컨텍스트에서 R 코드를 실행 하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 경우 작업 영역 지우기 방지

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 계산 컨텍스트에서 r 코드를 실행 하는 동안 r 명령을 사용 하 여 개체의 작업 영역을 지우거 나 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용 하 여 호출 된 r 스크립트의 일부로 작업 영역을 지우는 경우 작업 영역에서 다음 오류가 발생할 수 있습니다.  *revoScriptConnection 개체를 찾을 수 없습니다* .

`revoScriptConnection` 은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 호출된 R 세션에 대한 정보를 포함하는 R 작업 영역의 개체입니다. 그러나 R 코드에 작업 영역을 지우는 명령(예: `rm(list=ls()))`)이 포함되어 있으면 세션 및 R 작업 영역의 다른 개체에 대한 모든 정보도 지워집니다.

이 문제를 해결 하려면에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]R을 실행 하는 동안 변수 및 기타 개체를 무분별 지우는 것이 좋습니다. R 콘솔에서 작업 하는 경우 작업 영역을 지우는 것이 일반적 이지만 의도 하지 않은 결과가 발생할 수 있습니다.

* 특정 변수를 삭제 하려면 R `remove` 함수를 사용 합니다. 예를 들면 다음과 같습니다.`remove('name1', 'name2', ...)`
* 삭제할 변수가 여러 개인 경우 임시 변수 이름을 목록에 저장하고 주기적 가비지 수집을 수행합니다.

### <a name="8-restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>8. R 스크립트의 입력으로 제공될 수 있는 데이터에 대한 제한

R 스크립트에서는 다음 유형의 쿼리 결과를 사용할 수 없습니다.

- AlwaysEncrypted 열을 참조하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리의 데이터
  
- 마스킹된 열을 참조하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리의 데이터
  
     R 스크립트에서 마스킹된 데이터를 사용해야 하는 경우 가능한 해결 방법은 임시 테이블에 데이터 복사본을 만들고 해당 데이터를 대신 사용하는 것입니다.

### <a name="9-use-of-strings-as-factors-can-lead-to-performance-degradation"></a>9. 문자열을 요소로 사용 하면 성능이 저하 될 수 있습니다.

문자열 유형 변수를 요소로 사용 하면 R 작업에 사용 되는 메모리의 양을 크게 늘릴 수 있습니다. 이것은 일반적으로 R의 알려진 문제 이며 주제에 많은 문서가 있습니다. 예를 들어 [r의 경우 첫 번째 클래스가 아니라 r, John Mount, r-블로거)](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/) 또는 [stringsAsFactors에 대 한 요소를 참조 하세요. Roger Peng](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/)에의 한 권한 없는 소개. 

이 문제는 SQL Server 관련 되지 않지만 SQl Server에서 실행 되는 R 코드의 성능에 큰 영향을 줄 수 있습니다. 문자열은 일반적으로 varchar 또는 nvarchar로 저장 되 고, 문자열 데이터의 열에 고유 값이 많으면 내부적으로 이러한 값을 정수로 변환 하 고 R에 의해 문자열로 다시 변환 하는 과정에서 메모리 할당 오류가 발생할 수 있습니다.

다른 작업에 문자열 데이터 형식이 반드시 필요한 것은 아니지만 데이터 준비의 일부로 문자열 값을 숫자 (정수) 데이터 형식에 매핑하면 성능 및 확장 관점에서 도움이 됩니다.

이 문제와 기타 팁에 대 한 자세한 내용은 [R Services에 대 한 성능-데이터 최적화](r/r-and-data-optimization-r-services.md)를 참조 하세요.

### <a name="10-arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>10. SQL Server 데이터 원본에 대 한 인수 *Varstokeep* 및 *varstokeep* 은 지원 되지 않습니다.

RxDataStep 함수를 사용 하 여 테이블에 결과를 쓸 때는 *Varstokeep* 및 *varstokeep* 을 사용 하 여 작업의 일부로 포함 하거나 제외할 열을 쉽게 지정할 수 있습니다. 그러나 SQL Server 데이터 원본에 대해서는 이러한 인수를 사용할 수 없습니다.

### <a name="11-limited-support-for-sql-data-types-in-sp_execute_external_script"></a>11. Sp\_execute\_외부스크립트에서SQL데이터형식에대한제한된지원\_

SQL에서 지원 되는 모든 데이터 형식을 R에서 사용할 수 있는 것은 아닙니다. 문제를 해결 하려면 sp\_실행\_외부\_스크립트에 데이터를 전달 하기 전에 지원 되지 않는 데이터 형식을 지원 되는 데이터 형식으로 캐스팅 하는 것이 좋습니다.

자세한 내용은 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)을 참조 하세요.

### <a name="12-possible-string-corruption-using-unicode-strings-in-varchar-columns"></a>12. Varchar 열에서 유니코드 문자열을 사용 하 여 가능한 문자열 손상

에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] R/Python으로 varchar 열의 유니코드 데이터를 전달 하면 문자열이 손상 될 수 있습니다. 이는 데이터 정렬의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이러한 유니코드 문자열에 대 한 인코딩이 R/Python에서 사용 되는 기본 utf-8 인코딩과 일치 하지 않을 수 있기 때문입니다. 

에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] R/Python으로 ASCII가 아닌 문자열 데이터를 전송 하려면 utf-8 인코딩 (에서 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]사용 가능)을 사용 하거나 동일한에 nvarchar 형식을 사용 합니다.

### <a name="13-only-one-value-of-type-raw-can-be-returned-from-sp_execute_external_script"></a>13. 형식의 `raw` 값은 하나만 반환할 수 있습니다.`sp_execute_external_script`

R에서 이진 데이터 형식 (R **원시** 데이터 형식)이 반환 되는 경우 해당 값은 출력 데이터 프레임에 전송 되어야 합니다.

**Raw**이외의 데이터 형식을 사용 하는 경우 OUTPUT 키워드를 추가 하 여 저장 프로시저의 결과와 함께 매개 변수 값을 반환할 수 있습니다. 자세한 내용은 [매개 변수](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters)를 참조 하세요.

**Raw**유형의 값을 포함 하는 여러 출력 집합을 사용 하려면 저장 프로시저를 여러 번 호출 하거나 ODBC를 사용 하 여 결과 집합을로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 다시 전송 하는 것이 좋습니다.

### <a name="14-loss-of-precision"></a>14. 정밀도 손실

및 [!INCLUDE[tsql](../includes/tsql-md.md)] R은 다양 한 데이터 형식을 지원 하므로 숫자 데이터 형식의 경우 변환 하는 동안 정밀도가 떨어질 수 있습니다.

암시적 데이터 형식 변환에 대 한 자세한 내용은 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)을 참조 하세요.

### <a name="15-variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>15. TransformFunc 매개 변수를 사용 하는 경우 변수 범위 지정 오류

모델링 하는 동안 데이터를 변환 하려면 또는 `rxLogit`와 `rxLinmod` 같은 함수에 *transformFunc* 인수를 전달 하면 됩니다. 그러나 중첩 된 함수 호출은 로컬 계산 컨텍스트에서 올바르게 작동 하는 경우에도 SQL Server 계산 컨텍스트에서 범위 지정 오류를 일으킬 수 있습니다.

> *분석에 대 한 샘플 데이터 집합에 변수가 없습니다.*

예를 들어 로컬 전역 환경 `f` 에서 및 `g`라는 두 개의 함수를 정의 하 고 `g` 를 호출 `f`한다고 가정 합니다. `f` 와 관련 `g`된 분산 또는 원격 호출에서는와 `g` 를 `g` 원격 호출에 전달한 경우에도 `f` 를 찾을 수 없기 때문에에 대 한 호출이 실패할 수 있습니다.

이 문제가 발생한 경우 `f` 의 정의를 `g`의 정의 내에 포함하여 문제를 해결할 수 있습니다. `g` 앞의 모든 곳에서 `f`를 정상적으로 호출합니다.

이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

```R
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

오류를 방지 하려면 다음과 같이 정의를 다시 작성 합니다.

```R
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="16-data-import-and-manipulation-using-revoscaler"></a>16. RevoScaleR을 사용하여 데이터 가져오기 및 조작

데이터베이스에서 **varchar** 열을 읽는 경우 공백이 잘립니다. 이를 방지하려면 공백이 아닌 문자로 문자열을 묶습니다.

와 `rxDataStep` 같은 함수를 사용 하 여 **varchar** 열이 있는 데이터베이스 테이블을 만드는 경우 열 너비는 데이터의 샘플을 기반으로 예상 됩니다. 너비가 달라질 수 있는 경우 모든 문자열을 일반 길이로 패딩 해야 할 수 있습니다.

`rxImport` 또는 `rxTextToXdf` 에 대한 반복된 호출을 사용하여 행을 가져오고 추가하면서 여러 입력 파일을 단일.xdf 파일에 통합하는 경우 변환을 사용하여 변수의 데이터 형식을 변경할 수 없습니다.

### <a name="17-limited-support-for-rxexec"></a>17. RxExec에 대 한 제한 된 지원

SQL Server 2016 `rxExec` 에서는 RevoScaleR 패키지에서 제공 하는 함수를 단일 스레드 모드 에서만 사용할 수 있습니다.

### <a name="18-increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>18. RxGetVarInfo를 지원 하도록 최대 매개 변수 크기 늘리기

매우 많은 수의 변수가 있는 데이터 집합을 사용 하는 경우 (예: 4만 초과)에서와 `max-ppsize` `rxGetVarInfo`같은 함수를 사용 하려면 R을 시작할 때 플래그를 설정 합니다. `max-ppsize` 플래그는 포인터 보호 스택의 최대 크기를 지정합니다.

R 콘솔을 사용 하는 경우 (예: RGui .exe 또는 Rgui) 다음을 입력 하 여 _max-ppsize_ 값을 50만로 설정할 수 있습니다.

```R
R --max-ppsize=500000
```

### <a name="19-issues-with-the-rxdtree-function"></a>19. RxDTree 함수 문제

`rxDTree` 함수는 현재 수식 내 변환을 지원하지 않습니다. 특히 즉석에서 요소를 만들기 위해 `F()` 구문을 사용하는 것은 지원되지 않습니다. 그러나 숫자 데이터는 자동으로 범주화 됩니다.

순서가 지정된 요소는 `rxDTree`를 제외하고 모든 RevoScaleR 분석 함수의 요소와 동일하게 처리됩니다.

### <a name="20-datatable-as-an-outputdataset-in-r"></a>20. R의 OutputDataSet 인 Data. table

SQL Server `data.table` 2017 누적 `OutputDataSet` 업데이트 13 (CU13) 및 이전 버전에서는 R에서로를 사용 하는 것이 지원 되지 않습니다. 다음과 같은 메시지가 나타날 수 있습니다.

```
Msg 39004, Level 16, State 20, Line 2
A 'R' script error occurred during execution of 
'sp_execute_external_script' with HRESULT 0x80004004.
Msg 39019, Level 16, State 2, Line 2
An external script error occurred: 
Error in alloc.col(newx) : 
  Internal error: length of names (0) is not length of dt (11)
Calls: data.frame ... as.data.frame -> as.data.frame.data.table -> copy -> alloc.col

Error in execution.  Check the output for more information.
Error in eval(expr, envir, enclos) : 
  Error in execution.  Check the output for more information.
Calls: source -> withVisible -> eval -> eval -> .Call
Execution halted
```

`data.table`R의 `OutputDataSet` 는 SQL Server 2017 누적 업데이트 14 (CU14) 이상에서 지원 됩니다.

## <a name="python-script-execution-issues"></a>Python 스크립트 실행 문제

이 섹션에는 SQL Server에서 Python을 실행 하는 것과 관련 된 알려진 문제 및 Microsoft에서 게시 한 Python 패키지와 관련 된 문제 ( [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 및 [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)포함)가 포함 되어 있습니다.

### <a name="1-call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>1. 모델에 대 한 경로가 너무 긴 경우 사전 학습 된 모델에 대 한 호출이 실패 합니다.

SQL Server 2017의 초기 릴리스에 미리 학습 된 모델을 설치한 경우 학습 된 모델 파일의 전체 경로가 너무 길어서 Python을 읽을 수 없습니다. 이 제한은 이후 서비스 릴리스에서 해결 되었습니다.

몇 가지 잠재적인 해결 방법이 있습니다. 

+ 미리 학습 된 모델을 설치 하는 경우 사용자 지정 위치를 선택 합니다.
+ 가능 하면 C:\SQL\MSSQL14.와 같이 더 짧은 경로를 사용 하 여 사용자 지정 설치 경로 아래에 SQL Server 인스턴스를 설치 합니다. MSSQLSERVER.
+ Windows 유틸리티 [Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) 을 사용 하 여 더 짧은 경로에 모델 파일을 매핑하는 하드 링크를 만듭니다.
+ 최신 서비스 릴리스로 업데이트 합니다.

### <a name="2-error-when-saving-serialized-model-to-sql-server"></a>2. SQL Server 직렬화 된 모델을 저장할 때 오류 발생

원격 SQL Server 인스턴스에 모델을 전달 하 고 `rx_unserialize` [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)의 함수를 사용 하 여 이진 모델을 읽으려고 하면 다음과 같은 오류가 발생할 수 있습니다. 

> *NameError: 이름이 ' rx_unserialize_model '이 (가) 정의 되지 않았습니다.*

이 오류는 최신 버전의 serialization 함수를 사용 하 여 모델을 저장 했지만 모델을 deserialize 하는 SQL Server 인스턴스가 serialization API를 인식 하지 못하는 경우에 발생 합니다.

이 문제를 해결 하려면 SQL Server 2017 인스턴스를 CU3 이상으로 업그레이드 합니다.

### <a name="3-failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>3. Varbinary 변수를 초기화 하지 못하여 BxlServer에서 오류가 발생 함

을 사용 하 여 `sp_execute_external_script`SQL Server에서 Python 코드를 실행 하 고 코드에 varbinary (max), varchar (max) 또는 유사한 형식의 출력 변수가 있는 경우 변수를 초기화 하거나 스크립트의 일부로 설정 해야 합니다. 그렇지 않으면 데이터 교환 구성 요소인 BxlServer가 오류를 발생 시키고 작동이 중지 됩니다.

이 제한은 예정 된 서비스 릴리스에서 수정 될 예정입니다. 이 문제를 해결 하려면 변수가 Python 스크립트 내에서 초기화 되었는지 확인 합니다. 다음 예와 같이 유효한 값을 사용할 수 있습니다.

```sql
declare @b varbinary(max);
exec sp_execute_external_script
  @language = N'Python'
  , @script = N'b = 0x0'
  , @params = N'@b varbinary(max) OUTPUT'
  , @b = @b OUTPUT;
go
```

```sql
declare @b varchar(30);
exec sp_execute_external_script
  @language = N'Python'
  , @script = N' b = ""  '
  , @params = N'@b varchar(30) OUTPUT'
  , @b = @b OUTPUT;
go
```

### <a name="4-telemetry-warning-on-successful-execution-of-python-code"></a>4. Python 코드가 성공적으로 실행 되는 경우 원격 분석 경고

SQL Server 2017 CU2부터 Python 코드가 성공적으로 실행 되는 경우에도 다음 메시지가 나타날 수 있습니다.

> *외부 스크립트의 STDERR 메시지:* 
>  *~ PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: telemetry_state가 전역 선언 이전에 사용 되었습니다* .

이 문제는 SQL Server 2017 누적 업데이트 3 (CU3)에서 해결 되었습니다. 

### <a name="5-numeric-decimal-and-money-data-types-not-supported"></a>5. 숫자, 10 진수 및 money 데이터 형식이 지원 되지 않음

에서 Python `sp_execute_external_script`을 사용 하는 경우 2017 CU12 (누적 업데이트 12) SQL SERVER부터 결과 집합의 numeric, decimal 및 money 데이터 형식은 지원 되지 않습니다. 다음과 같은 메시지가 나타날 수 있습니다.

> *Code 39004, SQL 상태: S1000] HRESULT 0x80004004를 사용 하 여 실행 하는 동안 ' Python ' 스크립트 오류가 발생 했습니다.*

> *Code 39019, SQL 상태: S1000] 외부 스크립트 오류가 발생 했습니다.*
> 
> *SqlSatelliteCall 오류: 출력 스키마에 지원 되지 않는 형식이 있습니다. 지원 되는 형식: bit, smallint, int, datetime, smallmoney, real 및 float. char, varchar는 부분적으로 지원 됩니다.*

이 문제는 SQL Server 2017 누적 업데이트 14 (CU14)에서 수정 되었습니다.

### <a name="6-bad-interpreter-error-when-installing-python-packages-with-pip-on-linux"></a>6. Linux에서 pip를 사용 하 여 Python 패키지를 설치할 때 잘못 된 인터프리터 오류 

SQL Server 2019에서 **pip**를 사용 하려고 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

```bash
/opt/mssql/mlservices/runtime/python/bin/pip -h
```

그러면이 오류가 발생 합니다.

> *bash:/opt/mssql/mlservices/runtime/python/bin/pip:/opt/microsoft/mlserver/9.4.7/bin/python/python: 잘못 된 인터프리터: 해당 파일 또는 디렉터리가 없습니다.*

**해결 방법**

[Python 패키지 기관 (PyPA)](https://www.pypa.io)에서 **pip** 를 설치 합니다.

```bash
wget 'https://bootstrap.pypa.io/get-pip.py' 
/opt/mssql/mlservices/bin/python/python ./get-pip.py 
```

**권장**

[Sqlmlutils를 사용 하 여 Python 패키지 설치](package-management/install-additional-python-packages-on-sql-server.md)를 참조 하세요.

**적용 대상:** Linux에서 2019 SQL Server

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise 및 Microsoft R Open

이 섹션에서는 혁명 분석에서 제공 하는 R 연결, 개발 및 성능 도구와 관련 된 문제를 나열 합니다. 이러한 도구는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]이전 시험판 버전에서 제공 되었습니다.

일반적으로 이러한 이전 버전을 제거 하 고 SQL Server 또는 Microsoft R Server 최신 버전을 설치 하는 것이 좋습니다.

### <a name="1-revolution-r-enterprise-is-not-supported"></a>1. 혁명 R Enterprise는 지원 되지 않습니다.

모든 버전의 [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] 와 함께 혁명 R Enterprise를 함께 설치 하는 것은 지원 되지 않습니다.

R Enterprise에 대 한 기존 라이선스가 있는 경우 인스턴스 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결 하는 데 사용할 모든 워크스테이션과 별도의 컴퓨터에이 라이선스를 넣어야 합니다.

의 [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] 일부 시험판 버전에는 회전축 분석에서 만든 Windows 용 R 개발 환경이 포함 되어 있습니다. 이 도구는 더 이상 제공 되지 않으며 지원 되지 않습니다.

와 [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]의 호환성을 위해 Microsoft R Client를 대신 설치 하는 것이 좋습니다. [Visual Studio용 R 도구](https://www.visualstudio.com/vs/rtvs/) 및 [Visual Studio Code](https://code.visualstudio.com/) 도 Microsoft R 솔루션을 지원 합니다.

### <a name="2-compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>2. SQLite ODBC 드라이버와 RevoScaleR의 호환성 문제

SQLite ODBC 드라이버의 수정 버전 0.92이 RevoScaleR와 호환 되지 않습니다. 0\.88 ~-0.91 및 0.93 이상 버전은 호환 가능한 것으로 알려져 있습니다.

## <a name="next-steps"></a>다음 단계

[SQL Server에서 기계 학습 문제 해결](machine-learning-troubleshooting-faq.md)
