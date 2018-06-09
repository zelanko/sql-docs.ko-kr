---
title: 컴퓨터 학습 서비스의 알려진 문제 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 20a3742c9dfc956accd902539524724cac3f9b8c
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34563861"
---
# <a name="known-issues-in-machine-learning-services"></a>컴퓨터 학습 서비스의 알려진된 문제
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 기계 학습에서 SQL Server 2016 및 SQL Server 2017 옵션으로 제공 되는 구성 요소와 알려진된 문제 또는 제한을 설명 합니다.

지정 하지 않을 경우이 정보 모든 다음에 적용 됩니다.

SQL Server 2016

- R Services(In-database)
- Microsoft R Server(독립 실행형)

SQL Server 2017

- 기계 학습 R (In-database)에 대 한 서비스
- 기계 학습 Python (In-database)에 대 한 서비스
- Machine Learning Server(독립 실행형)

## <a name="setup-and-configuration-issues"></a>설치 및 구성 문제

참조에 대 한 프로세스와 관련 된 초기 설치 및 구성과 관련 된 일반적인 질문 설명은 [업그레이드 및 설치 FAQ](r/upgrade-and-installation-faq-sql-server-r-services.md)합니다. 업그레이드,-나란히 설치 및 새 Python 또는 R 구성 요소를 설치 하는 방법에 대 한 정보를 포함 합니다.

### <a name="unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>도메인 컨트롤러에 SQL Server 컴퓨터 학습 기능을 설치할 수 없습니다.

도메인 컨트롤러에 SQL Server 2016 R Services 또는 SQL Server 2017 컴퓨터 학습 서비스를 설치 하려고 하면 이러한 오류와 함께 설치 프로그램이 실패 합니다.

> *기능 설치 과정에서 오류가 발생 했습니다.*
> 
> *Id로 그룹을 찾을 수 없습니다.*
> 
> *구성 요소 오류 코드: 0x80131509*

