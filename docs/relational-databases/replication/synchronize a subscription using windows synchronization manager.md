---
title: "Windows 동기화 관리자를 사용하여 구독 동기화(Windows 동기화 관리자) | Microsoft Docs"
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
  - "동기화 [SQL Server 복제], Windows 동기화 관리자"
  - "Windows 동기화 관리자"
ms.assetid: 80f15dd6-e84d-4f96-9866-5b34ea531f1e
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Windows 동기화 관리자를 사용하여 구독 동기화(Windows 동기화 관리자)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Microsoft에 대 한 구독을 동기화 할 Windows 동기화 관리자만 사용할 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (사용할 수 있습니다도 오프 라인 파일과 웹 페이지를 동기화 할) 동기화 관리자와 동일한 컴퓨터에서 실행 되 고 있습니다. 동기화 관리자를 사용하려면 다음을 수행하십시오.  
  
1.  끌어오기 구독에 Windows 동기화 관리자와의 동기화를 사용 하도록 설정 된 **구독 속성-\< 구독자>: \< SubscriptionDatabase>** 대화 상자입니다. 이 대화 상자에 액세스 하는 방법에 대 한 자세한 내용은 참조 [뷰와 끌어오기 구독 속성을 수정](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)합니다.  
  
2.  Windows의 **시작** 메뉴를 통해 동기화 관리자에 액세스합니다.  
  
 동기화 관리자를 사용하면 병합 구독에 대해 대화형 해결 프로그램을 사용할 수 있습니다. 일반적으로 동기화하는 동안 감지된 충돌은 자동으로 해결되지만 대화형 해결이 설정된 경우에는 동기화하는 동안 사용자가 충돌을 해결할 수 있습니다. 동기화가 Windows 동기화 관리자 외부(예: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 복제 모니터의 예약 동기화 또는 요청 시 동기화)에서 수행된 경우 아티클에 지정된 해결 프로그램에 따라 사용자 개입 없이도 자동으로 충돌이 해결됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 및 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)]부터 64비트 버전의 Windows 동기화 관리자는 32비트 구독을 검색할 수 없습니다.  
  
### Windows 동기화 관리자를 통한 끌어오기 구독 동기화가 가능하도록 설정하려면  
  
1.  에 **일반** 의 페이지는 **구독 속성-\< 구독자>: \< SubscriptionDatabase>** 대화 상자에서 값 선택 **사용** 에 대 한는 **Windows 동기화 관리자를 사용 하 여** 옵션.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### 동기화 관리자로 끌어오기 구독을 동기화하려면  
  
1.  다음 중 한 가지 방법을 사용하여 동기화 관리자를 시작합니다.  
  
    -   Internet Explorer에서 **도구**, **동기화**를 차례로 클릭합니다.  
  
    -   **시작**을 클릭하고 **프로그램** 또는 **모든 프로그램**, **보조프로그램**을 차례로 가리킨 다음 **동기화**를 클릭합니다.  
  
    -   클릭 **시작**, 를 클릭 하 고 **실행 합니다.** 에 **실행** 대화 상자에서 **mobsync.exe** 에 **열려** 필드를 클릭 한 후 **확인**합니다.  
  
2.  **동기화할 항목** 대화 상자에서 동기화할 구독을 선택합니다. 구독은 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 아래에 나열되어 있습니다.  
  
3.  **동기화**를 클릭합니다.  
  
### 동기화 관리자로 끌어오기 구독을 다시 초기화하려면  
  
1.  **동기화할 항목** 대화 상자에서 구독을 선택한 다음 **속성**을 클릭합니다.  
  
2.  **SQL Server 구독 속성** 대화 상자에서 **구독 다시 초기화**를 클릭합니다.  
  
3.  **예**를 클릭합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     다음에 구독이 동기화되면 기본적으로 새 스냅숏이 구독 데이터베이스에 적용됩니다. 자세한 내용은 참조 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)합니다.  
  
> [!NOTE]  
>  병합 복제를 사용하면 스냅숏이 적용되기 전에 처리 중인 변경 내용이 게시자로 업로드되지만 동기화 관리자에서는 이 옵션을 사용할 수 없습니다. 변경 내용을 업로드하려면 구독을 다시 초기화하기 전에 동기화합니다.  
  
### 동기화 관리자에서 끌어오기 구독에 대한 속성을 설정하려면  
  
1.  **동기화할 항목** 대화 상자에서 구독을 선택한 다음 **속성**을 클릭합니다.  
  
2.  다음 탭에서 속성을 보고 수정합니다.  
  
    -   **ID**  
  
    -   **구독자 로그인**, **배포자 로그인**, 및 **게시자 로그인** (병합 복제에만)  
  
    -   **웹 서버 정보** (SQL Server 2005 이상을 실행 하는 구독자에서 병합 구독의 경우)에 대 한  
  
    -   **기타**  
  
     모든 연결에 대해 Windows 인증을 사용하는 것이 좋습니다. 배포 에이전트 및 병합 에이전트에 필요한 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하십시오.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### 동기화 관리자에서 끌어오기 구독을 제거하려면  
  
1.  **동기화할 항목** 대화 상자에서 구독을 선택한 다음 **속성**을 클릭합니다.  
  
2.  **SQL Server 구독 속성** 대화 상자에서 **구독 제거**를 클릭합니다.  
  
3.  **구독 제거** 대화 상자에서 옵션을 선택합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### 대화형 해결 프로그램을 사용하려면  
  
1.  대화형 해결을 사용할 아티클과 구독을 설정합니다. 자세한 내용은 참조 [병합 아티클에 대 한 대화형 충돌 해결 지정](../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md)합니다.  
  
2.  동기화 관리자에서 구독이 동기화를 시작하면 대화형 충돌 해결이 설정되어 있고 하나 이상의 아티클에 대한 충돌이 있는 경우 대화형 해결 프로그램이 자동으로 시작됩니다. 대화형 해결 프로그램은 권장 해결 방법(게시 및 구독을 만들 때 지정한 해결 프로그램에 기반함)과 함께 한 번에 하나의 충돌을 표시합니다.  
  
3.  선택적으로 대화형 해결 프로그램에 표시된 열을 편집한 다음 다음 단추 중 하나를 클릭하여 충돌을 해결합니다.  
  
    -   **제안 허용**  
  
    -   **게시자 허용**  
  
    -   **구독자 허용**  
  
    -   **모든 자동으로 해결** (현재 모든 충돌이 추가 입력 없이 해결)  
  
     그러면 선택한 행이 게시자 및/또는 구독자에 적용되고 후속 동기화 중에 토폴로지에 있는 다른 노드로 전파됩니다.  
  
> [!NOTE]  
>  편집을 수행한 경우에는 편집 내용이 해결을 위해 선택한 행의 일부인 경우에만 적용됩니다. 예를 들어 **게시자**에서 편집을 수행한 다음 **구독자 허용**을 클릭하면 편집 내용이 무시됩니다.  
  
## 참고 항목  
 [대화형 충돌 해결](../../relational-databases/replication/merge/interactive-conflict-resolution.md)  
  
  