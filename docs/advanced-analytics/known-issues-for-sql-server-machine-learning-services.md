---
title: R 언어 및 Python 통합-SQL Server Machine Learning Services의 알려진된 문제
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 19427de01c39dc4b4578fc31db1d610af829d770
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62650704"
---
# <a name="known-issues-in-machine-learning-services"></a>Machine Learning Services의 알려진된 문제
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 아티클에서 알려진된 문제 또는 기계 학습 구성 요소에 옵션으로 제공 되는 제한 사항 [SQL Server 2016 R Services](install/sql-r-services-windows-install.md) 고 [SQL Server 2017 Machine Learning Services R 및 Python](install/sql-machine-learning-services-windows-install.md).

## <a name="setup-and-configuration-issues"></a>설치 및 구성 문제

프로세스 및 초기 설치 및 구성과 관련 된 일반적인 질문에 대 한 참조 [업그레이드 및 설치 FAQ](r/upgrade-and-installation-faq-sql-server-r-services.md)합니다. 업그레이드, side-by-side-설치 및 새 R 또는 Python 구성 요소를 설치 하는 방법에 대 한 정보를 포함 하는 것입니다.

### <a name="1-inconsistent-results-in-mkl-computations-due-to-missing-environment-variable"></a>1. MKL 계산 환경 변수 누락으로 인해 일관성 없는 결과가

**적용 대상:** R_SERVER 이진 파일 9.0, 9.1, 9.2 또는 9.3.

R_SERVER는 Intel 수학 커널 라이브러리 (MKL)를 사용합니다. MKL을 포함 하는 계산에 시스템 환경 변수를 누락 된 경우 일관성 없는 결과가 발생할 수 있습니다. 

환경 변수를 설정 `'MKL_CBWR'=AUTO` R_SERVER에서 조건부 숫자 재현 되도록 합니다. 자세한 내용은 [소개에 조건부 숫자 재현성 (CNR)](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)합니다.

**해결 방법**

1. 제어판에서 클릭 **시스템 및 보안** > **System** > **고급 시스템 설정**  >   **환경 변수**합니다.

2. 새 사용자 또는 시스템 변수를 만듭니다. 

  + 변수 이름을 'MKL_CBWR'로 설정 합니다.
  + '자동'으로 '변수 값'을 설정 합니다.

3. R_SERVER 다시 시작 합니다. SQL Server에서 SQL Server 실행 패드 서비스를 다시 시작할 수 있습니다.

> [!NOTE]
> Linux의 SQL Server 2019 Preview를 실행 하는 경우 편집 하거나 만들 *.bash_profile* 사용자 홈 디렉터리에서 줄을 추가 `export MKL_CBWR="AUTO"`합니다. 이 파일을 입력 하 여 실행 `source .bash_profile` bash 명령 프롬프트에서. R_SERVER 입력 하 여 다시 시작 `Sys.getenv()` R 명령 프롬프트에서.

### <a name="2-r-script-runtime-error-sql-server-2017-cu5-cu7-regression"></a>2. R 스크립트 런타임 오류 (SQL Server 2017 CU5-CU7 회귀)

SQL Server 2017 누적 업데이트 5-7, 방법이에서 회귀 된 **rlauncher.config** 임시 디렉터리의 파일 경로 공백이 있는 파일입니다. 이 회귀 CU8에서 수정 됩니다.

R 스크립트를 실행 하는 경우 표시 됩니다 오류는 다음 메시지를 포함 합니다.

> *'R' 스크립트의 런타임과 통신할 수 없습니다. 'R' 런타임의 요구 사항을 확인 하세요.*
>
> 외부 스크립트의 STDERR 메시지: 
>
> *심각한 오류: 'R_TempDir'를 만들 수 없습니다.*

**해결 방법**

사용 가능 해지면 CU8을 적용 합니다. 또는 다시 만들 수 있습니다 **rlauncher.config** 실행 하 여 **registerrext** 제거한 후 설치 관리자 권한 명령 프롬프트에서를 사용 하 여 합니다. 

```cmd
<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /uninstall /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>

<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /install /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>
```

다음 예제에서는 "MSSQL14 기본 인스턴스가 사용 하 여 명령. MSSQLSERVER"설치" C:\Program Files\Microsoft SQL Server\":

```cmd
"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /uninstall /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER

"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /install /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER
```

### <a name="3-unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>3. 도메인 컨트롤러에 SQL Server machine learning 기능을 설치할 수 없습니다.

도메인 컨트롤러에 SQL Server 2016 R Services 또는 SQL Server 2017의 Machine Learning Services를 설치 하려고 하면 이러한 오류와 함께 설치가 실패 합니다.

> *기능 설치 프로세스 중 오류가 발생 했습니다.*
> 
> *그룹 id를 찾을 수 없습니다.*
> 
> *구성 요소 오류 코드: 0x80131509*

