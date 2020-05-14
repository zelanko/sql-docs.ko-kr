---
title: SQL Server 2017 릴리스 정보 | Microsoft Docs
description: 이 문서에서는 SQL Server 2017의 제한 사항 및 문제에 대해 설명하고 관련 정보에 대한 링크를 제공합니다.
ms.custom: ''
ms.date: 11/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 43e6451f54e55af8e9c782dbab8a23bc753a03bc
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2020
ms.locfileid: "83001131"
---
# <a name="sql-server-2017-release-notes"></a>SQL Server 2017 릴리스 정보
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]
이 문서에서는 SQL Server 2017의 관련 제한 사항 및 문제에 대해 설명합니다. 관련 정보는 다음을 참조하세요.
- [SQL Server 2017의 새로운 기능](../sql-server/what-s-new-in-sql-server-2017.md)
- [Linux 릴리스 노트의 SQL Server](../linux/sql-server-linux-release-notes.md)
- 최신 CU(누적 업데이트) 릴리스에 대한 자세한 내용: [SQL Server 2017 누적 업데이트](https://aka.ms/sql2017cu)

**SQL Server를 사용해 보세요.**
- [![평가 센터에서 다운로드](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=829477) [SQL Server 2017 다운로드](https://go.microsoft.com/fwlink/?LinkID=829477)
- [![가상 머신 만들기](../includes/media/azure-vm.png)](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) [SQL Server 2017이 있는 가상 머신 실행](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)

> [!NOTE]
> 이제 SQL Server 2019 미리 보기를 사용할 수 있습니다. 자세한 내용은 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15)을 참조하세요.

## <a name="sql-server-2017---general-availability-release-october-2017"></a>SQL Server 2017 - 일반 공급 릴리스(2017년 10월)
### <a name="database-engine"></a>데이터베이스 엔진

- **문제 및 고객에게 미치는 영향:** 업그레이드 후 기존 FILESTREAM 네트워크 공유를 더 이상 사용할 수 없습니다.

- **해결 방법:** 먼저 컴퓨터를 재부팅하고 FILESTREAM 네트워크 공유를 사용할 수 있는지 확인합니다. 공유를 여전히 사용할 수 없으면 다음 단계를 완료합니다.

    1. SQL Server 구성 관리자에서 SQL Server 인스턴스를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. 
    2. **FILESTREAM** 탭에서 **파일 I/O 스트리밍 액세스에 FILESTREAM 사용**을 선택 취소한 다음, **적용**을 클릭합니다.
    3. 원본 공유 이름으로 **파일 I/O 스트리밍 액세스에 FILESTREAM 사용**을 다시 선택하고 **적용**을 클릭합니다.

### <a name="master-data-services-mds"></a>MDS(Master Data Services)
- **문제 및 고객에게 미치는 영향:**   사용자 권한 페이지에서 엔터티 트리 뷰의 루트 수준에 대한 권한을 부여할 때 다음 오류가 표시됩니다. `"The model permission cannot be saved. The object guid is not valid"`

- **해결 방법:** 
  - 루트 수준이 아니라 트리 뷰의 하위 노드에 대한 권한을 부여합니다.

### <a name="analysis-services"></a>Analysis Services
- **문제 및 고객에게 미치는 영향:** 다음 원본에 대한 데이터 커넥터는 1400 호환성 수준의 표 형식 모델에서는 아직 사용할 수 없습니다.
  - Amazon Redshift
  - IBM Netezza
  - Impala
- **해결 방법:** 없음   

- **문제 및 고객에게 미치는 영향:** 큐브 뷰를 포함하는 1400 호환성 수준의 직접 쿼리 모델은 메타데이터 쿼리 또는 검색에 실패할 수 있습니다.
- **해결 방법:** 큐브 뷰를 제거하고 다시 배포합니다.

### <a name="tools"></a>도구
- **문제 및 고객에게 미치는 영향:** *DReplay* 실행이 실패하고 다음 메시지가 표시됩니다. "오류 DReplay 예기치 않은 오류가 발생했습니다!"
- **해결 방법:** 없음

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-release-candidate-rc2---august-2017"></a>SQL Server 2017 릴리스 후보(RC2 - 2017년 8월)
이 릴리스와 관련된 Windows의 SQL Server에 대한 릴리스 정보가 없습니다. [Linux 릴리스 노트의 SQL Server](../linux/sql-server-linux-release-notes.md)를 참조하세요.


![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-release-candidate-rc1---july-2017"></a>SQL Server 2017 릴리스 후보(RC1 - 2017년 7월)
### <a name="sql-server-integration-services-ssis-rc1---july-2017"></a>SSIS(SQL Server Integration Services)(RC1 - 2017년 7월)
- **문제 및 고객에게 미치는 영향:** 일관성과 가독성을 향상하기 위해 저장 프로시저 **[catalog].[create_execution]** 의 *runincluster* 매개 변수 이름이 *runinscaleout*으로 변경되었습니다.
- **해결 방법:** Scale Out에서 패키지를 실행하는 기존 스크립트가 있는 경우 매개 변수 이름을 *runincluster*에서 *runinscaleout*으로 변경해야만 RC1에서 스크립트가 작동합니다.

- **문제 및 고객에게 미치는 영향:** SSMS(SQL Server Management Studio) 17.1 및 이전 버전은 RC1의 Scale Out에서 패키지 실행을 트리거할 수 없습니다. 오류 메시지: “ *@runincluster* 은(는) 프로시저 **create_execution**의 매개 변수가 아닙니다.” 이 문제는 다음 릴리스인 SSMS 버전 17.2에서 해결됩니다. SSMS 17.2 이상 버전은 Scale Out에서 새 매개 변수 이름 및 패키지 실행을 지원합니다. 
- **해결 방법:** SSMS 버전 17.2가 나올 때까지:
  1. 기존 버전의 SSMS를 사용하여 패키지 실행 스크립트를 생성합니다.
  2. 스크립트에서 *runincluster* 매개 변수의 이름을 *runinscaleout*으로 변경합니다.
  3. 스크립트를 실행합니다.

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-21-may--2017"></a>SQL Server 2017 CTP 2.1(2017년 5월)
### <a name="documentation-ctp-21"></a>설명서(CTP 2.1)
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]의 설명서는 제한되며 내용은 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 설명서 집합에 포함되어 있습니다.  [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]와 관련된 문서의 내용은 **적용 대상**에서 설명합니다. 
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 관련 오프라인 콘텐츠는 제공되지 않습니다.

### <a name="sql-server-reporting-services-ctp-21"></a>SQL Server Reporting Services(CTP 2.1)

- **문제 및 고객에게 미치는 영향:** SQL Server Reporting Services와 Power BI Report Server가 둘 다 동일한 컴퓨터에 있는 경우 이 중 하나를 제거하면 보고서 서버 Configuration Manager를 사용하여 나머지 보고서 서버에 연결할 수 없습니다.
- **해결 방법** 이 문제를 해결하려면 서버 중 하나를 제거한 후 다음 작업을 수행해야 합니다.

    1. 관리자 모드로 명령 프롬프트를 시작합니다.
    2. 나머지 보고서 서버가 설치된 디렉터리로 이동합니다.

        *‘Power BI Report Server 기본 위치: C:\Program Files\Microsoft Power BI Report Server’*

        *‘SQL Server Reporting Services 기본 위치: C:\Program Files\Microsoft SQL Server Reporting Services’*

    3. 그런 다음 남아 있는 기능에 따라 *SSRS* 또는 *PBIRS* 폴더로 이동합니다.
    4. WMI 폴더로 이동합니다.
    5. 다음 명령 실행:

        ```console
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        다음과 같은 오류가 표시되는 경우에는 무시하세요.

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

### <a name="tsqllanguageservicemsi-ctp-21"></a>TSqlLanguageService.msi(CTP 2.1)

- **문제 및 고객에게 미치는 영향:** 2016 버전의 ‘TSqlLanguageService.msi’가 SQL 설치 프로그램을 통해서 또는 독립 실행형 재배포 가능 패키지로 설치된 컴퓨터에 설치한 후 v13.*(SQL 2016) 버전의 ‘Microsoft.SqlServer.Management.SqlParser.dll’ 및 ‘Microsoft.SqlServer.Management.SystemMetadataProvider.dll’이 제거됩니다.    이러한 어셈블리의 2016 버전에 종속된 모든 애플리케이션에서는 작동이 중지되고 *오류 : 파일 또는 어셈블리 ‘Microsoft.SqlServer.Management.SqlParser, Version=13.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91’ 또는 해당 종속성 중 하나를 로드할 수 없습니다. 지정한 파일을 찾을 수 없습니다.* 와 유사한 오류가 표시됩니다.

   또 TSqlLanguageService.msi의 2016 버전을 다시 설치하려고 하면 설치가 실패하고 ‘컴퓨터에 상위 버전이 이미 설치되어 있으므로 Microsoft SQL Server 2016 T-SQL 언어 서비스를 설치하지 못했습니다.’라는 메시지가 표시됩니다. 

- **해결 방법** 이 문제를 해결하고 어셈블리의 v13 버전에 종속된 애플리케이션을 수정하려면 다음 단계를 수행합니다.

   1. **프로그램 추가/제거**로 이동합니다.
   2. *Microsoft SQL Server 2019 T-SQL 언어 서비스 CTP2.1*을 찾아 마우스 오른쪽 단추로 클릭한 다음, **제거**를 선택합니다.
   3. 구성 요소를 제거한 후 중단된 애플리케이션을 복구하거나 적절한 버전의 *TSqlLanguageService.MSI*를 다시 설치합니다.

   이 해결 방법에서는 이러한 어셈블리의 v14 버전을 제거하므로 v14 버전에 종속된 애플리케이션이 더 이상 작동하지 않습니다. 이러한 어셈블리가 필요한 경우에는 2016 병렬 설치 없이 별도로 설치해야 합니다.

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="sql-server-2017-ctp-20-april--2017"></a>SQL Server 2017 CTP 2.0(2017년 4월)
### <a name="documentation-ctp-20"></a>설명서(CTP 2.0)
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]의 설명서는 제한되며 내용은 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] 설명서 집합에 포함되어 있습니다.  [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]와 관련된 문서의 내용은 **적용 대상**에서 설명합니다. 
- **문제 및 고객에게 미치는 영향:** [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 관련 오프라인 콘텐츠는 제공되지 않습니다.

### <a name="always-on-availability-groups"></a>Always On 가용성 그룹

- **문제 및 고객에게 미치는 영향:** SQL Server 주 버전이 주 복제본을 호스트하는 인스턴스보다 낮은 경우 가용성 그룹 보조 복제본을 호스트하는 SQL Server 인스턴스의 작동이 중단됩니다. 가용성 그룹을 호스트하는 지원되는 모든 버전의 SQL Server에서 SQL Server [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 2.0으로의 업그레이드에 영향을 미칩니다. 다음 조건에 해당하는 경우 이 문제가 발생할 수 있습니다. 

> 1. 사용자가 보조 복제본을 호스트하는 SQL Server 인스턴스를 [모범 사례](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md)에 따라 업그레이드합니다.
> 2. 업그레이드 후 장애 조치(failover)가 발생하고 가용성 그룹의 모든 보조 복제본에 대한 업그레이드를 완료하기 전에 새로 업그레이드된 보조 복제본이 주 복제본이 됩니다. 이전 주 복제본이 이제는 주 복제본보다 버전이 낮은 보조 복제본이 됩니다.
> 3. 가용성 그룹은 지원되지 않는 구성 상태가 되며 나머지 보조 복제본은 쉽게 작동이 중단될 수 있습니다. 

- **해결 방법** 새 주 복제본을 호스트하는 SQL Server 인스턴스에 연결하고 구성에서 잘못된 보조 복제본을 제거합니다.

   ```sql
   ALTER AVAILABILITY GROUP agName REMOVE REPLICA ON NODE instanceName;
   ```

   보조 복제본을 호스트하는 SQL Server의 인스턴스가 복구됩니다.

## <a name="more-information"></a>자세한 정보
- [SQL Server Reporting Services 릴리스 정보](../reporting-services/release-notes-reporting-services.md)관련 제한 사항 및 문제에 대해 설명합니다.
- [Machine Learning Services에 대한 알려진 문제](../machine-learning/known-issues-for-sql-server-machine-learning-services.md)
- [SQL Server 업데이트 센터 - 지원되는 모든 버전에 대한 링크 및 정보](https://msdn.microsoft.com/library/ff803383.aspx)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
