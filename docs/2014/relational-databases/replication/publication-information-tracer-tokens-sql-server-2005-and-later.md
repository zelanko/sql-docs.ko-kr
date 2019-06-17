---
title: 게시 정보, 추적 프로그램 토큰 (트랜잭션 게시, SQL Server 2005 이상) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.tracertokens.f1
ms.assetid: a115ba95-17ae-45df-91bd-5a1a35f3745f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 287d565947a13621fd3ba39cff6437ff76894c03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63021695"
---
# <a name="publication-information-tracer-tokens-transactional-publication-sql-server-2005-and-later"></a>게시 정보, 추적 프로그램 토큰(트랜잭션 게시, SQL Server 2005 이상)
  **추적 프로그램 토큰** 탭을 사용하여 연결 유효성을 검사하고 트랜잭션 복제를 사용하는 시스템의 대기 시간을 측정할 수 있습니다. 토큰(적은 양의 데이터)은 게시 데이터베이스의 트랜잭션 로그에 기록되고, 일반적인 복제된 트랜잭션인 것처럼 표시되고, 시스템을 통해 전달되며 다음을 계산할 수 있습니다.  
  
-   게시자에서 커밋된 트랜잭션과 배포자의 배포 데이터베이스에서 삽입된 해당 명령 사이의 경과 시간  
  
-   배포 데이터베이스에 삽입된 명령과 구독자에서 커밋된 해당 트랜잭션 사이의 경과 시간  
  
 이러한 계산을 잘 검토하면 다음을 비롯한 여러 가지 질문에 대답할 수 있습니다.  
  
-   게시자의 변경 내용을 받는 데 가장 오래 걸리는 구독자는 무엇입니까?  
  
-   추적 프로그램 토큰을 받아야 할 구독자가 있습니까? 있다면 아직 추적 프로그램 토큰을 받지 못한 구독자는 무엇입니까?  
  
## <a name="options"></a>변수  
 표에서 데이터를 표시하는 방식을 변경하려면 표를 마우스 오른쪽 단추로 클릭한 후 다음 옵션 중 하나를 클릭합니다.  
  
-   **정렬**: **열 정렬** 대화 상자에서 한 개 이상의 열에 대해 정렬합니다.  
  
-   **표시할 열 선택**: **열 선택** 대화 상자에서 표시할 열 및 해당 열이 표시되는 순서를 선택합니다.  
  
-   **필터**: **필터 설정** 대화 상자의 열 값에 따라 표의 행을 필터링합니다.  
  
-   **필터 지우기**: 표에 대 한 모든 필터 설정을 지웁니다.  
  
 필터 설정은 각 표에 대해 지정됩니다. 열 선택 및 정렬은 각 게시자에 대한 게시 표와 같이 동일한 유형의 모든 표에 적용됩니다.  
  
 **추적 프로그램 삽입**  
 게시자에서 트랜잭션 로그에 추적 프로그램 토큰을 삽입하려면 클릭합니다.  
  
 **삽입된 시간**  
 추적 프로그램 토큰이 삽입된 시간을 선택하여 해당 시간의 대기 시간 정보를 표시합니다. 기본적으로 가장 최근 시간의 정보가 표시됩니다.  
  
> [!NOTE]  
>  추적 프로그램 토큰 정보는 배포 데이터베이스의 기록 보존 기간에 의해 제어되는 다른 기록 데이터와 같은 시간 동안 유지됩니다. 배포 데이터베이스 속성 변경에 대한 자세한 내용은 [게시자 및 배포자 속성 보기 및 수정](view-and-modify-distributor-and-publisher-properties.md)을 참조하세요.  
  
 **구독**  
 게시에 대한 각 구독의 이름입니다.  
  
 **게시자에서 배포자로 연결**  
 게시자에서 트랜잭션이 커밋되는 시점과 배포자에서 배포 데이터베이스에 해당 명령이 삽입되는 시점 간에 경과한 시간입니다. 값 **보류 중** 은 토큰이 배포자에 아직 도달하지 않았음을 나타냅니다. 보류 상태가 지속되면 로그 판독기 에이전트가 실행 중인지 확인하십시오.  
  
 **배포자에서 구독자로 연결**  
 배포 데이터베이스에 명령이 삽입되는 시점과 구독자에서 해당 트랜잭션이 커밋되는 시점 간에 경과한 시간입니다. 값 **보류 중** 은 토큰이 구독자에 아직 도달하지 않았음을 나타냅니다. 보류 상태가 지속되면 배포 에이전트가 실행 중인지 확인하십시오.  
  
 **총 대기 시간**  
 게시자에서 트랜잭션이 커밋되는 시점과 구독자에서 해당 트랜잭션이 커밋되는 시점 간에 경과한 시간입니다. 이 시간은 현재 이 구독자에 대한 복제 시스템의 종단 간 대기 시간을 나타냅니다. 값 **보류 중** 은 토큰이 구독자에 아직 도달하지 않았음을 나타냅니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [복제 모니터 시작](monitor/start-the-replication-monitor.md)   
 [트랜잭션 복제에 대한 대기 시간 측정 및 연결 유효성 검사](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [복제 모니터로 성능 모니터링](monitor/monitor-performance-with-replication-monitor.md)   
 [복제 모니터링](monitoring-replication.md)   
 [복제 에이전트 개요](agents/replication-agents-overview.md)  
  
  