오류는 도메인 컨트롤러에서 서비스에는 기계 학습을 실행 하는 데 필요한 20 로컬 계정을 만들 없기 때문에 발생 합니다. 일반적으로 도메인 컨트롤러에 SQL Server를 설치 하지 않는 것이 좋습니다. 자세한 내용은 [지원 공지 2032911](https://support.microsoft.com/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont)합니다.

### <a name="4-install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>4. Microsoft R Client와 호환성을 위해 최신 서비스 릴리스 설치

최신 버전의 Microsoft R Client를 설치 하 고 SQL Server에서 원격 계산 컨텍스트에서 R을 실행 하는 경우 다음과 같은 오류가 표시 될 수 있습니다.

> *Microsoft R Client의 버전 9.x.x를 실행 하는 컴퓨터에 Microsoft R Server 버전 8.x.x와 호환 되지 않습니다. 호환되는 버전을 다운로드하여 설치하세요.*

SQL Server 2016 클라이언트에서 R 라이브러리 서버에서 R 라이브러리는 정확히 일치 해야 합니다. 제한이 없어졌습니다 릴리스에 대 한 R Server 9.0.1 이상. 그러나이 오류가 발생 하는 경우 클라이언트와 서버에서 사용 되 고, 필요한 경우 서버 버전과 일치 하도록 클라이언트를 업데이트 하는 R 라이브러리의 버전을 확인 합니다.

SQL Server R Services를 사용 하 여 설치 된 R 버전은 SQL Server 서비스 릴리스 설치 될 때마다 업데이트 됩니다. 했는지 확인 하십시오는 항상 최신 버전의 R 구성 요소에서 모든 서비스 팩을 설치 해야 합니다.

Microsoft R Client 9.0.0와의 호환성을 위해이 설명 하는 업데이트를 설치 [지원 문서](https://support.microsoft.com/kb/3210262)합니다.

R 패키지를 사용 하 여 문제를 방지 하려면 업그레이드할 수도 있습니다에 설명 된 대로 최신 수명 주기 지원 정책을 사용 하 여 서비스 계약을 변경 하 여 서버에 설치 된 R 라이브러리 버전 [절로](#bkmk_sqlbindr)합니다. 이렇게 하면 machine Learning Server (이전의 Microsoft R Server)의 업데이트에 사용 되는 동일한 일정에 따라 SQL Server와 함께 설치 된 R 버전이 업데이트 됩니다.

**적용 대상:** R Server 버전 9.0.0 사용 하 여 SQL Server 2016 R Services 또는 이전 버전

### <a name="5-r-components-missing-from-cu3-setup"></a>5. CU3 설치 프로그램에서 누락 된 R 구성 요소

Azure 가상 컴퓨터 수가 제한 된 SQL Server를 사용 하 여 포함 되어야 하는 R 설치 파일이 없으면 프로 비전 됩니다. 문제는 2018-01-23 2018-01-05에서 기간에 프로 비전 된 가상 컴퓨터에 적용 됩니다. 또한이 문제를 적용 한 경우 SQL Server 2017 CU3 업데이트 기간 동안 2018-01-05에서 2018-01-23 온-프레미스 설치를 달라질 수 있습니다.

R 설치 파일의 올바른 버전을 포함 하는 제공 서비스 릴리스가 되었습니다.

+ [SQL Server 2017 KB4052987 용 누적 업데이트 패키지 3](https://www.microsoft.com/download/details.aspx?id=56128)합니다.

구성 요소를 설치 하 고 SQL Server 2017 CU3 복구를 CU3부터를 제거 하 고 업데이트 된 버전을 다시 설치 합니다.

1. R 설치 관리자를 포함 하는 업데이트 CU3 설치 파일을 다운로드 합니다.
2. CU3을 제거 합니다. 제어판에서 검색할 **업데이트를 제거할**를 선택한 다음 "SQL Server 2017 (KB4052987) (64 비트)에 대 한 핫픽스 3015"입니다. 제거 단계를 진행 합니다.
3. KB4052987 방금 다운로드 한 업데이트를 두 번 클릭 하 여 CU3 업데이트를 다시 설치: `SQLServer2017-KB4052987-x64.exe`합니다. 설치 지침을 따릅니다.

### <a name="6-unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>6. SQL Server 2017 CTP 2.0 이상 오프 라인 설치에서 Python 구성 요소를 설치할 수 없습니다.

인터넷 액세스 없이 컴퓨터에서 SQL Server 2017의 시험판 버전을 설치한 경우 설치 관리자를 다운로드 한 Python 구성 요소 위치를 묻는 페이지를 표시 하려면 실패할 수 있습니다. 이러한 상황에서 Machine Learning 서비스 기능을 사용 하지만 Python 구성 요소가 아닌를 설치할 수 있습니다.

이 문제는 릴리스 버전에서 해결 됩니다. 또한 R 구성 요소에는이 제한이 적용 되지 않습니다.

**적용 대상:** SQL Server 2017 with Python

### <a name="bkmk_sqlbindr"></a> 에 연결할 때 이전 버전 SQL Server R Services의 클라이언트에서 사용 하 여 호환 되지 않는 버전 경고 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

R 코드를 실행할 때 계산 컨텍스트를 SQL Server 2016, 다음과 같은 오류가 표시 될 수 있습니다.

> *컴퓨터에서 Microsoft R Server 버전 8.0.3과 호환되지 않는 Microsoft R Client 버전 9.0.0을 실행 중입니다. 호환되는 버전을 다운로드하여 설치하세요.*

다음 두 문 중 하나는 true 인 경우이 메시지가 표시 됩니다.

+ 설치 마법사를 사용 하 여 클라이언트 컴퓨터에서 R Server (독립 실행형)를 설치한 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]합니다.
+ 사용 하 여 Microsoft R Server를 설치 합니다 [Windows installer를 별도](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)합니다.

서버와 클라이언트에는 사용 해야 합니다. 동일한 버전을 사용 하도록 _바인딩_, Microsoft R Server 9.0(spark 및 이후 버전의 SQL Server 2016 인스턴스에 R 구성 요소를 업그레이드 하려면 지원 합니다. 확인 하려면 R Services의 버전 참조에 대 한 업그레이드를 사용할 수에 대 한 지원이 [SqlBindR.exe를 사용 하 여 R Services 인스턴스 업그레이드](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

**적용 대상:** R Server 버전 9.0.0 사용 하 여 SQL Server 2016 R Services 또는 이전 버전

### <a name="7-setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>7. SQL Server 2016 서비스 릴리스 설치 프로그램에서 최신 버전의 R 구성 요소를 설치하지 못할 수 있음

누적 업데이트를 설치 하거나 인터넷에 연결 되어 있지 않은 컴퓨터에서 SQL Server 2016 용 서비스 팩을 설치할 때 설치 마법사를 다운로드 한 CAB 파일을 사용 하 여 R 구성 요소를 업데이트할 수 있는 프롬프트를 표시 하려면 실패할 수 있습니다. 이 오류는 일반적으로 여러 구성 요소는 데이터베이스 엔진과 함께 설치 된 경우에 발생 합니다.

이 문제를 해결 명령줄을 사용 하 고 지정 하 여 서비스 릴리스를 설치할 수는 `MRCACHEDIRECTORY` CU1 업데이트를 설치 하는이 예에 표시 된 대로 인수:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

최신 설치 관리자를 참조 하세요 [인터넷에 액세스 하지 않고 기계 학습 구성 요소 설치](install/sql-ml-component-install-without-internet-access.md)합니다.

**적용 대상:** R Server 버전 9.0.0 사용 하 여 SQL Server 2016 R Services 또는 이전 버전

### <a name="8-launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>8. 실행 패드 서비스가 버전이 R 버전과 다른 경우 시작 되지 않음

데이터베이스 엔진에서 별도로 SQL Server R Services를 설치 하 고 빌드 버전이 서로 하는 경우 시스템 이벤트 로그에서 다음 오류가 표시 될 수 있습니다.

> *SQL Server 실행 패드 서비스가 다음 오류로 인해 시작 하지 못했습니다. 서비스가 적시에 시작 또는 제어 요청에 응답 하지 않았습니다.*

예를 들어이 오류 수 릴리스 버전을 사용 하 여 데이터베이스 엔진을 설치 하는 경우에 발생할 데이터베이스 엔진을 업그레이드 하는 패치가 적용 및 다음 릴리스 버전을 사용 하 여 R Services 기능을 추가

이 문제를 방지 하려면 Launchpad.exe sqldk.dll 같은 SQL 이진 파일의 버전을 사용 하 여 버전을 비교할 파일 관리자와 같은 유틸리티를 사용 합니다. 모든 구성 요소를 동일한 버전 번호가 있어야 합니다. 하나의 구성 요소를 업그레이드하는 경우 설치된 다른 모든 구성 요소에 동일한 업그레이드를 적용해야 합니다.

실행 패드에 대 한 표시는 `Binn` 인스턴스에 대 한 폴더입니다. 예를 들어, SQL Server 2016의 기본 설치에서 경로일 수 있습니다 `C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`합니다. 

### <a name="9-remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>9. 원격 계산 컨텍스트는 Azure virtual machines에서 실행 중인 SQL Server 인스턴스의 방화벽에 의해 차단

설치한 후 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Windows Azure 가상 머신에서 있습니다 못할 가상 머신의 작업 영역 사용 해야하는 계산 컨텍스트를 사용 하도록 합니다. 이유는 기본적으로 Azure 가상 머신에서 방화벽 포함 네트워크 로컬 R 사용자 계정에 대 한 액세스를 차단 하는 규칙입니다.

대 안으로, Azure VM에서 엽니다 **고급 보안이 포함 된 Windows 방화벽**를 선택 **아웃 바운드 규칙**, 다음 규칙을 사용 하지 않도록 설정: **SQL Server 인스턴스 MSSQLSERVER의에서 R 로컬 사용자 계정에 대 한 네트워크 액세스 차단**합니다. 또한 활성화 규칙을 그대로 유지 수 있지만 보안 속성을 변경 **안전한 경우 허용**합니다.

### <a name="10-implied-authentication-in-sqlexpress"></a>10. SQLEXPRESS의 암시적 인증

SQL Server를 사용 하는 통합 Windows 인증을 사용 하 여 원격 데이터 과학 워크스테이션에서 R 작업을 실행할 때 *묵시적된 인증* 스크립트에서 필요할 수 있는 로컬 ODBC 호출을 생성 합니다. 그러나 SQL Server Express Edition의 RTM 빌드에서는 이 기능이 작동하지 않았습니다.

이 문제를 해결하려면 이후 서비스 릴리스로 업그레이드하는 것이 좋습니다.

업그레이드에 적절 하지 않은 경우 대 안으로 SQL 로그인을 사용 포함 된 ODBC 호출이 필요할 수 있는 원격 R 작업을 실행 합니다.

**적용 대상:** SQL Server 2016 R Services Express Edition

### <a name="11-performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>11. 다른 도구에서 SQL Server에서 사용 되는 라이브러리 라고 하는 경우의 성능 제한

Machine learning RGui 등 외부 응용 프로그램에서 SQL Server에 설치 된 라이브러리를 호출 하는 것이 가능 합니다. 이렇게 하면 새 패키지를 설치 하거나 짧은 코드 샘플에서 임시 테스트를 실행 하는 등의 특정 태스크를 수행 하는 가장 편리한 방법은 수 있습니다. 그러나 SQL Server 외부의 성능 제한 될 수 있습니다. 

예를 들어, SQL Server의 Enterprise Edition을 사용 하는 경우에 외부 도구를 사용 하 여 R 코드를 실행 하는 경우 단일 스레드 모드에서 R 실행 합니다. SQL Server의 성능 이점을 얻으려면, SQL Server 연결을 시작 하 고 사용 하 여 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 외부 스크립트 런타임에 호출 합니다.

일반적으로 기계 학습 라이브러리 외부 도구에서 SQL Server에서 사용 되는 호출 하지 마세요. 디버그 R 또는 Python 코드 해야 할 경우 SQL Server 외부에서 이렇게 하려면 일반적으로 쉽습니다. SQL Server에 있는 것과 동일한 라이브러리를 가져오려면 Microsoft R Client를 설치할 수 있습니다 [SQL Server 2017 Machine Learning Server (독립 실행형)](install/sql-machine-learning-standalone-windows-install.md), 또는 [SQL Server 2016 R Server (독립 실행형)](install/sql-r-standalone-windows-install.md)합니다.

### <a name="12-sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>12. SQL Server Data Tools 외부 스크립트에 필요한 권한을 지원 하지 않습니다.

를 사용 하면 Visual Studio 또는 SQL Server Data Tools 데이터베이스 프로젝트를 게시 하려면 모든 보안 주체에 외부 스크립트 실행을 특정 사용 권한이 있으면 다음과 같은 오류가 표시 될 수 있습니다.

> *TSQL 모델: 리버스 엔지니어링 데이터베이스 때 검색 하는 데 오류가 발생 했습니다. 사용 권한을 인식할 수 없습니다 및 가져오지 않았습니다.*

현재 DACPAC 모델은 R Services 또는 ANY EXTERNAL SCRIPT GRANT EXECUTE ANY EXTERNAL SCRIPT 등 Machine Learning 서비스에서 사용 권한을 지원 하지 않습니다. 이 문제는 향후 릴리스에서 해결될 예정입니다.

대 안으로 추가 권한 부여에서에서 문을 실행 배포 후 스크립트.

### <a name="13-external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>13. 외부 스크립트 실행이 리소스 거 버 넌 스 기본 값으로 인해 제한

Enterprise Edition에서 리소스 풀을 사용하여 외부 스크립트 프로세스를 관리할 수 있습니다. 일부 초기 릴리스 빌드에서 R 프로세스에 할당 될 수 있는 최대 메모리는 20% 였습니다. 따라서 서버에 32GB의 RAM이 있으면 R 실행 파일 (RTerm.exe 및 BxlServer.exe) 단일 요청에서 6.4GB 최대를 사용할 수 없습니다.

리소스 제한에서 발생 하는 경우 현재 기본값을 확인 합니다. 20% 충분 하지 않습니다, 경우에 대 한 설명서를 참조 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이 값을 변경 하는 방법에 있습니다.

**적용 대상:** SQL Server 2016 R Services, Enterprise Edition

## <a name="r-script-execution-issues"></a>R 스크립트 실행 문제

이 단원에는 R 라이브러리 및 RevoScaleR를 포함 하 여 Microsoft에서 게시 도구에 관련 된 일부 문제 뿐만 아니라 SQL Server에서 R을 실행 하려면 관련 된 알려진된 문제가 있습니다.

R 솔루션에 영향을 주는 기타 알려진된 문제에 대 한 참조를 [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues) 사이트입니다.

### <a name="1-access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>1. 기본이 아닌 위치에 SQL Server에서 R 스크립트를 실행 하는 경우 경고를 거부 하는 액세스

와 같은 기본이 아닌 위치에 설치 된 SQL Server 인스턴스의 경우 외부는 `Program Files` 폴더, ACCESS_DENIED 패키지를 설치 하는 스크립트를 실행 하려고 할 때 발생 하는 경고입니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

> *In `normalizePath(path.expand(path), winslash, mustWork)` : path[2]="~ExternalLibraries/R/8/1": 액세스가 거부 되었습니다.*

이유는 R 함수 경로 읽기를 시도 하 고 실패 built-in users 그룹 **SQLRUserGroup**, 읽기 액세스 하지 못합니다. 경고 발생 하는 현재 R 스크립트 실행을 차단 하지 않습니다 하지만 사용자가 다른 R 스크립트를 실행할 때마다 경고가 반복적으로 되풀이 될 수 있습니다.

기본 위치에 SQL Server를 설치한 경우이 오류가 발생 하지 않습니다를 모든 Windows 사용자에 게 사용 권한에서 읽기 때문에 `Program Files` 폴더입니다.

이 문제는 향후 서비스 릴리스의 ia 해결 합니다. 이 문제를 해결 하려면 그룹을 제공 **SQLRUserGroup**의 모든 상위 폴더에 대 한 읽기 액세스를 사용 하 여 `ExternalLibraries`입니다.

### <a name="2-serialization-error-between-old-and-new-versions-of-revoscaler"></a>2. RevoScaleR의 이전 및 새 버전 간에 직렬화 오류

원격 SQL Server 인스턴스를 serialize 된 형식을 사용 하 여 모델에 전달 해도 오류가 표시 될 수 있습니다. 

> *MemDecompress에서 오류 (데이터, 형식 = 압축 해제) memDecompress(2)의 내부 오류-3입니다.*

최신 버전의 serialization 함수를 사용 하 여 모델을 저장 하는 경우이 오류는 발생 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel), SQL Server 인스턴스는 모델을 역직렬화 하는 위치를 이전 버전의 SQL에서 RevoScaleR Api는 되었지만 Server 2017 CU2 이전 합니다.

해결 방법으로 SQL Server 2017 cu3 이상 인스턴스를 업그레이드할 수 있습니다.

API 버전은 동일 하거나 직렬화 API의 최신 버전을 사용 하는 서버에는 이전 serialization 함수를 사용 하 여 저장 된 모델을 이동 하는 경우에 오류가 표시 되지 않습니다.

즉, serialization 및 deserialization 작업에 대 한 RevoScaleR의 동일한 버전을 사용 합니다.

### <a name="3-real-time-scoring-does-not-correctly-handle-the-learningrate-parameter-in-tree-and-forest-models"></a>3. 실시간 점수 매기기 제대로 처리 하지 않습니다 합니다 _learningRate_ 트리 및 포리스트 모델의 매개 변수

의사 결정 트리 또는 의사 결정 포리스트 메서드를 사용 하 여 모델을 만들고 학습 속도 지정 하는 경우 사용 하는 경우 일관성 없는 결과가 표시 될 수 있습니다 `sp_rxpredict` 또는 SQL `PREDICT` 함수를 사용 하 여 비교 하 여 `rxPredict`입니다.

원인을 API의 오류는 직렬화 프로세스 모델 이며 제한 된 `learningRate` 매개 변수: 예를 들어 [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees), 또는

이 문제는 향후 서비스 릴리스에서 해결 됩니다.

### <a name="4-limitations-on-processor-affinity-for-r-jobs"></a>4. R 작업에 대한 프로세서 선호도 제한

SQL Server 2016의 초기 릴리스 빌드에서 첫 번째 k 그룹의 Cpu에 대해서만 프로세서 선호도 설정할 수 있습니다. 예를 들어 서버가 k 그룹이 두 개를 2 소켓 시스템인 경우 첫 번째 k 그룹의 프로세서만 R 프로세스에 사용 됩니다. 동일한 제한에는 R 스크립트 작업에 대 한 리소스 거 버 넌 스를 구성한 경우 적용 됩니다.

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

대 안으로, CAST를 사용 하려면 SQL 쿼리를 다시 작성할 수 있습니다 또는 변환 하 고 올바른 데이터 형식을 사용 하 여 R에 데이터를 제공 합니다. 일반적으로 성능이 더 좋아집니다 작업할 때 데이터를 사용 하 여 R 코드에서 데이터를 변경 하는 대신 SQL을 사용 하 여 합니다.

**적용 대상:** SQL Server 2016 R Services

### <a name="6-limits-on-size-of-serialized-models"></a>6. Serialize 된 모델의 크기에 대 한 제한

SQL Server 테이블에는 모델을 저장 하면 모델을 직렬화 하 고 이진 형식으로 저장 해야 합니다. 이론적으로이 메서드를 사용 하 여 저장할 수 있는 모델의 최대 크기에는 SQL Server에 있는 varbinary 열의 최대 크기는 2GB입니다.

큰 모델을 사용 하는 경우 다음 해결 방법을 사용할 수 있습니다.

+ 모델의 크기를 줄이기 위해 단계를 수행 합니다. 모델 개체에 많은 양의 정보를 포함 하는 몇 가지 오픈 소스 R 패키지 및 배포에 대 한 이러한 정보를 제거할 수 있습니다. 
+ 불필요 한 열을 제거 하려면 기능 선택을 사용 합니다.
+ 오픈 소스 알고리즘을 사용 하는 경우에 MicrosoftML RevoScaleR에 해당 알고리즘을 사용 하는 유사한 구현을 고려 합니다. 이러한 패키지 배포 시나리오에 최적화 되었습니다.
+ 모델 선별 된 후 이전 단계를 사용 하 여 크기를 줄일 경우 참조를 [memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress) SQL Server로 전달 하기 전에 모델의 크기를 줄이기 위해 기본 r에서 함수를 사용할 수 있습니다. 이 옵션은 모델은 2GB 한도 근접 하는 경우에 가장 적합 합니다.
+ 큰 모델에 대 한 SQL Server를 사용할 수 있습니다 [FileTable](../relational-databases/blob/filetables-sql-server.md) varbinary 열을 사용 하는 것이 아니라 모델을 저장 하는 기능입니다.

    Filetable을 사용 하려면 SQL server에서는 Filestream 파일 시스템 드라이버에 의해 관리 되는 Filetable에 저장 된 데이터 및 기본 방화벽 규칙 네트워크 파일 액세스를 차단 하기 때문에 방화벽 예외를 추가 해야 합니다. 자세한 내용은 [FileTable의 필수 구성 요소를 사용 하도록 설정](../relational-databases/blob/enable-the-prerequisites-for-filetable.md)합니다.

    FileTable을 사용 하도록 설정 하면 모델을 쓸 경로 FileTable API를 사용 하 여 SQL에서을 얻고 코드에서 해당 위치에 모델을 작성 합니다. 모델을 읽는 경우 SQL에서 경로 가져올 하 고 스크립트의 경로 사용 하 여 모델을 호출 합니다. 자세한 내용은 [파일 입 / 출력 Api를 사용 하 여 Filetable 액세스](../relational-databases/blob/access-filetables-with-file-input-output-apis.md)합니다.

### <a name="7-avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>7. R 코드를 실행 하면 작업 영역을 지우지 마세요는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 계산 컨텍스트

R 명령을 사용 하 여 R 코드를 실행 하는 동안 개체의 작업 영역을 선택 취소 하는 경우는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 계산 컨텍스트를 사용 하 여 호출 하거나 R 스크립트의 일부로 작업 영역을 선택 취소 하는 경우 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에이 오류가 표시 될 수 있습니다 : *작업 영역 개체 지우거 찾을 수 없음*

`revoScriptConnection` 은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 호출된 R 세션에 대한 정보를 포함하는 R 작업 영역의 개체입니다. 그러나 R 코드에 작업 영역을 지우는 명령(예: `rm(list=ls()))`)이 포함되어 있으면 세션 및 R 작업 영역의 다른 개체에 대한 모든 정보도 지워집니다.

위치에서 R을 실행 하는 동안 대 안으로, 변수 및 기타 개체를 무차별 지우지 마세요 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]합니다. 수 있는 경우에 작업 영역을 지우는 공통 R 콘솔에서 작업할 때 의도 하지 않은 결과가 발생 합니다.

* 특정 변수를 삭제 하려면 R을 사용 하 여 `remove` 함수: 예를 들어, `remove('name1', 'name2', ...)`
* 삭제할 변수가 여러 개인 경우 임시 변수 이름을 목록에 저장하고 주기적 가비지 수집을 수행합니다.

### <a name="8-restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>8. R 스크립트의 입력으로 제공될 수 있는 데이터에 대한 제한

R 스크립트에서는 다음 유형의 쿼리 결과를 사용할 수 없습니다.

- AlwaysEncrypted 열을 참조하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리의 데이터
  
- 마스킹된 열을 참조하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리의 데이터
  
     R 스크립트에서 마스킹된 데이터를 사용해야 하는 경우 가능한 해결 방법은 임시 테이블에 데이터 복사본을 만들고 해당 데이터를 대신 사용하는 것입니다.

### <a name="9-use-of-strings-as-factors-can-lead-to-performance-degradation"></a>9. 문자열의 요소는 성능 저하를 발생할 수 있습니다 사용 하 여

문자열 형식 변수를 사용 하 여 대로 요소에는 R 작업에 사용 되는 메모리의 양을 크게 증가할 수 있습니다. 일반적으로 이것은 R 사용 하 여 알려진된 문제 및 주제에 문서가 많이 있습니다. 예를 들어 참조 [요인은 r-bloggers에서 John 탑재 하 여 R의 일등 시민이 없습니다)](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/) 또는 [stringsAsFactors: 무단된 이력, Roger Peng 여](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/)입니다. 

문제를 SQL Server 관련 하지는 않지만 SQl Server에서 실행 되는 R 코드의 성능에는 영향을 크게 수 있습니다. 문자열은 일반적으로 varchar 또는 nvarchar로 저장 하 고 문자열 데이터의 열에 고유 값이 많은 경우 내부적으로 정수로 변환 하 고 R에서 문자열을 다시 변환 하는 프로세스 메모리 할당 오류도 발생할 수 있습니다.

반드시 필요 하지 문자열 데이터 형식의 다른 작업에 대 한 숫자 (integer) 문자열 값을 매핑할 경우 데이터 준비의 일부 성능 및 확장성 측면에서 유용한 것 처럼 데이터 형식입니다.

이 문제 및 기타 팁 자세한 내용은 참조 하세요. [R Services-데이터 최적화에 대 한 성능](r/r-and-data-optimization-r-services.md)합니다.

### <a name="10-arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>10. 인수 *varsToKeep* 하 고 *varsToDrop* SQL Server 데이터 원본에 대해 지원 되지 않습니다

RxDataStep 함수를 사용 하 여 테이블에 결과 쓸 때 사용 하 여 합니다 *varsToKeep* 하 고 *varsToDrop* 포함 하거나 제외할 작업의 일부로 열을 지정 하는 방법이 유용 합니다. 그러나 이러한 인수는 SQL Server 데이터 원본에 대해 지원 되지 않습니다.

### <a name="11-limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>11. Sp의 SQL 데이터 형식에 대 한 지원이 제한 됩니다\_실행할\_외부\_스크립트

SQL에서 지원 되는 일부 데이터 형식은 R에서 사용할 수 있습니다. Sp에 데이터를 전달 하기 전에 지원 되지 않는 데이터 형식을 지원 되는 데이터 형식으로 캐스팅 하십시오. 문제를 해결할\_실행할\_외부\_스크립트입니다.

자세한 내용은 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)합니다.

### <a name="12-possible-string-corruption-using-unicode-strings-in-varchar-columns"></a>12. Varchar 열에 유니코드 문자열을 사용 하 여 가능한 문자열 손상

Varchar 열에서 비유니코드 데이터 전달 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] R/python 문자열 손상에서 될 수 있습니다. 이러한 유니코드 문자열에 대 한 인코딩을 원인은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] R/Python에서 사용 되는 기본 utf-8 인코딩을 사용 하 여 데이터 정렬 일치 하지 않을 수 있습니다. 

