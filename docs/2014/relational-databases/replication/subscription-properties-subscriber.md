---
title: SQL Server 복제 구독 속성-구독자 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.subproperties.subscriber.f1
- sql12.rep.newsubwizard.subproperties.publisher.f1
helpviewer_keywords:
- Subscription Properties dialog box
ms.assetid: bef66929-3234-4a45-8ec4-3b271519d07a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7a37f7b086f33719d7e55826ff40f2202093119a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85004604"
---
# <a name="sql-server-replication-subscription-properties"></a>SQL Server 복제 구독 속성 
이 섹션에서는 **구독 속성** 대화 상자에 대 한 정보를 제공 합니다. 

## <a name="publisher-properties"></a>게시자 속성 
  게시자의 **구독 속성** 대화 상자를 사용하여 밀어넣기 구독에 대한 속성을 보고 설정할 수 있습니다. 끌어오기 구독에 대한 일부 속성도 볼 수 있지만 구독자의 **구독 속성** 대화 상자는 추가 속성을 표시하고 속성을 수정할 수 있게 해줍니다.  
  
 **구독 속성** 대화 상자의 각 속성에는 설명이 포함되어 있습니다. 속성을 클릭하면 대화 상자 아래쪽에 해당 설명이 표시됩니다. 이 항목에서는 밀어넣기 구독인 경우에만 게시자에 표시되는 여러 속성에 대한 추가 정보를 제공합니다. 속성은 다음 범주로 그룹화됩니다.  
  
-   모든 구독에 적용되는 속성    
-   트랜잭션 구독에 적용되는 속성    
-   병합 구독에 적용되는 속성  
  
 옵션이 읽기 전용으로 표시되면 구독을 만들 때만 해당 옵션을 설정할 수 있습니다. 새 구독 마법사에서 사용할 수 없는 옵션을 설정하려면 저장 프로시저를 사용하여 구독을 만듭니다. 자세한 내용은 [Create a Pull Subscription](create-a-pull-subscription.md) 및 [Create a Push Subscription](create-a-push-subscription.md)를 참조하세요.  

  
### <a name="options-for-all-subscriptions"></a>모든 구독에 대한 옵션  
 **보안**  
 **에이전트 프로세스 계정** 행을 클릭한 다음 속성 단추 (**...**)를 클릭하여 배포자에서 배포 에이전트 또는 병합 에이전트가 실행되는 계정을 변경합니다. 배포 에이전트 또는 병합 에이전트가 구독자로 연결하는 계정을 변경하려면 **구독자 연결**을 클릭한 다음 속성 단추 (**...**)를 클릭합니다.  
  
 각 에이전트에 필요한 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](security/replication-agent-security-model.md)을 참조하십시오.  
  
### <a name="publisher-options-for-transactional-subscriptions"></a>트랜잭션 구독에 대한 게시자 옵션  
 **트랜잭션 루핑 방지**  
 배포 에이전트가 구독자에서 나온 트랜잭션을 다시 구독자에 전송하는지 여부를 결정합니다. 이 옵션은 양방향 트랜잭션 복제에 사용됩니다. 자세한 내용은 [양방향 트랜잭션 복제](transactional/bidirectional-transactional-replication.md)를 참조 하세요.  
  
 **업데이트할 수 있는 구독**  
 구독자 변경 내용을 게시자로 다시 복제할 것인지 여부를 결정합니다. 지연 업데이트 또는 즉시 업데이트를 사용하여 변경 내용을 복제할 수 있습니다. **구독자 업데이트 방법** 은 사용할 방법을 결정합니다. 자세한 내용은 [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md)를 참조하세요.  
  
### <a name="options-for-merge-subscriptions"></a>병합 구독에 대한 옵션  
 **파티션 정의(HOST_NAME)**  
 매개 변수가 있는 필터를 사용하는 게시의 경우 병합 복제는 동기화하는 동안 **SUSER_SNAME()** 또는 **HOST_NAME()** 이라는 두 시스템 함수 중 하나(또는 필터가 두 함수를 참조하는 경우 둘 다)를 평가하여 구독자가 수신할 데이터를 결정합니다. 기본적으로 **HOST_NAME()** 은 병합 에이전트가 실행 중인 컴퓨터의 이름을 반환하지만 새 구독 마법사에서 이 값을 재정의할 수 있습니다. 매개 변수가 있는 필터에 대한 자세한 내용과 **HOST_NAME()** 을 재정의하는 방법은 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)를 참조하십시오.  
  
 **구독 유형** 및 **우선 순위**  
 구독이 클라이언트 구독인지 서버 구독인지를 표시합니다. 구독을 만든 후에는 구독 유형을 변경할 수 없습니다. 서버 구독은 데이터를 다른 구독자에 다시 게시할 수 있으며 충돌 해결을 위한 우선 순위를 할당 받을 수 있습니다.  
  
 새 구독 마법사에서 서버 구독 유형을 선택한 경우 구독자에는 충돌을 해결하는 동안 사용되는 우선 순위가 지정됩니다.  
  
 **대화형으로 충돌 해결**  
 병합 동기화를 수행하는 동안 충돌을 해결하기 위해 대화형 해결 프로그램 사용자 인터페이스를 사용할지 여부를 결정합니다. 이 인터페이스를 사용하려면 **Windows 동기화 관리자 사용** 값을 **사용**으로 설정해야 합니다. 자세한 내용은 [Interactive Conflict Resolution](merge/advanced-merge-replication-conflict-interactive-resolution.md)을 참조하세요.  


