---
title: "컴퓨터 학습 서비스의 알려진 문제 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/19/2017
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
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 2d21756a05e9e51379faa194ec331517e510988d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/21/2017

---
# <a name="known-issues-in-machine-learning-services"></a>컴퓨터 학습 서비스의 알려진된 문제

이 문서에서는 기계 학습에서 SQL Server 2016 및 SQL Server 2017 옵션으로 제공 되는 구성 요소와 알려진된 문제 또는 제한을 설명 합니다.

구체적으로 지정 되어 있지 않으면 여기 정보는 다음의 모든 적용 됩니다.

* SQL Server 2016

  - R Services(In-Database)
  - Microsoft R Server(독립 실행형)

* SQL Server 2017

  - 기계 학습 R (In-database)에 대 한 서비스
  - 기계 학습 Python (In-database)에 대 한 서비스
  - Machine Learning Server(독립 실행형)

## <a name="setup-and-configuration-issues"></a>설치 및 구성 문제

참조에 대 한 프로세스와 관련 된 초기 설치 및 구성과 관련 된 일반적인 질문 설명은 [업그레이드 및 설치 FAQ](r/upgrade-and-installation-faq-sql-server-r-services.md)합니다. 업그레이드,-나란히 설치 및 새 Python 또는 R 구성 요소를 설치 하는 방법에 대 한 정보를 포함 합니다.

### <a name="unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>SQL Server 2017 CTP 2.0 이상 오프 라인 설치에서 Python 구성 요소를 설치할 수 없습니다.

인터넷 액세스가 없는 컴퓨터에서 SQL Server 2017의 시험판 버전을 설치 하는 경우 설치 관리자 다운로드 된 Python 구성 요소 위치를 묻는 페이지를 표시 하려면 실패할 수 있습니다. 이러한 상황에서 컴퓨터 학습 서비스 기능을 사용 하지만 Python 구성 요소가 아닌를 설치할 수 있습니다.

릴리스 버전에서이 문제는 해결 됩니다. 에 대 한 해결책으로이 문제를 발생 하는 경우 설치 프로그램의 기간에 대 한 인터넷 액세스를 일시적으로 사용할 수 있습니다. 오른쪽에 이러한 제한이 적용 되지 않습니다.

**적용 대상:** python 2017 SQL Server

### <a name="install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>Microsoft R 클라이언트와의 호환성을 위해 최신 서비스 릴리스를 설치 합니다.

Microsoft R Client의 최신 버전을 설치 하 고 사용 하 여 원격 계산 컨텍스트에서 R SQL Server에서 실행 되도록 하는 경우에 다음과 같은 오류가 발생할 수 있습니다.

>*Microsoft R Client의 9.x.x 버전을 실행 하는 Microsoft R Server 버전 8.x.x와 호환 되지 않는 컴퓨터에 있습니다. 호환되는 버전을 다운로드하여 설치하세요.*

SQL Server 2016 R 라이브러리 클라이언트에서 R 라이브러리 서버에는 정확 하 게 일치 해야 합니다. 제한 나중에 R Server 9.0.1 보다 제거 릴리스 되었습니다. 그러나이 오류가 발생 하면 클라이언트와 서버에서 사용 되 고, 필요한 경우 서버 버전 일치 하도록 클라이언트를 업데이트 하는 R 라이브러리 버전을 확인 합니다.

SQL Server R Services와 함께 설치 되는 R의 버전은 SQL Server 서비스 릴리스가 설치 될 때마다 업데이트 됩니다. 하면 항상 최신 버전의 R 구성 요소를 갖출 수 있도록 모든 서비스 팩을 설치 해야 합니다.