비 ASCII 문자열 데이터를 보내지 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] R/python utf-8 인코딩을 사용 하 여 (에서 사용할 수 있는 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]) 하거나 동일한 nvarchar 형식을 사용 합니다.

### <a name="13-only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>13. 형식의 값을 하나만 `raw` 에서 반환할 수 있습니다 `sp_execute_external_script`

경우는 binary 데이터 형식 (R **원시** 데이터 형식) R에서 반환 된 값은 출력 데이터 프레임의 전송 되어야 합니다.

데이터 형식 이외의 **원시**, OUTPUT 키워드를 추가 하 여 저장된 프로시저의 결과 함께 매개 변수 값을 반환할 수 있습니다. 자세한 내용은 [매개 변수](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters)합니다.

형식의 값을 포함 하는 여러 출력 집합을 사용 하려는 경우 **원시**를 다시 설정 가능한 해결 방법은 저장된 프로시저를 여러 번 호출을 수행 하거나 결과 보낼 것 하나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ODBC를 사용 하 여 합니다.

### <a name="14-loss-of-precision"></a>14. 정밀도 손실

때문에 [!INCLUDE[tsql](../includes/tsql-md.md)] R 다양 한 데이터 형식을 지원 하 고, 숫자 데이터 형식 변환 하는 동안 정밀도의 손실 저하 될 수 있습니다.

