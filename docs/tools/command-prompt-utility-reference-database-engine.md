---
title: SQL 명령 프롬프트 유틸리티 (데이터베이스 엔진) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server]
- command prompt utilities [SQL Server], about command prompt utilities
- command prompt [SQL Server]
- utilities [SQL Server], command prompt
- command prompt [SQL Server], utilities
ms.assetid: 48364bd9-6ea7-45e9-a332-acf3d81bbfae
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 2b4dd847c828d18f30c161d9cfb1d8ab30e8ebb9
ms.sourcegitcommit: b4962530f90234017073b3fdd2248936b2de4e69
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71077532"
---
# <a name="sql-command-prompt-utilities-database-engine"></a>SQL 명령 프롬프트 유틸리티 (데이터베이스 엔진)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  명령 프롬프트 유틸리티를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 작업을 스크립트로 작성할 수 있습니다. 다음 표에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 제공하는 다양한 명령 프롬프트 유틸리티를 보여 줍니다.  

*기본* sql gui 및 명령줄 도구에 대 한 자세한 내용은 [sql 도구 개요](overview-sql-tools.md)를 참조 하세요.

  
|**유틸리티**|**설명**|**설치 위치**|  
|-----------------|---------------------|----------------------|  
|[bcp 유틸리티](../tools/bcp-utility.md)|[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스와 사용자가 지정한 형식의 데이터 파일 간에 데이터를 복사하는 데 사용합니다.|\<*드라이브*:>\Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[dta 유틸리티](../tools/dta/dta-utility.md)|작업을 분석하고 해당 작업에서 서버 성능을 최적화하기 위한 물리적 디자인 구조를 제시하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[dtexec 유틸리티](../integration-services/packages/dtexec-utility.md)|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 구성 및 실행하는 데 사용합니다. 이 명령 프롬프트 유틸리티의 사용자 인터페이스 버전을 **DTExecUI**라고 하며 이는 패키지 실행 유틸리티를 표시합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[dtutil 유틸리티](../integration-services/dtutil-utility.md)|SSIS 패키지를 관리하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[배포 유틸리티를 사용하여 모델 솔루션 배포](https://docs.microsoft.com/analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility)|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 프로젝트를 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스에 배포하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VShell\Common7\IDE|   
|[osql 유틸리티](../tools/osql-utility.md)|명령 프롬프트에서 [!INCLUDE[tsql](../includes/tsql-md.md)] 문, 시스템 프로시저 및 스크립트 파일을 입력할 수 있습니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[프로파일러 유틸리티](../tools/profiler-utility.md)|명령 프롬프트에서 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 를 시작하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[RS.exe 유틸리티&#40;SSRS&#41;](../reporting-services/tools/rs-exe-utility-ssrs.md)|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 보고서 서버를 관리하기 위한 스크립트를 실행하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rsconfig 유틸리티&#40;SSRS&#41;](../reporting-services/tools/rsconfig-utility-ssrs.md)|보고서 서버 연결을 구성하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rskeymgmt 유틸리티&#40;SSRS&#41;](../reporting-services/tools/rskeymgmt-utility-ssrs.md)|보고서 서버에서 암호화 키를 관리하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 애플리케이션](../tools/sqlagent90-application.md)|명령 프롬프트에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트를 시작하는 데 사용합니다.|\<드라이브>:\Program Files\Microsoft SQL Server\\<*instance_name*>\MSSQL\Binn|  
|[sqlcmd 유틸리티](../tools/sqlcmd-utility.md)|명령 프롬프트에서 [!INCLUDE[tsql](../includes/tsql-md.md)] 문, 시스템 프로시저 및 스크립트 파일을 입력할 수 있습니다.|\<*드라이브*:>\Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[SQLdiag 유틸리티](../tools/sqldiag-utility.md)|[!INCLUDE[msCoName](../includes/msconame-md.md)] 고객 서비스 지원 센터에 제공할 진단 정보를 수집하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqllogship 애플리케이션](../tools/sqllogship-application.md)|애플리케이션에서 백업, 복사 및 복원 작업을 실행하지 않고 로그 전달 구성에 대해 백업, 복사, 복원 작업 및 관련 정리 태스크를 수행하는 데 사용됩니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SqlLocalDB 유틸리티](../tools/sqllocaldb-utility.md)|프로그램 개발자를 대상으로 하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 실행 모드입니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlmaint 유틸리티](../tools/sqlmaint-utility.md)|이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 만든 데이터베이스 유지 관리 계획을 실행하는 데 사용합니다.|\<드라이브>:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn|  
|[sqlps 유틸리티](../tools/sqlps-utility.md)|PowerShell 명령 및 스크립트를 실행하는 데 사용합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 공급자 및 cmdlet을 로드하고 등록합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr 애플리케이션](../tools/sqlservr-application.md)|문제 해결을 위해 명령 프롬프트에서 [!INCLUDE[ssDE](../includes/ssde-md.md)] 인스턴스를 시작 및 중지하는 데 사용합니다.|\<드라이브>:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn|  
|[Ssms 유틸리티](../tools/sql-server-management-studio/ssms-utility.md)|명령 프롬프트에서 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 시작하는 데 사용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VSShell\Common7\IDE|  
|[tablediff 유틸리티](../tools/tablediff-utility.md)|두 테이블의 데이터를 비교하여 불일치가 있는지 확인하는 데 사용합니다. 복제 토폴로지 문제를 해결할 때 유용합니다.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]COM|  

## <a name="command-prompt-utilities-syntax-conventions"></a>명령 프롬프트 유틸리티 구문 규칙  
  
|**규칙**|**사용 대상**|  
|--------------------|------------------|  
|대문자|운영 체제 수준에서 사용하는 문 및 용어|  
|`monospace`|예제 명령 및 프로그램 코드|  
|*기울임꼴*|사용자가 제공하는 매개 변수|  
|**굵게**|표시된 대로 입력해야 하는 명령, 매개 변수 및 다른 구문|  
  
## <a name="see-also"></a>참고 항목  
 [복제 배포 에이전트](../relational-databases/replication/agents/replication-distribution-agent.md)   
 [복제 로그 판독기 에이전트](../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [복제 병합 에이전트](../relational-databases/replication/agents/replication-merge-agent.md)   
 [복제 큐 판독기 에이전트](../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
