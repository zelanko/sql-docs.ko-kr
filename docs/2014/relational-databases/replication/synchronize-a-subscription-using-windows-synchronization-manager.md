---
title: Windows Synchronization Manager (Windows Synchronization Manager)을 사용 하 여 구독 동기화 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- synchronization [SQL Server replication], Windows Synchronization Manager
- Windows Synchronization Manager
ms.assetid: 80f15dd6-e84d-4f96-9866-5b34ea531f1e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 04b1c5322408f66ab2a4023e3d215cc7e669eab6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62745762"
---
# <a name="synchronize-a-subscription-using-windows-synchronization-manager-windows-synchronization-manager"></a>Windows 동기화 관리자를 사용하여 구독 동기화(Windows 동기화 관리자)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 가 동기화 관리자와 같은 컴퓨터에서 실행 중인 경우에는 구독을 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시와 동기화하는 데만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 동기화 관리자를 사용할 수 있습니다. 동기화 관리자를 사용하면 오프라인 파일과 웹 페이지를 동기화할 수도 있습니다. 동기화 관리자를 사용하려면 다음을 수행하십시오.  
  
1.  **구독 속성 - \<Subscriber>: \<SubscriptionDatabase>** 대화 상자에서 Windows 동기화 관리자로 끌어오기 구독 동기화를 설정합니다. 이 대화 상자에 액세스하는 방법은 [끌어오기 구독 속성 보기 및 수정](view-and-modify-pull-subscription-properties.md)을 참조하세요.  
  
2.  Windows의 **시작** 메뉴를 통해 동기화 관리자에 액세스합니다.  
  
 동기화 관리자를 사용하면 병합 구독에 대해 대화형 해결 프로그램을 사용할 수 있습니다. 일반적으로 동기화하는 동안 감지된 충돌은 자동으로 해결되지만 대화형 해결이 설정된 경우에는 동기화하는 동안 사용자가 충돌을 해결할 수 있습니다. 동기화가 Windows 동기화 관리자 외부(예: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 복제 모니터의 예약 동기화 또는 요청 시 동기화)에서 수행된 경우 아티클에 지정된 해결 프로그램에 따라 사용자 개입 없이도 자동으로 충돌이 해결됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] 및 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)]부터 64비트 버전의 Windows 동기화 관리자는 32비트 구독을 검색할 수 없습니다.  
  
### <a name="to-enable-the-synchronization-of-pull-subscriptions-with-windows-synchronization-manager"></a>Windows 동기화 관리자를 통한 끌어오기 구독 동기화가 가능하도록 설정하려면  
  
1.  **구독 속성 - \<구독자>: \<SubscriptionDatabase>** 대화 상자의 일반 페이지에서 **Windows 동기화 관리자 사용** 옵션에 대한 **사용** 값을 선택합니다.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-synchronize-a-pull-subscription-with-synchronization-manager"></a>동기화 관리자로 끌어오기 구독을 동기화하려면  
  
1.  다음 중 한 가지 방법을 사용하여 동기화 관리자를 시작합니다.  
  
    -   Internet Explorer에서 **도구**, **동기화**를 차례로 클릭합니다.  
  
    -   **시작**을 클릭하고 **프로그램** 또는 **모든 프로그램**, **보조프로그램**을 차례로 가리킨 다음 **동기화**를 클릭합니다.  
  
    -   **시작**, **실행** 에 **실행** 대화 상자에서 `mobsync.exe` 에 **열기** 필드 및 클릭 **확인**합니다.  
  
2.  **동기화할 항목** 대화 상자에서 동기화할 구독을 선택합니다. 구독은 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 아래에 나열되어 있습니다.  
  
3.  **동기화**를 클릭합니다.  
  
### <a name="to-reinitialize-a-pull-subscription-with-synchronization-manager"></a>동기화 관리자로 끌어오기 구독을 다시 초기화하려면  
  
1.  **동기화할 항목** 대화 상자에서 구독을 선택한 다음 **속성**을 클릭합니다.  
  