암시적 데이터 형식 변환에 대 한 자세한 내용은 참조 하십시오 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)합니다.

### <a name="15-variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>15. TransformFunc 매개 변수를 사용 하는 경우 범위 지정 오류가 발생 하는 변수

데이터를 모델링 하는 동안 변환에 전달할 수 있습니다는 *transformFunc* 와 같은 함수에서 인수 `rxLinmod` 또는 `rxLogit`합니다. 그러나 중첩 된 함수 호출은 호출 하 여 로컬 계산 컨텍스트에서 올바르게 작동 하는 경우에 범위 지정 오류는 SQL Server 계산 컨텍스트에서 발생할 수 있습니다.

> *분석에 대 한 샘플 데이터 집합에 변수가 없습니다.*

예를 들어 두 함수를 정의 했다고 가정 `f` 하 고 `g`, 로컬 글로벌 환경에서 및 `g` 호출 `f`합니다. 분산 또는 원격 호출 관련 된 `g`에 대 한 호출 `g` 때문에이 오류와 함께 실패할 수 있습니다 `f` 전달한 경우에 찾을 수 없습니다 `f` 및 `g` 대 한 호출 합니다.

이 문제가 발생한 경우 `f` 의 정의를 `g`의 정의 내에 포함하여 문제를 해결할 수 있습니다. `g` 앞의 모든 곳에서 `f`를 정상적으로 호출합니다.