## <a name="subscriber-properties"></a>구독자 속성
  구독자에서 **구독 속성** 대화 상자를 사용하여 끌어오기 구독에 대한 속성을 보고 설정할 수 있습니다.  
  
 **구독 속성** 대화 상자의 각 속성에는 설명이 포함되어 있습니다. 속성을 클릭하면 대화 상자 아래쪽에 해당 설명이 표시됩니다. 이 항목에서는 여러 가지 속성에 대한 추가 정보를 제공합니다. 속성은 다음 범주로 그룹화됩니다.  
  
-   모든 구독에 적용되는 속성    
-   트랜잭션 구독에 적용되는 속성   
-   병합 구독에 적용되는 속성  
  
 옵션이 읽기 전용으로 표시되면 구독을 만들 때만 해당 옵션을 설정할 수 있습니다. 새 구독 마법사에서 사용할 수 없는 옵션을 설정하려면 저장 프로시저를 사용하여 구독을 만듭니다. 자세한 내용은 [Create a Pull Subscription](create-a-pull-subscription.md) 및 [Create a Push Subscription](create-a-push-subscription.md)를 참조하세요.  
  
> [!NOTE]  
>  구독에 대한 배포 에이전트 또는 병합 에이전트 작업이 아직 생성되지 않은 경우 많은 구독 속성이 표시되지 않습니다. 끌어오기 구독에 대한 에이전트 작업을 만들려면 [sp_addpullsubscription_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)(스냅샷 또는 트랜잭션 게시에 대한 구독) 또는 [sp_addmergepullsubscription_agent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)(병합 게시에 대한 구독)을 실행합니다.  
  
### <a name="options-for-all-subscriptions"></a>모든 구독에 대한 옵션  
 **스냅샷에서 게시된 데이터 초기화**  
 구독을 스냅샷으로 초기화할 것인지(기본값), 아니면 다른 방법으로 초기화할 것인지를 결정합니다. 구독 초기화에 대한 자세한 내용은 [구독 초기화](initialize-a-subscription.md)를 참조하세요.  
  
 **스냅샷 위치**  
 초기화 또는 다시 초기화 중에 스냅샷 파일에 액세스하는 위치를 결정합니다. 다음 위치 값 중 하나가 표시됩니다.  
  
-   **기본 위치**: 배포자를 구성할 때 정의되는 기본 위치입니다. 자세한 내용은 [기본 스냅숏 위치 지정](snapshot-options.md#snapshot-folder-locations)을 참조 하세요.    
-   **대체 폴더**: **게시 속성** 대화 상자에서 지정할 수 있는 대체 폴더입니다. 자세한 내용은 [Alternate Snapshot Folder Locations](alternate-snapshot-folder-locations.md)을 참조하세요.    
-   **동적 스냅샷 폴더**: 매개 변수가 있는 행 필터를 사용하는 병합 게시에 대한 스냅샷 위치입니다. 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md)을(를) 참조하세요.  
-   **FTP 폴더**: FTP(파일 전송 프로토콜) 서버에 액세스할 수 있는 폴더입니다. 자세한 내용은 [FTP를 통해 스냅샷 전송](transfer-snapshots-through-ftp.md)을 참조하세요.  
  
 **스냅샷 폴더**  
 **스냅샷 위치** 옵션에 대해 **기본 위치** 이외의 값을 선택하는 경우 스냅샷 폴더의 경로를 지정해야 합니다.  
  
 **Windows 동기화 관리자 사용**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 동기화 관리자를 사용하여 이 구독을 동기화할 수 있는지 여부를 결정합니다.  
  
 **보안**  
 **에이전트 프로세스 계정** 행을 클릭한 다음 속성 단추 (**...**)를 클릭하여 구독자에서 배포 에이전트 또는 병합 에이전트를 실행하는 계정을 변경합니다. 연결과 관련된 보안 옵션은 구독 유형에 따라 달라집니다.  
  
