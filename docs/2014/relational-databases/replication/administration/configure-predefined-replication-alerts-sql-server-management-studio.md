---
title: 미리 정의된 복제 경고 구성(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server replication]
- predefined replication alerts [SQL Server replication]
ms.assetid: c0414147-7ffe-4f9a-908c-71c1b5201584
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 103f461c29e2bd7534ad5cb96836f06c972a6c5e
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54130313"
---
# <a name="configure-predefined-replication-alerts-sql-server-management-studio"></a>미리 정의된 복제 경고 구성(SQL Server Management Studio)
  복제는 다음과 같은 미리 정의된 경고를 제공합니다. 이러한 경고는 복제 이벤트에 응답하도록 구성할 수 있습니다.  
  
-   **복제: 에이전트 성공**    
-   **복제: 에이전트 실패**    
-   **복제: 에이전트 다시 시도**    
-   **복제: 만료된 구독 삭제**    
-   **복제: 구독 유효성 검사 실패 후 다시 초기화**    
-   **복제: 구독자가 데이터 유효성 검사에 실패 했습니다.**    
-   **복제: 구독자에서 데이터 유효성 검사를 통과 했습니다.**    
-   **복제: 에이전트 사용자 지정 종료**  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]의 **경고** 폴더 또는 복제 모니터의 **경고** 탭에서 이러한 경고를 구성합니다. 이 탭에 액세스 하는 방법에 대 한 자세한 내용은 참조 하십시오 [정보 보기 및 태스크 수행 복제 모니터를 사용 하 여](../monitor/view-information-and-perform-tasks-replication-monitor.md)입니다.  
  
 복제 모니터는 이러한 경고 외에도 상태 및 성능과 관련된 일련의 경고를 제공합니다. 자세한 내용은 [임계값 설정 및 복제 모니터에서 경고](../monitor/set-thresholds-and-warnings-in-replication-monitor.md) 경고 인프라입니다. 자세한 내용은 [사용자 정의 이벤트 만들기](../../../ssms/agent/create-a-user-defined-event.md)를 참조하세요.  
  
### <a name="to-configure-a-predefined-replication-alert-in-management-studio"></a>Management Studio에서 미리 정의된 복제 경고를 구성하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 배포자에 연결한 다음 해당 서버 노드를 확장합니다.    
2.  **SQL Server 에이전트** 폴더를 확장한 다음 **경고** 폴더를 확장합니다.    
3.  복제 경고를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.    
4.  **\<AlertName> 경고 속성** 대화 상자에서 다음과 같은 옵션을 설정합니다.    
    -   **일반** 페이지에서 **사용**을 클릭하고 경고를 적용할 데이터베이스를 지정합니다.    
    -   **응답** 페이지에서 전자 메일의 발송 여부 및/또는 작업의 실행 여부를 지정합니다.  
  
         **복제: 구독자가 데이터 유효성 검사를 실패 했습니다**, 응답 작업을 지정할 수 있습니다이 경고에 대 한 복제를 제공 합니다. 선택 **작업 실행**, 한 다음 찾아보기 단추를 클릭 하 고 (**...** ). **작업 찾기** 대화 상자에서 **찾아보기**를 클릭합니다. **개체 찾아보기** 대화 상자에서 **데이터 유효성 검사에 실패한 구독 다시 초기화**를 선택합니다. 열린 두 대화 상자에서 **확인** 을 클릭합니다. 실행 시 이 작업은 구독을 다시 초기화하는 저장 프로시저에 대한 RPC(원격 프로시저 호출)를 사용합니다. 게시자가 원격 배포자를 사용하는 경우 배포자에서 게시자로의 RPC를 설정할 수 있도록 게시자에서 원격 서버 로그인을 정의해야 합니다.   
    -   **옵션** 페이지에서 응답 텍스트를 사용자 지정합니다.    
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-configure-an-alert-for-a-threshold-in-replication-monitor"></a>복제 모니터에서 임계값에 대한 경고를 구성하려면  
  
1.  **경고** 탭에서 **경고 구성**을 클릭합니다.    
2.  **복제 경고 구성** 대화 상자에서 경고를 선택한 다음 **구성**을 클릭합니다.    
3.  **\<AlertName> 경고 속성** 대화 상자에서 다음과 같은 옵션을 설정합니다.    
    -   **일반** 페이지에서 **사용**을 클릭하고 경고를 적용할 데이터베이스를 지정합니다.    
    -   **응답** 페이지에서 전자 메일의 발송 여부 및/또는 작업의 실행 여부를 지정합니다.    
         **복제: 구독자가 데이터 유효성 검사를 실패 했습니다**, 응답 작업을 지정할 수 있습니다이 경고에 대 한 복제를 제공 합니다. 선택 **작업 실행**, 한 다음 찾아보기 단추를 클릭 하 고 (**...** ). **작업 찾기** 대화 상자에서 **찾아보기**를 클릭합니다. **개체 찾아보기** 대화 상자에서 **데이터 유효성 검사에 실패한 구독 다시 초기화**를 선택합니다. 열린 두 대화 상자에서 **확인** 을 클릭합니다. 실행 시 이 작업은 구독을 다시 초기화하는 저장 프로시저에 대한 RPC(원격 프로시저 호출)를 사용합니다. 게시자가 원격 배포자를 사용하는 경우 배포자에서 게시자로의 RPC를 설정할 수 있도록 게시자에서 원격 서버 로그인을 정의해야 합니다.   
    -   **옵션** 페이지에서 응답 텍스트를 사용자 지정합니다.    
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]    
5.  **닫기**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 에이전트 이벤트에 대한 경고 사용](../agents/use-alerts-for-replication-agent-events.md)  
  
  
