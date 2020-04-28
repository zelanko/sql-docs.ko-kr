---
title: 작업 단계 관리 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [SQL Server replication]
- job steps [SQL Server Agent]
- jobs [SQL Server Agent], Integration Services package step
- executable programs as job steps
- operating systems [SQL Server], job steps
- Transact-SQL job step
- job steps [Transact-SQL]
- Integration Services packages, job steps
- replication job steps [SQL Server]
- logs [SQL Server], jobs
- SQL Server Agent jobs, job steps
- ActiveX scripting jobs [SQL Server]
- job steps [Analysis Services]
ms.assetid: 51352afc-a0a4-428b-8985-f9e58bb57c31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 27dfa9f596d63021eb5f22b2e0b25a306e7fa2b5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798223"
---
# <a name="manage-job-steps"></a>작업 단계 관리
  작업 단계는 데이터베이스나 서버에서 작업이 수행하는 동작입니다. 모든 작업에는 작업 단계가 하나 이상 있어야 합니다. 작업 단계가 될 수 있는 항목은 다음과 같습니다.  
  
-   실행 프로그램 및 운영 체제 명령  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문(저장 프로시저 및 확장 저장 프로시저 포함)  
  
-   PowerShell 스크립트  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX 스크립트  
  
-   복제 태스크  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 태스크  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지  
  
 모든 작업 단계는 특정 보안 컨텍스트에서 실행됩니다. 작업 단계에서 프록시를 지정하면 해당 작업 단계는 프록시의 자격 증명 보안 컨텍스트에서 실행됩니다. 작업 단계에서 프록시를 지정하지 않으면 작업 단계는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정의 컨텍스트에서 실행됩니다. sysadmin 고정 서버 역할의 멤버만이 프록시를 명시적으로 지정하지 않는 작업을 만들 수 있습니다.  
  
 작업 단계는 특정 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자의 컨텍스트에서 실행되기 때문에 해당 사용자는 작업 단계를 실행하는 데 필요한 권한과 구성이 있어야 합니다. 예를 들어 드라이브 문자나 UNC(Universal Naming Convention) 경로가 필요한 작업을 만드는 경우 작업 단계는 태스크를 테스트하는 동안 사용자의 Windows 사용자 계정으로 실행됩니다. 그러나 해당 작업 단계의 Windows 사용자도 필요한 권한, 드라이브 문자 구성 또는 필요한 드라이브에 대한 액세스 권한이 있어야 합니다. 그렇지 않으면 작업 단계가 실패합니다. 이런 문제가 발생하지 않도록 각 작업 단계의 프록시에 작업 단계에서 수행하는 태스크에 필요한 권한이 있는지 확인하십시오. 자세한 내용은 [SQL Server 데이터베이스 엔진 및 Azure SQL Database에 대 한 Security Center](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)를 참조 하세요.  
  
## <a name="job-step-logs"></a>작업 단계 로그  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서는 일부 작업 단계의 출력을 운영 체제 파일이나 msdb 데이터베이스의 sysjobstepslogs 테이블에 기록할 수 있습니다. 다음은 두 대상에 모두 출력을 기록할 수 있는 작업 단계 유형입니다.  
  
-   실행 프로그램 및 운영 체제 명령  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 태스크  
  
 sysadmin 고정 서버 역할의 멤버인 사용자가 실행한 작업 단계만 작업 단계 출력을 운영 체제 파일에 기록할 수 있습니다. msdb 데이터베이스에서 SQLAgentUserRole, SQLAgentReaderRole 또는 SQLAgentOperatorRole 고정 데이터베이스 역할의 멤버인 사용자가 작업 단계를 실행할 경우 이러한 작업 단계의 출력은 sysjobstepslogs 테이블에만 기록할 수 있습니다.  
  
 작업이나 작업 단계가 삭제되면 자동으로 작업 단계 로그가 삭제됩니다.  
  
> [!NOTE]  
>  복제 태스크와 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 작업 단계 로깅은 해당 하위 시스템에서 처리됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 이러한 유형의 작업 단계에 대한 작업 단계 로깅을 구성할 수 없습니다.  
  
## <a name="executable-programs-and-operating-system-commands-as-job-steps"></a>실행 프로그램 및 운영 체제 명령을 작업 단계로 사용  
 실행 프로그램과 운영 체제 명령을 작업 단계로 사용할 수 있습니다. 이러한 파일의 확장명은 .bat, .cmd, .com 또는 .exe입니다.  
  
 실행 프로그램이나 운영 체제 명령을 작업 단계로 사용할 경우에는 다음을 지정해야 합니다.  
  
-   명령이 성공한 경우 반환되는 프로세스 종료 코드를 지정합니다.  
  
-   실행할 명령입니다. 운영 체제 명령을 실행하려면 명령 자체를 지정하면 되고 외부 프로그램을 실행하려면 프로그램 이름과 프로그램 인수를 지정합니다(예: **C:\Program Files\Microsoft SQL Server\100\Tools\Binn\sqlcmd.exe -e -q "sp_who"**).  
  
    > [!NOTE]  
    >  실행 파일이 시스템 경로나 작업 단계가 실행되는 계정의 사용자 경로에 지정된 디렉터리에 있지 않은 경우 실행 파일의 전체 경로를 지정해야 합니다.  
  
