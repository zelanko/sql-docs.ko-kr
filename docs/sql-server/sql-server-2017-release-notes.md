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
ms.lasthandoff: 07/31/2017

---
# <a name="sql-server-2017-release-notes"></a>SQL Server 2017 릴리스 정보
이 항목에서는 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]관련 제한 사항 및 문제에 대해 설명합니다. 관련 내용은 다음을 참조하세요.

- [SQL Server 2017의 새로운 기능](../sql-server/what-s-new-in-sql-server-2017.md)
- [SQL Server on Linux Release notes](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-release-notes)관련 제한 사항 및 문제에 대해 설명합니다.
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
## <a name="sql-server-2017-ctp-21-may--2017"></a>SQL Server 2017 CTP 2.1(2017년 5월)
### <a name="documentation-ctp-21"></a>설명서(CTP 2.1)
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 에 대한 설명서는 제한되며 내용은 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 설명서 집합에 포함됩니다.  [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 과 관련된 문서의 내용은 **적용 대상**에서 설명합니다. 
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에 대한 오프라인 콘텐츠는 제공되지 않습니다.

### <a name="sql-server-reporting-services-ctp-21"></a>SQL Server Reporting Services(CTP 2.1)

- **문제 및 고객에게 미치는 영향:** SQL Server Reporting Services와 Power BI 보고서 서버가 모두 동일한 컴퓨터에 있는 경우 이 중 하나를 제거하면 더 이상 보고서 서버 구성 관리자를 사용하여 나머지 보고서 서버에 연결할 수 있습니다.
- **해결 방법** 이 문제를 해결하려면 서버 중 하나를 제거한 후 다음 작업을 수행해야 합니다.

    1. 관리자 모드로 명령 프롬프트를 시작합니다.
    2. 나머지 보고서 서버가 설치된 디렉터리로 이동합니다.

        *기본 Power BI 보고서 서버의 기본 위치: C:\Program Files\Microsoft Power BI 보고서 서버*

        *SQL Server Reporting Services의 기본 위치: C:\Program Files\Microsoft SQL Server Reporting Services*

    3. 다른 다음 남은 서버가 무엇인지에 따라 *SSRS* 또는 *PBIRS* 폴더로 이동합니다.
    4. WMI 폴더로 이동합니다.
    5. 다음 명령을 실행합니다.

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        다음 오류가 표시되는 경우 무시해도 됩니다.

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

### <a name="tsqllanguageservicemsi-ctp-21"></a>TSqlLanguageService.msi(CTP 2.1)

- **문제 및 고객에게 미치는 영향:** 2016 버전의 *TSqlLanguageService.msi*가 SQL 설치 프로그램을 통해서나 독립 실행형 재배포 가능 패키지로 설치된 컴퓨터에 설치한 후 v13.*(SQL 2016) 버전의 *Microsoft.SqlServer.Management.SqlParser.dll* 및 *Microsoft.SqlServer.Management.SystemMetadataProvider.dll*이 제거됩니다. 이러한 어셈블리의 2016 버전에 종속된 모든 응용 프로그램의 작동이 중단되고 *오류: 파일, 어셈블리 'Microsoft.SqlServer.Management.SqlParser, Version=13.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' 또는 종속 파일이나 어셈블리 중 하나를 로드할 수 없습니다. 지정한 파일을 찾을 수 없습니다.*와 유사한 오류가 표시됩니다.

   또 TSqlLanguageService.msi의 2016 버전을 다시 설치하려고 하면 설치가 실패하고 *컴퓨터에 상위 버전이 이미 설치되어 있으므로 Microsoft SQL Server 2016 T-SQL 언어 서비스를 설치하지 못했습니다.*라는 메시지가 표시됩니다.

- **해결 방법** 이 문제를 해결하고 어셈블리의 v13 버전에 종속된 응용 프로그램을 수정하려면 다음 단계를 수행합니다.

   1. **프로그램 추가/제거**로 이동합니다.
   1. *Microsoft SQL Server vNext T-SQL 언어 서비스 CTP2.1*을 찾아 마우스 오른쪽 단추로 클릭한 다음 **제거**를 선택합니다.
   1. 구성 요소를 제거한 후 중단된 응용 프로그램을 복구하거나 적절한 버전의 *TSqlLanguageService.MSI*를 다시 설치합니다.

   이 해결 방법에서는 이러한 어셈블리의 v14 버전을 제거하므로 v14 버전에 종속된 응용 프로그램이 더 이상 작동하지 않습니다. 이러한 어셈블리가 필요한 경우에는 2016 병렬 설치 없이 별도로 설치해야 합니다.

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-20-april--2017"></a>SQL Server 2017 CTP 2.0(2017년 4월)
### <a name="documentation-ctp-20"></a>설명서(CTP 2.0)
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 에 대한 설명서는 제한되며 내용은 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 설명서 집합에 포함됩니다.  [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 과 관련된 문서의 내용은 **적용 대상**에서 설명합니다. 
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]에 대한 오프라인 콘텐츠는 제공되지 않습니다.

### <a name="always-on-availability-groups"></a>Always On 가용성 그룹

- **문제 및 고객에게 미치는 영향:** SQL Server 주 버전이 주 복제본을 호스트하는 인스턴스보다 낮은 경우 가용성 그룹 보조 복제본을 호스트하는 SQL Server 인스턴스의 작동이 중단됩니다. 가용성 그룹을 호스트하는 지원되는 모든 버전의 SQL Server에서 SQL Server [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 2.0으로의 업그레이드에 영향을 미칩니다. 이 문제는 다음 단계에 따라 발생합니다. 

> 1. 사용자가 보조 복제본을 호스트하는 SQL Server 인스턴스를 [모범 사례](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)에 따라 업그레이드합니다.
> 2. 업그레이드 후 장애 조치(failover)가 발생하고 가용성 그룹의 모든 보조 복제본에 대한 업그레이드를 완료하기 전에 새로 업그레이드된 보조 복제본이 주 복제본이 됩니다. 이전 주 복제본이 이제 주 복제본보다 버전이 낮은 보조 복제본이 됩니다.
> 3. 가용성 그룹은 지원되지 않는 구성 상태가 되며 나머지 보조 복제본은 쉽게 작동이 중단될 수 있습니다. 

- **해결 방법** 새 주 복제본을 호스트하는 SQL Server 인스턴스에 연결하고 구성에서 잘못된 보조 복제본을 제거합니다.

   `ALTER AVAILABILITY GROUP agName REMOVE REPLICA ON NODE instanceName`

   보조 복제본을 호스트하는 SQL Server의 인스턴스가 복구됩니다.

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) SQL Server 엔지니어링 팀에 문의 
- [Stack Overflow(태그 sql-server) - 기술 관련 문의 사항](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN 포럼 - 기술 관련 문의 사항](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect - 버그 보고 및 기능 요청](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - R에 대한 일반 토론](https://www.reddit.com/r/SQLServer/)

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