오류는 도메인 컨트롤러에서 서비스에는 기계 학습을 실행 하는 데 필요한 20 로컬 계정을 만들 없기 때문에 발생 합니다. 일반적으로 도메인 컨트롤러에 SQL Server를 설치 하지 않는 것이 좋습니다. 자세한 내용은 참조 [지원 공지 2032911](https://support.microsoft.com/en-us/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont)합니다.

### <a name="install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>Microsoft R 클라이언트와의 호환성을 위해 최신 서비스 릴리스를 설치 합니다.

Microsoft R Client의 최신 버전을 설치 하 고 사용 하 여 원격 계산 컨텍스트에서 R SQL Server에서 실행 되도록 하는 경우에 다음과 같은 오류가 발생할 수 있습니다.

> *Microsoft R Client의 9.x.x 버전을 실행 하는 Microsoft R Server 버전 8.x.x와 호환 되지 않는 컴퓨터에 있습니다. 호환되는 버전을 다운로드하여 설치하세요.*

SQL Server 2016 R 라이브러리 클라이언트에서 R 라이브러리 서버에는 정확 하 게 일치 해야 합니다. 제한 나중에 R Server 9.0.1 보다 제거 릴리스 되었습니다. 그러나이 오류가 발생 하면 클라이언트와 서버에서 사용 되 고, 필요한 경우 서버 버전 일치 하도록 클라이언트를 업데이트 하는 R 라이브러리 버전을 확인 합니다.

SQL Server R Services와 함께 설치 되는 R의 버전은 SQL Server 서비스 릴리스가 설치 될 때마다 업데이트 됩니다. 하면 항상 최신 버전의 R 구성 요소를 갖출 수 있도록 모든 서비스 팩을 설치 해야 합니다.

Microsoft R 9.0.0 클라이언트와의 호환성을 보장 하려면이 설명 하는 업데이트를 설치 [지원 문서](https://support.microsoft.com/kb/3210262)합니다.

R 패키지 문제를 방지 하려면 업그레이드할 수 있습니다에 설명 된 대로 최신 수명 주기 지원 정책을 사용 하 여 서비스 계약을 변경 하 여 서버에 설치 된 R 라이브러리 버전 [절로](#bkmk_sqlbindr)합니다. 이렇게 하면 동일한 일정에 따라 시스템 학습 서버 (이전의 Microsoft R 서버)의 업데이트에 사용 되는 SQL Server와 함께 설치 되는 R의 버전 업데이트 됩니다.

**적용 대상:** R server 9.0.0 버전 SQL Server 2016 R Services 또는 이전 버전

### <a name="r-components-missing-from-cu3-setup"></a>C u 3 설치 프로그램에서 누락 된 R 구성 요소

Azure 가상 컴퓨터 수가 제한 된 SQL Server와 함께 포함 되어야 하는 R 설치 파일 없이 프로 비전 됩니다. 이 문제는 2018-01-23 2018-01-05에서 기간에 프로 비전 된 가상 컴퓨터에 적용 됩니다. 또한이 문제를 적용 한 경우 SQL Server 2017 CU3 업데이트 기간 동안 2018-01-05에서 2018-01-23 온-프레미스 설치를 달라질 수 있습니다.

서비스 릴리스는 올바른 버전의 R 설치 파일이 포함 된 제공 되었습니다.

+ [SQL Server 2017 KB4052987 용 누적 업데이트 패키지 3](https://www.microsoft.com/en-us/download/details.aspx?id=56128)합니다.

구성 요소를 설치 하 고 SQL Server 2017 CU3를 복구 하려면 CU3를 제거 하 고 업데이트 된 버전을 다시 설치 해야:

1. R 설치 관리자를 포함 하는 업데이트 된 CU3 설치 파일을 다운로드 합니다.
2. C u 3을 제거 합니다. 제어판에서 검색 **업데이트 제거**, 한 다음 "SQL Server 2017 (KB4052987) (64 비트)에 대 한 핫픽스 3015"를 선택 합니다. 제거 단계를 진행 합니다.
3. 방금 다운로드 한 KB4052987에 대 한 업데이트를 두 번 클릭 하 여 CU3 업데이트를 다시 설치: `SQLServer2017-KB4052987-x64.exe`합니다. 설치 지침을 따릅니다.

### <a name="unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>SQL Server 2017 CTP 2.0 이상 오프 라인 설치에서 Python 구성 요소를 설치할 수 없습니다.

인터넷 액세스가 없는 컴퓨터에서 SQL Server 2017의 시험판 버전을 설치 하는 경우 설치 관리자 다운로드 된 Python 구성 요소 위치를 묻는 페이지를 표시 하려면 실패할 수 있습니다. 이러한 상황에서 컴퓨터 학습 서비스 기능을 사용 하지만 Python 구성 요소가 아닌를 설치할 수 있습니다.

릴리스 버전에서이 문제는 해결 됩니다. 또한이 제한은 R 구성 요소에 적용 되지 않습니다.

**적용 대상:** python 2017 SQL Server

### <a name="bkmk_sqlbindr"></a> 사용 하 여 클라이언트는 이전 버전의 SQL Server R Services에 연결 하는 경우 호환 되지 않는 버전의 경고 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

R 코드를 실행 하면 SQL Server 2016 계산 컨텍스트, 다음과 같은 오류가 표시 될 수 있습니다.

> *컴퓨터에서 Microsoft R Server 버전 8.0.3과 호환되지 않는 Microsoft R Client 버전 9.0.0을 실행 중입니다. 호환되는 버전을 다운로드하여 설치하세요.*

다음 두 문 중 하나이 true 이면이 메시지가 표시 됩니다.

+ 설치 마법사를 사용 하 여 클라이언트 컴퓨터에 R Server (독립 실행형) 설치 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]합니다.
+ Microsoft R Server를 사용 하 여 설치한는 [Windows installer 구분](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)합니다.

서버와 클라이언트에 사용 해야 할 수는 동일한 버전 사용 하는지 확인 하려면 _바인딩_(SQL Server 2016의 경우 R 구성 요소를 업그레이드 하려면 Microsoft R Server 9.0 및 이상 버전에 대 한 지원). 여부를 확인 하려면 R 서비스 버전 참조에 대 한 업그레이드를 사용할 수에 대 한 지원이 [SqlBindR.exe를 사용 하 여 R 서비스의 인스턴스를 업그레이드](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

**적용 대상:** R server 9.0.0 버전 SQL Server 2016 R Services 또는 이전 버전

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>SQL Server 2016 서비스 릴리스 설치 프로그램에서 최신 버전의 R 구성 요소를 설치하지 못할 수 있음

누적 업데이트를 설치 하거나 인터넷에 연결 되어 있지 않은 컴퓨터에서 SQL Server 2016 용 서비스 팩을 설치할 때 설치 마법사는 다운로드 한 CAB 파일을 사용 하 여 R 구성 요소를 업데이트할 수 있는 프롬프트를 표시 하려면 실패할 수 있습니다. 이 오류는 일반적으로 여러 구성 요소는 데이터베이스 엔진와 함께 설치 된 경우에 발생 합니다.

이 문제를 해결 명령줄을 사용 하 고 지정 하 여 서비스 릴리스를 설치할 수는 `MRCACHEDIRECTORY` CU1 업데이트를 설치 하는이 예에 표시 된 대로 인수:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

최신 설치 관리자를 가져오려는 참조 [인터넷 연결 되지 않은 컴퓨터 학습 구성 요소를 설치](install/sql-ml-component-install-without-internet-access.md)합니다.

**적용 대상:** R server 9.0.0 버전 SQL Server 2016 R Services 또는 이전 버전

### <a name="launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>실행 패드 서비스 버전 R 버전 간에 차이가 있는 경우 시작 되지 않습니다.

SQL Server R Services를 별도로 설치 하는 데이터베이스 엔진에서 하는 경우 빌드 버전이 다르면 시스템 이벤트 로그에서 다음 오류가 표시 될 수 있습니다.

> *SQL Server 실행 패드 서비스 오류로 인해 시작 실패: 서비스가 시기 적절 하 게에서 시작 또는 제어 요청에 응답 하지 않았습니다.*

예를 들어이 오류 수 릴리스 버전을 사용 하 여 데이터베이스 엔진을 설치 하는 경우에 발생할 데이터베이스 엔진 업그레이드 패치를 적용 및 다음 릴리스 버전을 사용 하 여 R Services 기능을 추가 합니다.

이 문제를 방지 하려면 파일 관리자와 같은 유틸리티 사용 하 여 SQL 바이너리 sqldk.dll 등의 버전과 Launchpad.exe의 버전을 비교 합니다. 모든 구성 요소 버전 번호가 같은 있어야 합니다. 하나의 구성 요소를 업그레이드하는 경우 설치된 다른 모든 구성 요소에 동일한 업그레이드를 적용해야 합니다.

실행 패드에 대 한 확인은 `Binn` 인스턴스에 대 한 폴더입니다. 예를 들어 SQL Server 2016의 기본 설치 경로 수도 `C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`합니다. 

### <a name="remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>원격 계산 컨텍스트는 Azure 가상 컴퓨터에서 실행 되는 SQL Server 인스턴스에서 방화벽으로 차단

설치한 경우 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Windows Azure 가상 컴퓨터에서 있습니다 못할 가상 컴퓨터의 작업 영역을 사용 해야 하는 계산 컨텍스트를 사용 하도록 합니다. 기본적으로 Azure 가상 컴퓨터에서 방화벽에 네트워크 로컬 R 사용자 계정에 대 한 액세스를 차단 하는 규칙 위해서입니다.

문제를 해결 하려면 Azure VM에서 열고 **고급 보안이 포함 된 Windows 방화벽**선택, **아웃 바운드 규칙**, 다음 규칙을 사용 하지 않도록 설정 하 고: **R 로컬 사용자 계정에 대 한 네트워크 액세스 차단 SQL Server 인스턴스 MSSQLSERVER**합니다. 또한 활성화 규칙을 그대로 유지 하 있지만 보안 속성을 변경할 수 있습니다 **보안 연결만 허용**합니다.

### <a name="implied-authentication-in-sqlexpress"></a>SQLEXPRESS의 암시적 인증

Windows 통합 인증을 사용 하 여 원격 데이터 과학 워크스테이션에서 R 작업을 실행 하면 SQL Server 사용 *암시 된 인증이* 를 스크립트에 의해 필요할 수 있는 모든 로컬 ODBC 호출을 생성 합니다. 그러나 SQL Server Express Edition의 RTM 빌드에서는 이 기능이 작동하지 않았습니다.

이 문제를 해결하려면 이후 서비스 릴리스로 업그레이드하는 것이 좋습니다.

업그레이드 적절 하지 않은 문제를 해결할 사용 하 여 SQL 로그인 실행할 포함 된 ODBC 호출을 필요할 수 있는 원격 R 작업 합니다.

**적용 대상:** SQL Server 2016 R Services Express Edition

### <a name="performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>SQL Server에서 사용 되는 라이브러리는 다른 도구에서 호출 하는 경우 성능이 제한

기계 학습에서 관리자 권한 같은 외부 응용 프로그램을 SQL Server에 설치 된 라이브러리를 호출 하는 것이 불가능 합니다. 이렇게 하면 새 패키지를 설치 하거나 매우 짧은 코드 예제에서 애드혹 테스트를 실행 하는 등의 특정 작업을 수행 하는 가장 편리한 방법은 수 있습니다. 그러나 SQL Server 외부의 성능이 제한 될 수 있습니다. 

예를 들어 SQL Server의 Enterprise 버전을 사용 하는 경우에 외부 도구를 사용 하 여 R 코드를 실행 하는 경우 단일 스레드 모드에서 R 실행 합니다. SQL Server의 성능 이점을 얻으려면 SQL Server의 연결을 시작 및 사용 하 여 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 를 외부 스크립트 런타임을 호출 합니다.

일반적으로 기계 학습 외부 도구에서 SQL Server에서 사용 되는 라이브러리를 호출 하지 마십시오. 디버그 R Python 코드를 해야 하는 경우 SQL Server 외부에서 이렇게 하려면 일반적으로 쉽습니다. SQL Server에 있는 동일한 라이브러리를 가져오려면 Microsoft R 클라이언트를 설치할 수 있습니다 [SQL Server 2017 컴퓨터 학습 서버 (독립 실행형)](install/sql-machine-learning-standalone-windows-install.md), 또는 [SQL Server 2016 R 서버 (독립 실행형)](install/sql-r-standalone-windows-install.md)합니다.

### <a name="sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>SQL Server Data Tools 외부 스크립트에 필요한 사용 권한을 지원 하지 않습니다.

를 사용 하면 Visual Studio 또는 SQL Server Data Tools 데이터베이스 프로젝트를 게시 하는 모든 보안 주체에 외부 스크립트 실행에 특정 사용 권한이 있으면 다음과 같은 오류가 발생할 수 있습니다.

> *TSQL 모델: 리버스 엔지니어링 데이터베이스 때 발견 되 면 오류가 발생 했습니다. 인식 되지 않았으므로 사용 권한 및 가져오지 않았습니다.*

현재 DACPAC 모델은 R 서비스 또는 ANY EXTERNAL SCRIPT GRANT 또는 EXECUTE ANY EXTERNAL SCRIPT 같은 컴퓨터 학습 서비스에 사용 되는 권한을 지원 하지 않습니다. 이 문제는 향후 릴리스에서 해결될 예정입니다.

이 문제를 해결 추가 권한 부여에서에서 문을 실행 배포 후 스크립트.

### <a name="external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>외부 스크립트 실행은 리소스 거 버 넌 스 기본값 인해 조정

Enterprise Edition에서 리소스 풀을 사용하여 외부 스크립트 프로세스를 관리할 수 있습니다. 일부 초기 릴리스 빌드에서 R 프로세스에 할당 될 수 있는 최대 메모리는 20% 였습니다. 따라서 서버에 32GB의 RAM이 있으면 R 실행 파일 (예: RTerm.exe, BxlServer.exe) 단일 요청에서 6.4 g B의 최대는 사용할 수 있습니다.

리소스 제한이 발생 하면 현재 기본값을 확인 합니다. 20% 충분 없는 경우에 대 한 설명서를 참조 하십시오. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이 값을 변경 하는 방법에 있습니다.

**적용 대상:** SQL Server 2016 R 서비스, Enterprise Edition

## <a name="r-issues"></a>R 관련 문제

이 섹션에는 RevoScaleR를 포함 하 여 Microsoft에서 게시 하는 도구 및 R 라이브러리에 관련 된 몇 가지 문제 뿐 아니라 SQL Server에서 R을 실행 하는 관련 된 알려진된 문제가 포함 되어 있습니다.

R 솔루션에 영향을 줄 수 있는 기타 알려진된 문제에 대 한 참조는 [컴퓨터 학습 서버](https://docs.microsoft.com/machine-learning-server/resources-known-issues) 사이트입니다.

### <a name="access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>기본이 아닌 위치에서 SQL Server에서 R 스크립트를 실행 하는 경우 경고를 거부 하는 액세스

와 같은 기본이 아닌 위치에 설치 된 SQL Server 인스턴스의 경우 외부에서 `Program Files` 폴더에는 경고 ACCESS_DENIED가 패키지를 설치 하는 스크립트를 실행 하려고 할 때 발생 합니다. 예를 들어:

> *`normalizePath(path.expand(path), winslash, mustWork)` : 경로 [2] = "~ExternalLibraries/R/8/1": 액세스가 거부 되었습니다.*

R 함수는 경로 읽으려고 시도 및 실패 이유는 기본 제공 users 그룹 **SQLRUserGroup**, 읽기 권한이 없습니다. 경고 발생 하는 현재 R 스크립트 실행을 차단 하지 않습니다 되지만 사용자는 다른 R 스크립트를 실행할 때마다 경고가 반복적으로 되풀이 수 있습니다.

SQL Server의 기본 위치에 설치한 경우이 오류가 발생 하지 않습니다, 모든 Windows 사용자 읽기 권한이에 있어야 하기 때문에 `Program Files` 폴더입니다.

이 문제는 향후 서비스 릴리스에서 ia 해결 합니다. 이 문제를 해결 제공 그룹 **SQLRUserGroup**의 모든 상위 폴더에 대 한 읽기 권한이 있는 `ExternalLibraries`합니다.

### <a name="serialization-error-between-old-and-new-versions-of-revoscaler"></a>RevoScaleR의 이전 및 새 버전 간 serialization 오류

원격 SQL Server 인스턴스를 serialize 된 형식을 사용 하 여 모델을 전달 하면 오류가 발생할 수 있습니다. 

> *MemDecompress의 오류 (데이터, 유형 = 압축을 풀) memDecompress(2) 내부 오류-3입니다.*

최신 버전의 serialization 함수를 사용 하 여 모델을 저장 한 경우이 오류는 발생 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel), 모델을 역직렬화 하는 SQL Server 인스턴스는 이전 버전의 SQL에서 RevoScaleR Api에는 있지만 서버 2017 CU2 또는 이전 버전입니다.

이 문제를 해결 이상 c u 3으로 SQL Server 2017 인스턴스를 업그레이드할 수 있습니다.

API 버전은 동일 하거나 오래 된 serialization 함수로 serialization API의 최신 버전을 사용 하는 서버에 함께 저장 하는 모델을 이동 하는 경우에 오류가 표시 되지 않습니다.

즉, serialization 및 deserialization 작업에 대 한 RevoScaleR의 동일한 버전을 사용 합니다.

### <a name="real-time-scoring-does-not-correctly-handle-the-learningrate-parameter-in-tree-and-forest-models"></a>실시간 점수 매기기 제대로 처리 하지 않습니다는 _learningRate_ 트리 및 포리스트 모델의 매개 변수

의사 결정 트리 또는 의사 결정 포리스트 메서드를 사용 하 여 모델을 만들고 학습 속도 지정 하는 경우 사용 하는 경우 일관성 없는 결과가 표시 될 수 있습니다 `sp_rxpredict` 또는 SQL `PREDICT` 함수를 사용 하 여 비교할 때 `rxPredict`합니다.

원인을 API에서 오류 직렬화 프로세스 모델링 하 한으로 제한 됩니다는 `learningRate` 매개 변수: 예를 들어 [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees), 또는

이 문제는 향후 서비스 버전에서입니다.

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>R 작업에 대한 프로세서 선호도 제한

SQL Server 2016의 초기 릴리스 빌드에서 Cpu 첫 번째 k 그룹에서에 대 한 프로세서 선호도 설정할 수 있습니다. 예를 들어 서버 k 그룹이 두 개 듀얼 소켓 시스템인 경우 첫 번째 k 그룹에서에 프로세서 R 프로세스에 사용 됩니다. R 스크립트 작업에 대 한 리소스 관리를 구성 하는 경우 동일한 제한에 적용 됩니다.

이 문제는 SQL Server 2016 서비스 팩 1에서 해결되었습니다. 최신 서비스 릴리스로 업그레이드 하는 것이 좋습니다.

**적용 대상:** SQL Server 2016 R 서비스 RTM 버전

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>SQL Server 계산 컨텍스트에서 데이터를 읽는 경우 열 형식을 변경할 수 없음

계산 컨텍스트가 SQL Server 인스턴스로 설정된 경우 _colClasses_ 인수(또는 다른 유사한 인수)를 사용하여 R 코드에서 열의 데이터 형식을 변경할 수 없습니다.

예를 들어 CRSDepTimeStr 열이 정수가 아닌 경우 다음 문에서 오류가 발생합니다.

```R
data <- RxSqlServerData(
  sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall", 
  connectionString = connectionString, 
  colClasses = c(CRSDepTimeStr = "integer"))
```

이 문제를 해결 캐스트를 사용 하려면 SQL 쿼리를 다시 작성할 수 또는 변환 하 고 R에 올바른 데이터 형식을 사용 하 여 데이터를 제공 합니다. 일반적으로 성능이 더 좋아집니다 작업할 때는 데이터 R 코드의 데이터를 변경 하지 않고 SQL을 사용 하 여 합니다.

**적용 대상:** SQL Server 2016 R Services

### <a name="limits-on-size-of-serialized-models"></a>Serialize 된 모델의 크기에 대 한 제한

SQL Server 테이블에는 모델을 저장 하는 경우 모델을 직렬화 하 고 이진 형식으로 저장 해야 합니다. 이론상이 방법으로 저장할 수 있는 모델의 최대 크기에는 SQL Server의 varbinary 열의 최대 크기는 2GB입니다.

더 큰 모델을 사용 해야 하는 경우 다음 해결 방법을 사용할 수 있습니다.

+ 모델의 크기를 축소 하는 단계를 수행 합니다. 일부 오픈 소스 R 패키지는 모델 개체에 많은 양의 정보를 포함 하 고 배포에 대 한 이러한 정보를 제거할 수 있습니다. 
+ 기능 선택 사용 하 여 불필요 한 열을 제거 합니다.
+ 오픈 소스 알고리즘을 사용 하는 경우 고려 MicrosoftML 또는 RevoScaleR 해당 알고리즘을 사용 하는 구현 방법이 비슷합니다. 이러한 패키지는 배포 시나리오에 대해 최적화 되었습니다.
+ 한 후 모델 합리화 되었습니다 앞의 단계를 사용 하 여 크기 감소를 참조 하는 경우는 [memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress) 기본 r에서 함수를 SQL Server로 전달 하기 전에 모델의 크기를 줄이기 위해 사용할 수 있습니다. 이 옵션은 모델이 2GB 제한에 가까우면 가장 합니다.
+ 더 큰 모델에 대 한 SQL Server를 사용할 수 있습니다 [FileTable](..\relational-databases\blob\filetables-sql-server.md) varbinary 열을 사용 하지 않고 모델을 저장 하는 기능입니다.

    Filetable을 사용 하려면 SQL server에서는 Filestream 파일 시스템 드라이버에서 Filetable에 저장 된 데이터 관리 되 고 네트워크 파일 액세스를 차단 하는 기본 방화벽 규칙 때문에 방화벽 예외를 추가 해야 합니다. 자세한 내용은 참조 [FileTable에 대 한 필수 구성 요소를 사용 하도록 설정](../relational-databases/blob/enable-the-prerequisites-for-filetable.md)합니다. 

    FileTable을 설정한 후 모델을 작성 하 있습니다 경로 FileTable API를 사용 하 여 SQL에서 가져오고 그런 다음 사용자 코드에서 해당 위치에 모델을 작성 합니다. 모델 읽이 필요한 경우에 SQL에서 경로 가져옵니다을 스크립트에서 경로 사용 하 여 모델을 호출 합니다. 자세한 내용은 참조 [파일 입력 / 출력 Api를 사용 하 여 액세스 Filetable](../relational-databases/blob/access-filetables-with-file-input-output-apis.md)합니다.

### <a name="avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>R 코드를 실행 하는 경우 작업 영역을 선택 취소 하지 마십시오.는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 계산 컨텍스트

R 명령 개체의 작업 영역에서 R 코드를 실행 하는 동안 선택을 사용 하는 경우는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 계산 컨텍스트를 사용 하 여 호출 하거나 R 스크립트의 일환으로 작업 영역을 선택 취소 하는 경우 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md),이 오류가 발생할 수 있습니다 : *작업 영역 개체 revoScriptConnection 찾을 수 없음*

`revoScriptConnection` 은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 호출된 R 세션에 대한 정보를 포함하는 R 작업 영역의 개체입니다. 그러나 R 코드에 작업 영역을 지우는 명령(예: `rm(list=ls()))`)이 포함되어 있으면 세션 및 R 작업 영역의 다른 개체에 대한 모든 정보도 지워집니다.

R을 실행 하는 동안 문제를 해결 변수 및 기타 개체를 무분별 하 게 삭제를 방지 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]합니다. 가질 수 있습니다는 R 콘솔에서 작업할 때 작업 영역을 선택 취소 하는 것은 일반적인, 있지만 의도 하지 않은 결과입니다.

* 특정 변수를 삭제 하려면 R을 사용 하 여 `remove` 함수: 예를 들어 `remove('name1', 'name2', ...)`
* 삭제할 변수가 여러 개인 경우 임시 변수 이름을 목록에 저장하고 주기적 가비지 수집을 수행합니다.

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>R 스크립트의 입력으로 제공될 수 있는 데이터에 대한 제한

R 스크립트에서는 다음 유형의 쿼리 결과를 사용할 수 없습니다.

- AlwaysEncrypted 열을 참조하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리의 데이터
  
- 마스킹된 열을 참조하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리의 데이터
  
     R 스크립트에서 마스킹된 데이터를 사용해야 하는 경우 가능한 해결 방법은 임시 테이블에 데이터 복사본을 만들고 해당 데이터를 대신 사용하는 것입니다.

### <a name="use-of-strings-as-factors-can-lead-to-performance-degradation"></a>요소에 성능 저하를 발생할 수 있습니다 문자열 사용

문자열 형식 변수를 사용 하 여 처럼 요소에는 R 작업에 사용 되는 메모리 양을 크게 증가할 수 있습니다. 일반적으로 이것은 알려진된 문제 R 사용 하 고 주체에 문서가 많이 있습니다. 예를 들어 참조 [요소 R 블로거에서 John 탑재 하 여 R의 구성 요소가 없는)](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/) 또는 [stringsAsFactors: Roger Peng 여는 무단된 악력](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/)합니다. 

이 문제를 SQL Server 관련 하지는 않지만 SQl Server에서 실행 되는 R 코드의 성능에는 영향을 크게 수 있습니다. 문자열은 일반적으로 varchar 또는 nvarchar, 저장 하 고 내부적으로 정수, 문자열 r 다시로 이러한 변환 과정 문자열 데이터의 열에 고유 값이 많은 경우 메모리 할당 오류도 발생할 수 있습니다.

필요 하지 않은 절대적으로 문자열 데이터 형식의 다른 작업에 대 한 숫자 (정수) 문자열 값을 매핑할 데이터 준비의 일부 성능 및 확장성 측면에서 유용한 것 처럼 데이터 형식.

이 문제 및 기타 팁의 논의 알려면 [R Services-데이터 최적화에 대 한 성능](r/r-and-data-optimization-r-services.md)합니다.

### <a name="arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>인수 *varsToKeep* 및 *varsToDrop* SQL Server 데이터 원본에 대해 지원 되지 않습니다

RxDataStep 함수를 사용 하 여 테이블에 결과 쓸 때 사용 하는 *varsToKeep* 및 *varsToDrop* 포함 하거나 제외할 작업의 일부로 열을 지정 하는 편리한 방법입니다. 그러나 이러한 인수는 SQL Server 데이터 원본에 대해 지원 되지 않습니다.

### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>Sp의 SQL 데이터 형식에 대해 지원이 제한\_실행\_외부\_스크립트

SQL에서 지원 되는 일부 데이터 형식은 R에서 사용할 수 있습니다. Sp를 데이터를 전달 하기 전에 지원 되지 않는 데이터 형식을 지원 되는 데이터 형식으로 캐스팅 하십시오. 문제를 해결\_실행\_외부\_스크립트입니다.

자세한 내용은 참조 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)합니다.