## <a name="transact-sql-job-steps"></a>Transact-SQL 작업 단계  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업 단계를 만들 때는 다음을 수행해야 합니다.  
  
-   작업을 실행하는 데이터베이스를 확인합니다.  
  
-   실행할 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 입력합니다. 이 문에서 저장 프로시저나 확장 저장 프로시저를 호출할 수 있습니다.  
  
 필요에 따라 기존의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 파일을 작업 단계에 대한 명령으로 열 수 있습니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업 단계에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시를 사용하지 않습니다. 대신에 작업 단계가 작업 단계 소유자의 계정으로 실행되거나 작업 단계 소유자가 sysadmin 고정 서버 역할의 멤버인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정으로 실행됩니다. sysadmin 고정 서버 역할의 멤버는 sp_add_jobstep 저장 프로시저의 [!INCLUDE[tsql](../../includes/tsql-md.md)] database_user_name *매개 변수를 사용하여* 작업 단계가 다른 사용자의 컨텍스트에서 실행되도록 지정할 수도 있습니다. 자세한 내용은 [sp_add_jobstep &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)를 참조 하세요.  
  
> [!NOTE]  
>  단일 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업 단계에는 다수의 일괄 처리가 여러 개 포함될 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업 단계에는 포함된 GO 명령이 있을 수 있습니다.  
  
## <a name="powershell-scripting-job-steps"></a>PowerShell 스크립팅 작업 단계  
 PowerShell 스크립트 작업 단계를 만들 때 다음 둘 중 하나를 단계에 대한 명령으로 지정해야 합니다.  
  
-   PowerShell 스크립트 텍스트  
  
-   열려는 기존 PowerShell 스크립트 파일  
  
 에이전트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] powershell 하위 시스템은 powershell 세션을 열고 powershell 스냅인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 로드 합니다. 작업 단계 명령으로 사용 되는 PowerShell 스크립트는 powershell 공급자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 cmdlet을 참조할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 스냅인을 사용하여 PowerShell 스크립트를 작성하는 방법에 대한 자세한 내용은 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)을 참조하세요.  
  
## <a name="activex-scripting-job-steps"></a>ActiveX 스크립팅 작업 단계  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이후 버전에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에이전트에서 ActiveX 스크립팅 작업 단계가 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.  
  
 ActiveX 스크립팅 작업 단계를 만들 때는 다음을 수행해야 합니다.  
  
-   작업 단계를 작성하는 스크립트 언어를 확인합니다.  
  
-   ActiveX 스크립트를 작성합니다.  
  
 기존 ActiveX 스크립트 파일을 작업 단계에 대한 명령으로 열 수도 있습니다. 또한 Microsoft Visual Basic 등을 사용하여 ActiveX 스크립트 명령을 외부에서 컴파일한 다음 실행 프로그램으로 실행할 수 있습니다.  
  
 작업 단계 명령이 ActiveX 스크립트이면 SQLActiveScriptHost 개체를 사용하여 출력을 작업 단계 기록 로그로 인쇄하거나 COM 개체를 만들 수 있습니다. SQLActiveScriptHost는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 호스팅 시스템에서 스크립트 네임스페이스로 도입되는 전역 개체입니다. 이 개체에는 두 가지 메서드(Print 및 CreateObject)가 포함됩니다. 다음 예에서는 VBScript(Visual Basic Scripting Edition)에서 ActiveX 스크립팅이 작동하는 방식을 보여 줍니다.  
  
```  
' VBScript example for ActiveX Scripting job step  
' Create a Dmo.Server object. The object connects to the  
' server on which the script is running.  
  
Set oServer = CreateObject("SQLDmo.SqlServer")  
oServer.LoginSecure = True  
oServer.Connect "(local)"  
'Disconnect and destroy the server object  
oServer.DisConnect  
Set oServer = nothing
```  
  
## <a name="replication-job-steps"></a>복제 작업 단계  
 복제를 사용하여 게시와 구독을 만드는 경우 기본적으로 복제 작업이 만들어집니다. 만들어지는 작업 유형은 복제 유형(스냅샷, 트랜잭션 또는 병합)과 사용되는 옵션에 따라 결정됩니다.  
  
 복제 작업 단계는 다음 복제 에이전트 중 하나를 활성화합니다.  
  
-   스냅샷 에이전트(Snapshot 작업)  
  
-   로그 판독기 에이전트(LogReader 작업)  
  
-   배포 에이전트(Distribution 작업)  
  
-   병합 에이전트(Merge 작업)  
  
-   큐 판독기 에이전트(QueueReader 작업)  
  
 복제를 설정할 때 복제 에이전트 실행 방법을 지정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 시작 후 복제 에이전트가 연속해서 실행되도록 하거나, 요청 시 실행하거나, 일정에 따라 실행하는 세 가지 방법이 있습니다. 복제 에이전트에 대한 자세한 내용은 [복제 에이전트 개요](../../relational-databases/replication/agents/replication-agents-overview.md)를 참조하세요.  
  
