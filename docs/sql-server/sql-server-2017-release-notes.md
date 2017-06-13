---
title: "SQL Server 2017 릴리스 정보 | Microsoft Docs"
ms.custom: 
ms.date: 05/16/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
caps.latest.revision: 41
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 67c1c0f3a9da6cc5d050da5db8a493f5da934c2a
ms.openlocfilehash: fa45fea4ebb378f035b4b4af2b1fa8a20bc152a5
ms.contentlocale: ko-kr
ms.lasthandoff: 05/17/2017

---
# <a name="sql-server-2017-release-notes"></a>SQL Server 2017 릴리스 정보
이 항목에서는 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 관련 제한 사항 및 문제에 대해 설명합니다. 관련된 정보에 대 한 다음 항목을 참조 합니다.

- [SQL Server 2017의에서 새로운 기능](../sql-server/what-s-new-in-sql-server-2017.md)합니다.
- [Linux 릴리스 정보에서 SQL Server](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes)합니다.
- [SQL Server Reporting Services 릴리스 정보](../reporting-services/reporting-services-release-notes.md)합니다.

 **사용해보기:**    
   -   [![평가 센터에서 다운로드](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477) **[평가 센터](http://go.microsoft.com/fwlink/?LinkID=829477)**에서 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 다운로드

## <a name="sql-server-2017-ctp-21-may--2017"></a>SQL Server 2017 CTP 2.1 (2017 년 5 월)
### <a name="documentation-ctp-21"></a>설명서 (CTP 2.1)
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 에 대한 설명서는 제한되며 내용은 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 설명서 집합에 포함됩니다.  [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 과 관련된 문서의 내용은 **적용 대상**에서 설명합니다. 
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에 대한 오프라인 콘텐츠는 제공되지 않습니다.

### <a name="sql-server-reporting-services-ctp-21"></a>SQL Server Reporting Services (CTP 2.1)

- **문제 및 고객 미치는 영향:** SQL Server Reporting Services와 Power BI의 보고서 서버에 동일한 컴퓨터와 그 중 하나를 제거 하는 경우 더 이상 됩니다 나머지 보고서 서버 구성 관리자와 보고서 서버에 연결할 수 없습니다.
- **해결 방법** 이 문제를 해결 하려면 서버 중 하나를 제거한 후 다음 작업을 수행 해야 합니다.

    1. 관리자 모드에서 명령 프롬프트를 시작 합니다.
    2. 나머지 보고서 서버를 설치한 디렉터리로 이동 합니다.

        *기본 Power BI 보고서 서버에 대 한 위치: C:\Program Files\Microsoft Power BI 보고서 서버*

        *SQL Server Reporting Services의 기본 위치: C:\Program Files\Microsoft SQL Server Reporting Services*

    3. 다음 폴더로 이동 합니다. 이거나 *SSRS* 또는 *PBIRS* 남은 기능에 따라 합니다.
    4. WMI 폴더로 이동 합니다.
    5. 다음 명령을 실행합니다.

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        표시 경우 다음 오류를 무시할 수 있습니다.

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

### <a name="tsqllanguageservicemsi-ctp-21"></a>TSqlLanguageService.msi (CTP 2.1)

- **문제 및 고객 미치는 영향:** 의 2016 버전이 있는 컴퓨터에 설치한 후 *TSqlLanguageService.msi* (SQL 설치 프로그램을 통해 또는 독립 실행형 재배포 가능 패키지) v13.* (SQL 2016) 버전을 설치 *Microsoft.SqlServer.Management.SqlParser.dll* 및 *Microsoft.SqlServer.Management.SystemMetadataProvider.dll* 제거 됩니다. 2016 버전의 이러한 어셈블리에 종속 되어 있는 모든 응용 프로그램은 다음 작동이 중단, 유사한 오류가 제공: *오류: 파일 또는 어셈블리를 로드할 수 없습니다 ' Microsoft.SqlServer.Management.SqlParser, 버전 13.0.0.0, Culture = neutral, PublicKeyToken = 89845dcd8080cc91 =' 또는 해당 종속성 중 하나입니다. 지정 된 파일을 찾을 수 없습니다.*

   또한를 TSqlLanguageService.msi의 2016 버전을 다시 설치 하면 작업이 실패 메시지와 함께: *설치의 Microsoft SQL Server 2016 T-SQL 언어 서비스는 더 높은 버전의 컴퓨터에 이미 있기 때문에 실패 했습니다.*합니다.

- **해결 방법** 어셈블리의 버전을이 문제를 해결 하 고는 v13에 의존 하는 응용 프로그램을 수정 하려면 다음이 단계를 따릅니다.

   1. 로 이동 **프로그램 추가/제거**
   1. 찾을 *Microsoft SQL Server vNext T-SQL 언어 서비스 CTP2.1*마우스 오른쪽 단추로 클릭 하 고 선택 **제거**합니다.
   1. 구성 요소를 제거한 후 복구 중단 되는 응용 프로그램 (적절 한 버전의 다시 설치 하거나 *TSqlLanguageService.MSI*)

   이 해결 방법을 v14 버전에 종속 된 모든 응용 프로그램이 더 이상 작동 해당 어셈블리의 v14 버전을 제거 합니다. 어셈블리만 필요 하지만 모든 side-by-side-2016을 설치 하지 않고 별도 설치는 필요 합니다.

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-20-april--2017"></a>SQL Server 2017 CTP 2.0 (2017 년 4 월)
### <a name="documentation-ctp-20"></a>설명서 (CTP 2.0)
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 에 대한 설명서는 제한되며 내용은 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 설명서 집합에 포함됩니다.  [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 과 관련된 문서의 내용은 **적용 대상**에서 설명합니다. 
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에 대한 오프라인 콘텐츠는 제공되지 않습니다.

### <a name="always-on-availability-groups"></a>Always On 가용성 그룹

- **문제 및 고객 미치는 영향:** 가용성 그룹 보조 복제본을 호스팅하는 SQL Server 인스턴스는 SQL Server 주 버전은 주 복제본을 호스팅하는 인스턴스에 보다 낮은 경우 충돌 합니다. SQL server 가용성 그룹을 호스팅하는 SQL Server의 지원 되는 모든 버전에서 업그레이드에 영향을 줍니다 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 2.0. 이 다음 단계에서 발생합니다. 

> 1. SQL Server 인스턴스 호스팅 보조 복제본에 따라 업그레이드 [모범 사례](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)합니다.
> 2. 업그레이드 후 장애 조치가 발생 되 고 새로 업그레이드 된 보조 가용성 그룹에 있는 모든 보조 복제본에 대 한 업그레이드를 완료 하기 전에 기본 됩니다. 이전 주 주 보다 낮은 버전을이 보조 포함 되었습니다.
> 3. 가용성 그룹이 지원 되지 않는 구성 이며 남은 모든 보조 복제본이 충돌에 노출 될 수 있습니다. 

- **해결 방법** 새 주 복제본과 제거 구성에서 잘못 된 보조 복제본을 호스팅하는 SQL Server 인스턴스에 연결 합니다.

   `ALTER AVAILABILITY GROUP agName REMOVE REPLICA ON NODE instanceName`

   보조 복제본을 호스팅하는 SQL Server의 인스턴스를 복구 합니다.


![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-2017-ctp-14-march--2017"></a>SQL Server 2017 CTP 1.4 (2017 년 3 월)

### <a name="documentation-ctp-14"></a>설명서(CTP 1.4)
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 에 대한 설명서는 제한되며 내용은 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 설명서 집합에 포함됩니다.  [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 과 관련된 문서의 내용은 **적용 대상**에서 설명합니다. 
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에 대한 오프라인 콘텐츠는 제공되지 않습니다.

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-2017-ctp-13-february--2017"></a>SQL Server 2017 CTP 1.3 (2017 년 2 월)
### <a name="supported-installation-scenarios-ctp-13"></a>지원되는 설치 시나리오(CTP 1.3)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 는 테스트 버전으로만 제공됩니다.  프로덕션 배포는 지원되지 않습니다. [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 은 가상 컴퓨터에 설치하고 테스트하는 것이 좋습니다.

### <a name="documentation-ctp-13"></a>설명서(CTP 1.3)
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 에 대한 설명서는 제한되며 내용은 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 설명서 집합에 포함됩니다.  [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 과 관련된 문서의 내용은 **적용 대상**에서 설명합니다. 
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에 대한 오프라인 콘텐츠는 제공되지 않습니다.

### <a name="sql-server-integration-services-ssis-ctp-13"></a>SSIS(SQL Server Integration Services)(CTP 1.3)
#### <a name="cdc-components-not-supported-in-this-ctp-release"></a>이 CTP 릴리스에서는 CDC 구성 요소가 지원되지 않음
-   **문제 및 고객에게 미치는 영향**: 이 CTP 릴리스에서는 CDC 제어 작업, CDC 소스 및 CDC 분할자가 지원되지 않습니다.
-   **해결 방법**: 해결 방법이 없습니다.


![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="sql-server-2017-ctp-12-january--2017"></a>SQL Server 2017 CTP 1.2 (2017 년 1 월)
### <a name="supported-installation-scenarios-ctp-12"></a>지원되는 설치 시나리오(CTP 1.2)
[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 는 테스트 버전으로만 제공됩니다.  프로덕션 배포는 지원되지 않습니다. [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 은 가상 컴퓨터에 설치하고 테스트하는 것이 좋습니다.

### <a name="sql-server-database-engine-ctp-12"></a>SQL Server 데이터베이스 엔진(CTP 1.2)
- **문제 및 고객에게 미치는 영향:** 일부 경우에 MSSQLSERVER 서비스가 "시작 중" 상태에서 중단됩니다.
- **해결 방법:** 이 문제를 해결하려면
  -  `mssqlserver` 서비스 및 `keyiso` 서비스 간에 종속성을 만듭니다. 이 작업을 수행하는 한 가지 방법은 관리자 권한 명령 프롬프트에서 다음 명령을 실행하는 것입니다. `sc config mssqlserver depend= keyiso`
  - 컴퓨터를 다시 부팅합니다.

### <a name="documentation-ctp-12"></a>설명서(CTP 1.2)
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 에 대한 설명서는 제한되며 내용은 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 설명서 집합에 포함됩니다.  [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 과 관련된 문서의 내용은 **적용 대상**에서 설명합니다. 
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에 대한 오프라인 콘텐츠는 제공되지 않습니다.
 
### <a name="sql-server-integration-services-ssis-ctp-12"></a>SSIS(SQL Server Integration Services)(CTP 1.2)
#### <a name="deleting-the-ssis-catalog-may-fail-when-ssis-scale-out-is-installed"></a>SSIS 규모 확장이 설치되어 있으면 SSIS 카탈로그가 삭제되지 않을 수 있음
**문제 및 고객에게 미치는 영향:**SSIS 규모 확장 기능이 컴퓨터에 설치되어 있는 경우 "사용자가 현재 로그인되어 있기 때문에 *'login'* 로그인을 삭제할 수 없습니다."라는 오류가 발생하고 SSISDB 카탈로그 데이터베이스가 삭제되지 않을 수 있습니다.
   
**해결 방법**:
-   규모 확장 마스터 컴퓨터에서 "services.msc" 명령을 실행하여 서비스 창을 엽니다. SQL Server Integration Services 클러스터 마스터 서비스를 중지합니다.
-   마스터에 연결된 규모 확장 작업자 컴퓨터에서 "services.msc" 명령을 실행하여 서비스 창을 엽니다. SQL Server Integration Services 클러스터 작업자 서비스를 중지합니다.

이제 SSISDB 카탈로그 데이터베이스를 삭제할 수 있습니다.

### <a name="sql-server-master-data-services-ctp-12"></a>SQL Server Master Data Services(CTP 1.2)
#### <a name="transaction-may-not-work-when-the-entity-transaction-log-type-is-set-to-attribute"></a>엔터티 트랜잭션 로그 유형이 특성으로 설정되어 있으면 트랜잭션이 작동하지 않을 수 있음
**문제 및 고객에게 미치는 영향:** 엔터티 트랜잭션 로그 유형이 **에서** 특성 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] (기본값: **멤버**)으로 설정되어 있으면 다음 시나리오가 실패합니다.

* 엔터티 변경에 대한 트랜잭션이 웹 사이트에 표시되지 않습니다.
* 웹 사이트에서 **트랜잭션** 페이지를 열고 트랜잭션을 되돌릴 수 없습니다.
* 웹 사이트에서 트랜잭션 주석을 사용하여 엔터티를 업데이트할 수 없습니다.

**해결 방법**: 해결 방법이 없습니다.

#### <a name="copy-version-may-not-work-when-copy-only-committed-version-is-set-to-false"></a>**커밋된 버전만 복사** 가 false로 설정되어 있으면 버전 복사가 작동하지 않을 수 있음
-  **문제 및 고객에게 미치는 영향:** **커밋된 버전만 복사** 설정이 **아니요** (기본값: **예**)로 설정되어 있으면 버전 복사 작업이 실패할 수 있습니다. 오류 메시지가 없습니다.
-  **해결 방법**: 해결 방법이 없습니다.

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) SQL Server 엔지니어링 팀에 문의 
- [Stack Overflow(태그 sql-server) - 기술 관련 문의 사항](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN 포럼 - 기술 관련 문의 사항](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect - 버그 보고 및 기능 요청](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - R에 대한 일반 토론](https://www.reddit.com/r/SQLServer/)


![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)


