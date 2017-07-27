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
ms.translationtype: HT
ms.sourcegitcommit: 6aa73e749d4f308265dfe27a160802c15a391a3e
ms.openlocfilehash: a2950b6aef0e12653efbb9eb26fd3f1ae6cb951e
ms.contentlocale: ko-kr
ms.lasthandoff: 07/17/2017

---
# <a name="sql-server-2017-release-notes"></a>SQL Server 2017 릴리스 정보
이 항목에서는 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]관련 제한 사항 및 문제에 대해 설명합니다. 관련 내용은 다음을 참조하세요.

- [SQL Server 2017의에서 새로운 기능](../sql-server/what-s-new-in-sql-server-2017.md)합니다.
- [Linux 릴리스 정보에서 SQL Server](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes)합니다.
- [SQL Server Reporting Services 릴리스 정보](../reporting-services/reporting-services-release-notes.md)관련 제한 사항 및 문제에 대해 설명합니다.

 **사용해보기:**    
   -   [![평가 센터에서 다운로드](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477) **[평가 센터](http://go.microsoft.com/fwlink/?LinkID=829477)**에서 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 다운로드

## <a name="sql-server-2017-release-candidate-rc1---july-2017"></a>SQL Server 2017 릴리스 후보(RC1 - 2017년 7월)

### <a name="sql-server-integration-services-ssis-rc1---july-2017"></a>SSIS(SQL Server Integration Services)(RC1 - 2017년 7월)
- **문제 및 고객에게 미치는 영향:** 일관성과 가독성을 향상하기 위해 저장 프로시저 **[catalog].[create_execution]**의 *runincluster* 매개 변수 이름이 *runinscaleout*으로 변경되었습니다.
- **해결 방법:** Scale Out에서 패키지를 실행하는 기존 스크립트가 있는 경우 매개 변수 이름을 *runincluster*에서 *runinscaleout*으로 변경해야만 RC1에서 스크립트가 작동합니다.

- **문제 및 고객 미치는 영향:** SSMS(SQL Server Management Studio) 17.1 이전 버전은 RC1의 Scale Out에서 패키지 실행을 트리거할 수 없습니다. 오류 메시지: “*@runincluster*은(는) 프로시저 **create_execution**의 매개 변수가 아닙니다.” 이 문제는 다음 릴리스인 SSMS 버전 17.2에서 해결됩니다. SSMS 17.2 이상 버전은 Scale Out에서 새 매개 변수 이름 및 패키지 실행을 지원합니다. 
- **해결 방법:** SSMS 버전 17.2가 제공되기 전까지는 기존 버전의 SSMS를 사용하여 패키지 실행 스크립트를 생성한 다음 스크립트에서 *runincluster* 매개 변수의 이름을 *runinscaleout*으로 변경하고 스크립트를 실행할 수 있습니다.

![horizontal_bar](../sql-server/media/horizontal-bar.png)
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

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) SQL Server 엔지니어링 팀에 문의 
- [Stack Overflow(태그 sql-server) - 기술 관련 문의 사항](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN 포럼 - 기술 관련 문의 사항](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect - 버그 보고 및 기능 요청](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - R에 대한 일반 토론](https://www.reddit.com/r/SQLServer/)

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
