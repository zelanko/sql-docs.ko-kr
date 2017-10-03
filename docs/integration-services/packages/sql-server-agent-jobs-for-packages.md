---
title: "패키지에 대 한 SQL Server 에이전트 작업 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [Integration Services]
- automatic package execution
- scheduling packages [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: ecf7a5f9-b8a7-47f1-9ac0-bac07cb89e31
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 2cb08ab16291e87a25eb2596f75f4d01616a80db
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="sql-server-agent-jobs-for-packages"></a>패키지에 대한 SQL Server 에이전트 작업
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 실행을 자동화하고 예약할 수 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소 및 파일 시스템에 저장된 패키지를 예약할 수 있습니다.  
  
## <a name="sections-in-this-topic"></a>이 항목의 섹션  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [SQL Server 에이전트에서 작업 예약](#jobs)  
  
-   [Integration Services 패키지 일정 예약](#packages)  
  
-   [예약 패키지 문제 해결](#trouble)  
  
##  <a name="jobs"></a> Scheduling Jobs in SQL Server Agent  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 실행하여 태스크를 자동화 및 예약할 수 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 설치하는 서비스입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 실행되고 있어야만 작업이 자동으로 실행될 수 있습니다. 자세한 내용은 [Configure SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/configure-sql-server-agent)을 참조하세요.  
  
 **SQL Server 에이전트** 노드는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 인스턴스에 연결하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 개체 탐색기에 표시됩니다.  
  
 되풀이 태스크를 자동화하려면 **새 작업** 대화 상자를 사용하여 작업을 만들어야 합니다. 자세한 내용은 [작업 구현](https://docs.microsoft.com/sql/ssms/agent/implement-jobs)을 참조하세요.  
  
 작업을 만든 후 하나 이상의 단계를 추가해야 합니다. 한 개의 작업은 각각 다른 태스크를 수행하는 여러 단계를 포함할 수 있습니다. 자세한 내용은 [Manage Job Steps](https://docs.microsoft.com/sql/ssms/agent/manage-job-steps)을(를) 참조하세요.  
  
 작업 및 작업 단계를 만든 다음에는 작업을 실행하는 일정을 만들 수 있습니다. 그러나 수동으로 실행되는 예약되지 않은 작업도 만들 수 있습니다. 자세한 내용은 [일정을 만들고 작업에 연결](https://docs.microsoft.com/sql/ssms/agent/create-and-attach-schedules-to-jobs)을 참조하세요.  
  
 작업을 종료하거나 경고를 추가할 때 전자 메일 메시지를 보낼 운영자를 지정하는 등의 알림 옵션 설정으로 작업을 향상시킬 수 있습니다. 자세한 내용은 [경고](https://docs.microsoft.com/sql/ssms/agent/alerts)를 참조하세요.  
  
##  <a name="packages"></a> Scheduling Integration Services Packages  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 만들어 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 예약한 경우 **SQL Server Integration Services 패키지**에 하나 이상의 단계를 추가하고 단계 유형을 설정해야 합니다. 한 개의 작업은 각각 다른 패키지를 실행하는 여러 단계를 포함할 수 있습니다.  
  
 작업 단계에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 실행하는 것은 **dtexec** (dtexec.exe) 및 **DTExecUI** (dtexecui.exe) 유틸리티를 사용하여 패키지를 실행하는 것과 비슷합니다. 명령줄 옵션 또는 **패키지 실행 유틸리티** 대화 상자를 사용하여 패키지의 런타임 옵션을 설정하는 대신 **새 작업 단계** 대화 상자에서 런타임 옵션을 설정할 수 있습니다. 패키지를 실행하는 옵션에 대한 자세한 내용은 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)를 참조하십시오.  
  
 자세한 내용은 [SQL Server 에이전트를 사용하여 패키지 예약](#schedule)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 패키지를 실행하는 방법을 보여 주는 비디오는 MSDN Library의 비디오 홈 페이지에서 [방법: SQL Server 에이전트를 사용하여 패키지 실행 자동화(SQL Server 비디오)](http://go.microsoft.com/fwlink/?LinkId=141771)를 참조하세요.  
  
##  <a name="trouble"></a> 문제 해결  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 커맨드 라인에서 패키지가 성공적으로 실행되더라도 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에이전트 작업 단계를 시작하지 못할 수 있습니다. 이 문제에 대한 몇 가지 일반적인 이유와 권장 솔루션이 있습니다. 자세한 내용은 다음 리소스를 참조하십시오.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 기술 자료 문서 - [SQL Server 에이전트 작업 단계에서 SSIS 패키지를 호출할 때 SSIS 패키지가 실행되지 않는다](http://support.microsoft.com/kb/918760)  
  
-   MSDN Library의 비디오 - [문제 해결: SQL Server 에이전트를 사용하여 패키지 실행(SQL Server 비디오)](http://go.microsoft.com/fwlink/?LinkId=141772)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계에서 패키지를 시작한 후에 패키지 실행이 실패하거나 패키지가 성공적으로 실행되더라도 예기치 않은 결과가 발생할 수 있습니다. 이 문제를 해결하려면 다음 도구를 사용합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] MSDB 데이터베이스, [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소 또는 로컬 컴퓨터의 폴더에 저장된 패키지는 **로그 파일 뷰어** 뿐만 아니라 패키지 실행 중 생성된 로그 및 디버그 덤프 파일을 사용할 수 있습니다.  
  
     **로그 파일 뷰어를 사용하려면 다음을 수행합니다.**  
  
    1.  개체 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 마우스 오른쪽 단추로 누르고 **기록 보기**를 클릭합니다.  
  
    2.  **메시지** 열에 **작업이 실패했습니다.** 메시지가 있는 **로그 파일 요약** 상자에서 작업 실행을 찾습니다.  
  
    3.  작업 노드를 확장하고 작업 단계를 클릭하여 **로그 파일 요약** 상자 아래 영역에서 메시지의 세부 정보를 봅니다.  
  
-   SSISDB 데이터베이스에 저장된 패키지에 대해서도 **로그 파일 뷰어** 뿐만 아니라 패키지 실행 중 생성된 로그 및 디버그 덤프 파일을 사용할 수 있습니다. 또한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 대한 보고서를 사용할 수도 있습니다.  
  
     **보고서에서 작업 실행과 연결된 패키지 실행에 대한 정보를 찾으려면 다음을 수행합니다.**  
  
    1.  위의 단계별 지침에 따라 작업 단계에 대한 자세한 메시지를 봅니다.  
  
    2.  메시지에 나열된 실행 ID를 찾습니다.  
  
    3.  개체 탐색기에서 Integration Services 카탈로그 노드를 확장합니다.  
  
    4.  SSISDB를 마우스 오른쪽 단추로 클릭하고 보고서, 표준 보고서를 차례로 가리킨 다음 모든 실행을 클릭합니다.  
  
    5.  **모든 실행** 보고서의 **ID** 열에서 실행 ID를 찾습니다. 패키지 실행에 대한 정보를 보려면 **개요**, **모든 메시지**또는 **실행 성능** 을 클릭합니다.  
  
    개요, 모든 메시지 및 실행 성능 보고서에 대한 자세한 내용은 [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)를 참조합니다.  

## <a name="schedule"></a> SQL Server 에이전트를 사용하여 패키지 예약
  다음 절차에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계를 통해 패키지 실행을 자동화하여 패키지를 실행하는 단계를 제공합니다.  
  
### <a name="to-automate-package-execution-by-using-sql-server-agent"></a>SQL Server 에이전트를 사용하여 패키지 실행을 자동화하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 작업을 만들려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 또는 단계를 추가하려는 작업을 포함하는 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 노드를 확장하고 다음 태스크 중 하나를 수행합니다.  
  
    -   새 작업을 추가하려면 **작업** 을 마우스 오른쪽 단추로 클릭한 다음 **새 작업**을 클릭합니다.  
  
    -   기존 작업에 단계를 추가하려면 **작업**을 확장하고 해당 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  새 작업을 만드는 경우 **일반** 페이지에서 작업 이름을 지정하고 소유자 및 작업 범주를 선택한 다음 필요에 따라 작업 설명을 지정합니다.  
  
4.  작업을 예약할 수 있게 설정하려면 **사용**을 선택합니다.  
  
5.  예약하려는 패키지에 대한 작업 단계를 만들려면 **단계**를 클릭한 다음 **새로 만들기**를 클릭합니다.  
  
6.  작업 단계 유형에 대한 **Integration Services 패키지** 를 선택합니다.  
  
7.  **다음 계정으로 실행** 목록에서 **SQL Server 에이전트 서비스 계정** 을 선택하거나 작업 단계에 사용될 자격 증명이 있는 프록시 계정을 선택합니다. 프록시 계정을 만드는 방법은 [Create a SQL Server Agent Proxy](http://msdn.microsoft.com/library/142e0c55-a8b9-4669-be49-b9dc602d5988)를 참조하십시오.  
  
     **SQL Server 에이전트 서비스 계정** 대신 프록시 계정을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 패키지를 실행할 때 발생할 수 있는 일반적인 문제를 해결할 수 있습니다. 이들 문제에 대한 자세한 정보는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 기술 자료 문서 [SQL Server 에이전트 작업 단계에서 SSIS 패키지를 호출할 때 SSIS 패키지가 실행되지 않는다](http://support.microsoft.com/kb/918760)를 참고하십시오.  
  
    > **참고:** 프록시 계정에 사용하는 자격 증명의 암호가 변경되면 자격 증명 암호를 업데이트해야 합니다. 그렇지 않으면 작업 단계가 실패합니다.  
  
     SQL Server 에이전트 서비스 계정을 구성하는 방법에 대한 자세한 내용은 [SQL Server 에이전트의 서비스 시작 계정 설정&#40;SQL Server 구성 관리자&#41;](http://msdn.microsoft.com/library/46ffe818-ebb5-43a0-840b-923f219a2472)을 참조하세요.  
  
8.  **패키지 원본** 목록 상자에서 패키지의 원본을 클릭하고 작업 단계의 옵션을 구성합니다.  
  
     **다음 표에서는 패키지 원본에 대해 설명합니다.**  
  
    |패키지 원본|Description|  
    |--------------------|-----------------|  
    |**SSIS 카탈로그**|SSISDB 데이터베이스에 저장된 패키지입니다. 패키지는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포되는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트에 포함됩니다.|  
    |**SQL Server**|MSDB 데이터베이스에 저장된 패키지입니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 사용하여 패키지를 관리합니다.|  
    |**SSIS 패키지 저장소**|컴퓨터의 기본 폴더에 저장된 패키지입니다. 기본 폴더는  *\<드라이브 >*: files\microsoft SQL Server\110\DTS\Packages입니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스를 사용하여 패키지를 관리합니다.<br /><br /> 참고: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 의 구성 파일을 수정하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]서비스에서 관리할 파일 시스템에 추가로 폴더를 지정하거나 다른 폴더를 지정할 수 있습니다. 자세한 내용은 [Integration Services 서비스&#40;SSIS 서비스&#41;](../../integration-services/service/integration-services-service-ssis-service.md)를 참조하세요.|  
    |**파일 시스템**|컴퓨터의 임의 폴더에 저장된 패키지입니다.|  
  
     **다음 표에서는 선택한 패키지 원본에 따라 작업 단계에 사용할 수 있는 구성 옵션을 설명합니다.**  
  
    > **중요:** 패키지가 암호로 보호된 경우 **새 작업 단계** 대화 상자의 **일반** 페이지에 있는 탭( **패키지** 탭 제외)을 클릭하면 표시되는 **패키지 암호** 대화 상자에 암호를 입력해야 합니다. 그렇지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업은 패키지 실행에 실패합니다.  
  
     **패키지 원본**: SSIS 카탈로그  
  
    |탭|옵션|  
    |---------|-------------|  
    |**패키지**|**Server**<br /><br /> SSISDB 카탈로그를 호스팅하는 데이터베이스 서버 인스턴스의 이름을 입력하거나 선택합니다.<br /><br /> **SSIS 카탈로그** 가 패키지 원본이면 Microsoft Windows 사용자 계정을 사용하여 서버에 로그온할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용할 수 없습니다.|  
    ||**패키지**<br /><br /> 줄임표 단추를 클릭하고 패키지를 선택합니다.<br /><br /> **개체 탐색기** 에서 **Integration Services 카탈로그**노드의 하위 폴더에 있는 패키지를 선택합니다.|  
    |**매개 변수**<br /><br /> **구성** 탭에 위치합니다.|**Integration Services 프로젝트 변환 마법사** 를 사용하면 매개 변수로 패키지 구성을 바꿀 수 있습니다.<br /><br /> **매개 변수** 탭은 패키지를 디자인할 때 추가한 매개 변수를 표시합니다. 이때 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 사용하는 것도 방법이 될 수 있습니다. 탭은 패키지 배포 모델에서 프로젝트 배포 모델로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 변환할 때 패키지에 추가된 매개 변수도 표시합니다. 패키지에 포함된 매개 변수의 새 값을 입력합니다. 리터럴 값을 입력하거나 이미 매개 변수에 매핑한 서버 환경 변수에 포함된 값을 사용할 수 있습니다.<br /><br /> 리터럴 값을 입력하려면 매개 변수 옆에 있는 줄임표 단추를 클릭합니다. **실행할 리터럴 값 편집** 대화 상자가 나타납니다.<br /><br /> 환경 변수를 사용하려면 **환경** 을 클릭한 다음 사용하려는 변수를 포함하는 환경을 선택합니다.<br /><br /> **\*\* 중요 \*\*** 여러 환경에 포함된 변수에 여러 매개 변수 및/또는 연결 관리자 속성을 매핑하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 오류 메시지를 표시합니다. 지정된 실행의 경우 패키지는 단일 서버 환경에 포함된 값만으로 실행할 수 있습니다.<br /><br /> 서버 환경 만들기 및 지도 매개 변수로 대체 하는 방법에 대 한 정보를 참조 하십시오. [배포할 Integration Services (SSIS) 프로젝트 및 패키지](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)합니다.|  
    |**연결 관리자**<br /><br /> **구성** 탭에 위치합니다.|연결 관리자 속성의 값을 변경합니다. 예를 들어 서버 이름을 변경할 수 있습니다. 연결 관리자 속성에 대한 매개 변수가 SSIS 서버에 자동으로 생성됩니다. 속성 값을 변경하려면 리터럴 값을 입력하거나 이미 연결 관리자 속성에 매핑한 서버 환경 변수에 포함된 값을 사용할 수 있습니다.<br /><br /> 리터럴 값을 입력하려면 매개 변수 옆에 있는 줄임표 단추를 클릭합니다. **실행할 리터럴 값 편집** 대화 상자가 나타납니다.<br /><br /> 환경 변수를 사용하려면 **환경** 을 클릭한 다음 사용하려는 변수를 포함하는 환경을 선택합니다.<br /><br /> **\*\* 중요 \*\*** 여러 환경에 포함된 변수에 여러 매개 변수 및/또는 연결 관리자 속성을 매핑하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 오류 메시지를 표시합니다. 지정된 실행의 경우 패키지는 단일 서버 환경에 포함된 값만으로 실행할 수 있습니다.<br /><br /> 서버 환경을 만들고 연결 관리자 속성에 매핑하면 변수에 하는 방법에 대 한 정보를 참조 하십시오. [배포할 Integration Services (SSIS) 프로젝트 및 패키지](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)합니다.|  
    |**고급**<br /><br /> **구성** 탭에 위치합니다.|패키지 실행에 대해 다음과 같은 추가 설정을 구성합니다.|  
    ||**속성 재정의**:<br /><br /> 패키지 속성에 대한 새 값을 입력하고, 속성 경로를 지정하고, 속성 값이 중요한지 여부를 나타내려면 **추가** 를 클릭합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버는 중요한 데이터를 암호화합니다. 속성에 대한 설정을 편집하거나 제거하려면 **속성** 재정의 상자의 행을 클릭한 다음 **편집** 이나 **제거**를 클릭합니다. 다음 중 하나를 수행하여 속성 경로를 찾을 수 있습니다.<br /><br /> -XML 구성 파일(\*.dtsconfig)에서 속성 경로를 복사합니다. 경로는 파일의 구성 섹션에 경로 속성의 값으로 나열됩니다. MaximumErrorCount 속성에 대한 경로의 예는 \Package.Properties[MaximumErrorCount]와 같습니다.<br /><br /> - **패키지 구성 마법사** 를 실행하고 마지막 **마법사 완료** 페이지에서 속성 경로를 복사합니다. 그런 다음 마법사를 취소할 수 있습니다.<br /><br /> <br /><br /> 참고: **속성 재정의** 옵션은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 이전 릴리스에서 업그레이드된 구성을 포함하는 패키지용입니다. [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 를 사용하여 만들고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포한 패키지는 구성 대신 매개 변수를 사용합니다.|  
    ||**로깅 수준**<br /><br /> 패키지 실행에 대해 다음 로깅 수준 중 하나를 선택합니다. **성능** 또는 **자세한 정보** 로깅 수준을 선택하면 패키지 실행 성능에 영향을 줄 수 있습니다.<br /><br /> **없음**:<br />                          로깅이 해제됩니다. 패키지 실행 상태에만 기록됩니다.<br /><br /> **기본**:<br />                          사용자 지정 이벤트 및 진단 이벤트 외의 모든 이벤트가 기록됩니다. 로깅 수준의 기본값입니다.<br /><br /> **성능**:<br />                          성능 통계와 OnError 및 OnWarning 이벤트만 기록됩니다.<br /><br /> **자세한 정보**:<br />                          사용자 지정 이벤트 및 진단 이벤트를 포함한 모든 이벤트가 기록됩니다.<br /><br /> 선택한 로깅 수준은 SSISDB 보기 및 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 대한 보고서에 표시될 정보를 결정합니다. 자세한 내용은 [SSIS(Integration Services) 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.|  
    ||**오류 덤프**<br /><br /> 패키지 실행 시 오류가 발생할 때 덤프 파일을 생성할지 여부를 지정합니다. 이 파일은 문제를 해결하는 데 도움이 될 수 있는 패키지 실행에 대한 정보를 제공합니다. 이 옵션을 선택하고 실행 중에 오류가 발생하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 .mdmp 파일(이진 파일) 및 .tmp 파일(텍스트 파일)을 만듭니다. 기본적으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 파일을 저장 된  *\<드라이브 >:*files\microsoft SQL Server\110\Shared\ErrorDumps 폴더입니다.|  
    ||**32비트 런타임**<br /><br /> 64비트 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 설치된 64비트 컴퓨터에서 32비트 버전의 dtexec 유틸리티를 사용하는 패키지의 실행 여부를 나타냅니다.<br /><br /> 예를 들어 64비트 버전에서 사용할 수 없는 네이티브 OLE DB 공급자를 패키지에서 사용하는 경우 32비트 버전의 dtexec를 사용하여 패키지를 실행해야 합니다. 자세한 내용은 [Integration Services에 대한 64비트 고려 사항](http://msdn.microsoft.com/library/ms141766\(SQL.105\).aspx)을 참조하십시오.<br /><br /> 기본적으로 **SQL Server Integration Services 패키지** 작업 단계 유형을 선택하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 시스템에서 자동으로 호출된 dtexec 유틸리티 버전을 사용하여 패키지를 실행합니다. 시스템은 컴퓨터 프로세서와 컴퓨터에서 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 버전에 따라 32비트 또는 64비트 버전 유틸리티를 호출합니다.|  
  
     **패키지 원본**: SQL서버, SSIS 패키지 저장소 또는 파일 시스템  
  
     패키지에 설정하는 대부분의 옵션이 SQL Server, SSIS 패키지 저장소 또는 파일 시스템에 저장되며 **dtexec** 명령 프롬프트 유틸리티의 명령줄 옵션에 해당합니다. 유틸리티와 명령줄 옵션에 대한 자세한 내용은 [dtexec 유틸리티](../../integration-services/packages/dtexec-utility.md)를 참조하세요.  
  
    |탭|옵션|  
    |---------|-------------|  
    |**패키지**<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소에 저장된 패키지의 탭 옵션입니다.|**Server**<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서비스에 대해 데이터베이스 서버 인스턴스의 이름을 입력하거나 선택합니다.|  
    ||**Windows 인증 사용**<br /><br /> Microsoft Windows 사용자 계정으로 서버에 로그온하려면 이 옵션을 선택합니다.|  
    ||**SQL Server 인증 사용**<br /><br /> 사용자가 지정한 로그인 이름과 암호를 사용하여 트러스트되지 않은 연결로부터 연결하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 계정이 설정되었는지 및 지정한 암호가 전에 기록한 암호와 일치하는지를 확인하여 인증을 수행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 로그인 계정을 찾을 수 없으면 인증이 실패하고 오류 메시지가 나타납니다.|  
    ||**사용자 이름**|  
    ||**암호**|  
    ||**패키지**<br /><br /> 줄임표 단추를 클릭하고 패키지를 선택합니다.<br /><br /> **개체 탐색기** 에서 **저장된 패키지**노드의 하위 폴더에 있는 패키지를 선택합니다.|  
    |**패키지**<br /><br /> 파일 시스템에 저장된 패키지의 탭 옵션입니다.|**패키지**<br /><br /> 패키지 파일의 전체 경로를 입력하거나 줄임표 단추를 클릭한 다음 패키지를 선택합니다.|  
    |**구성**|특정 구성으로 패키지를 실행할 XML 구성 파일을 추가합니다. 패키지 구성을 사용하여 런타임 시 패키지 속성 값을 업데이트합니다.<br /><br /> 이 옵션은 **dtexec** 의 **/ConfigFile**옵션에 해당합니다.<br /><br /> 패키지 구성이 적용되는 방법을 이해하려면 [Package Configurations](../../integration-services/packages/package-configurations.md)을 참조하십시오. 패키지 구성을 만드는 방법은 [Create Package Configurations](../../integration-services/packages/create-package-configurations.md)를 참조하십시오.|  
    |**명령 파일**|**dtexec**에 실행할 추가 옵션을 별도 파일에 지정합니다.<br /><br /> 예를 들어 패키지를 실행하는 동안 하나 이상의 지정된 이벤트가 발생하는 경우 디버그 덤프 파일을 생성하려면 /Dump *errorcode* 옵션을 포함하는 파일을 포함할 수 있습니다.<br /><br /> **명령 파일** 옵션을 사용하면 여러 파일을 만들어서 적절한 파일을 지정하는 방법으로 한 패키지에 대해 다른 옵션 집합을 실행할 수 있습니다.<br /><br /> **명령 파일** 옵션은 **dtexec** 의 **/CommandFile**옵션에 해당합니다.|  
    |**데이터 원본**|패키지에 포함된 연결 관리자를 봅니다. 연결 문자열을 수정하려면 연결 관리자를 클릭하고 연결 문자열을 클릭합니다.<br /><br /> 이 옵션은 **dtexec** 의 **/Connection**옵션에 해당합니다.|  
    |**실행 옵션**|**유효성 검사 경고 발생 시 패키지 실패**<br /> 경고 메시지가 오류로 간주되는지 여부를 나타냅니다. 이 옵션을 선택하고 유효성 검사 중 경고가 발생하면 패키지는 유효성 검사 중 실패합니다. 이 옵션은 **dtexec** 의 **/WarnAsError**옵션에 해당합니다.<br /><br /> **패키지를 실행하지 않고 유효성 검사**<br /> 유효성 검사 단계 후에 실제로 패키지를 실행하지 않고 패키지 실행을 중지할지 여부를 나타냅니다. 이 옵션은 **dtexec** 의 **/Validate**옵션에 해당합니다.<br /><br /> **MacConcurrentExecutables 속성 무시**<br /> 패키지에서 동시에 실행할 수 있는 실행 파일 수를 지정합니다. -1 값은 패키지가 실행할 수 있는 최대 파일 수가 패키지를 실행하는 컴퓨터의 프로세서 총 수에 2를 더한 값과 같음을 의미합니다. 이 옵션은 **dtexec** 의 **/MaxConcurrent**옵션에 해당합니다.<br /><br /> **패키지 검사점 사용**<br /> 패키지 실행 중 검사점 사용 여부를 나타냅니다. 자세한 내용은 [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md)을 참조하세요.<br /><br /> 이 옵션은 **dtexec** 의 **/CheckPointing**옵션에 해당합니다.<br /><br /> **다시 시작 옵션 무시**<br /> 패키지의 **CheckpointUsage** 속성에 대해 새 값이 설정되었는지를 나타냅니다. **다시 시작 옵션** 목록 상자에서 값을 선택합니다.<br /><br /> 이 옵션은 **dtexec** 의 **/Restart**옵션에 해당합니다.<br /><br /> **32비트 런타임 사용**<br /> 64비트 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 설치된 64비트 컴퓨터에서 32비트 버전의 dtexec 유틸리티를 사용하는 패키지의 실행 여부를 나타냅니다.<br /><br /> 예를 들어 64비트 버전에서 사용할 수 없는 네이티브 OLE DB 공급자를 패키지에서 사용하는 경우 32비트 버전의 dtexec를 사용하여 패키지를 실행해야 합니다. 자세한 내용은 [Integration Services에 대한 64비트 고려 사항](http://msdn.microsoft.com/library/ms141766\(SQL.105\).aspx)을 참조하십시오.<br /><br /> 기본적으로 **SQL Server Integration Services 패키지** 작업 단계 유형을 선택하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 시스템에서 자동으로 호출된 dtexec 유틸리티 버전을 사용하여 패키지를 실행합니다. 시스템은 컴퓨터 프로세서와 컴퓨터에서 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 버전에 따라 32비트 또는 64비트 버전 유틸리티를 호출합니다.|  
    |**로깅**|로그 공급자를 패키지 실행과 연결합니다.<br /><br /> **텍스트 파일용 SSIS 로그 공급자**<br /> ASCII 텍스트 파일에 로그 항목을 기록합니다.<br /><br /> **SQL Server용 SSIS 로그 공급자**<br /> MSDB 데이터베이스의 sysssislog 테이블에 로그 항목을 기록합니다.<br /><br /> **SQL Server Profiler용 SSIS 로그 공급자**<br /> SQL Server 프로파일러를 사용하여 볼 수 있는 추적 정보를 기록합니다.<br /><br /> **Windows 이벤트 로그용 SSIS 로그 공급자**<br /> Windows 이벤트 로그의 응용 프로그램 로그에 로그 항목을 기록합니다.<br /><br /> **XML 파일용 SSIS 로그 공급자**<br /> XML 파일에 로그 파일을 기록합니다.<br /><br /> 텍스트 파일, XML 파일 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로파일러 로그 공급자의 경우 패키지에 포함된 파일 연결 관리자를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 공급자의 경우 패키지에 포함된 OLE DB 연결 관리자를 선택합니다.<br /><br /> 이 옵션은 **dtexec** 의 **/Logger**옵션에 해당합니다.|  
    |**값 설정**|패키지 속성 설정을 재정의합니다. **속성** 상자에서 **속성 경로** 및 **값** 열에 값을 입력합니다. 속성 하나에 대한 값을 입력하면, **속성** 상자에 빈 행이 나타나고 다른 속성에 대한 값을 입력할 수 있게 됩니다.<br /><br /> 속성 상자에서 속성을 제거하려면 행을 클릭한 다음 **제거**를 클릭합니다.<br /><br /> 다음 중 하나를 수행하여 속성 경로를 찾을 수 있습니다.<br /><br /> -XML 구성 파일(\*.dtsconfig)에서 속성 경로를 복사합니다. 경로는 파일의 구성 섹션에 경로 속성의 값으로 나열됩니다. MaximumErrorCount 속성에 대한 경로의 예는 \Package.Properties[MaximumErrorCount]와 같습니다.<br /><br /> - **패키지 구성 마법사** 를 실행하고 마지막 **마법사 완료** 페이지에서 속성 경로를 복사합니다. 그런 다음 마법사를 취소할 수 있습니다.|  
    |**확인**|**서명된 패키지만 실행**<br /> 패키지 서명 확인 여부를 나타냅니다. 패키지가 서명되지 않았거나 서명이 잘못된 경우 패키지가 실패합니다. 이 옵션은 **dtexec** 의 **/VerifySigned**옵션에 해당합니다.<br /><br /> **패키지 빌드 확인**<br /> 패키지의 빌드 번호가 이 옵션 옆에 있는 **빌드** 상자에 입력된 빌드 번호와 비교하여 검증되었는지를 나타냅니다. 일치하지 않을 경우 패키지가 실행되지 않습니다. 이 옵션은 **dtexec** 의 **/VerifyBuild**옵션에 해당합니다.<br /><br /> **패키지 ID 확인**<br /> 패키지의 GUID가 이 옵션 옆에 있는 **패키지 ID** 상자에 입력된 package ID와 비교하여 검증되었는지를 나타냅니다. 이 옵션은 **dtexec** 의 **/VerifyPackageID**옵션에 해당합니다.<br /><br /> **버전 ID 확인**<br /> 패키지의 버전 GUID가 이 옵션 옆에 있는 **버전 ID** 상자에 입력된 버전 ID와 비교하여 검증되었는지를 나타냅니다. 이 옵션은 **dtexec** 의 **/VerifyVersionID**옵션에 해당합니다.|  
    |**명령줄**|dtexec의 명령줄 옵션을 수정합니다. 옵션에 대한 자세한 내용은 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)를 참조하십시오.<br /><br /> **원래 옵션 복원**<br /> **작업 단계 속성**대화 상자의 **패키지**, **구성**, **명령 파일**, **데이터 원본**, **실행 옵션**, **로깅**, **값 설정** , **확인** 탭에 설정한 명령줄 옵션을 사용합니다.<br /><br /> **수동으로 명령 편집**<br /> **명령줄** 상자에 명령줄 옵션을 추가로 입력합니다.<br /><br /> 작업 단계에 변경한 내용을 저장하기 위해 **확인** 을 클릭하기 전에 **원래 옵션 복원** 을 클릭하면 **명령줄**상자에 추가로 입력한 옵션을 모두 삭제할 수 있습니다.<br /><br /> **\*\* 팁 \*\*** 명령 프롬프트 창에 명령줄을 복사하고 `dtexec`를 추가하여 명령줄에서 패키지를 실행할 수 있습니다. 이렇게 하면 명령줄 텍스트를 쉽게 생성할 수 있습니다.|  
  
9. **확인** 을 클릭하여 설정을 저장하고 **새 작업 단계** 대화 상자를 닫습니다.  
  
    > **참고:** **SSIS 카탈로그**에 저장된 패키지의 경우 해결되지 않은 매개 변수 또는 연결 관리자 속성 설정이 있으면 **확인** 단추가 비활성화됩니다. 확인되지 않은 설정은 서버 환경 변수에 포함된 값을 사용하여 매개 변수나 속성을 설정하는 경우 다음 조건 중 하나를 충족하면 발생합니다.  
    >   
    >  **구성** 탭의 **환경** 확인란이 선택되어 있지 않습니다.  
    >   
    >  변수를 포함하는 서버 환경이 **구성** 탭의 목록 상자에 선택되어 있지 않습니다.  
  
10. 작업 단계 일정을 만들려면 **페이지 선택** 창에서 **일정** 을 클릭합니다. 일정 구성 방법에 대한 자세한 정보는 [Schedule a Job](http://msdn.microsoft.com/library/f626390a-a3df-4970-b7a7-a0529e4a109c)을 참조하십시오.  
  
    > [!TIP]  
    >  일정에 이름을 지정할 때 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 일정과 쉽게 구분할 수 있도록 고유하고 설명이 포함된 이름을 사용하는 것이 좋습니다.  

## <a name="see-also"></a>관련 항목:  
 [프로젝트 및 패키지 실행](deploy-integration-services-ssis-projects-and-packages.md)  

## <a name="external-resources"></a>외부 리소스  
  
-   [웹 사이트의 기술 자료 문서 -](http://support.microsoft.com/kb/918760)SQL Server 에이전트 작업 단계에서 SSIS 패키지를 호출할 때 SSIS 패키지가 실행되지 않는다 [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   MSDN Library의 비디오 - [문제 해결: SQL Server 에이전트를 사용하여 패키지 실행(SQL Server 비디오)](http://go.microsoft.com/fwlink/?LinkId=141772)  
  
-   MSDN Library의 비디오 - [방법: SQL Server 에이전트를 사용하여 패키지 실행 자동화(SQL Server 비디오)](http://go.microsoft.com/fwlink/?LinkId=141771)  
  
-   mssqltips.com의 기술 문서 - [Windows PowerShell을 사용하여 SQL Server 에이전트 작업 확인(Checking SQL Server Agent jobs using Windows PowerShell)](http://go.microsoft.com/fwlink/?LinkId=165675)  
  
-   mssqltips.com의 기술 문서 - [SQL 에이전트 작업 설정 또는 해제 시 자동 경고](http://go.microsoft.com/fwlink/?LinkId=165676)  
  
-   mssqltips.com의 블로그 항목 - [Windows 이벤트 로그에 쓰도록 SQL 에이전트 작업 구성](http://go.microsoft.com/fwlink/?LinkId=220745)  
  
  