이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

```R
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

오류를 방지 하려면 다음과 같이 정의 다시 작성 합니다.

```R
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="16-data-import-and-manipulation-using-revoscaler"></a>16. RevoScaleR을 사용하여 데이터 가져오기 및 조작

때 **varchar** 열에서에서 읽는 데이터베이스 공백이 잘립니다. 이를 방지하려면 공백이 아닌 문자로 문자열을 묶습니다.

때와 같은 함수 `rxDataStep` 이 있는 데이터베이스 테이블을 만드는 데 사용 됩니다 **varchar** 열, 열 너비는 데이터의 샘플 기반 예상 됩니다. 너비가 달라질 수 있는 경우 모든 문자열 길이을 채우려면 해야 할 수도 있습니다.

`rxImport` 또는 `rxTextToXdf` 에 대한 반복된 호출을 사용하여 행을 가져오고 추가하면서 여러 입력 파일을 단일.xdf 파일에 통합하는 경우 변환을 사용하여 변수의 데이터 형식을 변경할 수 없습니다.

### <a name="17-limited-support-for-rxexec"></a>17. RxExec에 대 한 제한 된 지원

SQL Server 2016에는 `rxExec` 함수는 단일 스레드 모드 에서만에서 제공에서 RevoScaleR 패키지를 사용할 수 있습니다.

