---
title: 게시자 정보, 게시 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publisherinfo.publications.f1
ms.assetid: 0b2e3d4e-03b7-4c31-8f96-48648d750010
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3a1725843b5d893ea8ef6f884252a4b2f5cdd6d4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48152669"
---
# <a name="publisher-information-publications"></a>게시자 정보, 게시
  **게시** 탭은 왼쪽 창에서 선택한 게시자에서의 모든 게시에 대한 요약 정보를 제공합니다.  
  
## <a name="options"></a>변수  
 표에서 데이터를 표시하는 방식을 변경하려면 표를 마우스 오른쪽 단추로 클릭한 후 다음 옵션 중 하나를 클릭합니다.  
  
-   **정렬**: **열 정렬** 대화 상자에서 한 개 이상의 열에 대해 정렬합니다.  
  
-   **표시할 열 선택**: **열 선택** 대화 상자에서 표시할 열 및 해당 열이 표시되는 순서를 선택합니다.  
  
-   **필터**: **필터 설정** 대화 상자의 열 값에 따라 표의 행을 필터링합니다.  
  
-   **필터 지우기**: 표에 대한 모든 필터 설정을 지웁니다.  
  
 필터 설정은 각 표에 대해 지정됩니다. 열 선택 및 정렬은 각 게시자에 대한 게시 표와 같이 동일한 유형의 모든 표에 적용됩니다.  
  
 **상태**  
 해당 구독의 가장 높은 우선 순위 상태에 의해 결정되는 각 게시 상태입니다. 기본적으로 게시 정보가 포함된 표는 **상태** 열을 기준으로 정렬됩니다. 다음 목록에서는 가능한 상태 값 및 값 정렬 순서를 보여 줍니다. 예를 들어 오류는 항상 표의 맨 위에 표시됩니다.  
  
-   Error  
  
-   성능 심각  
  
-   실패한 명령 다시 시도 중  
  
-   확인  
  
 상태 값 **성능 심각** 은 트랜잭션 구독과 병합 구독에 적용되며 트랜잭션 구독의 경우 임계값이 설정된 경우에만 표시할 수 있습니다. 성능 측정 및 임계값 설정에 대한 자세한 내용은 [복제 모니터로 성능 모니터링](monitor/monitor-performance-with-replication-monitor.md) 및 [복제 모니터에 임계값 및 경고 설정](monitor/set-thresholds-and-warnings-in-replication-monitor.md)을 참조하세요.  
  
 **게시**  
 *PublicationDatabaseName: PublicationName*형식의 각 게시의 이름입니다.  
  
 **구독**  
 각 게시에 대한 구독 수입니다.  
  
 **동기화 중**  
 각 게시에 대해 현재 동기화 중인 구독 수입니다.  
  
-   트랜잭션 복제에서 "동기화 중"은 배포 에이전트가 실행 중이지만 데이터를 반드시 복제할 필요가 없음을 의미합니다.  
  
-   병합 복제에서 "동기화 중"은 병합 에이전트가 실행 중이며 데이터가 현재 복제되고 있음을 의미합니다.  
  
-   스냅숏 복제에서 "동기화 중"은 배포 에이전트가 실행 중이며 데이터가 현재 복제되고 있음을 의미합니다.  
  
 **현재 평균 성능** 및 **현재 가장 낮은 성능**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에만 해당됩니다. 게시에 대한 모든 구독의 평균 성능 등급과 가장 낮은 성능 등급입니다. 등급은 복제 모니터에서 측정한 가장 최근 측정값을 기반으로 하며 이전 구독 성능을 반영하지 않습니다.  
  
 트랜잭션 복제의 경우 복제 모니터는 성능 임계값이 정의된 게시에 대해서만 값을 표시합니다. 게시에 대해 성능 임계값을 정의하지 않으면 이 열에 **사용 안 함**이 표시됩니다. 병합 복제의 경우 복제 모니터는 같은 유형의 연결(전화 접속 또는 LAN)별로 50개 이상의 변경 사항을 5번 동기화한 후에 값을 표시합니다. 50개 이상의 변경 사항에 대해 동기화가 5번 미만으로 수행되었거나 가장 최근에 동기화가 수행된 변경 사항이 50개 미만인 경우에는 이 열이 비어 있습니다.  
  
 성능 등급은 다음 값 중 하나입니다.  
  
-   최고  
  
-   좋음  
  
-   보통  
  
-   나쁨  
  
-   심각  
  
 성능 등급 정의 방법 및 성능 임계값 설정 방법은 [복제 모니터로 성능 모니터링](monitor/monitor-performance-with-replication-monitor.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [복제 모니터 시작](monitor/start-the-replication-monitor.md)   
 [게시자에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [복제 모니터링](monitoring-replication.md)  
  
  