2.  **SQL Server 구독 속성** 대화 상자에서 **구독 다시 초기화**를 클릭합니다.  
  
3.  **예**를 클릭합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     다음에 구독이 동기화되면 기본적으로 새 스냅숏이 구독 데이터베이스에 적용됩니다. 자세한 내용은 [구독 다시 초기화](reinitialize-subscriptions.md)를 참조하세요.  
  
> [!NOTE]  
>  병합 복제를 사용하면 스냅숏이 적용되기 전에 처리 중인 변경 내용이 게시자로 업로드되지만 동기화 관리자에서는 이 옵션을 사용할 수 없습니다. 변경 내용을 업로드하려면 구독을 다시 초기화하기 전에 동기화합니다.  
  
### <a name="to-set-properties-for-a-pull-subscription-in-synchronization-manager"></a>동기화 관리자에서 끌어오기 구독에 대한 속성을 설정하려면  
  
1.  **동기화할 항목** 대화 상자에서 구독을 선택한 다음 **속성**을 클릭합니다.  
  
2.  다음 탭에서 속성을 보고 수정합니다.  
  
    -   **ID**  
  
    -   **구독자 로그인**, **배포자 로그인**및 **게시자 로그인** (병합 복제의 경우만 해당)  
  
    -   **웹 서버 정보** (SQL Server 2005 이상을 실행하는 구독자에서 병합 구독의 경우)  
  
    -   **기타**  
  
     모든 연결에 대해 Windows 인증을 사용하는 것이 좋습니다. 배포 에이전트 및 병합 에이전트에 필요한 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](security/replication-agent-security-model.md)을 참조하십시오.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-remove-a-pull-subscription-from-synchronization-manager"></a>동기화 관리자에서 끌어오기 구독을 제거하려면  
  
1.  **동기화할 항목** 대화 상자에서 구독을 선택한 다음 **속성**을 클릭합니다.  
  
2.  **SQL Server 구독 속성** 대화 상자에서 **구독 제거**를 클릭합니다.  
  
3.  **구독 제거** 대화 상자에서 옵션을 선택합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-use-the-interactive-resolver"></a>대화형 해결 프로그램을 사용하려면  
  
1.  대화형 해결을 사용할 아티클과 구독을 설정합니다. 자세한 내용은 [병합 아티클에 대한 상호 충돌 해결 지정](../../relational-databases/replication/publish/specify-merge-replication-properties.md#interactive-conflict-resolution)을 참조하세요.
  
2.  동기화 관리자에서 구독이 동기화를 시작하면 대화형 충돌 해결이 설정되어 있고 하나 이상의 아티클에 대한 충돌이 있는 경우 대화형 해결 프로그램이 자동으로 시작됩니다. 대화형 해결 프로그램은 권장 해결 방법(게시 및 구독을 만들 때 지정한 해결 프로그램에 기반함)과 함께 한 번에 하나의 충돌을 표시합니다.  
  
3.  선택적으로 대화형 해결 프로그램에 표시된 열을 편집한 다음 다음 단추 중 하나를 클릭하여 충돌을 해결합니다.  
  
    -   **제안 허용**  
  
    -   **게시자 허용**  
  
    -   **구독자 허용**  
  
    -   **모든 충돌 자동 해결** - 추가 입력 없이 현재 모든 충돌이 해결됩니다.  
  
     그러면 선택한 행이 게시자 및/또는 구독자에 적용되고 후속 동기화 중에 토폴로지에 있는 다른 노드로 전파됩니다.  
  
> [!NOTE]  
>  편집을 수행한 경우에는 편집 내용이 해결을 위해 선택한 행의 일부인 경우에만 적용됩니다. 예를 들어 **게시자**에서 편집을 수행한 다음 **구독자 허용**을 클릭하면 편집 내용이 무시됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [대화형 충돌 해결](merge/advanced-merge-replication-conflict-interactive-resolution.md)  
  