### <a name="18-increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>18. RxGetVarInfo를 지원 하도록 최대 매개 변수 크기 늘리기

매우 많은 변수를 사용 하 여 데이터 집합 (예: 40,000 개)를 사용 하면 설정 된 `max-ppsize` 플래그와 같은 함수를 사용 하는 R을 시작 하면 `rxGetVarInfo`합니다. `max-ppsize` 플래그는 포인터 보호 스택의 최대 크기를 지정합니다.

R 콘솔 (RGui.exe 또는 RTerm.exe 등)를 사용 하는 경우에 값을 설정할 수 있습니다 _최대 ppsize_ 입력 하 여 500000으로:

```R
R --max-ppsize=500000
```

### <a name="19-issues-with-the-rxdtree-function"></a>19. RxDTree 함수 문제

`rxDTree` 함수는 현재 수식 내 변환을 지원하지 않습니다. 특히 즉석에서 요소를 만들기 위해 `F()` 구문을 사용하는 것은 지원되지 않습니다. 그러나 숫자 데이터는 자동으로 범주화 됩니다.

순서가 지정된 요소는 `rxDTree`를 제외하고 모든 RevoScaleR 분석 함수의 요소와 동일하게 처리됩니다.

## <a name="python-script-execution-issues"></a>Python 스크립트 실행 문제

