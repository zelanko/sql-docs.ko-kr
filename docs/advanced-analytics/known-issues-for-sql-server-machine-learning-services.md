---
title: "컴퓨터 학습 서비스에 대 한 알려진 문제 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2b37a63a-5ff5-478e-bcc2-d13da3ac241c
caps.latest.revision: 53
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7b9d53a87490e83f888b47b1cff87191b9693a8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="known-issues-for-machine-learning-services"></a>컴퓨터 학습 서비스에 대 한 알려진된 문제

이 항목의 알려진된 문제 또는 제한 기계 학습에서 SQL Server 2016 및 SQL Server 2017 옵션으로 제공 되는 구성 요소를 설명 합니다.

구체적으로 지정 되어 있지 않으면 다음에 적용 됩니다.

+ SQL Server 2016

  - R Services(In-Database)
  - Microsoft R Server(독립 실행형)

+ SQL Server 2017

  - 기계 학습 R (In-database)에 대 한 서비스
  - 기계 학습 Python (In-database)에 대 한 서비스
  - Machine Learning Server(독립 실행형)

## <a name="setup-and-configuration-issues"></a>설치 및 구성 문제

초기 설치 및 구성 관련 된 처리 하 고 일반적인 질문에 대 한 설명을 여기에 나열 됩니다: [업그레이드 및 설치 FAQ](r/upgrade-and-installation-faq-sql-server-r-services.md)합니다.

또한 업그레이드,-나란히 설치 및 새 Python 또는 R 구성 요소를 설치 하는 방법에 대 한 내용은이 문서를 참조 하십시오.

### <a name="unable-to-install-python-components-in-in-offline-installs-of-sql-server-2017"></a>Python 구성 요소에서 SQL Server 2017의 오프 라인 설치에 설치할 수 없습니다.

설치 관리자 다운로드 된 Python 구성 요소;의 위치를 묻는 페이지를 표시 하지 않을 수 있습니다 인터넷 액세스가 없는 컴퓨터에서 SQL Server 2017을 설치 하는 경우 따라서 컴퓨터 학습 서비스 기능을 사용 하지만 Python 구성 요소가 아닌 설치 됩니다.

이 문제는 예정 된 릴리스에서 수정 될 예정입니다. 이 문제를 해결 설치 중에 인터넷 액세스를 일시적으로 사용할 수 있습니다. 오른쪽에 이러한 제한이 적용 되지 않습니다.

**적용 대상:** python 2017 SQL Server

### <a name="install-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>Microsoft R Client와 호환성을 위해 최신 서비스 릴리스 설치

최신 버전의 Microsoft R 클라이언트를 설치 하 고 사용 하 여 R에서 실행 하려면 원격을 사용 하 여 SQL Server 계산 컨텍스트를 다음과 같은 오류가 발생할 수 있습니다.

*Microsoft R 클라이언트의 버전 9.x.x를 실행 하는 Microsoft R Server 버전 8.x.x와 호환 되지 않는 컴퓨터에 있습니다. 호환되는 버전을 다운로드하여 설치하세요.*

SQL Server 2016 R 라이브러리 클라이언트에서 R 라이브러리 서버에는 정확 하 게 일치 해야 합니다. 나중에 R Server 9.0.1 보다 해제 제한에 대 한 제거 된 것입니다. 그러나이 오류가 발생 하면 클라이언트에서의 R 라이브러리 버전을 사용 하 고 nad 필요한 경우 서버 업데이트 서버 버전과 일치 하도록 클라이언트를 확인 합니다.

SQL Server R Services와 함께 설치 되는 R의 버전은 SQL Server 서비스 릴리스가 설치 될 때마다 업데이트 됩니다. 따라서 하면 항상 최신 버전의 R 구성 요소를 갖출 수 있도록 모든 서비스 팩을 설치 해야 합니다.

