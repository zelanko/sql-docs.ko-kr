---
title: '작업 단계 속성: 새 작업 단계 (일반 페이지) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.job.stepgeneral.f1
ms.assetid: 8d1885ba-4386-4528-8f2b-68c16852720c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9c8f8bc17b6a4c4792858c64144788aa12b858a3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062247"
---
# <a name="job-step-properties-new-job-step-general-page"></a>작업 단계 속성: 새 작업 단계(일반 페이지)
  이 페이지를 사용 하 여 에이전트 작업 단계의 속성을 확인 하 고 변경 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하거나 새 작업 단계를 정의할 수 있습니다.  
  
 이 페이지로 이동하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 확장한 다음 **작업**을 마우스 오른쪽 단추로 클릭하고 **새 작업**을 클릭한 다음 **단계** 페이지를 선택하고 **새로 만들기**를 클릭합니다. 개체 탐색기에서 작업을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭한 다음 **단계** 를 선택하고 **새로 만들기**, **삽입**또는 **편집**을 클릭하여 이 페이지로 이동할 수도 있습니다.  
  
## <a name="options"></a>옵션  
 **단계 이름**  
 작업 단계의 이름을 설정합니다.  
  
 **형식**  
 작업 단계에서 사용하는 하위 시스템을 설정합니다. 선택한 하위 시스템에 따라 작업 단계 정의에 표시되는 옵션이 달라집니다.  
  
 **다음 계정으로 실행**  
 작업 단계에 사용할 프록시 계정을 설정합니다. sysadmin 고정 서버 역할의 멤버는 **SQL 에이전트 서비스 계정**도 지정할 수 있습니다.  
  
 **Database**  
 작업 단계가 실행되는 데이터베이스를 설정합니다. 일부 작업 단계 유형에 대해서는 이 옵션을 사용할 수 없습니다.  
  
 **명령**  
 작업 단계에서 실행하는 명령을 설정합니다.  
  
## <a name="options-for-transact-sql-job-steps"></a>Transact-SQL 작업 단계 옵션  
 **열기**  
 파일에서 명령을 로드합니다.  
  
 **모두 선택**  
 명령의 텍스트를 선택합니다.  
  
 **복사**  
 선택한 텍스트를 클립보드에 복사합니다.  
  
 **붙여넣기**  
 클립보드의 내용을 붙여 넣습니다.  
  
 **구문 분석**  
 명령의 구문을 확인합니다.  
  
## <a name="options-for-activex-script-job-steps"></a>ActiveX 스크립트 작업 단계 옵션  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이후 버전에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에이전트에서 ActiveX 스크립팅 하위 시스템이 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.  
  
 **VBScript**  
 작업 단계에 사용할 언어로 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic Scripting Edition을 지정합니다.  
  
 **JScript**  
 작업 단계에 사용할 언어로 JScript를 지정합니다.  
  
 **기타**  
 다른 스크립트 언어로 작성된 작업 단계에 사용할 언어 이름을 입력합니다.  
  
 **열기**  
 파일에서 명령을 로드합니다.  
  
 **모두 선택**  
 명령의 텍스트를 선택합니다.  
  
 **복사**  
 선택한 텍스트를 복사합니다.  
  
 **붙여넣기**  
 클립보드의 내용을 붙여 넣습니다.  
  
## <a name="options-for-operating-system-cmdexec-job-steps"></a>운영 체제(CmdExec) 작업 단계 옵션  
 **성공한 명령의 프로세스 종료 코드**  
 성공을 나타내기 위해 명령에서 반환하는 종료 코드를 입력합니다.  
  
 **열기**  
 파일에서 명령을 로드합니다.  
  
 **모두 선택**  
 명령의 텍스트를 선택합니다.  
  
 **복사**  
 선택한 텍스트를 복사합니다.  
  
 **붙여넣기**  
 클립보드의 내용을 붙여 넣습니다.  
  
## <a name="options-for-powershell-job-steps"></a>PowerShell 작업 단계 옵션  
 **열기**  
 파일로부터 스크립트를 로드합니다.  
  
 **모두 선택**  
 스크립트의 텍스트를 선택합니다.  
  
 **복사**  
 선택한 텍스트를 복사합니다.  
  
 **붙여넣기**  
 클립보드의 내용을 붙여 넣습니다.  
  
## <a name="options-for-replication-distributor-job-steps"></a>복제 배포자 작업 단계 옵션  
 **모두 선택**  
 명령의 텍스트를 선택합니다.  
  
 **복사**  
 선택한 텍스트를 복사합니다.  
  
 **붙여넣기**  
 클립보드의 내용을 붙여 넣습니다.  
  
## <a name="options-for-replication-merge-job-steps"></a>복제 병합 작업 단계 옵션  
 **모두 선택**  
 명령의 텍스트를 선택합니다.  
  
 **복사**  
 선택한 텍스트를 복사합니다.  
  
 **붙여넣기**  
 클립보드의 내용을 붙여 넣습니다.  
  
