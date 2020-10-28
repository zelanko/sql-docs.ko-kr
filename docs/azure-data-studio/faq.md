---
title: Azure Data Studio FAQ
description: Azure Data Studio의 기능, Azure Data Studio를 사용해야 하는 사용자, Azure Data Studio의 비용과 같은 자주 묻는 질문을 살펴봅니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: alayu, maghan
ms.custom: seodec18
ms.date: 10/20/2020
ms.openlocfilehash: 0e32a9e0a9e7dfd14c56c31a065f692c535b24fb
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257353"
---
# <a name="azure-data-studio-faq"></a>Azure Data Studio FAQ

## <a name="what-is-azure-data-studio"></a>Azure Data Studio란?

Azure Data Studio는 Windows, macOS 및 Linux에서 온-프레미스 및 클라우드 데이터 플랫폼의 Azure Data 제품군을 사용하는 데이터 전문가를 위한 오픈 소스 플랫폼 간 데스크톱 환경입니다. 이전에는 SQL Operations Studio라는 미리 보기 이름으로 릴리스되었던 Azure Data Studio는 매우 빠른 IntelliSense, 코드 조각, 원본 제어 통합 및 통합 터미널을 사용하여 최신 편집기 환경을 제공합니다. 데이터 플랫폼 사용자를 대상으로 설계되었으며 쿼리 결과 세트의 기본 제공 차트 기능과 사용자 지정이 가능한 대시보드를 포함합니다.

연구를 통해 사용자들이 SQL Server Management Studio를 사용하여 다른 작업을 수행하는 것보다 쿼리 편집에 훨씬 더 많은 시간을 투입하고 있다는 사실이 확인되었습니다. 이러한 이유로 Azure Data Studio는 가장 많이 사용되는 기능에 좀 더 주안점을 두고, 추가 환경을 선택적 확장으로 제공하도록 디자인되었습니다. 이를 통해 모든 사용자는 가장 자주 사용하는 워크플로로 환경을 사용자 지정할 수 있습니다.

## <a name="how-much-does-azure-data-studio-cost"></a>Azure Data Studio 비용은 얼마나 되나요?

Azure Data Studio는 프라이빗 또는 상업용도 모두 무료로 사용할 수 있습니다.

## <a name="who-should-use-azure-data-studio"></a>Azure Data Studio는 어떤 사용자를 대상으로 하나요?

누구나 Azure Data Studio를 사용할 수 있습니다. 그러나 데이터베이스 개발자, 데이터베이스 관리자, 시스템 관리자 및 독립 소프트웨어 공급업체에서 수행하는 작업을 간소화하도록 디자인되었습니다.

## <a name="what-can-i-do-with-azure-data-studio"></a>Azure Data Studio로 어떤 작업을 할 수 있나요?

Azure Data Studio는 Visual Studio Code를 기반으로 구축되었으며 SQL Server, Azure SQL Database, Azure Synapse Analytics를 사용할 때 간단한 키보드 중심의 최신 코드 워크플로 환경을 제공합니다. Azure Data Studio는 여러 탭 창, 다양한 SQL 편집기, IntelliSense, 키워드 완성, 코드 조각 및 코드 탐색, 원본 제어 통합(Git 및 TFS)과 같은 기본 제공 기능을 통해 매일 사용하는 핵심 환경을 간단하고 편리하게 만들어줍니다. 요청 시 쿼리를 실행하고, 결과를 텍스트, JSON 또는 Excel로 결과를 보고, 저장하며, 데이터를 편집하고, 즐겨 사용하는 데이터베이스 연결을 구성 및 관리하고, 익숙한 개체 검색 환경에서 데이터베이스 개체를 찾아볼 수 있습니다.