Microsoft R 9.0.0 클라이언트와의 호환성을 보장 하려면이 설명 하는 업데이트를 설치 [지원 문서](https://support.microsoft.com/kb/3210262)합니다.

R 패키지 문제를 방지 하려면 업그레이드할 수 있습니다에 설명 된 최신 수명 주기 정책을 변경 하 여 서버에 설치 된 R 라이브러리 버전 [절로](#bkmk_sqlbindr)합니다. 이렇게 하면 SQL Server와 함께 설치 되는 R의 버전 업데이트 됩니다 동일한 일정에 따라 서버와 클라이언트 모두 항상 있다고 Microsoft 오른쪽의 최신 릴리스를 사용 하면 Microsoft R Server에 대 한 업데이트가 게시 되는

**적용 대상:** R server 9.0.0 버전 SQL Server 2016 R Services 또는 이전 버전

### <a name="bkmk_sqlbindr"></a>사용 하 여 클라이언트는 이전 버전의 SQL Server R Services에 연결 하는 경우 호환 되지 않는 버전의 경고[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

SQL Server 2016 계산 컨텍스트에서 R 코드를 실행할 고 때는 다음과 같은 두 개의 문이 true 인 경우 다음과 같은 오류가 표시 될 수 있습니다.
* 설치 마법사를 사용 하 여 클라이언트 컴퓨터에 R Server (독립 실행형) 설치 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]합니다.
* Microsoft R Server를 사용 하 여 설치한는 [Windows installer 구분](https://docs.microsoft.com/r-server/install/r-server-install-windows)합니다.

>*컴퓨터에서 Microsoft R Server 버전 8.0.3과 호환되지 않는 Microsoft R Client 버전 9.0.0을 실행 중입니다. 호환되는 버전을 다운로드하여 설치하세요.*

사용할 수 있습니다 _바인딩_ Microsoft R Server 9.0 및 이상 버전에서 SQL Server 2016 인스턴스 R 구성 요소를 업그레이드 합니다. 여부를 확인 하려면 R 서비스 버전 참조에 대 한 업그레이드를 사용할 수에 대 한 지원이 [SqlBindR.exe를 사용 하 여 R 서비스의 인스턴스를 업그레이드](/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

**적용 대상:** R server 9.0.0 버전 SQL Server 2016 R Services 또는 이전 버전

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>SQL Server 2016 서비스 릴리스 설치 프로그램에서 최신 버전의 R 구성 요소를 설치하지 못할 수 있음

누적 업데이트를 설치 하거나 인터넷에 연결 되어 있지 않은 컴퓨터에서 SQL Server 2016 용 서비스 팩을 설치할 때 설치 마법사는 다운로드 한 CAB 파일을 사용 하 여 R 구성 요소를 업데이트할 수 있는 프롬프트를 표시 하려면 실패할 수 있습니다. 이 오류는 일반적으로 여러 구성 요소는 데이터베이스 엔진와 함께 설치 된 경우에 발생 합니다.

이 문제를 해결 명령줄을 사용 하 고 지정 하 여 서비스 릴리스를 설치할 수는 */MRCACHEDIRECTORY* CU1 업데이트를 설치 하는이 예에 표시 된 대로 인수:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

최신 설치 관리자를 가져오려는 참조 [인터넷 연결 되지 않은 컴퓨터 학습 구성 요소를 설치](r/installing-ml-components-without-internet-access.md)합니다.

**적용 대상:** R server 9.0.0 버전 SQL Server 2016 R Services 또는 이전 버전

### <a name="launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>실행 패드 서비스 버전 R 버전 간에 차이가 있는 경우 시작 되지 않습니다.

SQL Server R Services를 별도로 설치 하는 데이터베이스 엔진에서 하는 경우 빌드 버전이 다르면 시스템 이벤트 로그에서 다음 오류가 표시 될 수 있습니다.

>_SQL Server 실행 패드 서비스 오류로 인해 시작 실패: 서비스가 시기 적절 하 게에서 시작 또는 제어 요청에 응답 하지 않았습니다._

예를 들어이 오류 수 릴리스 버전을 사용 하 여 데이터베이스 엔진을 설치 하는 경우에 발생할 데이터베이스 엔진 업그레이드 패치를 적용 및 다음 릴리스 버전을 사용 하 여 R Services 기능을 추가 합니다.

이 문제를 방지하려면 모든 구성 요소에 동일한 버전 번호가 있는지 확인합니다. 하나의 구성 요소를 업그레이드하는 경우 설치된 다른 모든 구성 요소에 동일한 업그레이드를 적용해야 합니다.

SQL Server 2016의 각 릴리스에 대 한 필요한 R 버전 번호의 목록을 보려면 참조 [설치 R components without](r/installing-ml-components-without-internet-access.md)합니다.

### <a name="remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>원격 계산 컨텍스트는 Azure 가상 컴퓨터에서 실행 되는 SQL Server 인스턴스에서 방화벽으로 차단

설치한 경우 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Windows Azure 가상 컴퓨터에서 있습니다 못할 가상 컴퓨터의 작업 영역을 사용 해야 하는 계산 컨텍스트를 사용 하도록 합니다. 기본적으로 Azure 가상 컴퓨터에서 방화벽에 네트워크 로컬 R 사용자 계정에 대 한 액세스를 차단 하는 규칙 위해서입니다.

문제를 해결 하려면 Azure VM에서 열고 **고급 보안이 포함 된 Windows 방화벽**선택, **아웃 바운드 규칙**, 다음 규칙을 사용 하지 않도록 설정 하 고: **R 로컬 사용자 계정에 대 한 네트워크 액세스 차단 SQL Server 인스턴스 MSSQLSERVER**합니다. 또한 활성화 규칙을 그대로 유지 하 있지만 보안 속성을 변경할 수 있습니다 **보안 연결만 허용**합니다.

### <a name="implied-authentication-in-sqlexpress"></a>SQLEXPRESS의 암시적 인증

Windows 통합 인증을 사용 하 여 원격 데이터 과학 워크스테이션에서 R 작업을 실행 하면 SQL Server 사용 *암시 된 인증이* 를 스크립트에 의해 필요할 수 있는 모든 로컬 ODBC 호출을 생성 합니다. 그러나 SQL Server Express Edition의 RTM 빌드에서는 이 기능이 작동하지 않았습니다.

이 문제를 해결하려면 이후 서비스 릴리스로 업그레이드하는 것이 좋습니다.

업그레이드할 수 없는 경우 SQL 로그인을 사용하여 포함된 ODBC 호출이 필요할 수 있는 원격 R 작업을 실행할 수 있습니다.

**적용 대상:** SQL Server 2016 R Services Express Edition

### <a name="performance-limits-when-r-libraries-are-called-from-other-r-tools"></a>R 라이브러리는 기타 R 도구에서 호출 하는 경우 성능이 제한

R 도구 및 SQL Server에 대 한 관리자 권한 같은 외부 R 응용 프로그램에서 설치 되는 라이브러리를 호출 하는 것이 불가능 합니다. 새 패키지를 설치할 때 또는 매우 짧은 코드 예제에서 애드혹 테스트를 실행할 때이 호출 유용할 수 있습니다.

그러나 수는 SQL Server 외부의 성능이 제한 될 수 있습니다. 예를 들어 SQL Server의 Enterprise Edition을 구매한 경우에 외부 도구를 사용 하 여 R 코드를 실행 하는 경우 단일 스레드 모드에서 R 실행 합니다. 성능이 SQL Server 연결을 초기화 하 고 사용 하 여 R 코드를 실행 하는 경우 더 나은 해야 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), R 라이브러리를 호출 하는 합니다.

* R tools 외부에서 SQL Server에서 사용 되는 R 라이브러리를 호출 하지 마십시오.
* SQL Server를 사용 하지 않고 SQL Server 컴퓨터에 광범위 한 R 코드를 실행 해야 하는 경우 R Microsoft R Client 등의 개별 인스턴스를 설치 하 고 R 개발 도구는 새 라이브러리를 가리키는지 확인 합니다.

자세한 내용은 [독립 실행형 R 서버 만들기](r/create-a-standalone-r-server.md)를 참조하세요.

### <a name="the-r-script-is-throttled-due-to-resource-governance-default-values"></a>R 스크립트는 리소스 거 버 넌 스 기본값 인해 조정

Enterprise Edition에서 리소스 풀을 사용하여 외부 스크립트 프로세스를 관리할 수 있습니다. 일부 초기 릴리스 빌드에서 R 프로세스에 할당 될 수 있는 최대 메모리는 20% 였습니다. 따라서 서버에 32GB의 RAM이 있으면 R 실행 파일 (예: RTerm.exe, BxlServer.exe) 단일 요청에서 6.4 g B의 최대는 사용할 수 있습니다.

리소스 제한이 발생 하면 현재 기본값을 확인 합니다. 20% 충분 없는 경우에 대 한 설명서를 참조 하십시오. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이 값을 변경 하는 방법에 있습니다.

**적용 대상:** SQL Server 2016 R 서비스, Enterprise Edition

## <a name="r-code-execution-and-package-or-function-issues"></a>R 코드 실행 및 패키지 또는 함수 문제

이 섹션에는 RevoScaleR를 포함 하 여 Microsoft에서 게시 하는 도구 및 R 라이브러리에 관련 된 몇 가지 문제 뿐 아니라 SQL Server에서 R을 실행 하는 관련 된 알려진된 문제가 포함 되어 있습니다.

R 솔루션에 영향을 줄 수 있는 기타 알려진된 문제에 대해 알아보려면는 [Microsoft R Server 사이트](https://msdn.microsoft.com/microsoft-r/rserver-known-issues)합니다.

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>R 작업에 대한 프로세서 선호도 제한

SQL Server 2016의 초기 릴리스 빌드에서 Cpu 첫 번째 k 그룹에서에 대 한 프로세서 선호도 설정할 수 있습니다. 예를 들어 서버 k 그룹이 두 개 듀얼 소켓 시스템인 경우 첫 번째 k 그룹에서에 프로세서 R 프로세스에 사용 됩니다. R 스크립트 작업에 대 한 리소스 관리를 구성 하는 경우 동일한 제한에 적용 됩니다.

이 문제는 SQL Server 2016 서비스 팩 1에서 해결되었습니다. 최신 서비스 릴리스로 업그레이드 하는 것이 좋습니다.

**적용 대상:** SQL Server 2016 R 서비스 RTM 버전

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>SQL Server 계산 컨텍스트에서 데이터를 읽는 경우 열 형식을 변경할 수 없음

계산 컨텍스트가 SQL Server 인스턴스로 설정된 경우 _colClasses_ 인수(또는 다른 유사한 인수)를 사용하여 R 코드에서 열의 데이터 형식을 변경할 수 없습니다.

예를 들어 CRSDepTimeStr 열이 정수가 아닌 경우 다음 문에서 오류가 발생합니다.

```r
data <- RxSqlServerData(sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall",
                                connectionString = connectionString,
                                colClasses = c(CRSDepTimeStr = "integer"))
```

이 문제를 해결 캐스트를 사용 하려면 SQL 쿼리를 다시 작성할 수 또는 변환 하 고 R에 올바른 데이터 형식을 사용 하 여 데이터를 제공 합니다. 일반적으로 성능이 더 좋아집니다 작업할 때는 데이터 R 코드의 데이터를 변경 하지 않고 SQL을 사용 하 여 합니다.

**적용 대상:** SQL Server 2016 R Services

### <a name="avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>R 코드를 실행 하는 경우 작업 영역을 선택 취소 하지 마십시오.는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 계산 컨텍스트

R 명령을 사용 하 여 개체의 작업 영역에서 R 코드를 실행 하는 동안 선택을 취소 하는 경우는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 계산 컨텍스트를 사용 하 여 호출 하거나 R 스크립트의 일환으로 작업 영역을 선택 취소 하는 경우 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md),이 표시 될 수 있습니다 오류: 

>*작업 영역 개체 'revoScriptConnection' 찾을 수 없습니다*

`revoScriptConnection` 은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 호출된 R 세션에 대한 정보를 포함하는 R 작업 영역의 개체입니다. 그러나 R 코드에 작업 영역을 지우는 명령(예: `rm(list=ls()))`)이 포함되어 있으면 세션 및 R 작업 영역의 다른 개체에 대한 모든 정보도 지워집니다.

R을 실행 하는 동안 문제를 해결 변수 및 기타 개체를 무분별 하 게 삭제를 방지 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]합니다. 가질 수 있습니다는 R 콘솔에서 작업할 때 작업 영역을 선택 취소 하는 것은 일반적인, 있지만 의도 하지 않은 결과입니다.

* 특정 변수를 삭제 하려면 R을 사용 하 여 *제거* 함수: `remove('name1', 'name2', ...)`합니다.
* 삭제할 변수가 여러 개인 경우 임시 변수 이름을 목록에 저장하고 주기적 가비지 수집을 수행합니다.

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>R 스크립트의 입력으로 제공될 수 있는 데이터에 대한 제한

R 스크립트에서는 다음 유형의 쿼리 결과를 사용할 수 없습니다.

- AlwaysEncrypted 열을 참조하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리의 데이터
  
- 마스킹된 열을 참조하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리의 데이터
  
     R 스크립트에서 마스킹된 데이터를 사용해야 하는 경우 가능한 해결 방법은 임시 테이블에 데이터 복사본을 만들고 해당 데이터를 대신 사용하는 것입니다.

### <a name="arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>인수 *varsToKeep* 및 *varsToDrop* SQL Server 데이터 원본에 대해 지원 되지 않습니다

RxDataStep 함수를 사용 하 여 테이블에 결과 쓸 때 사용 하는 *varsToKeep* 및 *varsToDrop* 포함 하거나 제외할 작업의 일부로 열을 지정 하는 편리한 방법입니다. 그러나 이러한 인수는 SQL Server 데이터 원본에 대해 지원 되지 않습니다.

### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>SQL 데이터 형식에 대 한 제한 된 지원`sp_execute_external_script`

SQL에서 지원되는 일부 데이터 형식은 R에서 사용할 수 없습니다. 해결 방법으로, sp_execute_external_script에 데이터를 전달하기 전에 지원되지 않는 데이터 형식을 지원되는 데이터 형식으로 캐스팅하는 것이 좋습니다.

자세한 내용은 참조 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)합니다.