## <a name="options-for-replication-queue-reader-job-steps"></a>복제 큐 판독기 작업 단계 옵션  
 **Database**  
 작업 단계에 사용할 데이터베이스입니다.  
  
 **모두 선택**  
 명령의 텍스트를 선택합니다.  
  
 **복사**  
 선택한 텍스트를 복사합니다.  
  
 **붙여넣기**  
 클립보드의 내용을 붙여 넣습니다.  
  
## <a name="options-for-replication-snapshot-job-steps"></a>복제 스냅샷 작업 단계 옵션  
 **모두 선택**  
 명령의 텍스트를 선택합니다.  
  
 **복사**  
 선택한 텍스트를 복사합니다.  
  
 **붙여넣기**  
 클립보드의 내용을 붙여 넣습니다.  
  
## <a name="options-for-replication-transaction-log-reader-job-steps"></a>복제 트랜잭션 로그 판독기 작업 단계 옵션  
 **모두 선택**  
 명령의 텍스트를 선택합니다.  
  
 **복사**  
 선택한 텍스트를 복사합니다.  
  
 **붙여넣기**  
 클립보드의 내용을 붙여 넣습니다.  
  
## <a name="options-for-sql-server-analysis-services-command-job-steps"></a>SQL Server Analysis Services 명령 작업 단계 옵션  
 **Server**  
 작업 단계를 실행할 서버를 선택합니다.  
  
 **열기**  
 파일에서 명령을 로드합니다.  
  
 **모두 선택**  
 명령의 텍스트를 선택합니다.  
  
 **복사**  
 선택한 텍스트를 복사합니다.  
  
 **붙여넣기**  
 클립보드의 내용을 붙여 넣습니다.  
  
## <a name="options-for-sql-server-analysis-services-query-job-steps"></a>SQL Server Analysis Services 쿼리 작업 단계 옵션  
 **Server**  
 작업 단계를 실행할 서버를 선택합니다.  
  
 **Database**  
 작업 단계에 사용할 데이터베이스입니다.  
  
 **열기**  
 파일에서 명령을 로드합니다.  
  
 **모두 선택**  
 명령의 텍스트를 선택합니다.  
  
 **복사**  
 선택한 텍스트를 복사합니다.  
  
 **붙여넣기**  
 클립보드의 내용을 붙여 넣습니다.  
  
## <a name="options-for-integration-services-package-execution-job-steps"></a>Integration Services 패키지 실행 작업 단계 옵션  
  
### <a name="general-tab"></a>일반 탭  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) 패키지가 있는 위치와 사용할 인증 모드를 지정합니다. 이 탭을 선택하면 다음 옵션을 사용할 수 있습니다.  
  
 **패키지 원본**  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지가 저장된 위치를 지정합니다. 다음 중 하나를 선택합니다.  
  
-   **SQL Server**  
  
-   **파일 시스템**  
  
-   **SSIS 패키지 저장소**  
  
 **Server**  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지가 저장된 서버 이름을 입력합니다. 이 옵션은 **패키지 원본** 에 대해 **SQL Server** 또는 **SSIS 패키지 저장소**를 지정한 경우에만 사용할 수 있습니다.  
  
 **Windows 인증 사용**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 시 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증이 사용됩니다.  
  
 **SQL Server 인증 사용**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증이 사용됩니다. 이 인증 방법을 선택하는 경우 해당 **사용자 이름** 과 **암호**를 입력합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증은 이전 버전과의 호환성을 위해 제공됩니다. 보안 향상을 위해 가능하면 Windows 인증을 사용합니다.  
  
 **패키지**  
 패키지 위치를 입력합니다.  
  
> [!IMPORTANT]  
>  암호로 보호된 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지의 경우 **구성** 탭을 클릭하여 **패키지 암호** 대화 상자에 암호를 입력합니다. 그렇지 않으면 암호로 보호된 패키지를 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업이 실패합니다.  
  
### <a name="configurations-tab"></a>구성 탭  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지의 구성 옵션을 지정합니다. 이 탭을 선택하면 다음 옵션을 사용할 수 있습니다.  
  
 **구성 파일**  
 패키지의 구성 파일을 나열합니다.  
  
 **추가**  
 패키지의 구성 파일을 추가합니다.  
  
 **제거**  
 패키지의 구성 파일을 제거합니다.  
  
 **위로 이동**  
 선택한 구성 파일을 위로 이동합니다.  
  
 **아래로 이동**  
 선택한 구성 파일을 아래로 이동합니다.  
  
