---
title: "병합 게시에 대한 데이터 충돌 보기 및 해결 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3b82b75bafb038123cf460266d195497972fbf08
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="view-and-resolve-data-conflicts-for-merge-publications"></a>병합 게시에 대한 충돌 보고 및 해결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  병합 복제에서의 충돌은 각 아티클에 대해 지정된 해결 프로그램에 따라 해결됩니다. 기본적으로 충돌은 사용자가 개입할 필요 없이 해결됩니다. 그러나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 복제 충돌 뷰어에서 충돌을 보고 해결 결과를 변경할 수 있습니다.  
  
 지정된 충돌 보존 기간(기본값: 14일) 동안 복제 충돌 뷰어에서 충돌 데이터를 확인할 수 있습니다. 충돌 보존 기간을 설정하려면 다음 중 하나를 수행하십시오.  
  
-   [sp_addmergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)의 **@conflict_retention** 매개 변수에 보존 값을 지정합니다.  
  
-   **@property** 매개 변수에 대해 **conflict_retention** 값을 지정하고 [sp_changemergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)의 **@value** 매개 변수에 대해 보존 값을 지정합니다.  
  
 기본적으로 충돌 정보는 다음 위치에 저장됩니다.  
  
-   게시 호환성 수준이 90RTM 이상일 경우 게시자 및 구독자.  
  
-   게시 호환성 수준이 80RTM 미만일 경우 게시자  
  
-   구독자가 [!INCLUDE[ssEW](../../includes/ssew-md.md)]을 실행하는 경우 게시자. 충돌 데이터는 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자에 저장할 수 없습니다.  
  
 충돌 정보의 저장소는 **conflict_logging** 게시 속성에 의해 제어됩니다. 자세한 내용은 [sp_addmergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 및 [sp_changemergepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)을 참조하세요.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 대화형 해결 프로그램을 사용하여 동기화하는 동안 대화형으로 충돌을 해결할 수도 있습니다. 대화형 해결 프로그램은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 동기화 관리자를 통해 사용할 수 있습니다. 자세한 내용은 [Windows 동기화 관리자를 사용하여 구독 동기화&#40;Windows 동기화 관리자&#41;](../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md)를 참조하세요.  
  
### <a name="to-view-and-resolve-conflicts-for-merge-publications"></a>병합 게시에 대한 충돌을 보고 해결하려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자(또는 구독자)에 연결한 다음 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  충돌을 확인할 게시를 마우스 오른쪽 단추로 클릭한 다음 **충돌 보기**를 클릭합니다.  
  
    > [!NOTE]  
    >  **conflict_logging** 속성에 **'subscriber'** 값을 지정한 경우에는 **충돌 보기** 메뉴 옵션을 사용할 수 없습니다. 충돌을 보려면 명령 프롬프트에서 ConflictViewer.exe를 시작합니다. 기본적으로 ConflictViewer.exe는 Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE 디렉터리에 있습니다. 유효한 시작 매개 변수 목록을 보려면 ConflictViewer.exe -?를 실행합니다.  
  
4.  **충돌 테이블 선택** 대화 상자에서 충돌을 확인하려는 데이터베이스, 게시 및 테이블을 선택합니다.  
  
5.  복제 충돌 뷰어에서 다음을 수행할 수 있습니다.  
  
    -   상단 표 오른쪽의 단추를 사용하여 행을 필터링합니다.  
  
    -   상단 표에서 행을 선택하여 해당 행에 대한 정보를 하단 표에 표시합니다.  
  
    -   상단 표에서 하나 이상의 행을 선택한 다음 **제거**를 클릭합니다. 이것은 **적용되는 내용 전송** 단추를 클릭하는 것과 같으며 데이터는 변경되지 않습니다.  
  
    -   속성 단추 (**...**)를 클릭하여 충돌과 관련된 열에 대한 자세한 정보를 확인합니다.  
  
    -   데이터를 전송하기 전에 **충돌 시 적용되는 내용** 또는 **충돌 시 변경 내용 무시** 열의 데이터를 편집합니다. 열이 회색인 경우 데이터는 읽기 전용입니다.  
  
    -   **적용되는 내용 전송** 을 클릭하면 충돌 시 적용되도록 지정한 행을 적용합니다.  
  
    -   **무시되는 내용 전송** 을 클릭하면 해결을 재정의하고 충돌 시 무시되도록 지정한 값을 토폴로지의 모든 노드로 전파합니다.  
  
    -   **이 충돌 정보 기록** 을 선택하여 충돌 데이터를 파일에 기록합니다. 파일의 위치를 지정하려면 **보기** 메뉴를 가리킨 다음 **옵션**을 클릭합니다. 값을 입력하거나 찾아보기 단추 (**...**)를 클릭한 다음 해당 파일을 검색합니다. **확인** 을 클릭하여 **옵션** 대화 상자를 종료합니다.  
  
6.  복제 충돌 뷰어를 닫습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [병합 아티클 해결 프로그램 지정](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
  
