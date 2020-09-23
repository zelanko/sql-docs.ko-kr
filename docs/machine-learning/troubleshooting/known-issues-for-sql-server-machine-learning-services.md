---
title: Python 및 R의 알려진 문제
description: 이 문서에서는 SQL Server Machine Learning Services 및 SQL Server 2016 R Services에서 제공되는 Python 및 R 구성 요소의 알려진 문제 또는 제한 사항을 설명합니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/15/2020
ms.topic: troubleshooting
author: dphansen
ms.author: davidph
ms.custom: contperfq4
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 914f8626a297dd233d6b22230d579623e0e98cf6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495054"
---
# <a name="known-issues-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services의 알려진 문제
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

이 문서에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) 및 [SQL Server 2016 R Services](../r/sql-server-r-services.md)에서 제공되는 Python 및 R 구성 요소의 알려진 문제 또는 제한 사항을 설명합니다.

## <a name="setup-and-configuration-issues"></a>설치 및 구성 문제

초기 설치 및 구성과 관련된 프로세스에 대한 설명은 [SQL Server Machine Learning Services 설치](../install/sql-machine-learning-services-windows-install.md)를 참조하세요. 업그레이드, 함께 설치, 새로운 R 또는 Python 구성 요소 설치에 대한 정보가 포함되어 있습니다.

### <a name="1-inconsistent-results-in-mkl-computations-due-to-missing-environment-variable"></a>1. 환경 변수 누락으로 인한 MKL 계산 결과 불일치

**적용 대상:** R_SERVER 이진 파일 9.0, 9.1, 9.2 또는 9.3.

R_SERVER는 Intel MKL(Math Kernel Library)을 사용합니다. MKL을 포함하는 계산의 경우 시스템에 환경 변수가 없으면 결과가 불일치할 수 있습니다. 

환경 변수 `'MKL_CBWR'=AUTO`를 설정하여 R_SERVER에서 Conditional Numerical Reproducibility를 확인합니다. 자세한 내용은 [Introduction to Conditional Numerical Reproducibility(CNR)](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)를 참조하세요.

**해결 방법**

1. 제어판에서 **시스템 및 보안** > **시스템** > **고급 시스템 설정** > **환경 변수**를 클릭합니다.

2. 새 사용자 또는 시스템 변수를 만듭니다. 

   + 변수 이름을 'MKL_CBWR'로 설정합니다.
   + '변수 값'을 'AUTO'로 설정합니다.

3. R_SERVER를 다시 시작합니다. SQL Server에서 SQL Server 실행 패드 서비스를 다시 시작할 수 있습니다.

> [!NOTE]
> Linux에서 SQL Server 2019를 실행하는 경우 사용자 홈 디렉터리에서 *.bash_profile*을 편집하거나 만들어 `export MKL_CBWR="AUTO"` 줄을 추가합니다. Bash 명령 프롬프트에서 `source .bash_profile`을 입력하여 이 파일을 실행합니다. R 명령 프롬프트에서 `Sys.getenv()`를 입력하여 R_SERVER를 다시 시작합니다.

### <a name="2-r-script-runtime-error-sql-server-2017-cu5-cu7-regression"></a>2. R 스크립트 런타임 오류(SQL Server 2017 CU5~CU7 재발)

SQL Server 2017의 경우 누적 업데이트 5부터 7까지 임시 디렉터리 파일 경로에 공백이 포함되는 재발이 **rlauncher.config** 파일에 있습니다. 이 재발은 CU8에서 수정되었습니다.

R 스크립트를 실행할 때 표시되는 오류에는 다음 메시지가 포함됩니다.

> *'R' 스크립트의 런타임과 통신할 수 없습니다. 'R' 런타임의 요구 사항을 확인하세요.*
>
> 외부 스크립트의 STDERR 메시지: 
>
> *치명적인 오류: 'R_TempDir'을 만들 수 없습니다.*

**해결 방법**

CU8을 사용할 수 있게 되면 CU8을 적용합니다. 또는 관리자 권한 명령 프롬프트에서 uninstall/install로 **registerrext**를 실행하여 **rlauncher**를 다시 만들 수 있습니다. 

```cmd
<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /uninstall /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>

<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /install /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>
```

다음 예는 기본 인스턴스 "MSSQL14.MSSQLSERVER"가 "C:\Program Files\Microsoft SQL Server”에 설치된 명령을 보여 줍니다\".

```cmd
"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /uninstall /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER

"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /install /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER
```

### <a name="3-unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>3. 도메인 컨트롤러에 SQL Server 기계 학습 기능을 설치할 수 없음

SQL Server 2016 R Services 또는 SQL Server Machine Learning Services를 도메인 컨트롤러에 설치하려고 하면 다음 오류와 함께 설치에 실패합니다.

> *기능 설치 프로세스 중에 오류가 발생했습니다.*
>
> *ID로 그룹을 찾을 수 없습니다.*
>
> *구성 요소 오류 코드: 0x80131509*