### <a name="command-files-tab"></a>명령 파일 탭  
 패키지의 명령 파일을 선택합니다. 명령 파일은 목록에 나타나는 순서대로 처리됩니다. 이 탭을 선택하면 다음 옵션을 사용할 수 있습니다.  
  
 **명령 파일**  
 패키지의 명령 파일을 나열합니다.  
  
 **추가**  
 명령 파일을 추가합니다.  
  
 **제거**  
 선택한 명령 파일을 제거합니다.  
  
 **위로 이동**  
 선택한 명령 파일을 위로 이동합니다.  
  
 **아래로 이동**  
 선택한 명령 파일을 아래로 이동합니다.  
  
### <a name="data-sources-tab"></a>데이터 원본 탭  
 패키지에 지정된 데이터 원본이 이 탭에 표시됩니다.  
  
 **연결 관리자**  
 데이터 원본의 이름을 표시합니다.  
  
 **설명**  
 데이터 원본에 대한 설명을 표시합니다.  
  
 **연결 문자열**  
 데이터 원본에 대한 연결 문자열을 표시합니다.  
  
### <a name="execution-options-tab"></a>실행 옵션 탭  
 이 탭에서 패키지의 실행 옵션을 표시하거나 변경합니다.  
  
 **유효성 검사 경고 발생 시 패키지 실패**  
 유효성 검사 경고가 발생하는 경우 패키지 실행이 실패하도록 하려면 이 옵션을 선택합니다.  
  
 **패키지를 실행하지 않고 유효성 검사**  
 작업 단계에서 패키지를 실행하지 않고 유효성을 검사하도록 하려면 이 옵션을 선택합니다.  
  
 **최대 동시 실행 파일 수**  
 한 번에 실행할 수 있는 최대 실행 파일 수입니다.  
  
 **패키지 검사점 사용**  
 작업 단계에서 패키지 검사점을 사용하도록 하려면 이 옵션을 선택합니다.  
  
 **검사점 파일**  
 패키지 검사점 파일의 이름을 입력합니다.  
  
 **...**  
 패키지 검사점 파일을 찾아봅니다.  
  
 **다시 시작 옵션 무시**  
 이 작업 단계에 대해 패키지에 지정된 것과 다른 다시 시작 옵션을 지정하려면 이 옵션을 선택합니다.  
  
 **다시 시작 옵션**  
 패키지가 다시 시작될 때 수행할 동작을 선택합니다.  
  
### <a name="logging-tab"></a>로깅 탭  
 이 탭에서 패키지의 로그 공급자를 표시하거나 변경합니다.  
  
 **로그 공급자**  
 로그 공급자의 ClassID를 선택합니다.  
  
 **구성 문자열**  
 로그 공급자의 구성 문자열을 입력합니다.  
  
 **제거**  
 로그 공급자를 제거합니다.  
  
### <a name="set-values-tab"></a>값 설정 탭  
 이 탭에서 패키지의 속성 값을 표시하거나 변경합니다.  
  
 **속성 경로**  
 속성 경로를 표시하거나 변경합니다.  
  
 **값**  
 속성 값을 표시하거나 변경합니다.  
  
 **제거**  
 속성을 제거합니다.  
  
### <a name="verification-tab"></a>확인 탭  
 이 탭에서 작업 단계의 확인 옵션을 선택합니다.  
  
 **서명된 패키지만 실행**  
 서명된 패키지만 실행합니다. 이 옵션을 선택하면 패키지가 서명되지 않은 경우 작업 단계가 실패합니다.  
  
 **패키지 빌드 확인**  
 특정 빌드 번호가 있는 패키지만 실행합니다. 이 옵션을 선택하면 지정한 빌드 번호가 패키지에 없는 경우 작업 단계가 실패합니다.  
  
 **빌드**  
 패키지의 빌드 번호를 입력합니다.  
  
 **패키지 ID 확인**  
 특정 ID가 있는 패키지만 실행합니다. 이 옵션을 선택하면 지정한 ID가 패키지에 없는 경우 작업 단계가 실패합니다.  
  
 **패키지 ID**  
 패키지 ID를 입력합니다.  
  
 **버전 ID 확인**  
 특정 버전 ID가 있는 패키지만 실행합니다. 이 옵션을 선택하면 지정한 버전 ID가 패키지에 없는 경우 작업 단계가 실패합니다.  
  
 **버전 ID**  
 버전 ID를 입력합니다.  
  
### <a name="command-line-tab"></a>명령줄 탭  
 패키지의 명령줄 옵션을 지정합니다. 이 탭을 선택하면 다음 옵션을 사용할 수 있습니다.  
  
 **원래 옵션 복원**  
 이 대화 상자에 설정된 명령줄 옵션을 사용합니다.  
  
 **수동으로 명령줄 편집**  
 명령줄 창에서 옵션을 지정합니다.  
  
 **명령줄**  
 이 패키지에 사용할 명령줄 옵션을 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
 [작업 단계 관리](manage-job-steps.md)   
 [패키지에 대 한 SQL Server 에이전트 작업](../../integration-services/packages/sql-server-agent-jobs-for-packages.md)   
 [복제 에이전트 관리](../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