Azure Data Studio 사용자 인터페이스 안에 있는 통합 터미널 창에서 즐겨 사용하는 명령줄 도구(예: Bash, PowerShell, sqlcmd, bcp, psql 및 ssh)를 사용할 수 있습니다. 개발 또는 테스트 목적으로 데이터베이스 복사본을 만들기 위한 데이터베이스 개체용 CREATE 및 INSERT 스크립트를 쉽게 생성하고 실행할 수 있습니다. 새 데이터베이스 및 데이터베이스 개체(예: 테이블, 뷰, 저장 프로시저, 사용자, 로그인, 역할 등)를 만들거나 기존 데이터베이스 개체를 업데이트하는 스마트 코드 조각 및 풍부한 그래픽 환경으로 생산성을 높일 수 있습니다. 다양한 사용자 지정 가능 대시보드를 사용하여 온-프레미스, Azure 또는 임의 클라우드의 데이터베이스에서 성능 병목 현상을 모니터링하고 신속하게 해결할 수 있습니다.

Azure Data Studio는 데이터베이스를 백업 및 복원하는 일관된 환경을 제공합니다. SQL Server Always On 가용성 그룹에 대한 계획된 지원을 통해 중요 업무용 SQL Server 데이터베이스에 대한 AG를 쉽게 구성, 모니터링하고 문제를 해결하며, 재해 발생 시 보조 데이터베이스로 빠르게 장애 조치(failover) 할 수 있습니다. Azure Data Studio는 선택한 운영 체제에서 선택한 데이터베이스의 DevOps 수명 주기 동안 생산성을 높일 수 있도록 디자인되었습니다. 결과적으로 사용자는 항상 제어되며, 위험을 줄이고, 문제를 더 빠르게 해결하고, 고객의 기대를 초과하는 가치를 지속적으로 전달할 수 있습니다.

## <a name="is-azure-data-studio-open-source"></a>Azure Data Studio는 오픈 소스인가요?