### <a name="possible-string-corruption"></a>가능한 문자열 손상

문자열 데이터의 모든 왕복 [!INCLUDE[tsql](../includes/tsql-md.md)] R로 이동한 다음를 [!INCLUDE[tsql](../includes/tsql-md.md)] 다시 손상 될 수 있습니다. 이 R에서 사용 되는 인코딩이 서로 다르고 인해 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], 다양 한 데이터 정렬 및 R에서 지원 되는 언어 및 [!INCLUDE[tsql](../includes/tsql-md.md)]합니다. ASCII가 아닌 인코딩의 모든 문자열은 잠재적으로 잘못 처리될 수 있습니다.

R에 문자열 데이터를 보낼 때 ASCII 표현으로 가능 하면 변환 합니다.

이러한 제한도 SQL Server와 Python 간에 전달 되는 데이터에 적용 됩니다. 멀티 바이트 문자를 u t F-8로 전달 하 고 유니코드로 저장 해야 합니다.

### <a name="only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>형식의 값을 하나만 `raw` 에서 반환 될 수`sp_execute_external_script`

경우는 binary 데이터 형식 (R **원시** 데이터 형식)의 값을 출력 데이터 프레임에서 전송 해야 R에서 반환 됩니다.

데이터 형식 사용 이외의 **원시**, OUTPUT 키워드를 추가 하 여 저장된 프로시저의 결과 함께 매개 변수 값을 반환할 수 있습니다. 자세한 내용은 참조 [출력 매개 변수를 사용 하 여 데이터를 반환할](https://technet.microsoft.com/library/ms187004.aspx)합니다.

형식의 값을 포함 하는 여러 출력 집합이 사용 하려는 경우 **원시**, 한 가지 가능한 해결 방안은 저장된 프로시저를 여러 번 호출 하거나 결과 보내려고 다시 원래 대로 설정 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ODBC를 사용 하 여 합니다.

### <a name="loss-of-precision"></a>정밀도 손실

때문에 [!INCLUDE[tsql](../includes/tsql-md.md)] R 다양 한 데이터 형식을 지원 하 고, 숫자 데이터 형식 변환 하는 동안 정밀도의 손실 저하 될 수 있습니다.

암시적 데이터 형식 변환에 대 한 자세한 내용은 참조 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)합니다.

