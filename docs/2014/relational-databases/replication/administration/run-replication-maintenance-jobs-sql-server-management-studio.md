---
title: 복제 유지 관리 작업 실행(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server replication]
ms.assetid: 0dc485a0-5a50-41eb-a29d-f2b2fb920174
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 19faa0690069d6c16be7591547f4a242ac2469fc
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52805588"
---
# <a name="run-replication-maintenance-jobs-sql-server-management-studio"></a>복제 유지 관리 작업 실행(SQL Server Management Studio)
  복제는 다음 유지 관리 작업을 사용합니다.  
  
-   **데이터 유효성 검사에 실패한 구독 다시 초기화**  
  
-   **에이전트 기록 정리: 배포**  
  
-   **배포에 대한 복제 모니터링 리프레셔**  
  
-   **복제 에이전트 점검**  
  
-   **배포 기록 정리: 배포**  
  
-   **만료된 구독 정리**  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]의 **Jobs** 폴더와 복제 모니터의 **에이전트** 탭에서 이러한 작업을 시작하고 중지합니다. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../monitor/start-the-replication-monitor.md)을 참조하세요. 동일한 폴더와 탭에서 사용 가능한 **작업 속성 - \<Job>** 대화 상자에서 각 작업의 속성을 보고 수정합니다.  
  
### <a name="to-start-or-stop-a-replication-maintenance-job-in-management-studio"></a>Management Studio에서 복제 유지 관리 작업을 시작하거나 중지하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 배포자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **SQL Server 에이전트** 폴더를 확장한 다음 **작업** 폴더를 확장합니다.  
  
3.  작업을 마우스 오른쪽 단추로 클릭한 다음 **작업 시작** 또는 **작업 중지**를 클릭합니다.  
  
### <a name="to-start-or-stop-a-replication-maintenance-job-in-replication-monitor"></a>복제 모니터에서 복제 유지 관리 작업을 시작하거나 중지하려면  
  
1.  복제 모니터에서 게시자 그룹을 확장한 다음 해당 게시자를 선택합니다.  
  
2.  **에이전트** 탭을 클릭합니다.  
  
3.  표에서 작업을 마우스 오른쪽 단추로 클릭한 다음 **작업 시작** 또는 **작업 중지**를 클릭합니다.  
  
### <a name="to-view-and-modify-properties-for-a-replication-maintenance-job-in-management-studio"></a>Management Studio에서 복제 유지 관리 작업의 속성을 보고 수정하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 배포자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **SQL Server 에이전트** 폴더를 확장한 다음 **작업** 폴더를 확장합니다.  
  
3.  작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **작업 속성 - \<Job>** 대화 상자에서 필요한 경우 속성을 수정한 다음 **확인**을 클릭합니다.  
  
### <a name="to-view-and-modify-properties-for-a-replication-maintenance-job-in-replication-monitor"></a>복제 모니터에서 복제 유지 관리 작업의 속성을 보고 수정하려면  
  
1.  복제 모니터에서 게시자 그룹을 확장한 다음 해당 게시자를 선택합니다.  
  
2.  **에이전트** 탭을 클릭합니다.  
  
3.  표에서 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **작업 속성 - \<Job>** 대화 상자에서 필요한 경우 속성을 수정한 다음 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [게시자에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [복제 에이전트 관리](../agents/replication-agent-administration.md)  
  
  