Azure Data Studio 및 해당 데이터 공급자용 소스 코드는 GitHub에서 사용할 수 있습니다. Visual Studio Code를 기준으로 하는 프런트 엔드 [Azure Data Studio](https://github.com/microsoft/azuredatastudio)의 소스 코드는 소프트웨어를 수정하고 사용할 수 있지만 클라우드 서비스에서 재배포하거나 호스트할 수는 없도록 하는 소스 코드 EULA에 따라 사용할 수 있습니다. 데이터 공급자용 소스 코드는 MIT 라이선스([https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice))에 따라 사용할 수 있습니다.

## <a name="do-we-plan-to-open-source-ssms"></a>원본 SSMS를 열 예정인가요?

아니요. 그러나 차세대 다중 OS CLI 및 GUI 도구는 오픈 소스입니다. 예를 들어, VS Code, mssql-scripter 및 msql-CLI에 대한 mssql 확장은 GitHub에서 모든 오픈 소스입니다. Azure Data Studio의 소스 코드는 GitHub에서 사용할 수 있습니다.  

## <a name="now-that-there-is-azure-data-studio-does-microsoft-plan-to-deprecate-ssms-and-ssdt"></a>Azure Data Studio가 있으므로 Microsoft는 SSMS와 SSDT의 사용을 중단하게 되나요? 

아니요. 차세대 다중 OS 및 다중 DB CLI/GUI 도구 외에도 주력 Windows 도구(SSMS, SSDT, PowerShell)에 대한 투자는 계속될 예정입니다. 고객이 각자의 시나리오에 대해 원하는 플랫폼에서 원하는 도구를 사용할 수 있도록 지원하는 것이 목표입니다. Azure Data Studio는 SQL Server Management Studio에서 가장 많이 사용되는 기능으로 확인된 쿼리 편집 및 데이터 개발 환경에 보다 주안점을 두고 있습니다. 백업, 복원, 에이전트 작업 관리, 서버 프로파일링 등의 고가치 관리 기능을 Azure Data Studio에서 확장으로 사용할 수도 있습니다. Azure Data Studio는 플랫폼 간 기능이므로 사용자는 원하는 플랫폼에서 작업할 수 있습니다. 그러나 SQL Server Management Studio 또한 계속해서 광범위한 관리 기능을 제공하면서 플랫폼 관리 작업을 위한 주력 도구로 사용될 것입니다. 

## <a name="when-should-i-use-azure-data-studio-or-sql-server-management-studio"></a>Azure Data Studio 또는 SQL Server Management Studio는 어떤 경우에 사용해야 하나요?

*Azure Data Studio를 사용하는 경우:*

- 대부분 쿼리를 편집 또는 실행하는 경우입니다.
- 결과 집합을 빠르게 차트로 만들고 시각화하는 기능이 필요합니다.
- sqlcmd 또는 PowerShell을 사용하여 통합 터미널을 통해 대부분의 관리 작업을 실행할 수 있습니다.
- 마법사 환경이 별로 필요하지 않습니다.
- 심층 관리 또는 플랫폼 관련 구성을 수행할 필요가 없습니다.
- macOS 또는 Linux에서 실행해야 합니다.

*SQL Server Management Studio를 사용하는 경우:*

- 복잡한 관리 또는 플랫폼 구성을 수행하고 있습니다.
- 사용자 관리, 취약성 평가 및 보안 기능 구성을 비롯한 보안 관리를 수행하고 있습니다.
- 성능 튜닝 관리자 및 대시보드를 사용해야 합니다.
- 데이터베이스 다이어그램 및 테이블 디자이너를 사용합니다.
- 등록된 서버에 액세스해야 합니다.
- 활성 쿼리 통계 또는 클라이언트 통계를 사용합니다.

## <a name="feature-comparison"></a>기능 비교

### <a name="shell-features"></a>셸 기능

|기능|Azure Data Studio|SSMS|
|:---|:---|:---|
|Azure 로그인|예|예|
|대시보드|예| |
|확장|예| |
|통합 터미널|예||
|개체 탐색기|예|예|
|개체 스크립팅|예|예|
|프로젝트 시스템|예||
|테이블에서 선택|예|예|
|원본 코드 제어|예||
|작업창|예||
|어둡게 모드를 포함한 테마|예||
|Azure Resource Explorer|미리 보기||
|스크립트 생성 마법사||예|
|개체 속성||예|
|테이블 디자이너||예|

### <a name="query-editor"></a>쿼리 편집기

|기능|Azure Data Studio|SSMS|
|:---|:---|:---|
|차트 뷰어|예||
|CSV, JSON, XLSX로 결과 내보내기|예||
|파일로 결과 저장||예|
|텍스트로 결과 표시||예|
|IntelliSense|예|예|
|코드 조각|예|예|
|플랜 표시|미리 보기|예|
|클라이언트 통계||예|
|활성 쿼리 통계||예|
|쿼리 옵션||예|
|공간 뷰어||예|
|SQLCMD|예|예|

### <a name="operating-system-support"></a>운영 체제 지원

|기능|Azure Data Studio|SSMS|
|:---|:---|:---|
|Windows|예|예|
|macOS|예||
|Linux|예||

### <a name="data-engineering"></a>데이터 엔지니어링

|기능|Azure Data Studio|SSMS|
|:---|:---|:---|
|외부 데이터 마법사|미리 보기||
|HDFS 통합|미리 보기||
|Notebooks|미리 보기||

### <a name="database-administration"></a>데이터베이스 관리

|기능|Azure Data Studio|SSMS|
|:---|:---|:---|
|백업/복원|예|예|
|플랫 파일 가져오기|예|예|
|SQL 에이전트|미리 보기|예|
|SQL 프로파일러|미리 보기|예|
|Always On||예|
|Always Encrypted||예|
|데이터 복사 마법사||예|
|데이터 튜닝 관리자||예|
|데이터베이스 다이어그램||예|
|오류 로그 뷰어||예|
|유지 관리 계획||예|
|다중 서버 쿼리||예|
|정책 기반 관리||예|
|PolyBase||예|
|쿼리 저장소||예|
|등록된 서버||예|
|복제||예|
|보안 관리||예|
|Service Broker||예|
|SQL 평가|미리 보기|예|
|SQL 메일||예|
|Template Explorer||예|
|취약성 평가||예|
|XEvent 관리||예|

### <a name="database-development"></a>데이터베이스 개발
|기능|Azure Data Studio|SSMS|
|:---|:---|:---|
|DACPAC 가져오기\내보내기|예|예|
|SQL 프로젝트|미리 보기||
|스키마 비교|예||



## <a name="azure-data-studio-is-missing-a-feature-that-is-in-ssmsssdt-will-you-add-it"></a>Azure Data Studio에 SSMS/SSDT 기능이 없습니다. 추가하시겠습니까?

시나리오 및 고객/비즈니스 요구에 따라 다릅니다. 우선 순위를 지정하는 데 도움이 되도록 [GitHub](https://github.com/microsoft/azuredatastudio/issues)에서 제안 사항을 제시하고 기존 제안에 투표하세요.

## <a name="i-understand-azure-data-studio-and-the-mssql-extension-for-vs-code-are-powered-by-a-new-tools-service-that-uses-smo-apis-under-the-covers-is-smo-available-on-linux-and-macos"></a>Azure Data Studio와 VS Code용 mssql 확장은 내부적으로 SMO API를 사용하는 새 도구 서비스를 통해 지원됩니다. SMO를 Linux 및 macOS에서 사용할 수 있나요?

SMO API는 Linux 또는 macOS에서는 아직 사용할 수 없습니다. Azure Data Studio에 필요한 SMO API의 하위 세트를 .NET Core로 이식했으므로 로드맵의 일부로 확장할 계획입니다. SQL Tools 서비스는 GitHub [https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice)에 있습니다.

## <a name="do-you-plan-to-port-the-dacfx-apis-andor-sqlpackageexe-andor-ssdt-to-linux-and-macos"></a>DACFx API 및/또는 sqlpackage.exe 및/또는 SSDT를 Linux 및 macOS로 이식할 계획인가요?

이 중 일부가 완료되었습니다.  [SqlPackage.exe](../tools/sqlpackage-download.md)는 이제 Windows, macOS 및 Linux용 .NET Core에서 사용할 수 있습니다.  SQL 프로젝트(SSDT) 기능은 Azure Data Studio의 [SQL Database 프로젝트 확장](extensions/sql-database-project-extension.md)에서 사용하도록 설정됩니다.

## <a name="will-sql-powershell-cmdlets-be-available-on-linux-and-macos"></a>SQL PowerShell cmdlet을 Linux 및 macOS에서 사용할 수 있나요?

SQL PowerShell은 현재 PowerShell 갤러리에서 사용 가능하며, Windows에서 SQL PowerShell을 통해 Linux의 SQL처럼 모든 시스템에서 실행되는 SQL Server를 사용할 수 있습니다. Linux 및 macOS에서 SQL PowerShell cmdlet을 제공할 예정입니다. 우선 순위를 지정하는 데 도움이 되도록 [GitHub](https://github.com/microsoft/azuredatastudio/issues)에서 제안을 제출해 주세요.

## <a name="who-usually-uses-azure-data-studio"></a>일반적으로 Azure Data Studio의 사용자는 누구인가요?

개발자와 DBA가 일반적으로 Azure Data Studio의 사용자입니다.

## <a name="does-azure-data-studio-integrate-with-azure-synapse-analytics"></a>Azure Data Studio는 Azure Synapse Analytics와 통합되나요?

예. Azure Data Studio의 Azure Synapse Analytics 지원은 현재 Azure SQL Managed Instance 및 SQL Server 2019 빅 데이터와 함께 미리 보기로 제공됩니다.

## <a name="why-is-azure-data-studio-important-for-big-data-scenarios"></a>빅 데이터 시나리오에 Azure Data Studio가 중요한 이유는 무엇인가요?

SQL Server는 해당 기능을 빅 데이터 공간으로 확장하므로 이러한 사용 사례를 지원하기 위한 새로운 도구가 필요합니다. 이 때문에 Azure Data Studio에서는 SQL Server 도구 세트에 포함된 Notebook 환경과 원격 SQL Server 및 Oracle 인스턴스에서 데이터에 쉽고 빠르게 액세스할 수 있는 새로운 외부 테이블 만들기 마법사를 포함하여 새로운 SQL Server 빅 데이터 환경을 제공했습니다.