### <a name="variable-scoping-error-when-you-use-the-transformfunc-parameter-the-sample-data-set-for-the-analysis-has-no-variables"></a>변수 범위 지정 오류가 transformFunc 매개 변수를 사용 하는 경우: *분석에 대 한 샘플 데이터 집합에 변수가 없습니다*

데이터를 모델링 하는 동안 변형 하려면 전달할 수 있습니다는 *transformFunc* 와 같은 함수에 인수 `rxLinmod` 또는 `rxLogit`합니다. 그러나 중첩 된 함수 호출은 호출 하 여 로컬 계산 컨텍스트에서 올바르게 작동 하는 경우에 범위 지정 오류는 SQL Server 계산 컨텍스트를 발생할 수 있습니다.

예를 들어 두 개의 함수를 정의 했다고 가정 `f` 및 `g`, 로컬 글로벌 환경에서 및 `g` 호출 `f`합니다. `g`가 포함된 분산 또는 원격 호출에서는 `g` 와 `f` 를 원격 호출로 전달한 경우에도 `f` 를 찾을 수 없으므로 `g` 에 대한 호출에 실패할 수 있습니다.

이 문제가 발생한 경우 `f` 의 정의를 `g`의 정의 내에 포함하여 문제를 해결할 수 있습니다. `g` 앞의 모든 곳에서 `f`를 정상적으로 호출합니다.

