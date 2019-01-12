---
title: 게시 정보, 에이전트(트랜잭션 게시) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.downlevelagents.tran.f1
ms.assetid: 38ef2f54-53bb-4053-876d-86f8f06a4519
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7a4542370eff5ad631701f0bf988929ad56e8799
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54125823"
---
# <a name="publication-information-agents-transactional-publication"></a>게시 정보, 에이전트(트랜잭션 게시)
  **에이전트** 탭은 선택한 게시에 대한 에이전트의 요약 정보를 표시합니다. 스냅숏 에이전트 및 로그 판독기 에이전트에 대한 정보는 모든 트랜잭션 게시에 대해 표시됩니다. 큐 판독기 에이전트에 대한 정보는 지연 업데이트 구독이 설정된 트랜잭션 게시에 대해 표시됩니다.  
  
## <a name="options"></a>변수  
 에이전트 관련 태스크와 자세한 정보를 보려면 해당 에이전트에 대한 행을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 옵션을 클릭합니다. 표에서 데이터를 표시하는 방식을 변경하려면 표를 마우스 오른쪽 단추로 클릭한 후 다음 옵션 중 하나를 클릭합니다.  
  
-   **정렬**: 하나 이상의 열에 정렬 된 **정렬 열** 대화 상자.  
  
-   **표시할 열 선택**: 열을 표시 및 표시 되는 순서를 선택 합니다 **열 선택** 대화 상자.  
  
-   **필터**: 열 값에 따라 표의 행을 필터링 합니다 **필터 설정** 대화 상자.  
  
-   **필터 지우기**: 표에 대한 모든 필터 설정을 지웁니다.  
  
 필터 설정은 각 표에 대해 지정됩니다. 열 선택 및 정렬은 각 게시자에 대한 게시 표와 같이 동일한 유형의 모든 표에 적용됩니다.  
  
 **상태**  
 게시와 연결된 각 복제 에이전트의 상태입니다. 다음 목록에서는 가능한 상태 값을 보여 줍니다.  
  
-   Error  
  
-   실패한 명령 다시 시도 중  
  
-   실행 중이 아님  
  
-   실행 중  
  
-   완료  
  
 **에이전트**  
 게시와 연결된 각 복제 에이전트의 이름입니다. 배포 에이전트는 이 게시에 대한 구독과 연결됩니다. 자세한 내용은 [정보 보기 및 태스크 수행 복제 모니터를 사용 하 여](monitor/view-information-and-perform-tasks-replication-monitor.md)입니다.  
  
 **마지막 시작 시간**  
 마지막으로 에이전트가 시작된 시간입니다.  
  
 **기간**  
 에이전트가 실행된 시간입니다. 에이전트가 현재 실행되고 있는 경우 이 시간은 경과된 시간을 나타내고 에이전트가 이전에 실행된 경우에는 총 시간을 나타냅니다.  
  
 **마지막 동작**  
 가장 최근의 에이전트 실행에서 수행된 마지막 동작입니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 모니터 시작](monitor/start-the-replication-monitor.md)   
 [정보 및 복제 모니터를 사용 하 여 수행할 작업 보기](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [복제 모니터링](monitoring-replication.md)  
  
  