### <a name="possible-string-corruption"></a>가능한 문자열 손상

문자열 데이터의 모든 왕복 [!INCLUDE[tsql](../includes/tsql-md.md)] R로 이동한 다음를 [!INCLUDE[tsql](../includes/tsql-md.md)] 다시 손상 될 수 있습니다. 이 R에서 사용 되는 인코딩이 서로 다르고 인해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], 다양 한 데이터 정렬 및 R에서 지원 되는 언어 및 [!INCLUDE[tsql](../includes/tsql-md.md)]합니다. ASCII가 아닌 인코딩의 모든 문자열은 잠재적으로 잘못 처리될 수 있습니다.

R에 문자열 데이터를 보낼 때 ASCII 표현으로 가능 하면 변환 합니다.

이러한 제한도 SQL Server와 Python 간에 전달 되는 데이터에 적용 됩니다. 멀티 바이트 문자를 u t F-8로 전달 하 고 유니코드로 저장 해야 합니다.

### <a name="only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>형식의 값을 하나만 `raw` 에서 반환 될 수 `sp_execute_external_script`

경우는 binary 데이터 형식 (R **원시** 데이터 형식)의 값을 출력 데이터 프레임에서 전송 해야 R에서 반환 됩니다.

데이터 형식 사용 이외의 **원시**, OUTPUT 키워드를 추가 하 여 저장된 프로시저의 결과 함께 매개 변수 값을 반환할 수 있습니다. 자세한 내용은 참조 [매개 변수](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters)합니다.