## <a name="analysis-services-job-steps"></a>Analysis Services 작업 단계  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 명령 작업 단계와 쿼리 작업 단계라는 서로 다른 유형의 두 가지 Analysis Services 작업 단계를 지원합니다.  
  
### <a name="analysis-services-command-job-steps"></a>Analysis Services 명령 작업 단계  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 명령 작업 단계를 만들 때는 다음을 수행해야 합니다.  
  
-   작업 단계를 실행할 데이터베이스 OLAP 서버를 확인합니다.  
  
-   실행할 문을 입력합니다. 문은 XML for [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] **Execute** 메서드여야 합니다. 전체 SOAP Envelope 또는 XML for [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] **Discover** 메서드를 포함할 수 없습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서는 전체 SOAP Envelope와 **Discover** 메서드를 지원하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계에서는 지원하지 않습니다.  
  
### <a name="analysis-services-query-job-steps"></a>Analysis Services 쿼리 작업 단계  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 쿼리 작업 단계를 만들 때는 다음을 수행해야 합니다.  
  
-   작업 단계를 실행할 데이터베이스 OLAP 서버를 확인합니다.  
  
-   실행할 문을 입력합니다. 이 문은 MDX(Multidimensional Expressions) 쿼리여야 합니다.  
  
 MDX에 대 한 자세한 내용은 [Mdx 쿼리 기본 사항 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services)를 참조 하세요.  
  
## <a name="integration-services-packages"></a>Integration Services 패키지  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 작업 단계를 만들 때는 다음을 수행해야 합니다.  
  
-   패키지 원본을 확인합니다.  
  
-   패키지 위치를 확인합니다.  
  
-   패키지에 구성 파일이 필요한 경우 구성 파일을 확인합니다.  
  
-   패키지에 명령 파일이 필요한 경우 명령 파일을 확인합니다.  
  
-   패키지에 사용할 확인 옵션을 지정합니다. 예를 들어 패키지에 서명이나 특정 패키지 ID가 필요하도록 지정할 수 있습니다.  
  
-   패키지의 데이터 원본을 확인합니다.  
  
-   패키지의 로그 공급자를 확인합니다.  
  
-   패키지를 실행하기 전에 설정할 변수와 값을 지정합니다.  
  
-   실행 옵션을 확인합니다.  
  
-   명령줄 옵션을 추가하거나 수정합니다.  
  
 SSIS 카탈로그에 패키지를 배포하고 패키지 원본으로 **SSIS 카탈로그** 를 지정한 경우 이러한 구성 정보의 상당 부분은 패키지에서 자동으로 가져옵니다. **구성** 탭에서 환경, 매개 변수 값, 연결 관리자 값, 속성 무효화 및 패키지가 32비트 런타임 환경에서 실행되는지 여부를 지정할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 실행하는 작업 단계 만들기에 대한 자세한 내용은 [패키지에 대한 SQL Server 에이전트 작업](../../integration-services/packages/sql-server-agent-jobs-for-packages.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
|||  
|-|-|  
|**설명**|**항목**|  
|실행 프로그램으로 작업 단계를 만드는 방법에 대해 설명합니다.|[CmdExec 작업 단계 만들기](create-a-cmdexec-job-step.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 사용 권한을 다시 설정하는 방법에 대해 설명합니다.|[Configure a User to Create and Manage SQL Server Agent Jobs](configure-a-user-to-create-and-manage-sql-server-agent-jobs.md)|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 작업 단계를 만드는 방법에 대해 설명합니다.|[Create a Transact-SQL Job Step](create-a-transact-sql-job-step.md)|  
|Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 Transact-SQL 작업 단계의 옵션을 정의하는 방법에 대해 설명합니다.|[Define Transact-SQL Job Step Options](define-transact-sql-job-step-options.md)|  
|ActiveX 스크립트 작업 단계를 만드는 방법에 대해 설명합니다.|[Create an ActiveX Script Job Step](create-an-activex-script-job-step.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Analysis Services 명령과 쿼리를 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계를 만들고 정의하는 방법에 대해 설명합니다.|[Create an Analysis Services Job Step](create-an-analysis-services-job-step.md)|  
|작업 실행 중에 오류가 발생하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 수행해야 하는 동작에 대해 설명합니다.|[Set Job Step Success or Failure Flow](set-job-step-success-or-failure-flow.md)|  
|작업 단계 속성 대화 상자에서 작업 단계의 세부 사항을 보는 방법에 대해 설명합니다.|[View Job Step Information](view-job-step-information.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계 로그를 삭제하는 방법에 대해 설명합니다.|[Delete a Job Step Log](delete-a-job-step-log.md)|  
  
## <a name="see-also"></a>참고 항목  
 [sysjobstepslogs &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/dbo-sysjobstepslogs-transact-sql)   
 [작업 만들기](create-jobs.md)   
 [sp_add_job&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql)  