예를 들어

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

rgui.exe 또는 rterm.exe 등에서 R 콘솔을 사용하는 경우 다음을 입력하여 max-ppsize 값을 500000으로 설정할 수 있습니다.

```r
R --max-ppsize=500000
```

사용 하는 경우는 [!INCLUDE[rsql_developr](../includes/rsql-developr-md.md)] 환경을 설정할 수 있습니다는 `max-ppsize` RevoIDE 실행 파일에 다음 호출 하 여 플래그:

```
RevoIDE.exe /RCommandLine --max-ppsize=500000  
```

### <a name="issues-with-the-rxdtree-function"></a>RxDTree 함수 문제

`rxDTree` 함수는 현재 수식 내 변환을 지원하지 않습니다. 특히 즉석에서 요소를 만들기 위해 `F()` 구문을 사용하는 것은 지원되지 않습니다. 그러나 숫자 데이터는 자동으로 범주화 됩니다.

순서가 지정된 요소는 `rxDTree`를 제외하고 모든 RevoScaleR 분석 함수의 요소와 동일하게 처리됩니다.

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise 및 Microsoft R Open

이 섹션은 R 연결, 개발 및 Revolution Analytics에서 제공 되는 성능 도구 관련 문제를 나열 합니다. 이러한 도구는 이전 시험판 버전의 제공 된 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]합니다.