이 섹션에서는 Microsoft에서 게시 하는 Python 패키지와 관련 된 문제 뿐만 아니라 SQL Server에서 Python을 실행 하려면 관련 된 알려진된 문제가 포함 [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 고 [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="1-call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>1. 모델에 경로가 너무 깁니다. 미리 학습 된 모델 호출 실패

SQL Server 2017의 초기 릴리스에서 미리 학습 된 모델을 설치한 경우에 학습 된 모델 파일에 전체 경로를 읽는 Python에 대 한 너무 길 수 있습니다. 이 제한은 이후 서비스 릴리스로에서 해결 됩니다.

잠재적 해결 방법을 몇 가지 있습니다. 

+ 미리 학습 된 모델을 설치 하면 사용자 지정 위치를 선택 합니다.
+ 가능한 경우 C:\SQL\MSSQL14 같은 더 짧은 경로 사용 하 여 사용자 지정 설치 경로 있는 SQL Server 인스턴스를 설치 합니다. MSSQLSERVER입니다.
+ Windows 유틸리티를 사용 하 여 [Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) 더 짧은 경로 모델 파일에 매핑되는 하드 링크를 만듭니다.
+ 최신 서비스 릴리스를 업데이트 합니다.

### <a name="2-error-when-saving-serialized-model-to-sql-server"></a>2. SQL Server에 대 한 모델을 직렬화 하는 저장 하는 동안 오류가 발생 했습니다.

원격 SQL Server 인스턴스에 모델을 전달 하 고 사용 하 여 이진 모델을 읽으려고 시도 합니다 `rx_unserialize` 함수 [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), 오류가 표시 될 수 있습니다: 

> *Nameerror 였습니다: 이름 'rx_unserialize_model' 정의 되지 않았습니다.*

이 오류는 최신 버전의 serialization 함수를 사용 하 여 모델을 저장 하지만 모델 역직렬화는 SQL Server 인스턴스를 직렬화 API를 인식 하지 못하는 경우 발생 합니다.

문제를 해결 하려면 SQL Server 2017 cu3 이상 인스턴스를 업그레이드 합니다.

### <a name="3-failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>3. BxlServer에서는 오류가 발생 하는 varbinary 변수 초기화 실패

SQL Server를 사용 하 여 Python 코드를 실행 하는 경우 `sp_execute_external_script`, 코드에 출력 형식 varbinary (max), varchar (max) 또는 이와 유사한 종류의 변수, 변수를 초기화 하거나 스크립트의 일부로 설정 해야 합니다. 그렇지 않으면 오류가 및 작동 중지 데이터 exchange 구성 요소, BxlServer를 발생 시킵니다.

이 제한은 향후 서비스 릴리스에서 수정 될 예정입니다. 대 안으로 Python 스크립트 내 변수 초기화 되는지 확인 합니다. 다음 예제와 같이 유효한 값을 사용할 수 있습니다.

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

### <a name="4-telemetry-warning-on-successful-execution-of-python-code"></a>4. Python 코드의 실행 성공 시 원격 분석 경고

SQL Server 2017 CU2부터, 그렇지 않으면 Python 코드가 성공적으로 실행 하는 경우에 다음과 같은 메시지가 나타날 수 있습니다.

> *외부 스크립트의 STDERR 메시지:*
>  *~PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: telemetry_state 됩니다 전역 선언 전에 사용*


이 문제는 SQL Server 2017 누적 업데이트 3 (CU3)에서 수정 되었습니다. 

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise 및 Microsoft R Open

이 섹션에서는 R 연결, 개발 및 Revolution Analytics에서 제공 하는 성능 도구 관련 문제를 나열 합니다. 이러한 도구는 이전 시험판 버전의 제공 된 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]합니다.

일반적으로 이전 버전을 제거 하 고 최신 버전의 SQL Server 또는 Microsoft R Server를 설치 하는 것이 좋습니다.

### <a name="1-revolution-r-enterprise-is-not-supported"></a>1. Revolution R Enterprise 지원 되지 않습니다.

모든 버전의 Revolution R Enterprise 나란히 설치 [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] 지원 되지 않습니다.

Revolution R Enterprise에 대 한 기존 라이선스가 있는 경우 둘 다에서 별도 컴퓨터에 배치 해야 합니다는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스와 연결 하는 데 원하는 모든 워크스테이션을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스.

일부 이전 버전의 [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] Revolution Analytics에서 만든 Windows 용 R 개발 환경을 포함 합니다. 이 도구는 더 이상 제공 하 고 지원 되지 않습니다.

호환성을 위해 [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], 대신 Microsoft R Client를 설치 하는 것이 좋습니다. [Visual Studio 용 R 도구](https://www.visualstudio.com/vs/rtvs/) 하 고 [Visual Studio Code](https://code.visualstudio.com/) Microsoft R 솔루션도 지원 합니다.

### <a name="2-compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>2. SQLite ODBC 드라이버와 RevoScaleR의 호환성 문제

SQLite ODBC 드라이버의 수정 버전 0.92는 RevoScaleR과 호환 되지 않습니다. 수정 버전 0.88 ~ 0.91 및 0.93 및 나중에 호환 가능한 것으로 알려져 있습니다.

## <a name="see-also"></a>참고자료

[SQL Server 2016의 새로운 기능](../sql-server/what-s-new-in-sql-server-2016.md)

[SQL Server에서 기계 학습 문제 해결](machine-learning-troubleshooting-faq.md)