형식의 값을 포함 하는 여러 출력 집합이 사용 하려는 경우 **원시**, 한 가지 가능한 해결 방안은 저장된 프로시저를 여러 번 호출 하거나 결과 보내려고 다시 원래 대로 설정 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ODBC를 사용 하 여 합니다.

### <a name="loss-of-precision"></a>정밀도 손실

때문에 [!INCLUDE[tsql](../includes/tsql-md.md)] R 다양 한 데이터 형식을 지원 하 고, 숫자 데이터 형식 변환 하는 동안 정밀도의 손실 저하 될 수 있습니다.

암시적 데이터 형식 변환에 대 한 자세한 내용은 참조 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)합니다.

### <a name="variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>변수 범위 지정 오류가 transformFunc 매개 변수를 사용 하는 경우

데이터를 모델링 하는 동안 변형 하려면 전달할 수 있습니다는 *transformFunc* 와 같은 함수에 인수 `rxLinmod` 또는 `rxLogit`합니다. 그러나 중첩 된 함수 호출은 호출 하 여 로컬 계산 컨텍스트에서 올바르게 작동 하는 경우에 범위 지정 오류는 SQL Server 계산 컨텍스트를 발생할 수 있습니다.

> *분석에 대 한 샘플 데이터 집합에 변수가 없습니다.*