일반적으로 이러한 이전 버전을 제거 하 고 최신 버전의 SQL Server 또는 Microsoft R Server를 설치 하는 것이 좋습니다.

### <a name="running-side-by-side-versions-of-revolution-r-enterprise"></a>Revolution R Enterprise의 병렬-버전 실행

버전의 Revolution R Enterprise 나란히 설치 [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] 지원 되지 않습니다.

다른 버전의 Revolution R Enterprise를 사용할 라이선스가 있는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 사용할 모든 워크스테이션과 별도의 컴퓨터에 라이선스를 두어야 합니다.

### <a name="the-use-of-an-r-productivity-environment-is-not-supported"></a>R 생산성 환경 사용 지원 되지 않습니다.

일부 시험판 버전의 [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] Revolution Analytics에서 만든 Windows 용 R 개발 환경을 포함 합니다. 이 도구를 더 이상 제공 하 고 지원 되지 않습니다.

호환성을 위해 [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], Microsoft R Client 또는 Microsoft R Server Revolution Analytics 도구를 대신 설치 하는 것이 좋습니다. [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/) 및 [Visual Studio Code](https://code.visualstudio.com/) 도 Microsoft R 솔루션을 지원 합니다.

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>SQLite ODBC 드라이버와 RevoScaleR의 호환성 문제

SQLite ODBC 드라이버의 수정 버전 0.92는 RevoScaleR과 호환 되지 않습니다. 수정 버전 0.88 ~ 0.91 및 0.93 이상은 및 나중에 호환 가능한 것으로 알려져 있습니다.

## <a name="python-code-execution-or-python-package-issues"></a>Python 코드 실행 또는 Python 패키지 문제

이 섹션에서는으로 SQL Server, Microsoft에서 게시 Python 패키지에 관련 된 문제에 대해 Python을 실행 하는 관련 된 알려진된 문제가 포함 하 여 [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 및 [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).


## <a name="see-also"></a>참고 항목

[SQL Server 2016의 새로운 기능](../sql-server/what-s-new-in-sql-server-2016.md)

[SQL Server의 기계 학습 문제 해결](machine-learning-troubleshooting-faq.md)

