---
title: SQL 도구 및 SQL Server, Azure SQL 데이터베이스 및 Azure SQL 데이터 웨어하우스 유틸리티 | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: misc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ''
caps.latest.revision: 0
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 295704322a3ddb1e630c9dafbdf1ebcf37fdefad
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="sql-tools-and-utilities-for-sql-server-azure-sql-database-and-azure-sql-data-warehouse"></a>SQL 도구 및 SQL Server, Azure SQL 데이터베이스 및 Azure SQL 데이터 웨어하우스 유틸리티
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

(쿼리, 모니터 등)을 관리 하려면 데이터베이스 도구가 필요 합니다. 사용 가능한 몇 가지 데이터베이스 도구가 있습니다. 데이터베이스 또는 windows에서는 클라우드에서 실행 될 수 있습니다 하는 동안 [Linux](../linux/sql-server-linux-overview.md), 데이터베이스와 동일한 플랫폼에서 실행 되도록 도구에 필요 하지 않습니다. 

이 문서에서는 SQL 데이터베이스 작업에 사용 가능한 도구에 대 한 정보를 제공 합니다. 


## <a name="tools-to-run-queries-and-manage-databases"></a>쿼리를 실행 하 고 데이터베이스 관리 도구  

| 도구 | Description |
|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)] 실행 하는 경우 항상 데이터베이스 관리를 위한 무료, 간단한 도구입니다. 이 미리 보기 릴리스에서 확장 된 TRANSACT-SQL 편집기와 데이터베이스의 작동 상태에 대 한 사용자 지정 가능한 정보를 포함 하 여 데이터베이스 관리 기능을 제공 합니다. **[!INCLUDE[name-sos](../includes/name-sos-short.md)] Windows, macOS 등 및 Linux에서 실행**합니다.|
| [SSMS(SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) | SQL Server Management Studio (SSMS)를 사용 하 여 쿼리를 디자인 하 고 SQL Server, Azure SQL 데이터베이스 및 Azure SQL 데이터 웨어하우스 관리. **Windows에서 실행 되는 SSMS**합니다.|
| [SSDT(SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md) | SQL Server, Azure SQL 데이터베이스 및 Azure SQL 데이터 웨어하우스에 대 한 강력한 개발 환경으로 Visual Studio를 설정 합니다. **Windows에서 실행 되는 SSDT**합니다.|
|[mssql cli](mssql-cli.md)|mssql cli에는 SQL Server를 쿼리 하기 위한 대화형 명령줄 도구는 합니다. **mssql cli Windows, macOS 등 및 Linux에서 실행**|
| [Visual Studio Code](https://code.visualstudio.com/)| Visual Studio Code를 설치 하면 설치 여 [확장명이 mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) Microsoft SQL Server, Azure SQL 데이터베이스 및 SQL 데이터 웨어하우스를 개발 하기 위한 합니다. **Visual Studio 코드 창, macOS 등 및 Linux에서 실행**합니다.|

## <a name="which-tool-should-i-choose"></a>도구를 선택 해야 합니까?

- SQL Server 인스턴스 또는 데이터베이스에서 Windows, Linux 또는 Mac에서 간단한 편집기에서 관리 하 시겠습니까? [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) 선택
- SQL Server 인스턴스 또는 전체 GUI 지 원하는 Windows에서 데이터베이스를 관리 하 시겠습니까? [SSMS(SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) 선택
- 만들거나 데이터베이스 코드를 컴파일 타임 유효성 검사를 포함 하 여 유지 관리 하려는 리팩터링 및 디자이너를 Windows에서 지원? [SSDT(SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md) 선택
- IntelliSense, 구문 높은 조명 옵션이 있는 명령줄 도구를 SQL Server에 쿼리할 원하는 등? 선택 [mssql cli](mssql-cli.md)
- Windows, Linux 또는 Mac에서 간단한 편집기에서 T-SQL 스크립트를 작성 하 시겠습니까? 선택 [Visual Studio Code](https://code.visualstudio.com/) 및 [mssql 확장](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="additional-tools"></a>추가 도구

| 도구 | Description |
|:--|:--|
| [구성 관리자](../tools/configuration-manager/sql-server-configuration-manager-help.md) | SQL Server 구성 관리자 SQL Server 서비스를 구성 하 고 네트워크 연결을 구성을 사용 하 고 있습니다. Windows에서 실행 되는 configuration Manager|
|[mssql conf](../linux/sql-server-linux-configure-mssql-conf.md)|Mssql conf를 사용 하 여 Linux에서 실행 중인 SQL Server를 구성 합니다.|
| [SQL Server Migration Assistant](../ssma/sql-server-migration-assistant.md) | SQL Server Migration Assistant를 사용하여 Microsoft Access, DB2, MySQL, Oracle 및 Sybase에서 SQL Server로 데이터베이스를 마이그레이션하는 작업을 자동화할 수 있습니다.|
| [Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md) | Distributed Replay 기능을 사용 하 여 향후 SQL Server 업그레이드의 영향을 쉽게 평가할 수 있도록 합니다. 하드웨어와 운영 체제 업그레이드 및 SQL Server 튜닝에 따르는 영향도 쉽게 평가할 Distributed Replay를 사용할 수도 있습니다. |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | Ssbdiagnose 유틸리티는 Service Broker 서비스를 구성 하거나 Service Broker 대화의 문제를 보고합니다. |


## <a name="command-line-utilities"></a>명령줄 유틸리티

  명령줄 유틸리티를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 작업을 스크립트로 작성할 수 있습니다. 다음 표에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 제공하는 명령 프롬프트 유틸리티를 보여 줍니다.  
  
|**유틸리티**|**설명**|**설치 위치**|  
|-----------------|---------------------|----------------------|  
|[bcp 유틸리티](../tools/bcp-utility.md)|[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스와 사용자가 지정한 형식의 데이터 파일 간에 데이터를 복사하는 데 사용합니다.|\<*드라이브*:>\Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[dta 유틸리티](../tools/dta/dta-utility.md)|작업을 분석하고 해당 작업에서 서버 성능을 최적화하기 위한 물리적 디자인 구조를 제시하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[dtexec 유틸리티](../integration-services/packages/dtexec-utility.md)|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 구성 및 실행하는 데 사용합니다. 이 명령 프롬프트 유틸리티의 사용자 인터페이스 버전을 **DTExecUI**라고 하며 이는 패키지 실행 유틸리티를 표시합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[dtutil 유틸리티](../integration-services/dtutil-utility.md)|SSIS 패키지를 관리하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[배포 유틸리티를 사용하여 모델 솔루션 배포](../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트를 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스에 배포하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VShell\Common7\IDE|  
|[mssql-scripter (공개 미리 보기)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/17/try-new-sql-server-command-line-tools-to-generate-t-sql-scripts-and-monitor-dynamic-management-views/)|SQL Server, Azure SQL 데이터베이스 및 Azure SQL 데이터 웨어하우스의 데이터베이스 개체에 대 한 CREATE 및 삽입 T-SQL 스크립트를 생성 하는 데 사용 합니다.|참조 우리의 [GitHub 리포지토리](https://github.com/Microsoft/sql-xplat-cli) 다운로드 및 사용 정보에 대 한 합니다.| 
|[osql 유틸리티](../tools/osql-utility.md)|명령 프롬프트에서 [!INCLUDE[tsql](../includes/tsql-md.md)] 문, 시스템 프로시저 및 스크립트 파일을 입력할 수 있습니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[프로파일러 유틸리티](../tools/profiler-utility.md)|명령 프롬프트에서 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 를 시작하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[RS.exe 유틸리티&#40;SSRS&#41;](../reporting-services/tools/rs-exe-utility-ssrs.md)|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 서버를 관리하기 위한 스크립트를 실행하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rsconfig 유틸리티&#40;SSRS&#41;](../reporting-services/tools/rsconfig-utility-ssrs.md)|보고서 서버 연결을 구성하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rskeymgmt 유틸리티&#40;SSRS&#41;](../reporting-services/tools/rskeymgmt-utility-ssrs.md)|보고서 서버에서 암호화 키를 관리하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 응용 프로그램](../tools/sqlagent90-application.md)|명령 프롬프트에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트를 시작하는 데 사용합니다.|\<드라이브>:\Program Files\Microsoft SQL Server\\<*instance_name*>\MSSQL\Binn|  
|[sqlcmd 유틸리티](../tools/sqlcmd-utility.md)|명령 프롬프트에서 [!INCLUDE[tsql](../includes/tsql-md.md)] 문, 시스템 프로시저 및 스크립트 파일을 입력할 수 있습니다.|\<*드라이브*:>\Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[SQLdiag 유틸리티](../tools/sqldiag-utility.md)|[!INCLUDE[msCoName](../includes/msconame-md.md)] 고객 서비스 지원 센터에 제공할 진단 정보를 수집하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqllogship 응용 프로그램](../tools/sqllogship-application.md)|응용 프로그램에서 백업, 복사 및 복원 작업을 실행하지 않고 로그 전달 구성에 대해 백업, 복사, 복원 작업 및 관련 정리 태스크를 수행하는 데 사용됩니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SqlLocalDB 유틸리티](../tools/sqllocaldb-utility.md)|프로그램 개발자를 대상으로 하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 실행 모드입니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\|  
|[sqlmaint 유틸리티](../tools/sqlmaint-utility.md)|이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 만든 데이터베이스 유지 관리 계획을 실행하는 데 사용합니다.|\<드라이브>:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn|  
|[sqlps 유틸리티](../tools/sqlps-utility.md)|PowerShell 명령 및 스크립트를 실행하는 데 사용합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 공급자 및 cmdlet을 로드하고 등록합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr 응용 프로그램](../tools/sqlservr-application.md)|문제 해결을 위해 명령 프롬프트에서 [!INCLUDE[ssDE](../includes/ssde-md.md)] 인스턴스를 시작 및 중지하는 데 사용합니다.|\<드라이브>:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn|  
|[Ssms 유틸리티](../tools/sql-server-management-studio/ssms-utility.md)|명령 프롬프트에서 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 시작하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VSShell\Common7\IDE|  
|[tablediff 유틸리티](../tools/tablediff-utility.md)|두 테이블의 데이터를 비교하여 불일치가 있는지 확인하는 데 사용합니다. 복제 토폴로지 문제를 해결할 때 유용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]COM|  

## <a name="sql-command-prompt-utilities-syntax-conventions"></a>SQL 명령 프롬프트 유틸리티 구문 표기 규칙  
  
|**규칙**|**사용 대상**|  
|--------------------|------------------|  
|대문자|운영 체제 수준에서 사용하는 문 및 용어|  
|`monospace`|예제 명령 및 프로그램 코드|  
|*기울임꼴*|사용자가 제공하는 매개 변수|  
|**굵게**|표시된 대로 입력해야 하는 명령, 매개 변수 및 다른 구문|  