예를 들어 두 개의 함수를 정의 했다고 가정 `f` 및 `g`, 로컬 글로벌 환경에서 및 `g` 호출 `f`합니다. 에 배포 하거나 원격 관련 된 호출 `g`에 대 한 호출 `g` 때문에이 오류와 함께 실패할 수 있습니다 `f` 전달한 경우에 찾을 수 없습니다 `f` 및 `g` 원격 호출을 합니다.

이 문제가 발생한 경우 `f` 의 정의를 `g`의 정의 내에 포함하여 문제를 해결할 수 있습니다. `g` 앞의 모든 곳에서 `f`를 정상적으로 호출합니다.

예를 들어:

```r
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

이 오류를 방지 하려면 다음과 같이 정의 다시 작성 합니다.

```r
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="data-import-and-manipulation-using-revoscaler"></a>RevoScaleR을 사용하여 데이터 가져오기 및 조작

때 **varchar** 열에서에서 읽은 데이터베이스 공백이 잘립니다. 이를 방지하려면 공백이 아닌 문자로 문자열을 묶습니다.

때와 같은 함수가 `rxDataStep` 이 있는 데이터베이스 테이블을 만드는 데 **varchar** 열, 열 너비는 데이터의 샘플을 기반으로 예상 합니다. 너비가 달라질 수 있는 경우 모든 문자열 길이을 열 패딩해야 할 수 있습니다.