이 오류는 도메인 컨트롤러에서 서비스가 기계 학습을 실행하는 데 필요한 20개의 로컬 계정을 만들 수 없기 때문에 발생합니다. 일반적으로 도메인 컨트롤러에 SQL Server를 설치하지 않는 것이 좋습니다. 자세한 내용은 [지원 공지 2032911](https://support.microsoft.com/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont)을 참조하세요.

### <a name="4-install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>4. Microsoft R Client와의 호환성을 위해 최신 서비스 릴리스 설치

최신 버전의 Microsoft R Client를 설치하여 원격 컴퓨팅 컨텍스트에서 R을 SQL Server에서 실행하는 데 사용하는 경우 다음과 같은 오류가 발생할 수 있습니다.

> *컴퓨터에서 Microsoft R Server 버전 8.x.x와 호환되지 않는 Microsoft R Client 버전 9.x.x를 실행 중입니다. 호환되는 버전을 다운로드하여 설치하세요.*

SQL Server 2016에서는 클라이언트의 R 라이브러리와 서버의 R 라이브러리가 정확히 일치해야 합니다. 이 제한은 Microsoft R Server 9.0.1 이후 릴리스에서 제거되었습니다. 하지만 이 오류가 발생하는 경우 클라이언트와 서버에서 사용하는 R 라이브러리 버전을 확인하고 필요하다면 서버 버전과 일치하도록 클라이언트를 업데이트하세요.

SQL Server 서비스 릴리스가 설치될 때마다 SQL Server R Services와 함께 설치된 R 버전이 업데이트됩니다. R 구성 요소를 항상 최신 버전으로 유지하려면 모든 서비스 팩을 설치해야 합니다.

Microsoft R Client 9.0.0과의 호환성을 위해 이 [지원 문서](https://support.microsoft.com/kb/3210262)에 설명된 업데이트를 설치하세요.

R 패키지 문제를 방지하기 위해 [다음 섹션](#bkmk_sqlbindr)에 설명된 대로 Modern Lifecycle Support 정책을 사용하도록 서비스 계약을 변경하여 서버에 설치된 R 라이브러리 버전을 업그레이드할 수도 있습니다. 이렇게 하면 SQL Server와 함께 설치되는 R 버전이 Machine Learning Server(이전의 Microsoft R Server)의 업데이트에 사용되는 것과 동일한 일정에 따라 업데이트됩니다.

**적용 대상:** SQL Server 2016 R Services(Microsoft R Server 버전 9.0.0 이전 버전)

### <a name="5-r-components-missing-from-cu3-setup"></a>5. CU3 설치에서 R 구성 요소가 누락됨

제한된 수의 Azure 가상 머신은 SQL Server에 포함되어야 하는 R 설치 파일 없이 프로비전되었습니다. 이 문제는 2018-01-05~2018-01-23 기간에 프로비전된 가상 머신에 해당됩니다. 2018-01-05~2018-01-23 기간 동안 SQL Server 2017용 CU3 업데이트를 적용한 경우에도 이 문제가 온-프레미스 설치에 영향을 줄 수 있습니다.

올바른 버전의 R 설치 파일이 포함된 서비스 릴리스가 제공되었습니다.

+ [SQL Server 2017용 누적 업데이트 패키지 3 KB4052987](https://www.microsoft.com/download/details.aspx?id=56128).

구성 요소를 설치하고 SQL Server 2017 CU3를 복구하려면 CU3를 제거하고 업데이트된 버전을 다시 설치해야 합니다.

1. R 설치 관리자를 포함하는 업데이트된 CU3 설치 파일을 다운로드합니다.
2. CU3를 제거합니다. 제어판에서 **업데이트 제거**를 검색한 다음 "SQL Server 2017에 대한 핫픽스 3015(KB4052987)(64비트)"를 선택합니다. 제거 단계를 진행합니다.
3. 방금 다운로드한 KB4052987에 대한 업데이트를 두 번 클릭하여 CU3 업데이트를 다시 설치합니다`SQLServer2017-KB4052987-x64.exe`. 설치 지침을 따릅니다.

### <a name="6-unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>6. SQL Server 2017 CTP 2.0 이상 버전의 오프라인 설치에서 Python 구성 요소를 설치할 수 없음

인터넷에 액세스할 수 없는 컴퓨터에 SQL Server 2017의 시험판 버전을 설치하는 경우 설치 관리자에서 다운로드한 Python 구성 요소의 위치를 묻는 페이지를 표시하지 못할 수 있습니다. 이러한 인스턴스에서는 Machine Learning Servcies 구성 요소는 설치할 수 있지만 Python 구성 요소는 설치할 수 없습니다.

이 문제는 릴리스 버전에서 해결되었습니다. 또한 이 제한 사항은 R 구성 요소에는 적용되지 않습니다.

**적용 대상:** SQL Server 2017 with Python

### <a name="warning-of-incompatible-version-when-you-connect-to-an-older-version-of-sql-server-r-services-from-a-client-by-using-sssqlv14_md"></a><a name="bkmk_sqlbindr"></a>[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]를 사용하여 클라이언트에서 이전 버전의 SQL Server R Services에 연결하는 경우 호환되지 않는 버전 경고

SQL Server 2016 컴퓨팅 컨텍스트에서 R 코드를 실행하면 다음과 같은 오류가 표시될 수 있습니다.

> *컴퓨터에서 Microsoft R Server 버전 8.0.3과 호환되지 않는 Microsoft R Client 버전 9.0.0을 실행 중입니다. 호환되는 버전을 다운로드하여 설치하세요.*

이 메시지는 다음 두 문장 중 하나가 참인 경우 표시됩니다.

+ [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 설치 마법사를 사용하여 클라이언트 컴퓨터에 Microsoft R Server(독립 실행형)를 설치했습니다.
+ [별도의 Windows Installer](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)를 사용하여 Microsoft R Server를 설치했습니다.

서버와 클라이언트가 동일한 버전을 사용하도록 하려면 Microsoft R Server 9.0 이상 릴리스에서 지원되는 _바인딩_을 사용하여 SQL Server 2016 인스턴스의 R 구성 요소를 업그레이드해야 할 수 있습니다. 업그레이드 지원이 가능한 R Services 버전인지 확인하려면 [SqlBindR.exe를 사용하여 R Services 인스턴스 업그레이드](../install/upgrade-r-and-python.md)를 참조하세요.

**적용 대상:** SQL Server 2016 R Services(Microsoft R Server 버전 9.0.0 이전 버전)

### <a name="7-setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>7. SQL Server 2016 서비스 릴리스 설치 프로그램에서 최신 버전의 R 구성 요소를 설치하지 못할 수 있음

인터넷에 연결되지 않은 컴퓨터에 SQL Server 2016용 서비스 팩을 설치하거나 누적 업데이트를 설치하는 경우 다운로드한 CAB 파일을 사용하여 R 구성 요소를 업데이트할 수 있는 프롬프트를 설치 마법사에서 표시하지 못할 수 있습니다. 이 오류는 일반적으로 데이터베이스 엔진과 함께 여러 구성 요소가 설치된 경우 발생합니다.

해결 방법으로 명령줄을 사용하고 이 예에 나온 것처럼 CU1 업데이트를 설치하는 `MRCACHEDIRECTORY` 인수를 지정하여 서비스 릴리스를 설치할 수 있습니다.

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

최신 설치 관리자를 다운로드하려면 [인터넷 액세스 없이 기계 학습 구성 요소 설치](../install/sql-ml-component-install-without-internet-access.md)를 참조하세요.

**적용 대상:** SQL Server 2016 R Services(Microsoft R Server 버전 9.0.0 이전 버전)

### <a name="8-launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>8. 버전이 R 버전과 다른 경우 실행 패드 서비스가 시작되지 않음

데이터베이스 엔진과 별도로 SQL Server R Services를 설치하고 빌드 버전이 서로 다른 경우 시스템 이벤트 로그에 다음과 같은 오류가 표시될 수 있습니다.

> *다음 오류 때문에 SQL Server 실행 패드 서비스를 시작하지 못했습니다. 서비스가 적절한 시간 내에 시작 또는 제어 요청에 응답하지 않았습니다.*

예를 들어 릴리스 버전을 사용하여 데이터베이스 엔진을 설치하고 패치를 적용하여 데이터베이스 엔진을 업그레이드한 다음 릴리스 버전을 사용하여 R Services 기능을 추가하는 경우 이 오류가 발생할 수 있습니다.

이 문제를 방지하려면 파일 관리자와 같은 유틸리티를 사용하여 Launchpad.exe의 버전을 sqldk.dll과 같은 SQL 이진 파일과 비교합니다. 모든 구성 요소의 버전 번호가 동일해야 합니다. 하나의 구성 요소를 업그레이드하는 경우 설치된 다른 모든 구성 요소에 동일한 업그레이드를 적용해야 합니다.

인스턴스의 `Binn` 폴더에서 실행 패드를 찾습니다. 예를 들어 SQL Server 2016의 기본 설치에서는 경로가 `C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`일 수 있습니다. 

### <a name="9-remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>9. Azure 가상 머신에서 실행되는 SQL Server 인스턴스의 방화벽에 의해 원격 컴퓨팅 컨텍스트가 차단됨

Azure 가상 머신에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 설치한 경우 가상 머신의 작업 영역을 사용해야 하는 컴퓨팅 컨텍스트를 사용하지 못할 수 있습니다. 이는 기본적으로 Azure 가상 머신 방화벽에 로컬 R 사용자 계정에 대한 네트워크 액세스를 차단하는 규칙이 있기 때문입니다.

이 문제를 해결하려면 Azure VM에서 **고급 보안이 포함된 Windows 방화벽**을 열고 **아웃바운드 규칙**을 선택한 후 다음 규칙을 사용하지 않도록 설정합니다. **SQL Server 인스턴스 MSSQLSERVER의 R 로컬 사용자 계정에 대한 네트워크 액세스를 차단합니다**. 규칙을 사용하도록 설정된 상태로 둘 수도 있지만 보안 속성을 **안전한 경우 허용**으로 변경합니다.

### <a name="10-implied-authentication-in-sqlexpress"></a>10. SQLEXPRESS의 암시적 인증

통합 Windows 인증을 사용하여 원격 데이터 과학 워크스테이션에서 R 작업을 실행하는 경우 SQL Server는 *암시적 인증*을 사용하여 스크립트에 필요할 수 있는 로컬 ODBC 호출을 생성합니다. 그러나 SQL Server Express Edition의 RTM 빌드에서는 이 기능이 작동하지 않았습니다.

이 문제를 해결하려면 이후 서비스 릴리스로 업그레이드하는 것이 좋습니다.

업그레이드할 수 없는 경우 해결 방법으로 SQL 로그인을 사용하여 포함된 ODBC 호출이 필요할 수 있는 원격 R 작업을 실행할 수 있습니다.

**적용 대상:** SQL Server 2016 R Services Express Edition

### <a name="11-performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>11. SQL Server가 사용하는 라이브러리를 다른 도구에서 호출하는 경우의 성능 제한

RGui와 같은 외부 애플리케이션에서 SQL Server용으로 설치된 기계 학습 라이브러리를 호출할 수 있습니다. 이렇게 하는 것이 새 패키지를 설치하거나 매우 짧은 코드 샘플에서 임시 테스트를 실행하는 등의 특정 작업을 수행하는 가장 편리한 방법일 수도 있습니다. 하지만 SQL Server 외부에서는 성능이 제한될 수 있습니다.

예를 들어 SQL Server Enterprise Edition을 사용하더라도 외부 도구를 사용하여 R 코드를 실행하면 단일 스레드 모드에서 R이 실행됩니다. SQL Server에서 성능상 이점을 얻으려면 SQL Server 연결을 시작하고 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 외부 스크립트 런타임을 호출합니다.

일반적으로 SQL Server가 사용하는 기계 학습 라이브러리를 외부 도구에서 호출하지 않는 것이 좋습니다. R 또는 Python 코드를 디버깅해야 하는 경우 일반적으로 SQL Server 외부에서 수행하는 것이 더 쉽습니다. SQL Server에 있는 것과 동일한 라이브러리를 얻으려면 Microsoft R Client 또는 [SQL Server 2017 Machine Learning Server(독립 실행형)](../install/sql-machine-learning-standalone-windows-install.md)를 설치할 수 있습니다.

### <a name="12-sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>12. SQL Server Data Tools가 외부 스크립트에 필요한 권한을 지원하지 않음

Visual Studio 또는 SQL Server Data Tools를 사용하여 데이터베이스 프로젝트를 게시할 때 보안 주체에게 외부 스크립트 실행과 관련한 권한이 있는 경우 다음과 같은 오류가 발생할 수 있습니다.

> *TSQL 모델: 데이터베이스를 리버스 엔지니어링하는 동안 오류가 발생 했습니다. 권한을 인식할 수 없으며 가져오지 못했습니다.*

현재 DACPAC 모델은 GRANT ANY EXTERNAL SCRIPT 또는 EXECUTE ANY EXTERNAL SCRIPT 같이 R Services 또는 Machine Learning Services에서 사용하는 권한을 지원하지 않습니다. 이 문제는 향후 릴리스에서 해결될 예정입니다.

해결 방법으로 배포 후 스크립트에서 추가 GRANT 문을 실행합니다.

### <a name="13-external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>13. 리소스 거버넌스 기본값으로 인해 외부 스크립트 실행이 제한됨

Enterprise Edition에서 리소스 풀을 사용하여 외부 스크립트 프로세스를 관리할 수 있습니다. 일부 초기 릴리스 빌드에서는 R 프로세스에 할당할 수 있는 최대 메모리가 20%였습니다. 따라서 서버에 32GB의 RAM이 있는 경우 R 실행 파일(RTerm.exe 및 BxlServer.exe)은 단일 요청에 최대 6.4GB를 사용할 수 있었습니다.

리소스 제한이 발생하는 경우 현재 기본값을 확인합니다. 20%로 부족한 경우 이 값을 변경하는 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 설명서를 참조하세요.

**적용 대상:** SQL Server 2016 R Services, Enterprise Edition

### <a name="14-error-when-using-sp_execute_external_script-without-libcso-on-linux"></a>14. Linux에서 `libc++.so` 없이 `sp_execute_external_script`를 사용하는 경우 오류 발생

`libc++.so`가 설치되지 않은 클린 Linux 컴퓨터에서는 `commonlauncher.so`가 `libc++.so`를 로드하지 못해 Java 또는 외부 언어를 사용하여 `sp_execute_external_script`(SPEES) 쿼리를 실행하는 데 실패합니다.

예를 들면 다음과 같습니다.

```sql
EXECUTE sp_execute_external_script @language = N'Java'
    , @script = N'JavaTestPackage.PassThrough'
    , @parallel = 0
    , @input_data_1 = N'select 1'
WITH RESULT SETS((col1 INT NOT NULL))
GO
```

다음과 유사한 메시지와 함께 이 작업이 실패합니다.

```text
Msg 39012, Level 16, State 14, Line 0

Unable to communicate with the runtime for 'Java' script for request id: 94257840-1704-45E8-83D2-2F74AEB46CF7. Please check the requirements of 'Java' runtime.
```

`mssql-launchpadd` 로그에 다음과 유사한 오류 메시지가 표시됩니다.

```text
Oct 18 14:03:21 sqlextmls launchpadd[57471]: [launchpad] 2019/10/18 14:03:21 WARNING: PopulateLauncher failed: Library /opt/mssql-extensibility/lib/commonlauncher.so not loaded. Error: libc++.so.1: cannot open shared object file: No such file or directory
```

**해결 방법**

다음 해결 방법 중 하나를 수행할 수 있습니다.

1. `/opt/mssql/lib`에서 기본 시스템 경로 `/lib64`로 `libc++*`를 복사합니다.

1. `/var/opt/mssql/mssql.conf`에 다음 항목을 추가하여 경로를 노출합니다.

   ```text
   [extensibility]
   readabledirectories = /opt/mssql
   ```

**적용 대상:** Linux의 SQL Server 2019

### <a name="15-installation-or-upgrade-error-on-fips-enabled-servers"></a>15. FIPS 사용 서버에서 설치 또는 업그레이드 오류

[FIPS(Federal Information Processing Standard)](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/system-cryptography-use-fips-compliant-algorithms-for-encryption-hashing-and-signing) 사용 서버에서 **Machine Learning Services 및 언어 확장** 기능을 사용하여 SQL Server 2019를 설치하거나 SQL Server 인스턴스를 업그레이드하면 다음 오류가 표시됩니다.

> 확장성 기능을 설치하는 동안 오류가 발생했습니다. 오류 메시지: AppContainer를 만들지 못했습니다. 오류 메시지 없음, 이 구현은 Windows Platform FIPS 유효성을 검사한 암호화 알고리즘의 일부가 아닙니다.

**해결 방법**

**Machine Learning Services 및 언어 확장** 기능을 사용하여 SQL Server 2019를 설치하거나 SQL Server 인스턴스를 업그레이드하기 전에 FIPS를 사용하지 않도록 설정합니다. 설치 또는 업그레이드가 완료되면 FIPS를 다시 활성화할 수 있습니다.

**적용 대상:** SQL Server 2019

## <a name="r-script-execution-issues"></a>R 스크립트 실행 문제

이 섹션에는 SQL Server에서의 R 실행과 관련된 알려진 문제뿐 아니라 RevoScaleR를 포함하여 Microsoft에서 게시한 R 라이브러리 및 도구와 관련된 몇 가지 문제가 포함되어 있습니다.

R 솔루션에 영향을 줄 수 있는 알려진 추가 문제는 [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues) 사이트를 참조하세요.

### <a name="1-access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>1. 기본 위치가 아닌 위치에 있는 SQL Server에서 R 스크립트를 실행할 때 액세스 거부 경고

SQL Server 인스턴스가 `Program Files` 폴더 외부와 같이 기본이 아닌 위치에 설치된 경우 패키지를 설치하는 스크립트를 실행하려고 할 때 ACCESS_DENIED 경고가 발생합니다. 다음은 그 예입니다.

> *`normalizePath(path.expand(path), winslash, mustWork)` : path[2]="~ExternalLibraries/R/8/1": 액세스가 거부되었습니다*

그 이유는 기본 제공 사용자 그룹 **SQLRUserGroup**에 읽기 권한이 없는 경우에 R 함수가 경로를 읽으려고 시도하고 실패하기 때문입니다. 발생한 경고는 현재 R 스크립트의 실행을 차단하지 않지만 사용자가 다른 R 스크립트를 실행할 때마다 경고가 반복적으로 되풀이될 수 있습니다.

SQL Server를 기본 위치에 설치한 경우에는 모든 Windows 사용자에게 `Program Files` 폴더에 대한 읽기 권한이 있으므로 이 오류가 발생하지 않습니다.

이 문제는 예정된 서비스 릴리스에서 해결됩니다. 해결 방법으로 그룹 **SQLRUserGroup**에게 `ExternalLibraries`의 모든 부모 폴더에 대한 읽기 액세스 권한을 제공하세요.

### <a name="2-serialization-error-between-old-and-new-versions-of-revoscaler"></a>2. RevoScaleR 이전 버전과 새 버전 간의 직렬화 오류

직렬화된 형식을 사용하여 모델을 원격 SQL Server 인스턴스에 전달하면 다음과 같은 오류가 발생할 수 있습니다. 

> *memDecompress(데이터, 유형 = 압축 풀기) 내부 오류의 오류 -3/memDecompress(2).*

이 오류는 직렬화 함수 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)의 최신 버전을 사용하여 모델을 저장했지만 모델을 역직렬화하는 SQL Server 인스턴스에 SQL Server 2017 CU2 이전 버전의 RevoScaleR API 이전 버전이 있는 경우에 발생합니다.

해결 방법으로 SQL Server 2017 인스턴스를 CU3 이상으로 업그레이드할 수 있습니다.

API 버전이 동일하거나 이전 직렬화 함수를 사용하여 저장된 모델을 최신 버전의 직렬화 API를 사용하는 서버로 이동하는 경우에는 오류가 표시되지 않습니다.

즉, 직렬화 작업과 역직렬화 작업에 동일한 버전의 RevoScaleR를 사용하세요.

### <a name="3-real-time-scoring-does-not-correctly-handle-the-_learningrate_-parameter-in-tree-and-forest-models"></a>3. 실시간 채점이 트리 및 포리스트 모델에서 _learningRate_ 매개 변수를 올바르게 처리하지 않음

의사 결정 트리 또는 의사 결정 포리스트 방법을 사용하 여 모델을 만들고 학습 속도를 지정하는 경우 `sp_rxpredict` 또는 SQL `PREDICT` 함수를 사용하면 `rxPredict`를 사용할 때에 비해 일관되지 않은 결과가 나타날 수 있습니다.

원인은 직렬화된 모델을 처리하는 API의 오류이며, `learningRate` 매개 변수(예: [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)에서 또는)로 제한됩니다. 또는

이 문제는 예정된 서비스 릴리스에서 해결됩니다.

### <a name="4-limitations-on-processor-affinity-for-r-jobs"></a>4. R 작업에 대한 프로세서 선호도 제한

SQL Server 2016의 초기 릴리스 빌드에서는 첫 번째 k 그룹의 CPU에 대해서만 프로세서 선호도를 설정할 수 있습니다. 예를 들어 서버가 2개의 k 그룹이 있는 2 소켓 시스템인 경우 첫 번째 k 그룹의 프로세서만 R 프로세스에 사용됩니다. R 스크립트 작업에 대한 리소스 관리를 구성하는 경우 동일한 제한 사항이 적용됩니다.

이 문제는 SQL Server 2016 서비스 팩 1에서 해결되었습니다. 최신 서비스 릴리스로 업그레이드하는 것이 좋습니다.

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

해결 방법으로 CAST 또는 CONVERT를 사용하고 올바른 데이터 형식을 사용하여 R에 데이터를 제공하도록 쿼리를 다시 작성할 수 있습니다. 일반적으로 R 코드에서 데이터를 변경하는 대신 SQL을 사용하여 데이터 작업을 할 때 성능이 더 좋습니다.

**적용 대상:** SQL Server 2016 R Services

### <a name="6-limits-on-size-of-serialized-models"></a>6. 직렬화된 모델 크기 제한

모델을 SQL Server 테이블에 저장하는 경우 모델을 직렬화하여 이진 형식으로 저장해야 합니다. 이론적으로 이 메서드를 사용하여 저장할 수 있는 모델의 최대 크기는 SQL Server의 varbinary 열 최대 크기인 2GB입니다.

더 큰 모델을 사용해야 하는 경우 다음 해결 방법을 사용할 수 있습니다.

+ 모델 크기를 줄이기 위한 단계를 수행합니다. 일부 오픈 소스 R 패키지에는 모델 개체에 많은 정보가 포함되어 있으며 이 정보 중 상당수는 배포를 위해 제거할 수 있습니다. 
+ 기능 선택을 사용하여 불필요한 열을 제거합니다.
+ 오픈 소스 알고리즘을 사용하는 경우 MicrosoftML 또는 RevoScaleR에서 해당하는 알고리즘을 사용한 유사한 구현을 고려해 보세요. 이러한 패키지는 배포 시나리오에 맞게 최적화되었습니다.
+ 이전 단계를 사용하여 모델을 합리화하고 크기를 줄인 후에는 모델을 SQL Server로 전달하기 전에 기본 R의 [memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress) 함수를 사용하여 모델 크기를 줄일 수 있는지 확인합니다. 이 옵션은 모델이 2GB 제한에 근접한 경우에 가장 적합합니다.
+ 더 큰 모델의 경우 varbinary 열을 사용하지 않고 SQL Server [FileTable](../../relational-databases/blob/filetables-sql-server.md) 기능을 사용하여 모델을 저장할 수 있습니다.

    FileTable에 저장된 데이터는 SQL Server의 Filestream 파일 시스템 드라이버에 의해 관리되고 기본 방화벽 규칙이 네트워크 파일 액세스를 차단하기 때문에 FileTable을 사용하려면 방화벽 예외를 추가해야 합니다. 자세한 내용은[FileTable에 대한 필수 구성 요소 사용 설정](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)을 참조하세요.

    FileTable을 사용하도록 설정한 후 모델을 쓰려면 FileTable API를 사용하여 SQL에서 경로를 가져온 다음 코드에서 해당 위치에 모델을 씁니다. 모델을 읽어야 하는 경우에는 SQL에서 경로를 가져온 다음 스크립트에서 경로를 사용하여 모델을 호출합니다. 자세한 내용은 [파일 입출력 API를 사용하여 FileTable 액세스](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)를 참조하세요.

### <a name="7-avoid-clearing-workspaces-when-you-execute-r-code-in-a-ssnoversion-compute-context"></a>7. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨팅 컨텍스트에서 R 코드를 실행하는 경우에는 작업 영역을 지우지 마세요.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨팅 컨텍스트에서 R 코드를 실행하는 동안 R 명령을 사용하여 작업 영역에서 개체를 지우거나 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 호출된 R 스크립트의 일부로 작업 영역을 지우는 경우 다음 오류가 발생할 수 있습니다. *작업 영역 개체 'revoScriptConnection'을 찾을 수 없습니다.*

`revoScriptConnection` 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 호출된 R 세션에 대한 정보를 포함하는 R 작업 영역의 개체입니다. 그러나 R 코드에 작업 영역을 지우는 명령(예: `rm(list=ls()))`)이 포함되어 있으면 세션 및 R 작업 영역의 다른 개체에 대한 모든 정보도 지워집니다.

해결 방법으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 R을 실행하는 동안에는 변수 및 기타 개체를 무차별로 지우지 마세요. R 콘솔에서 작업할 때 작업 영역을 지우는 것은 일반적이지만 의도하지 않은 결과가 발생할 수 있습니다.

+ 특정 변수를 삭제하려면 R `remove` 함수를 사용합니다(예: `remove('name1', 'name2', ...)`).
+ 삭제할 변수가 여러 개인 경우 임시 변수 이름을 목록에 저장하고 주기적 가비지 수집을 수행합니다.

### <a name="8-restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>8. R 스크립트의 입력으로 제공될 수 있는 데이터에 대한 제한

R 스크립트에서는 다음 유형의 쿼리 결과를 사용할 수 없습니다.

- AlwaysEncrypted 열을 참조하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리의 데이터
  
- 마스킹된 열을 참조하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리의 데이터
  
     R 스크립트에서 마스킹된 데이터를 사용해야 하는 경우 가능한 해결 방법은 임시 테이블에 데이터 복사본을 만들고 해당 데이터를 대신 사용하는 것입니다.

### <a name="9-use-of-strings-as-factors-can-lead-to-performance-degradation"></a>9. 문자열을 요소로 사용하면 성능이 저하될 수 있습니다.

문자열 유형 변수를 요소로 사용하면 R 작업에 사용되는 메모리의 양이 크게 늘어날 수 있습니다. 이것은 R의 일반적으로 알려진 문제이며 이 주제에 대한 많은 문서가 있습니다. 예를 들어 [Factors are not first-class citizens in R, by John Mount, in R-bloggers](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/) 또는 [stringsAsFactors: An unauthorized biography, by Roger Peng](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/)을 참조하세요. 

이 문제는 SQL Server에 고유한 문제는 아니지만 SQL Server에서 실행되는 R 코드의 성능에 큰 영향을 줄 수 있습니다. 문자열은 일반적으로 varchar 또는 nvarchar로 저장되며, 문자열 데이터의 열에 고유한 값이 많으면 내부적으로 이러한 값을 정수로 변환하고 R에 의해 문자열로 다시 변환하는 과정에서 메모리 할당 오류가 발생할 수도 있습니다.

다른 작업에 문자열 데이터 형식이 반드시 필요하지 않은 경우 데이터 준비의 일부로 문자열 값을 숫자(정수) 데이터 형식에 매핑하면 성능 및 확장 관점에서 도움이 됩니다.

이 문제에 대한 논의와 그 밖의 팁은 [R 서비스 성능 - 데이터 최적화](../r/r-and-data-optimization-r-services.md)를 참조하세요.

### <a name="10-arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>10. SQL Server 데이터 원본의 경우 *varsToKeep* 및 *varsToDrop* 인수가 지원되지 않습니다.

rxDataStep 함수를 사용하여 테이블에 결과를 쓸 때 *varsToKeep* 및 *varsToDrop*을 사용하면 작업의 일부로 포함하거나 제외할 열을 쉽게 지정할 수 있습니다. 하지만 SQL Server 데이터 원본의 경우 이러한 인수가 지원되지 않습니다.

### <a name="11-limited-support-for-sql-data-types-in-sp_execute_external_script"></a>11. sp\_execute\_external\_script에서 SQL 데이터 형식 지원이 제한됨

SQL에서 지원되는 일부 데이터 형식은 R에서 사용할 수 없습니다. 해결 방법으로 sp\_execute\_external\_script에 데이터를 전달하기 전에 지원되지 않는 데이터 형식을 지원되는 데이터 형식으로 캐스팅하는 것이 좋습니다.

자세한 내용은 [R 라이브러리 및 데이터 형식](../r/r-libraries-and-data-types.md)을 참조하세요.

### <a name="12-possible-string-corruption-using-unicode-strings-in-varchar-columns"></a>12. varchar 열에서 유니코드 문자열 사용 시 가능한 문자열 손상

varchar 열의 유니코드 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 R/Python으로 전달하면 문자열이 손상될 수 있습니다. 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬에서의 해당 유니코드 문자열 인코딩이 R/Python에서 사용되는 기본 UTF-8 인코딩과 일치하지 않을 수 있기 때문입니다. 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 R/Python으로 ASCII가 아닌 문자열 데이터를 전송하려면 UTF-8 인코딩([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]에서 사용 가능)을 사용하거나 동일 데이터에 nvarchar 형식을 사용하세요.

### <a name="13-only-one-value-of-type-raw-can-be-returned-from-sp_execute_external_script"></a>13. `sp_execute_external_script`에서 `raw` 형식의 값 하나만 반환될 수 있음

R에서 이진 데이터 형식(R **원시** 데이터 형식)이 반환되는 경우 값은 출력 데이터 프레임으로 전송되어야 합니다.

**원시** 이외의 데이터 형식의 경우 OUTPUT 키워드를 추가하여 저장 프로시저의 결과와 함께 매개 변수 값을 반환할 수 있습니다. 자세한 내용은 [매개 변수](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters)를 참조하세요.

**원시** 형식의 값을 포함하는 여러 출력 집합을 사용하려는 경우 한 가지 가능한 해결 방법은 저장 프로시저를 여러 번 호출하거나 ODBC를 사용하여 결과 집합을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 다시 보내는 것입니다.

### <a name="14-loss-of-precision"></a>14. 정밀도 손실

[!INCLUDE[tsql](../../includes/tsql-md.md)]과 R은 다양한 데이터 형식을 지원하므로 숫자 데이터 형식은 변환 도중 정밀도가 떨어질 수 있습니다.

암시적 데이터 형식 변환에 대한 자세한 내용은 [R 라이브러리 및 데이터 형식](../r/r-libraries-and-data-types.md)을 참조하십시오.

### <a name="15-variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>15. transformFunc 매개 변수를 사용하는 경우 변수 범위 지정 오류

모델링 중에 데이터를 변환하려면 `rxLinmod` 또는 `rxLogit` 같은 함수에서 *transformFunc* 인수를 전달할 수 있습니다. 그러나 중첩된 함수 호출은 로컬 컴퓨팅 컨텍스트에서 올바르게 작동하는 경우에도 SQL Server 컴퓨팅 컨텍스트에서 범위 지정 오류를 일으킬 수 있습니다.

> *분석을 위한 샘플 데이터 집합에 변수가 없습니다.*

예를 들어 로컬 전역 환경에서 두 개의 함수 `f`와 `g`를 정의했고 `g`가 `f`를 호출한다고 가정해 보겠습니다. `g`가 포함된 분산 또는 원격 호출에서는 `f`와 `g`를 원격 호출에 전달했더라도 `f`를 찾을 수 없으므로 `g`에 대한 호출이 이 오류와 함께 실패할 수 있습니다.

이 문제가 발생한 경우 `f` 의 정의를 `g`의 정의 내에 포함하여 문제를 해결할 수 있습니다. `g` 앞의 모든 곳에서 `f`를 정상적으로 호출합니다.

다음은 그 예입니다.

```R
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

오류를 방지하려면 다음과 같이 정의를 다시 작성합니다.

```R
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="16-data-import-and-manipulation-using-revoscaler"></a>16. RevoScaleR을 사용하여 데이터 가져오기 및 조작

데이터베이스에서 **varchar** 열을 읽을 때 공백이 잘립니다. 이를 방지하려면 공백이 아닌 문자로 문자열을 묶습니다.

`rxDataStep`과 같은 함수를 사용하여 **varchar** 열이 포함된 데이터베이스 테이블을 만드는 경우 열 너비는 데이터의 샘플을 기반으로 예상됩니다. 너비가 달라질 수 있는 경우 모든 문자열을 공통 길이로 패딩해야 할 수 있습니다.

`rxImport` 또는 `rxTextToXdf` 에 대한 반복된 호출을 사용하여 행을 가져오고 추가하면서 여러 입력 파일을 단일.xdf 파일에 통합하는 경우 변환을 사용하여 변수의 데이터 형식을 변경할 수 없습니다.

### <a name="17-limited-support-for-rxexec"></a>17. rxExec에 대한 제한적 지원

SQL Server 2016에서는 RevoScaleR 패키지가 제공하는 `rxExec` 함수를 단일 스레드 모드에서만 사용할 수 있습니다.

### <a name="18-increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>18. rxGetVarInfo를 지원하도록 최대 매개 변수 크기 늘리기

매우 많은 변수(예: 40,000개)가 있는 데이터 집합을 사용하는 경우 `rxGetVarInfo`와 같은 함수를 사용하려면 R을 시작할 때 `max-ppsize` 플래그를 설정해야 합니다. `max-ppsize` 플래그는 포인터 보호 스택의 최대 크기를 지정합니다.

RGui.exe 또는 RTerm.exe 등 R 콘솔을 사용하는 경우 다음을 입력하여 _max-ppsize_ 값을 500000으로 설정할 수 있습니다.

```R
R --max-ppsize=500000
```

### <a name="19-issues-with-the-rxdtree-function"></a>19. rxDTree 함수 문제

`rxDTree` 함수는 현재 수식 내 변환을 지원하지 않습니다. 특히 즉석에서 요소를 만들기 위해 `F()` 구문을 사용하는 것은 지원되지 않습니다. 그러나 숫자 데이터는 자동으로 범주화됩니다.

순서가 지정된 요소는 `rxDTree`를 제외하고 모든 RevoScaleR 분석 함수의 요소와 동일하게 처리됩니다.

### <a name="20-datatable-as-an-outputdataset-in-r"></a>20. R에서 OutputDataSet인 Data.table

SQL Server 2017 누적 업데이트 13(CU13) 및 이전 버전에서는 R에서 `data.table`을 `OutputDataSet`로 사용할 수 없습니다. 다음 메시지가 나타날 수 있습니다.

``` text
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

R에서 `data.table`을 `OutputDataSet`로 사용하는 것은 SQL Server 2017 누적 업데이트 14(CU13) 이상에서 지원됩니다.

### <a name="21-running-a-long-script-fails-while-installing-a-library"></a>21. 라이브러리를 설치하는 동안 긴 스크립트 실행 실패

장기 실행 외부 스크립트 세션을 실행하고 dbo가 다른 데이터베이스에 병렬로 라이브러리를 설치하려는 경우 스크립트가 종료될 수 있습니다.

예를 들어 마스터에 대해 다음 외부 스크립트를 실행합니다.

```sql
USE MASTER
DECLARE @language nvarchar(1) = N'R'
DECLARE @script nvarchar(max) = N'Sys.sleep(100)'
DECLARE @input_data_1 nvarchar(max) = N'select 1'
EXEC sp_execute_external_script @language = @language, @script = @script, @input_data_1 = @input_data_1 with result sets none
go
```

dbo가 병렬로 LibraryManagementFunctional에 라이브러리를 설치하는 동안:

```sql
USE [LibraryManagementFunctional]
go

CREATE EXTERNAL LIBRARY [RODBC] FROM (CONTENT = N'/home/ani/var/opt/mssql/data/RODBC_1.3-16.tar.gz') WITH (LANGUAGE = 'R')
go

DECLARE @language nvarchar(1) = N'R'
DECLARE @script nvarchar(14) = N'library(RODBC)'
DECLARE @input_data_1 nvarchar(8) = N'select 1'
EXEC sp_execute_external_script @language = @language, @script = @script, @input_data_1 = @input_data_1
go
```

마스터에 대한 이전의 장기 실행 외부 스크립트는 다음과 같은 오류 메시지와 함께 종료됩니다.

> *'sp_execute_external_script'를 실행하는 동안 HRESULT 0x800704d4와 함께 ‘R’ 스크립트 오류가 발생했습니다.*

**해결 방법**

라이브러리 설치를 장기 실행 쿼리와 병렬로 실행하지 마세요. 또는 설치가 완료된 후 장기 실행 쿼리를 다시 실행합니다.

**적용 대상:** Linux의 SQL Server 2019 및 빅 데이터 클러스터만 해당.

### <a name="22-sql-server-stops-responding-when-executing-r-scripts-containing-parallel-execution"></a>22. 병렬 실행을 포함하는 R 스크립트 실행할 때 SQL Server가 응답을 멈춤

SQL Server 2019는 병렬 실행을 사용하는 R 스크립트에 영향을 주는 재발을 포함합니다. 예를 들어 병렬 패키지를 사용하는 스크립트 및 `RxLocalPar` 컴퓨팅 컨텍스트와 함께 `rxExec`를 사용하는 경우가 포함됩니다. 이 문제의 원인은 SQL Server에서 실행하는 동안 병렬 패키지가 null 디바이스에 쓸 때 발생하는 오류 때문입니다.

**적용 대상:** SQL Server 2019.

### <a name="23-precision-loss-for-moneynumericdecimalbigint-data-types"></a>23. money/numeric/decimal/bigint 데이터 형식에서 전체 자릿수 손실

`sp_execute_external_script`를 사용하여 R 스크립트를 실행하면 money, numeric, decimal 및 bigint 데이터 형식을 입력 데이터로 사용할 수 있습니다. 그러나 이들 데이터 형식은 R의 숫자 형식으로 변환되기 때문에 값이 매우 크거나 소수 부분을 가지는 경우 전체 자릿수 손실이 발생합니다.

+ **money**: 경우에 따라 센트 값이 정확하지 않으며 경고가 발생합니다. 경고: 센트 값을 정확하게 나타낼 수 없습니다.  
+ **numeric/decimal**: `sp_execute_external_script`를 사용하는 R 스크립트는 이들 데이터 형식의 전체 범위를 지원하지 않으며 마지막 몇 자리(특히 소수 부분)가 변경됩니다.
+ **bigint**: R에서는 최대 53비트 정수만 지원하며 이후로 전체 자릿수 손실이 발생하기 시작합니다.

## <a name="python-script-execution-issues"></a>Python 스크립트 실행 문제

이 섹션에는 SQL Server에서의 R 실행과 관련된 알려진 문제뿐 아니라 [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 및 [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)을 포함하여 Microsoft에서 게시한 Python 패키지와 관련된 문제가 포함되어 있습니다.

### <a name="1-call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>1. 모델 경로가 너무 긴 경우 미리 학습된 모델에 대한 호출 실패

SQL Server 2017의 초기 릴리스에 미리 학습된 모델을 설치한 경우 학습된 모델 파일의 전체 경로가 너무 길어서 Python이 읽을 수 없습니다. 이 제한 사항은 향후 서비스 릴리스에서 해결됩니다.

몇 가지 잠재적인 해결 방법이 있습니다.

+ 미리 학습된 모델을 설치하는 경우 사용자 지정 위치를 선택합니다.
+ 가능하면 경로가 짧은 사용자 지정 설치 경로(예: C:\SQL\MSSQL14.MSSQLSERVER)에 SQL Server 인스턴스를 설치합니다.
+ Windows 유틸리티 [Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx)을 사용하여 모델 파일을 더 짧은 경로에 매핑하는 하드 링크를 만듭니다.
+ 최신 서비스 릴리스로 업데이트합니다.

### <a name="2-error-when-saving-serialized-model-to-sql-server"></a>2. 직렬화된 모델을 SQL Server에 저장할 때 오류 발생

원격 SQL Server 인스턴스에 모델을 전달하고 [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)에서 `rx_unserialize` 함수를 사용하여 이진 모델을 읽으려고 하면 다음 오류가 발생할 수 있습니다. 

> *NameError: 이름 'rx_unserialize_model'이 정의되지 않았습니다.*

이 오류는 직렬화 함수의 최신 버전을 사용하여 모델을 저장했지만 모델을 역직렬화하는 SQL Server 인스턴스가 직렬화 API를 인식하지 못하는 경우에 발생합니다.

이 문제를 해결하려면 SQL Server 2017 인스턴스를 CU3 이상으로 업그레이드하세요.

### <a name="3-failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>3. varbinary 변수를 초기화하지 못하여 BxlServer에서 오류 발생

`sp_execute_external_script`를 사용하여 SQL Server에서 Python 코드를 실행하고 코드에 varbinary(max), varchar(max) 또는 유사한 형식의 출력 변수가 있는 경우 변수를 초기화하거나 스크립트의 일부로 설정해야 합니다. 그렇지 않으면 데이터 교환 구성 요소인 BxlServer에 오류가 발생하고 작동이 중지됩니다.

이 제한은 예정된 서비스 릴리스에서 해결될 예정입니다. 해결 방법으로 변수가 Python 스크립트 내에서 초기화되었는지 확인합니다. 다음 예와 같이 유효한 값이면 어떤 값도 사용할 수 있습니다.

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

### <a name="4-telemetry-warning-on-successful-execution-of-python-code"></a>4. Python 코드가 성공적으로 실행될 때 원격 분석 경고

SQL Server 2017 CU2부터 Python 코드가 성공적으로 실행되는 경우에도 다음 메시지가 나타날 수 있습니다.

> *외부 스크립트의 STDERR 메시지:* 
>  *~PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: 전역 선언 전에 telemetry_state가 사용됨*

이 문제는 SQL Server 2017 누적 업데이트 3(CU3)에서 해결되었습니다. 

### <a name="5-numeric-decimal-and-money-data-types-not-supported"></a>5. 숫자, 10진수 및 money 데이터 형식이 지원되지 않음

SQL Server 2017 누적 업데이트 12(CU12)부터 `sp_execute_external_script`에서 Python을 사용하는 경우 WITH RESULT SETS의 숫자, 10진수 및 Money 데이터 형식이 지원되지 않습니다. 다음 메시지가 나타날 수 있습니다.

> *[코드: 39004, SQL 상태: S1000]  'sp_execute_external_script'를 실행하는 동안 HRESULT 0x80004004와 함께 'Python' 스크립트 오류가 발생했습니다.*
>
> *[코드: 39019, SQL 상태: S1000]  외부 스크립트 오류가 발생했습니다:*
>
> *SqlSatelliteCall 오류: 출력 스키마에 지원되지 않는 형식이 있습니다. 지원되는 형식: bit, smallint, int, datetime, smallmoney, real 및 float. char, varchar는 부분적으로 지원됩니다.*

이 문제는 SQL Server 2017 누적 업데이트 14(CU14)에서 해결되었습니다.

### <a name="6-bad-interpreter-error-when-installing-python-packages-with-pip-on-linux"></a>6. Linux에서 pip를 사용하여 Python 패키지를 설치할 때 잘못된 인터프리터 오류 

SQL Server 2019에서 **pip**를 사용하려는 경우. 예를 들면 다음과 같습니다.

```bash
/opt/mssql/mlservices/runtime/python/bin/pip -h
```

그러면 다음 오류가 발생합니다.

> *bash: /opt/mssql/mlservices/runtime/python/bin/pip: /opt/microsoft/mlserver/9.4.7/bin/python/python: 잘못된 인터프리터: 지정한 파일이나 디렉터리가 없습니다.*

**해결 방법**

[Python Package Authority(PyPA)](https://www.pypa.io)에서 **pip**를 설치합니다.

```bash
wget 'https://bootstrap.pypa.io/get-pip.py' 
/opt/mssql/mlservices/bin/python/python ./get-pip.py 
```

**권장**

[sqlmlutils로 Python 패키지 설치](../package-management/install-additional-python-packages-on-sql-server.md)를 참조하세요.

**적용 대상:** Linux의 SQL Server 2019

### <a name="7-unable-to-install-python-packages-using-pip-after-installing-sql-server-2019-on-windows"></a>7. Windows에 SQL Server 2019를 설치한 후 pip를 사용하 여 Python 패키지를 설치할 수 없음

Windows에 SQL Server 2019를 설치한 후 DOS 명령줄에서 **pip**를 통해 python 패키지를 설치하려고 하면 실패합니다. 예를 들면 다음과 같습니다.

```bash
pip install quantfolio
```

다음 오류가 반환됩니다.

> *pip는 TLS/SSL이 필요한 위치로 구성되어 있지만 Python의 SSL 모듈을 사용할 수 없습니다.*

이는 Anaconda 패키지와 관련된 문제입니다. 이 문제는 예정된 서비스 릴리스에서 해결될 예정입니다.

**해결 방법**

다음 파일을 복사합니다.

+ `libssl-1_1-x64.dll`
+ `libcrypto-1_1-x64.dll`

다음 폴더에서: <br>
`C:\Program Files\Microsoft SQL Server\MSSSQL15.MSSQLSERVER\PYTHON_SERVICES\Library\bin`

다음 폴더로: <br>
`C:\Program Files\Microsoft SQL Server\MSSSQL15.MSSQLSERVER\PYTHON_SERVICES\DLLs`

그런 다음 새 DOS 명령 셸 프롬프트를 엽니다.

**적용 대상:** Windows의 SQL Server 2019

### <a name="8-error-when-using-sp_execute_external_script-without-libcaboso-on-linux"></a>8. Linux에서 `libc++abo.so` 없이 `sp_execute_external_script`를 사용하는 경우 오류 발생

`libc++abi.so`가 설치되지 않은 클린 Linux 컴퓨터에서 `sp_execute_external_script`(SPEES) 쿼리를 실행하면 "지정한 파일이나 디렉터리가 없습니다" 오류와 함께 실패합니다.

다음은 그 예입니다.

```text
EXEC sp_execute_external_script
    @language = N'Python'
    , @script = N'
OutputDataSet = InputDataSet'
    , @input_data_1 = N'select 1'
    , @input_data_1_name = N'InputDataSet'
    , @output_data_1_name = N'OutputDataSet'
    WITH RESULT SETS (([output] int not null));
Msg 39012, Level 16, State 14, Line 0
Unable to communicate with the runtime for 'Python' script for request id: 94257840-1704-45E8-83D2-2F74AEB46CF7. Please check the requirements of 'Python' runtime.
STDERR message(s) from external script:

Failed to load library /opt/mssql-extensibility/lib/sqlsatellite.so with error libc++abi.so.1: cannot open shared object file: No such file or directory.

SqlSatelliteCall error: Failed to load library /opt/mssql-extensibility/lib/sqlsatellite.so with error libc++abi.so.1: cannot open shared object file: No such file or directory.
STDOUT message(s) from external script:
SqlSatelliteCall function failed. Please see the console output for more information.
Traceback (most recent call last):
  File "/opt/mssql/mlservices/libraries/PythonServer/revoscalepy/computecontext/RxInSqlServer.py", line 605, in rx_sql_satellite_call
    rx_native_call("SqlSatelliteCall", params)
  File "/opt/mssql/mlservices/libraries/PythonServer/revoscalepy/RxSerializable.py", line 375, in rx_native_call
    ret = px_call(functionname, params)
RuntimeError: revoscalepy function failed.
Total execution time: 00:01:00.387
```

**해결 방법**

다음 명령 실행:

```bash
sudo cp /opt/mssql/lib/libc++abi.so.1 /opt/mssql-extensibility/lib/
```

**적용 대상:** Linux의 SQL Server 2019

### <a name="9-cannot-install-tensorflow-package-using-sqlmlutils"></a>9. **sqlmlutils**를 사용하여 **tensorflow** 패키지를 설치할 수 없음

[sqlmlutils 패키지](../package-management/install-additional-python-packages-on-sql-server.md?view=sql-server-ver15)는 SQL Server 2019에 Python 패키지를 설치하는 데 사용됩니다. 그러나 sqlmlutils를 사용하여 **tensorflow** 패키지를 설치할 수는 없습니다. tensorflow 패키지는 SQL Server에 설치된 버전보다 최신 버전의 numpy에 종속됩니다. 그러나 numpy는 미리 설치된 시스템 패키지이기 때문에 sqlmlutils가 tensorflow를 설치할 때 업데이트할 수 없습니다.

**해결 방법**

관리자 모드에서 명령 프롬프트를 사용하여 다음 명령에서 "MSSQLSERVER"를 SQL 인스턴스의 이름으로 바꿔 명령을 실행합니다.

   ```cmd
   "C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES\python.exe" -m pip install --upgrade tensorflow
   ```

   "TLS/SSL" 오류가 발생하는 경우 이 문서의 앞부분에서 [7. pip를 사용하여 Python 패키지를 설치할 수 없음](#7-unable-to-install-python-packages-using-pip-after-installing-sql-server-2019-on-windows)을 참조하세요.

**적용 대상:** Windows의 SQL Server 2019

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise 및 Microsoft R Open

이 섹션에서는 Revolution Analytics에서 제공하는 R 연결, 개발 및 성능 도구와 관련된 문제를 나열합니다. 이러한 도구는 이전 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 시험판 버전에서 제공되었습니다.

일반적으로 이전 버전을 제거하고 최신 버전의 SQL Server R Services 또는 Microsoft R Server를 설치하는 것이 좋습니다.

### <a name="1-revolution-r-enterprise-is-not-supported"></a>1. Revolution R Enterprise가 지원되지 않음

Revolution R Enterprise를 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]의 버전과 함께 설치하는 것은 지원되지 않습니다.

Revolution R Enterprise의 기존 라이선스가 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용할 모든 워크스테이션과 별도의 컴퓨터에 라이선스를 두어야 합니다.

일부 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 시험판 버전에는 Revolution Analytics를 통해 생성된 Windows용 R 개발 환경이 포함되어 있었습니다. 이 도구는 더 이상 제공되지 않으며 지원되지 않습니다.

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]와의 호환성을 위해 Microsoft R Client를 대신 설치하는 것이 좋습니다. [Visual Studio용 R 도구](https://marketplace.visualstudio.com/items?itemName=MikhailArkhipov007.RTVS2019) 및 [Visual Studio Code](https://code.visualstudio.com/)도 Microsoft R 솔루션을 지원합니다.

### <a name="2-compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>2. SQLite ODBC 드라이버와 RevoScaleR의 호환성 문제

SQLite ODBC 드라이버의 수정 버전 0.92는 RevoScaleR와 호환되지 않습니다. 0\.88~0.91 및 0.93 이상 버전은 호환 가능한 것으로 알려져 있습니다.

## <a name="next-steps"></a>다음 단계

[SQL Server의 기계 학습 문제 해결](machine-learning-troubleshooting-overview.md)
