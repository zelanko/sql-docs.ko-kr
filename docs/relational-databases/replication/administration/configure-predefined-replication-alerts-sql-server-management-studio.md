---
title: "미리 정의된 복제 경고 구성(SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "경고 [SQL Server 복제]"
  - "미리 정의된 복제 경고 [SQL Server 복제]"
ms.assetid: c0414147-7ffe-4f9a-908c-71c1b5201584
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# 미리 정의된 복제 경고 구성(SQL Server Management Studio)
  복제는 다음과 같은 미리 정의된 경고를 제공합니다. 이러한 경고는 복제 이벤트에 응답하도록 구성할 수 있습니다.  
  
-   **복제: 에이전트 성공**  
  
-   **복제: 에이전트 실패**  
  
-   **복제: 에이전트 다시 시도**  
  
-   **복제: 만료된 구독 삭제**  
  
-   **복제: 유효성 검사 실패 후에 구독이 다시 초기화되었습니다.**  
  
-   **복제: 구독자가 데이터 유효성 검사에 실패했습니다.**  
  
-   **복제: 구독자가 데이터 유효성 검사를 통과했습니다.**  
  
-   **복제: 에이전트 사용자 지정 종료**  
  
 이러한 경고를 구성 된 **경고** 폴더에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 또는 **경고** 복제 모니터의 탭 합니다. 이 탭에 액세스 하는 방법에 대 한 자세한 내용은 참조 [정보 보기 및 구독 & #40;에 대 한 작업 수행 복제 모니터 & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)합니다.  
  
 복제 모니터는 이러한 경고 외에도 상태 및 성능과 관련된 일련의 경고를 제공합니다. 자세한 내용은 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)를 참조하세요. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 경고 인프라를 사용하여 다른 복제 이벤트에 대한 경고도 정의할 수 있습니다. 자세한 내용은 참조 [사용자 정의 이벤트 만들기](../../../ssms/agent/create-a-user-defined-event.md)합니다.  
  
### Management Studio에서 미리 정의된 복제 경고를 구성하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 배포자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **SQL Server 에이전트** 폴더를 확장한 다음 **경고** 폴더를 확장합니다.  
  
3.  복제 경고를 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **속성**합니다.  
  
4.  옵션 설정의 **\< AlertName> 속성 경고** 대화 상자:  
  
    -   **일반** 페이지에서 **사용**을 클릭하고 경고를 적용할 데이터베이스를 지정합니다.  
  
    -   에 **응답** 페이지에서 지정 하 고 있는지 여부를 전자 메일을 보낼지 및/또는 작업을 실행 해야 합니다.  
  
         경고의 **복제: 구독자가 데이터 유효성 검사에 실패 했습니다**, 응답 작업을 지정할 수 있습니다이 경고에 대 한 복제가 제공: 선택 **작업 실행**, 찾아보기 단추를 클릭 하 고 (**...**). **작업 찾기** 대화 상자에서 **찾아보기**를 클릭합니다. **개체 찾아보기** 대화 상자에서 **데이터 유효성 검사에 실패한 구독 다시 초기화**를 선택합니다. 열린 두 대화 상자에서 **확인** 을 클릭합니다. 실행 시 이 작업은 구독을 다시 초기화하는 저장 프로시저에 대한 RPC(원격 프로시저 호출)를 사용합니다. 게시자가 원격 배포자를 사용하는 경우 배포자에서 게시자로의 RPC를 설정할 수 있도록 게시자에서 원격 서버 로그인을 정의해야 합니다.  
  
    -   **옵션** 페이지에서 응답 텍스트를 사용자 지정합니다.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### 복제 모니터에서 임계값에 대한 경고를 구성하려면  
  
1.  **경고** 탭에서 **경고 구성**을 클릭합니다.  
  
2.  **복제 경고 구성** 대화 상자에서 경고를 선택한 다음 **구성**을 클릭합니다.  
  
3.  옵션 설정의 **\< AlertName> 속성 경고** 대화 상자:  
  
    -   **일반** 페이지에서 **사용**을 클릭하고 경고를 적용할 데이터베이스를 지정합니다.  
  
    -   에 **응답** 페이지에서 지정 하 고 있는지 여부를 전자 메일을 보낼지 및/또는 작업을 실행 해야 합니다.  
  
         경고의 **복제: 구독자가 데이터 유효성 검사에 실패 했습니다**, 응답 작업을 지정할 수 있습니다이 경고에 대 한 복제가 제공: 선택 **작업 실행**, 찾아보기 단추를 클릭 하 고 (**...**). **작업 찾기** 대화 상자에서 **찾아보기**를 클릭합니다. **개체 찾아보기** 대화 상자에서 **데이터 유효성 검사에 실패한 구독 다시 초기화**를 선택합니다. 열린 두 대화 상자에서 **확인** 을 클릭합니다. 실행 시 이 작업은 구독을 다시 초기화하는 저장 프로시저에 대한 RPC(원격 프로시저 호출)를 사용합니다. 게시자가 원격 배포자를 사용하는 경우 배포자에서 게시자로의 RPC를 설정할 수 있도록 게시자에서 원격 서버 로그인을 정의해야 합니다.  
  
    -   **옵션** 페이지에서 응답 텍스트를 사용자 지정합니다.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  **닫기**를 클릭합니다.  
  
## 참고 항목  
 [복제 에이전트 이벤트에 대한 경고 사용](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)  
  
  