`rxImport` 또는 `rxTextToXdf` 에 대한 반복된 호출을 사용하여 행을 가져오고 추가하면서 여러 입력 파일을 단일.xdf 파일에 통합하는 경우 변환을 사용하여 변수의 데이터 형식을 변경할 수 없습니다.

### <a name="limited-support-for-rxexec"></a>RxExec에 대 한 제한 된 지원

SQL Server 2016에서의 `rxExec` 단일 스레드 모드에서 여는 RevoScaleR 패키지를 사용할 수 있습니다는 제공 된 함수입니다.

병렬 처리에 대 한 `rxExec` 여러 프로세스에서 이후 버전에 대 한 계획입니다.

### <a name="increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>RxGetVarInfo를 지원 하도록 최대 매개 변수 크기

예를 들어 (40000)을 통해 매우 많은 수의 변수를 데이터 집합을 사용 하면 설정 된 `max-ppsize` 플래그와 같은 함수를 사용 하는 R을 시작할 때 `rxGetVarInfo`합니다. `max-ppsize` 플래그는 포인터 보호 스택의 최대 크기를 지정합니다.

R 콘솔 (RGui.exe 또는 RTerm.exe 등)를 사용 하는 경우의 값을 설정할 수 있습니다 _max ppsize_ 을 입력 하 여 500000:

```R
R --max-ppsize=500000
```

### <a name="issues-with-the-rxdtree-function"></a>RxDTree 함수 문제

`rxDTree` 함수는 현재 수식 내 변환을 지원하지 않습니다. 특히 즉석에서 요소를 만들기 위해 `F()` 구문을 사용하는 것은 지원되지 않습니다. 그러나 숫자 데이터는 자동으로 범주화 됩니다.

순서가 지정된 요소는 `rxDTree`를 제외하고 모든 RevoScaleR 분석 함수의 요소와 동일하게 처리됩니다.

## <a name="python-code-execution-or-python-package-issues"></a>Python 코드 실행 또는 Python 패키지 문제

이 섹션에서는으로 SQL Server, Microsoft에서 게시 Python 패키지에 관련 된 문제에 대해 Python을 실행 하는 관련 된 알려진된 문제가 포함 하 여 [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 및 [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>미리 학습 된 모델에 호출이 실패 하는 경우 모델의 경로를 너무 깁니다.

초기 버전 SQL Server 2017의 미리 학습 된 모델을 설치한 경우에 학습 된 모델 파일에 전체 경로를 읽을 Python에 대 한 너무 길 수 있습니다. 이 제한 사항은 다음 서비스 릴리스에서 고정 되어 있습니다.

가능한 해결 방법 몇 가지가 있습니다. 

+ 미리 학습 된 모델을 설치 하면 사용자 지정 위치를 선택 합니다.
+ 가능 하면 C:\SQL\MSSQL14 같은 더 짧은 경로 사용 하 여 사용자 지정 설치 경로에서 SQL Server 인스턴스를 설치 합니다. MSSQLSERVER입니다.
+ Windows 유틸리티를 사용 하 여 [Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) 모델 파일을 경로가 더 짧은 매핑되는 하드 링크를 만들려고 합니다.
+ 최신 서비스 릴리스 버전으로 업데이트 합니다.

### <a name="error-when-saving-serialized-model-to-sql-server"></a>저장 하는 동안 오류가 발생 했습니다. SQL Server에는 모델을 직렬화

원격 SQL Server 인스턴스에 모델을 전달 하 고 사용 하 여 이진 모델을 읽으려고 시도 `rx_unserialize` 에서 작동 [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)는 오류가 발생할 수 있습니다. 

> *NameError: 이름 'rx_unserialize_model'가 정의 되지 않았습니다.*

이 오류는 최신 버전의 serialization 함수를 사용 하 여 모델을 저장 했지만 모델을 역직렬화 하는 SQL Server 인스턴스 API serialization을 인식 하지 못하는 경우 발생 합니다.

이 문제를 해결 하려면 이상 c u 3으로 SQL Server 2017 인스턴스를 업그레이드 합니다.

### <a name="failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>BxlServer에 varbinary 변수 초기화에 실패 하면 오류가 발생

SQL Server를 사용 하 여에서 Python 코드를 실행 하는 경우 `sp_execute_external_script`, 및 코드에 출력 형식 varbinary (max), varchar (max) 또는 유사한 종류의 변수, 변수 또는 초기화 스크립트의 일부로 설정 해야 합니다. 그렇지 않으면 데이터 exchange 구성 요소, BxlServer, 작동을 중지 하 고 오류가 발생 합니다.

이 제한 사항은 향후 서비스 릴리스에서 수정 될 예정입니다. 이 문제를 해결 Python 스크립트 내 변수 초기화 되는지 확인 합니다. 다음 예제와 같이 유효한 값을 사용할 수 있습니다.

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

### <a name="telemetry-warning-on-successful-execution-of-python-code"></a>Python 코드의 성공적인 실행에 대 한 원격 분석 경고

SQL Server 2017 CU2부터, 그렇지 않으면 Python 코드가 성공적으로 실행 하는 경우에 다음과 같은 메시지가 나타날 수 있습니다.

> *외부 스크립트의 STDERR 메시지:*
> **~PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: telemetry_state은 전역 선언 앞에 사용*


이 문제는 SQL Server 2017 누적 업데이트 3 (CU3)에서 해결 되었습니다. 

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise 및 Microsoft R Open

이 섹션은 R 연결, 개발 및 Revolution Analytics에서 제공 되는 성능 도구 관련 문제를 나열 합니다. 이러한 도구는 이전 시험판 버전의 제공 된 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]합니다.

일반적으로 이러한 이전 버전을 제거 하 고 최신 버전의 SQL Server 또는 Microsoft R Server를 설치 하는 것이 좋습니다.

### <a name="revolution-r-enterprise-is-not-supported"></a>Revolution R Enterprise 지원 되지 않습니다.

버전의 Revolution R Enterprise 나란히 설치 [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] 지원 되지 않습니다.

Revolution R Enterprise에 대 한 기존 라이선스를 설정한 경우 둘 다에서 별도 컴퓨터에 설정 해야는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스와에 연결 하는 데 사용할 모든 워크스테이션과 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스.

일부 시험판 버전의 [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] Revolution Analytics에서 만든 Windows 용 R 개발 환경을 포함 합니다. 이 도구는 더 이상 제공 하 고 지원 되지 않습니다.

호환성을 위해 [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], 대신 Microsoft R Client를 설치 하는 것이 좋습니다. [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/) 및 [Visual Studio Code](https://code.visualstudio.com/) 도 Microsoft R 솔루션을 지원 합니다.

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>SQLite ODBC 드라이버와 RevoScaleR의 호환성 문제

SQLite ODBC 드라이버의 수정 버전 0.92는 RevoScaleR과 호환 되지 않습니다. 수정 버전 0.88 ~ 0.91 및 0.93 이상은 및 나중에 호환 가능한 것으로 알려져 있습니다.

## <a name="see-also"></a>참고자료

[SQL Server 2016의 새로운 기능](../sql-server/what-s-new-in-sql-server-2016.md)

[SQL Server의 기계 학습 문제 해결](machine-learning-troubleshooting-faq.md)
