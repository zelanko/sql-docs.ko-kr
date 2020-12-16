---
title: 복제 에이전트 모니터링 | Microsoft 문서
description: SQL Server 복제 모니터는 복제 작업에 대한 구조적 뷰를 제공하며 특정 에이전트에 대한 정보를 찾을 수 있게 해 줍니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], agents
- Log Reader Agent, monitoring
- Replication Monitor, agents
- Merge Agent, monitoring
- Queue Reader Agent, monitoring
- Snapshot Agent, monitoring
- agents [SQL Server replication], monitoring
- Distribution Agent, monitoring
ms.assetid: d06ed24f-82d7-4b9e-9e40-cc9780476a71
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: ddaa4698033f06db589ca550f39d434173e012e7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477844"
---
# <a name="monitor-replication-agents"></a>복제 에이전트 모니터링
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제 모니터는 복제 작업에 대한 구조적 뷰를 제공할 뿐만 아니라 특정 에이전트에서 정보를 간단하게 찾을 수 있게 해줍니다. 다음 목록에는 각 에이전트, 에이전트를 찾을 수 있는 복제 모니터의 탭 및 이러한 탭에 액세스하는 방법을 설명하는 항목에 대한 링크가 포함되어 있습니다.  
  
-   다음 에이전트는 복제 모니터에서 게시와 연결됩니다.  
  
    -   스냅샷 에이전트  
  
    -   로그 판독기 에이전트  
  
    -   큐 판독기 에이전트  
  
     이러한 에이전트와 연결된 정보 및 작업은 **에이전트**(각 게시자 및 구독에 대해 사용 가능) 및 **경고**(각 게시에 대해 사용 가능) 탭을 통해 액세스할 수 있습니다. 자세한 내용은 [복제 모니터를 사용하여 정보 보기 및 태스크 수행](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)을 참조하세요.  
  
-   다음 에이전트는 복제 모니터에서 구독과 연결됩니다.  
  
    -   배포 에이전트  
  
    -   병합 에이전트  
  
     이러한 에이전트와 연결된 정보 및 작업은 **구독 조사 목록**(각 게시자에 대해 사용 가능) 또는 **모든 구독** 탭(각 게시에 대해 사용 가능)을 통해 액세스할 수 있습니다. 자세한 내용은 [복제 모니터를 사용하여 정보 보기 및 태스크 수행](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)을 참조하세요.  
  
## <a name="using-sql-server-management-studio-to-monitor-replication-agents"></a>SQL Server Management Studio를 사용하여 복제 에이전트 모니터링  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]는 복제 에이전트 모니터링을 위한 다음 대화 상자를 제공합니다.  
  
-   **스냅샷 에이전트 상태 보기** (모든 게시용)  
  
-   **로그 판독기 에이전트 상태 보기** (모든 트랜잭션 게시용)  
  
-   **동기화 상태 보기** (모든 구독용. 이 대화 상자로 배포 에이전트 및 병합 에이전트에 액세스할 수 있음)  
  
 복제 모니터는 각 에이전트에 대한 추가 정보를 제공하고 큐 판독기 에이전트 사용 시 해당 에이전트를 모니터링합니다. 자세한 내용은 [복제 모니터를 사용하여 정보 보기 및 태스크 수행](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)을 참조하세요.
  
#### <a name="to-monitor-the-snapshot-agent-and-log-reader-agent"></a>스냅샷 에이전트 및 로그 판독기 에이전트를 모니터링하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  게시를 마우스 오른쪽 단추로 클릭한 다음 **로그 판독기 에이전트 상태 보기** 또는 **스냅샷 에이전트 상태 보기** 를 클릭합니다.  
  
4.  **로그 판독기 에이전트 상태 보기** 또는 **스냅샷 에이전트 상태 보기** 대화 상자에서 다음을 수행하십시오.  
  
    -   에이전트 상태를 확인합니다.  
  
    -   필요에 맞게 에이전트를 시작 또는 중지합니다.  
  
    -   **모니터** 를 클릭하여 **복제 모니터** 를 시작합니다.  
  
5.  **닫기** 를 클릭합니다.  
  
#### <a name="to-monitor-the-distribution-agent-and-merge-agent-from-the-publisher"></a>게시자에서 배포 에이전트 및 병합 에이전트를 모니터링하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  모니터링할 구독에 대한 게시를 확장합니다.  
  
4.  해당 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 상태 보기** 를 클릭합니다.  
  
5.  **동기화 상태 보기** 대화 상자에서 다음을 수행하십시오.  
  
    -   에이전트 상태를 확인합니다.  
  
    -   필요에 맞게 에이전트를 시작 또는 중지합니다.  
  
    -   밀어넣기 구독의 경우 **모니터** 를 클릭하여 **복제 모니터** 를 시작합니다.  
  
    -   끌어오기 구독의 경우 **작업 기록 보기** 를 클릭하여 에이전트 로그의 출력을 표시하는 **로그 파일 뷰어** 를 시작합니다.  
  
6.  **닫기** 를 클릭합니다.  
  
#### <a name="to-monitor-the-distribution-agent-and-merge-agent-from-the-subscriber"></a>구독자에서 배포 에이전트 및 병합 에이전트를 모니터링하려면  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]에서 구독자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 구독** 폴더를 확장합니다.  
  
3.  모니터링할 구독을 마우스 오른쪽 단추로 클릭한 다음 **동기화 상태 보기** 를 클릭합니다.  
  
4.  **동기화 상태 보기** 대화 상자에서 다음을 수행하십시오.  
  
    -   에이전트 상태를 확인합니다.  
  
    -   필요에 맞게 에이전트를 시작 또는 중지합니다.  
  
    -   **작업 기록 보기** 를 클릭하여 에이전트 로그의 출력을 표시하는 **로그 파일 뷰어** 를 시작합니다.  
  
5.  **닫기** 를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 에이전트 개요](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