Microsoft R Client 9.0.0과 호환성을 위해 이 [지원 문서](https://support.microsoft.com/kb/3210262)에 설명된 업데이트를 설치해야 합니다.

R 패키지 문제를 방지 하려면 업그레이드할 수 있습니다에 설명 된 대로 최신 수명 주기 정책을 변경 하 여 서버에 설치 된 R 라이브러리 버전 [이 여기서](#bkmk_sqlbindr)합니다. 이렇게 하면 동일한 일정에 따라 서버와 클라이언트 모두 항상는 최신 버전은 Microsoft R입니다. 확인 되는 Microsoft R Server에 대 한 업데이트가 게시 되는 SQL Server와 함께 설치 된 R 버전 업데이트 됩니다.

**적용 대상:** R server 9.0.0 버전 SQL Server 2016 R Services 또는 이전 버전

### <a name="bkmk_sqlbindr"></a>사용 하 여 클라이언트에서 이전 버전의 SQL Server R Services에 연결할 때 호환 되지 않는 버전의 경고[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 용 설치 마법사 또는 [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)용 새 독립 실행형 설치 관리자를 사용하여 클라이언트 컴퓨터에 Microsoft R Server를 설치했으며 이전 버전의 SQL Server R Services를 사용하는 계산 컨텍스트에서 R 코드를 실행하는 경우 다음과 같은 오류가 표시될 수 있습니다.

*컴퓨터에서 Microsoft R Server 버전 8.0.3과 호환되지 않는 Microsoft R Client 버전 9.0.0을 실행 중입니다. 호환되는 버전을 다운로드하여 설치하세요.*

**SqlBindR.exe** 도구는 호환되는 9.0 버전으로 SQL Server 인스턴스 업그레이드를 지원하기 위해 Microsoft R Server 9.0 릴리스에서 제공됩니다. 9.0으로 R Services 인스턴스 업그레이드 지원은 향후 서비스 릴리스의 일부로 SQL Server에 추가될 예정입니다. 이후 업그레이드 될 버전에는 SQL Server 2016 RTM CU3 + 및 SP1 이상, 및 SQL Server 2017 CTP 1.1 포함 됩니다.

**적용 대상:** R server 9.0.0 버전 SQL Server 2016 R Services 또는 이전 버전

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>SQL Server 2016 서비스 릴리스 설치 프로그램에서 최신 버전의 R 구성 요소를 설치하지 못할 수 있음

인터넷에 연결되지 않은 컴퓨터에 SQL Server 2016용 서비스 팩을 설치하거나 누적 업데이트를 설치하는 경우 다운로드한 CAB 파일을 사용하여 R 구성 요소를 업데이트할 수 있는 프롬프트를 설치 마법사에서 표시하지 못할 수 있습니다. 이 오류는 일반적으로 데이터베이스 엔진과 함께 여러 구성 요소가 설치될 때 발생합니다.

이 문제를 해결 명령줄을 사용 하 고 지정 하 여 서비스 릴리스를 설치할 수는 */MRCACHEDIRECTORY* CU1 업데이트를 설치 하는이 예에 표시 된 대로 인수:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

최신 설치 관리자를 가져오려는 참조 [컴퓨터 학습 구성 요소 설치 인터넷 연결 되지 않은](r/installing-ml-components-without-internet-access.md)합니다.

**적용 대상:** R server 9.0.0 버전 SQL Server 2016 R Services 또는 이전 버전

### <a name="launchpad-services-fails-to-start-if-version-is-different-than-r-version"></a>버전이 R 버전과 다른 경우 실행 패드 서비스가 시작되지 않음

R Services를 별도로 설치 하는 데이터베이스 엔진에서 하는 경우 빌드 버전이 다르면 시스템 이벤트 로그에이 오류가 표시 될 수 있습니다: _SQL Server 실행 패드 서비스 오류로 인해 시작 실패: 서비스 제공 되지 않았습니다 시기 적절 하 게에서 시작 또는 제어 요청에 응답 합니다._

예를 들어 릴리스 버전을 사용하여 데이터베이스 엔진을 설치하고 패치를 적용하여 데이터베이스 엔진을 업그레이드한 다음 릴리스 버전을 사용하여 R Services를 추가하는 경우 이 오류가 발생할 수 있습니다.

이 문제를 방지하려면 모든 구성 요소에 동일한 버전 번호가 있는지 확인합니다. 하나의 구성 요소를 업그레이드하는 경우 설치된 다른 모든 구성 요소에 동일한 업그레이드를 적용해야 합니다.

각 SQL Server 2016 릴리스에 필요한 R 버전 번호 목록을 보려면 [인터넷에 액세스하지 않고 R 구성 요소 설치](r/installing-ml-components-without-internet-access.md)를 참조하세요.

### <a name="remote-compute-contexts-blocked-by-firewall-in-sql-server-instances-running-on-azure-virtual-machines"></a>Azure 가상 컴퓨터에서 실행되는 SQL Server 인스턴스의 방화벽에 의해 차단되는 원격 계산 컨텍스트

Microsoft Azure 가상 컴퓨터에 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 을 설치한 경우 가상 컴퓨터의 작업 영역을 사용해야 하는 계산 컨텍스트를 사용하지 못할 수 있습니다. 이는 기본적으로 Azure VM 방화벽에 로컬 R 사용자 계정에 대한 네트워크 액세스를 차단하는 규칙이 있기 때문입니다.

이 문제를 해결하려면 Azure VM에서 **고급 보안이 포함된 Windows 방화벽**을 열고 **아웃바운드 규칙**을 선택하여 "SQL Server 인스턴스 MSSQLSERVER의 R 로컬 사용자 계정에 대한 네트워크 액세스 차단" 규칙을 사용하지 않도록 설정합니다.

### <a name="implied-authentication-in-sqlexpress"></a>SQLEXPRESS의 암시적 인증

Windows 통합 인증을 사용하여 원격 데이터 과학 워크스테이션에서 R 작업을 실행하는 경우 SQL Server는 *암시적 인증* 을 사용하여 스크립트에 필요할 수 있는 로컬 ODBC 호출을 생성합니다. 그러나 SQL Server Express Edition의 RTM 빌드에서는 이 기능이 작동하지 않았습니다.

이 문제를 해결하려면 이후 서비스 릴리스로 업그레이드하는 것이 좋습니다.

업그레이드할 수 없는 경우 SQL 로그인을 사용하여 포함된 ODBC 호출이 필요할 수 있는 원격 R 작업을 실행할 수 있습니다.

**적용 대상:** SQL Server 2016 R Services Express Edition

### <a name="performance-limits-when-r-libraries-are-called-from-standalone-r-tools"></a>R 라이브러리는 독립 실행형 R 도구에서 호출 하는 경우 성능이 제한

R 도구 및 SQL Server R Services에 대 한 관리자 권한 같은 외부 R 응용 프로그램에서 설치 되는 라이브러리를 호출 하는 것이 불가능 합니다. 새 패키지를 설치 하거나 매우 짧은 코드 예제에서 애드혹 테스트를 실행 하는 경우에 유용할 수 있습니다.

그러나 수는 SQL Server 외부의 성능 제한 됩니다. 예를 들어 SQL Server의 Enterprise Edition을 구매한 경우에 R이 실행 단일 스레드 모드에서 외부 도구를 사용 하 여 R 코드를 실행 합니다. 성능은 SQL Server 연결을 초기화 하 고 사용 하 여 R 코드를 실행 하는 경우에 뛰어난 것 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), R 라이브러리를 대신 호출 됩니다입니다.

+ SQL Server에서 사용하는 R 라이브러리를 외부 R 도구에서 호출하지 마세요.
+ SQL server를 사용 하지 않고 SQL Server 컴퓨터에 광범위 한 R 코드를 실행 해야 할 경우 Microsoft R Client 같이 R의 개별 인스턴스를 설치 하 고 R 개발 도구는 새 라이브러리를 가리키는지 확인 합니다.

자세한 내용은 [독립 실행형 R 서버 만들기](r/create-a-standalone-r-server.md)를 참조하세요.

### <a name="r-script-throttled-due-to-resource-governance-default-values"></a>R 스크립트 리소스 거 버 넌 스 기본값 인해 조정

Enterprise Edition에서 리소스 풀을 사용하여 외부 스크립트 프로세스를 관리할 수 있습니다. 일부 초기 릴리스 빌드에서 R 프로세스에 할당 될 수 있는 최대 메모리는 20%입니다. 따라서 서버에 32GB의 RAM이 있는 경우 R 실행 파일(RTerm.exe 및 BxlServer.exe)은 단일 요청에 최대 6.4GB을 사용할 수 있었습니다.

리소스 제한에 도달할 경우 현재 기본값을 확인하고, 20%가 충분하지 않으면 이 값을 변경하는 방법에 대한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설명서를 참조하세요.

**적용 대상:** SQL Server 2016 R 서비스, Enterprise Edition

## <a name="r-code-execution-and-package-or-function-issues"></a>R 코드 실행 및 패키지 또는 함수 문제

이 섹션에는 R 라이브러리 및 도구 RevoScaleR를 포함 하 여 Microsoft에서 게시와 관련 된 몇 가지 문제 뿐 아니라 SQL Server에서 R을 실행 하는 관련 된 알려진된 문제가 포함 되어 있습니다.

Microsoft R Server 사이트를 참조 하는 R 솔루션에 영향을 줄 수 있는 기타 알려진된 문제에 대 한: [Microsoft R server 알려진 문제](https://msdn.microsoft.com/microsoft-r/rserver-known-issues)

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>R 작업에 대한 프로세서 선호도 제한

SQL Server 2016의 초기 릴리스 빌드에서 Cpu 첫 번째 k 그룹에서에 대 한 프로세서 선호도 설정할 수 있습니다. 예를 들어 서버가 2개의 k 그룹이 있는 2 소켓 시스템인 경우 첫 번째 k 그룹의 프로세서만 R 프로세스에 사용됩니다. R 스크립트 작업에 대한 리소스 관리를 구성하는 경우 동일한 제한이 적용됩니다.

이 문제는 SQL Server 2016 서비스 팩 1에서 해결되었습니다.

**적용 대상:** SQL Server 2016 R 서비스 RTM 버전

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>SQL Server 계산 컨텍스트에서 데이터를 읽는 경우 열 형식을 변경할 수 없음

계산 컨텍스트가 SQL Server 인스턴스로 설정된 경우 _colClasses_ 인수(또는 다른 유사한 인수)를 사용하여 R 코드에서 열의 데이터 형식을 변경할 수 없습니다.

예를 들어 CRSDepTimeStr 열이 정수가 아닌 경우 다음 문에서 오류가 발생합니다.

~~~~
data <- RxSqlServerData(sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall",
                                connectionString = connectionString,
                                colClasses = c(CRSDepTimeStr = "integer"))
~~~~

이 문제는 향후 릴리스에서 해결될 예정입니다.

해결 방법으로, CAST 또는 CONVERT를 사용하고 올바른 데이터 형식으로 R에 데이터를 제공하도록 SQL 쿼리를 다시 작성할 수 있습니다. 일반적으로 R 코드에서 데이터를 변경하는 대신 SQL을 사용하여 데이터 작업을 하는 것이 성능에 더 좋습니다.

**적용 대상:** SQL Server 2016 R Services

### <a name="avoid-clearing-workspaces-when-executing-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 계산 컨텍스트에서 R 코드를 실행하는 경우에는 작업 영역을 지우지 마세요.

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 계산 컨텍스트에서 R 코드를 실행하는 동안 R 명령을 사용하여 작업 영역에서 개체를 지우거나 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 호출된 R 스크립트의 일부로 작업 영역을 지우는 경우 다음 오류가 발생할 수 있습니다. *작업 영역 개체 'revoScriptConnection'을 찾을 수 없습니다.*

`revoScriptConnection` 은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 호출된 R 세션에 대한 정보를 포함하는 R 작업 영역의 개체입니다. 그러나 R 코드에 작업 영역을 지우는 명령(예: `rm(list=ls()))`)이 포함되어 있으면 세션 및 R 작업 영역의 다른 개체에 대한 모든 정보도 지워집니다.

해결 방법으로, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 R을 실행하는 동안에는 변수 및 기타 개체를 무차별 지우지 마세요. R 콘솔에서 작업할 때 작업 영역을 지우는 것은 일반적이지만 의도하지 않은 결과가 발생할 수 있습니다.

+ 특정 변수를 삭제하려면 R *remove* 함수를 사용합니다. `remove('name1', 'name2', ...)`
+ 삭제할 변수가 여러 개인 경우 임시 변수 이름을 목록에 저장하고 주기적 가비지 수집을 수행합니다.

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>R 스크립트의 입력으로 제공될 수 있는 데이터에 대한 제한

R 스크립트에서는 다음 유형의 쿼리 결과를 사용할 수 없습니다.

- AlwaysEncrypted 열을 참조하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리의 데이터
  
- 마스킹된 열을 참조하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리의 데이터
  
     R 스크립트에서 마스킹된 데이터를 사용해야 하는 경우 가능한 해결 방법은 임시 테이블에 데이터 복사본을 만들고 해당 데이터를 대신 사용하는 것입니다.

### <a name="arguments-varstokeep-and-varstodrop-not-supported-for-sql-server-data-sources"></a>인수 *varsToKeep* 및 *varsToDrop* SQL Server 데이터 원본에 대해 지원 되지 않습니다

RxDataStep 함수를 사용 하 여 테이블에 결과 쓸 때 사용 하는 *varsToKeep* 및 *varsToDrop* 포함 하거나 제외할 작업의 일부로 열을 지정 하는 편리한 방법입니다. 현재,이 인수는 SQL Server 데이터 원본에 대해 지원 되지 않습니다.

이 제한 사항은 이후 릴리스에서 제거 됩니다.

### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>SQL 데이터 형식에 대 한 제한 된 지원`sp_execute_external_script`

SQL에서 지원되는 일부 데이터 형식은 R에서 사용할 수 없습니다. 해결 방법으로, sp_execute_external_script에 데이터를 전달하기 전에 지원되지 않는 데이터 형식을 지원되는 데이터 형식으로 캐스팅하는 것이 좋습니다.

자세한 내용은 참조 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)합니다.

### <a name="possible-string-corruption"></a>가능한 문자열 손상

[!INCLUDE[tsql](../includes/tsql-md.md)] 에서 R로 이동한 다음 다시 [!INCLUDE[tsql](../includes/tsql-md.md)] 로 이동하는 문자열 데이터의 왕복은 손상을 일으킬 수 있습니다. 이는 R과 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 사용되는 인코딩이 서로 다르고, R과 [!INCLUDE[tsql](../includes/tsql-md.md)]에서 지원되는 데이터 정렬 및 언어가 서로 다르기 때문입니다. ASCII가 아닌 인코딩의 모든 문자열은 잠재적으로 잘못 처리될 수 있습니다.

문자열 데이터를 R로 보낼 때 가능하면 ASCII 표현으로 변환하세요.

### <a name="only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>형식의 값을 하나만 `raw` 에서 반환 될 수`sp_execute_external_script`

R에서 이진 데이터 형식(R **raw** 데이터 형식)이 반환되는 경우 값은 출력 데이터 프레임의 값이어야 합니다.

후속 릴리스에서는 여러 **raw** 출력에 대한 지원이 추가될 예정입니다.

여러 출력 집합이 필요한 경우 한 가지 가능한 해결 방안은 저장 프로시저를 여러 번 호출하고 ODBC를 사용하여 결과 집합을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로 다시 보내는 것입니다.

OUTPUT 키워드를 추가하여 저장 프로시저의 결과와 함께 매개 변수 값을 반환할 수 있습니다. 자세한 내용은 [OUTPUT 매개 변수를 사용하여 데이터 반환](https://technet.microsoft.com/library/ms187004.aspx)을 참조하세요.

### <a name="loss-of-precision"></a>정밀도 손실

[!INCLUDE[tsql](../includes/tsql-md.md)] 과 R은 서로 다른 데이터 형식을 지원하므로 숫자 데이터 형식의 경우 변환하는 동안 정밀도가 떨어질 수 있습니다.

암시적 데이터 형식 변환에 대한 자세한 내용은 [Working with R Data Types](r/r-libraries-and-data-types.md)을 참조하십시오.

### <a name="variable-scoping-error-the-sample-data-set-for-the-analysis-has-no-variables-when-using-the-transformfunc-parameter"></a>transformFunc 매개 변수를 사용할 때 "분석할 샘플 데이터 집합에 변수가 없습니다"라는 변수 범위 지정 오류가 발생함

*rxLinmod* 또는 `rxLinmod` 와 같은 함수에서 `rxLogit` to transf와 같은 함수에서m the data while modelling. 그러나 중첩된 함수 호출은 로컬 계산 컨텍스트에서 올바르게 작동하는 경우에도 SQL Server 계산 컨텍스트에서 범위 지정 오류를 일으킬 수 있습니다.

예를 들어 로컬 글로벌 환경에서 두 개의 함수 `f` 와 `g` 를 정의했으며 `g` 가 `f`를 호출한다고 가정해 보겠습니다. `g`가 포함된 분산 또는 원격 호출에서는 `g` 와 `f` 를 원격 호출로 전달한 경우에도 `f` 를 찾을 수 없으므로 `g` 에 대한 호출에 실패할 수 있습니다.

이 문제가 발생한 경우 `f` 의 정의를 `g`의 정의 내에 포함하여 문제를 해결할 수 있습니다. `g` 앞의 모든 곳에서 `f`를 정상적으로 호출합니다.

예를 들어

```  
f <- function(x) { 2*x + 3 }  
g <- function(y) {   
              a <- 10 * y  
               f(a)  
}  
  
```  


이 오류를 방지 하려면 다음과 같이 다시 작성:

```  
g <- function(y){  
              f <- function(x) { 2*x +3}  
              a <- 10 * y  
              f(a)  
}  
  
```  

### <a name="data-import-and-manipulation-using-revoscaler"></a>RevoScaleR을 사용하여 데이터 가져오기 및 조작

데이터베이스에서 **varchar** 열을 읽는 경우 공백이 잘립니다. 이를 방지하려면 공백이 아닌 문자로 문자열을 묶습니다.

`rxDataStep` 과 같은 함수를 사용하여 **varchar** 열이 포함된 데이터베이스 테이블을 만드는 경우 열 너비는 데이터의 샘플을 기반으로 예상됩니다. 너비가 달라질 수 있는 경우 모든 문자열을 열 길이에 패딩해야 할 수 있습니다.

`rxImport` 또는 `rxTextToXdf` 에 대한 반복된 호출을 사용하여 행을 가져오고 추가하면서 여러 입력 파일을 단일.xdf 파일에 통합하는 경우 변환을 사용하여 변수의 데이터 형식을 변경할 수 없습니다.

### <a name="limited-support-for-rxexec"></a>RxExec에 대 한 제한 된 지원

SQL Server 2016에서의 `rxExec` RevoScaleR 패키지에서 제공 하는 함수를 단일 스레드 모드에만 사용할 수 있습니다.

여러 프로세스에 걸친 `rxExec` 병렬 처리는 곧 출시될 릴리스에 추가될 예정입니다.

### <a name="increase-maximum-parameter-size-to-support-rxgetvarinfo"></a>rxGetVarInfo를 지원하도록 최대 매개 변수 크기 늘리기

매우 많은 변수(예: 40,000개)가 있는 데이터 집합을 사용하는 경우 `max-ppsize` 와 같은 함수를 사용하려면 R을 시작할 때 `rxGetVarInfo`플래그를 설정해야 합니다.  `max-ppsize` 플래그는 포인터 보호 스택의 최대 크기를 지정합니다.

rgui.exe 또는 rterm.exe 등에서 R 콘솔을 사용하는 경우 다음을 입력하여 max-ppsize 값을 500000으로 설정할 수 있습니다.

```  
R --max-ppsize=500000  
```  
  
[!INCLUDE[rsql_developr](../includes/rsql-developr-md.md)] 환경을 사용하는 경우 RevoIDE 실행 파일을 호출하여 `max-ppsize` 플래그를 설정할 수 있습니다.

```  
RevoIDE.exe /RCommandLine --max-ppsize=500000  
```  

### <a name="issues-with-the-rxdtree-function"></a>RxDTree 함수 문제

`rxDTree` 함수는 현재 수식 내 변환을 지원하지 않습니다. 특히 즉석에서 요소를 만들기 위해 `F()` 구문을 사용하는 것은 지원되지 않습니다. 그러나 숫자 데이터는 자동으로 범주화됩니다.

순서가 지정된 요소는 `rxDTree`를 제외하고 모든 RevoScaleR 분석 함수의 요소와 동일하게 처리됩니다.

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise 및 Microsoft R Open

이 섹션에서는 Revolution Analytics에서 제공하는 R 연결, 개발 및 성능 도구와 관련된 문제를 보여 줍니다. 이러한 도구는 이전  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]시험판 버전에서 제공되었습니다. 

일반적으로 이러한 이전 버전을 제거 하 고 최신 버전의 SQL Server 또는 Microsoft R Server를 설치 하는 것이 좋습니다.

### <a name="running-side-by-side-versions-of-revolution-r-enterprise"></a>Revolution R Enterprise의 병렬 버전 실행

Revolution R Enterprise를 [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] 버전과 함께 설치하는 것은 지원되지 않습니다.

다른 버전의 Revolution R Enterprise를 사용할 라이선스가 있는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용할 모든 워크스테이션과 별도의 컴퓨터에 라이선스를 두어야 합니다.

### <a name="use-of-r-productivity-environment-not-supported"></a>지원 되지 않습니다 R 생산성 환경 사용

일부 [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] 시험판 버전에는 Revolution Analytics를 통해 생성된 Windows용 R 개발 환경이 포함되어 있었습니다. 이 도구는 더 이상 제공 되지 않으며 지원 되지 않습니다.

호환성을 위해 [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], Microsoft R Client 또는 Microsoft R Server Revolution Analytics 도구를 대신 설치 하는 것이 좋습니다. [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/) 는 Microsoft R 솔루션을 지원하는 다른 권장 클라이언트입니다.

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>SQLite ODBC 드라이버와 RevoScaleR의 호환성 문제

SQLite ODBC 드라이버의 수정 버전 0.92는 RevoScaleR과 호환되지 않습니다. 수정 버전 0.88~0.91 및 0.93 이상은 호환됩니다.

## <a name="see-also"></a>참고 항목

[SQL Server 2016의 새로운 기능](../sql-server/what-s-new-in-sql-server-2016.md)