-   트랜잭션 게시에 대한 구독의 경우: 배포 에이전트를 배포자에 연결하는 계정을 변경하려면 **배포자 연결**을 클릭한 다음 속성 단추(**...**)를 클릭합니다.    
-   트랜잭션 게시에 대한 즉시 업데이트 구독의 경우: 위에서 설명한 배포자 연결 외에도 구독자에서 게시자로 변경 내용을 전파하는 데 사용하는 방법을 변경할 수 있습니다. **게시자 연결**을 클릭한 다음 속성 단추(**...**)를 클릭합니다.  
-   병합 게시에 대한 구독: **게시자 연결**을 클릭한 다음 속성 단추 (**...**)를 클릭합니다.  
  
 각 에이전트에 필요한 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](security/replication-agent-security-model.md)을 참조하십시오.  
  
### <a name="options-for-transactional-subscriptions"></a>트랜잭션 구독에 대한 옵션  
 **업데이트할 수 있는 구독**  
 구독자 변경 내용을 게시자로 다시 복제할 것인지 여부를 결정합니다. 지연 업데이트 또는 즉시 업데이트를 사용하여 변경 내용을 복제할 수 있습니다. **구독자 업데이트 방법** 은 사용할 방법을 결정합니다. 자세한 내용은 [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md)를 참조하세요.  
  
### <a name="options-for-merge-subscriptions"></a>병합 구독에 대한 옵션  
 **파티션 정의(HOST_NAME)**  
 매개 변수가 있는 필터를 사용하는 게시의 경우 병합 복제는 동기화하는 동안 **SUSER_SNAME()** 또는 **HOST_NAME()** 이라는 두 시스템 함수 중 하나(또는 필터가 두 함수를 참조하는 경우 둘 다)를 평가하여 구독자가 수신할 데이터를 결정합니다. 기본적으로 **HOST_NAME()** 은 병합 에이전트가 실행 중인 컴퓨터의 이름을 반환하지만 새 구독 마법사에서 이 값을 재정의할 수 있습니다. 매개 변수가 있는 필터에 대한 자세한 내용과 **HOST_NAME()** 을 재정의하는 방법은 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)를 참조하십시오.  
  
 **구독 유형** 및 **우선 순위**  
 구독이 클라이언트 구독인지 서버 구독인지를 표시합니다. 구독을 만든 후에는 구독 유형을 변경할 수 없습니다. 서버 구독은 데이터를 다른 구독자에 다시 게시할 수 있으며 충돌 해결을 위한 우선 순위를 할당 받을 수 있습니다.  
  
 새 구독 마법사에서 서버 구독 유형을 선택한 경우 구독자에는 충돌을 해결하는 동안 사용되는 우선 순위가 지정됩니다.  
  
 **대화형으로 충돌 해결**  
 병합 동기화를 수행하는 동안 충돌을 해결하기 위해 대화형 해결 프로그램 사용자 인터페이스를 사용할지 여부를 결정합니다. 이 인터페이스를 사용하려면 **Windows 동기화 관리자 사용** 값을 **사용**으로 설정해야 합니다. 자세한 내용은 [Interactive Conflict Resolution](merge/advanced-merge-replication-conflict-interactive-resolution.md)을 참조하세요.  
  
 **웹 동기화**  
 **웹 동기화 사용** 은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 인터넷 정보 서비스(IIS) 서버에 연결하여 구독을 동기화할지 여부를 결정합니다. 이 옵션은 게시가 웹 동기화용으로 설정되어 있는 경우에만 사용할 수 있습니다. 자세한 내용은 [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md)를 참조하세요.  
  
 **웹 동기화 사용** 에 대해 **True**를 선택한 경우 다음을 수행하십시오.  
  
-   **웹 서버 주소**에 IIS 서버의 전체 주소를 입력합니다.   
-   **웹 서버 연결** 행을 클릭한 다음 속성 단추 (**...**)를 클릭하여 구독자를 IIS 서버에 연결하는 계정을 설정 또는 변경합니다.   
-   필요한 경우 **웹 서버 제한 시간** 을 변경합니다. 제한 시간은 웹 동기화 요청이 만료되기 전까지의 시간(초)입니다.  
  
 구성에 대한 자세한 내용은 [Configure Web Synchronization](configure-web-synchronization.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [끌어오기 구독 속성 보기 및 수정](view-and-modify-pull-subscription-properties.md)   
 [밀어넣기 구독 속성 보기 및 수정](view-and-modify-push-subscription-properties.md)   
 [Subscribe to Publications](subscribe-to-publications.md)  
  
  
