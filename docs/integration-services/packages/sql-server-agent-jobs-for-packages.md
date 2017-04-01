---
title: "패키지에 대한 SQL Server 에이전트 작업 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "작업 [Integration Services]"
  - "자동 패키지 실행"
  - "패키지 일정 예약 [Integration Services]"
  - "SQL Server 에이전트 [Integration Services]"
ms.assetid: ecf7a5f9-b8a7-47f1-9ac0-bac07cb89e31
caps.latest.revision: 54
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 53
---
# 패키지에 대한 SQL Server 에이전트 작업
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 실행을 자동화하고 예약할 수 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소 및 파일 시스템에 저장된 패키지를 예약할 수 있습니다.  
  
## 이 항목의 섹션  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [SQL Server 에이전트에서 작업 예약](#jobs)  
  
-   [Integration Services 패키지 일정 예약](#packages)  
  
-   [예약 패키지 문제 해결](#trouble)  
  
##  <a name="jobs"></a> SQL Server 에이전트에서 작업 예약  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 실행하여 태스크를 자동화 및 예약할 수 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 설치하는 서비스입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 실행되고 있어야만 작업이 자동으로 실행될 수 있습니다. 자세한 내용은 [Configure SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md)을 참조하세요.  
  
 **SQL Server 에이전트** 노드는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 인스턴스에 연결하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 개체 탐색기에 표시됩니다.  
  
 되풀이 태스크를 자동화하려면 **새 작업** 대화 상자를 사용하여 작업을 만들어야 합니다. 자세한 내용은 [작업 구현](../../ssms/agent/implement-jobs.md)을 참조하세요.  
  
 작업을 만든 후 하나 이상의 단계를 추가해야 합니다. 한 개의 작업은 각각 다른 태스크를 수행하는 여러 단계를 포함할 수 있습니다. 자세한 내용은 [Manage Job Steps](../../ssms/agent/manage-job-steps.md)을(를) 참조하세요.  
  
 작업 및 작업 단계를 만든 다음에는 작업을 실행하는 일정을 만들 수 있습니다. 그러나 수동으로 실행되는 예약되지 않은 작업도 만들 수 있습니다. 자세한 내용은 [일정을 만들고 작업에 연결](../../ssms/agent/create-and-attach-schedules-to-jobs.md)을 참조하세요.  
  
 작업을 종료하거나 경고를 추가할 때 전자 메일 메시지를 보낼 운영자를 지정하는 등의 알림 옵션 설정으로 작업을 향상시킬 수 있습니다. 자세한 내용은 [경고](../../ssms/agent/alerts.md)를 참조하세요.  
  
##  <a name="packages"></a> Integration Services 패키지 일정 예약  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 만들어 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 예약한 경우 **SQL Server Integration Services 패키지**에 하나 이상의 단계를 추가하고 단계 유형을 설정해야 합니다. 한 개의 작업은 각각 다른 패키지를 실행하는 여러 단계를 포함할 수 있습니다.  
  
 작업 단계에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 실행하는 것은 **dtexec**(dtexec.exe) 및 **DTExecUI**(dtexecui.exe) 유틸리티를 사용하여 패키지를 실행하는 것과 비슷합니다. 명령줄 옵션 또는 **패키지 실행 유틸리티** 대화 상자를 사용하여 패키지의 런타임 옵션을 설정하는 대신 **새 작업 단계** 대화 상자에서 런타임 옵션을 설정할 수 있습니다. 패키지를 실행하는 옵션에 대한 자세한 내용은 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)를 참조하십시오.  
  
 자세한 내용은 [SQL Server 에이전트를 사용하여 패키지 예약](../../integration-services/packages/schedule-a-package-by-using-sql-server-agent.md)을 참조하세요.  
  
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
  
         개요, 모든 메시지 및 실행 성능 보고서에 대한 자세한 내용은 [Reports for the Integration Services Server](../../integration-services/performance/reports-for-the-integration-services-server.md)를 참조합니다.  
  
## 외부 리소스  
  
-   [웹 사이트의 기술 자료 문서 -](http://support.microsoft.com/kb/918760)SQL Server 에이전트 작업 단계에서 SSIS 패키지를 호출할 때 SSIS 패키지가 실행되지 않는다 [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   MSDN Library의 비디오 - [문제 해결: SQL Server 에이전트를 사용하여 패키지 실행(SQL Server 비디오)](http://go.microsoft.com/fwlink/?LinkId=141772)  
  
-   MSDN Library의 비디오 - [방법: SQL Server 에이전트를 사용하여 패키지 실행 자동화(SQL Server 비디오)](http://go.microsoft.com/fwlink/?LinkId=141771)  
  
-   mssqltips.com의 기술 문서 - [Windows PowerShell을 사용하여 SQL Server 에이전트 작업 확인(Checking SQL Server Agent jobs using Windows PowerShell)](http://go.microsoft.com/fwlink/?LinkId=165675)  
  
-   mssqltips.com의 기술 문서 - [SQL 에이전트 작업 설정 또는 해제 시 자동 경고](http://go.microsoft.com/fwlink/?LinkId=165676)  
  
-   mssqltips.com의 블로그 항목 - [Windows 이벤트 로그에 쓰도록 SQL 에이전트 작업 구성](http://go.microsoft.com/fwlink/?LinkId=220745)  
  
  