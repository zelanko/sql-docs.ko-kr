---
title: 게시자 정보, 구독 조사 목록 (스냅숏 게시, SQL Server 2005 이상) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publisherinfo.subscriptionssummary.snapshot.f1
ms.assetid: 2ebeee62-7f54-4c77-9d37-15708bc5cc23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0b84f87aff9684cc08fc0d91fc5de364f816125a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63262152"
---
# <a name="publisher-information-subscription-watch-list-snapshot-publication-sql-server-2005-and-later"></a>게시자 정보, 구독 조사 목록(스냅샷 게시, SQL Server 2005 이상)
  **구독 조사 목록** 탭은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전을 실행하는 배포자에 대해 사용할 수 있으며 선택한 게시자에서 사용 가능한 모든 게시의 구독 정보를 표시합니다. 구독 목록을 필터링하여 오류, 경고 및 성능이 저조한 구독을 볼 수 있습니다. 이 탭에서는 관리자가 게시자에서의 모든 복제 작업을 모니터링할 수 있는 단일 위치를 제공합니다. 복제 모니터는 선택한 복제 유형과 **표시** 드롭다운 목록 상자에서 선택한 옵션에 기반하여 주의가 필요한 모든 구독을 표시합니다. 이 탭에 표시되는 항목은 현재 상태와 성능에 기반하기 때문에 현재 **표시** 목록 상자의 옵션과 일치하는 구독만 이 페이지에 표시됩니다.  
  
## <a name="options"></a>옵션  
 자세한 내용 및 구독과 관련된 태스크를 보려면 해당 구독에 대한 행을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 옵션을 클릭합니다. 표에서 데이터를 표시하는 방식을 변경하려면 표를 마우스 오른쪽 단추로 클릭한 후 다음 옵션 중 하나를 클릭합니다.  
  
-   **정렬**: **열 정렬** 대화 상자에서 한 개 이상의 열에 대해 정렬합니다.  
  
-   **표시할 열 선택**: **열 선택** 대화 상자에서 표시할 열 및 해당 열이 표시되는 순서를 선택합니다.  
  
-   **필터**: **필터 설정** 대화 상자의 열 값에 따라 표의 행을 필터링합니다.  
  
-   **필터 지우기**: 표에 대한 모든 필터 설정을 지웁니다.  
  
 필터 설정은 각 표에 대해 지정됩니다. 열 선택 및 정렬은 각 게시자에 대한 게시 표와 같이 동일한 유형의 모든 표에 적용됩니다.  
  
 **스냅샷 구독 표시**  
 선택한 게시자에 대해 표시할 구독 유형(트랜잭션, 스냅샷 또는 병합)을 선택합니다.  
  
 **표시**  
 선택한 구독 유형에 대해 표시할 구독 상태를 선택합니다. 예를 들어 오류가 있는 구독만 표시하도록 선택할 수 있습니다.  
  
 **상태**  
 스냅샷 에이전트 또는 배포 에이전트의 상태에 따라 결정되는 각 구독의 상태입니다. 우선 순위가 높은 상태가 표시됩니다.  
  
 기본적으로 구독 정보가 포함된 표는 **상태** 열을 기준으로 정렬됩니다. 다음 목록에서는 가능한 상태 값 및 값 정렬 순서를 보여 줍니다. 예를 들어 오류는 항상 표의 맨 위에 표시됩니다.  
  
-   Error  
  
-   곧 만료됨/만료됨  
  
-   초기화되지 않은 구독  
  
-   실패한 명령 다시 시도 중  
  
-   동기화 중  
  
-   비동기화 중  
  
 정렬 순서는 지정한 구독의 상태가 두 가지 이상일 경우에 표시할 값도 결정합니다. 예를 들어 구독에 오류가 있고 곧 만료될 예정이면 **상태** 열에 **오류**가 표시됩니다.  
  
 **곧 만료됨/만료됨** 및 **초기화되지 않은 구독** 상태 값은 경고입니다. 경고를 표시할 때 **상태** 열은 에이전트가 실행 중인지 여부도 표시합니다. 예를 들어 상태가 **실행 중, 곧 만료됨/만료됨**과 같이 표시될 수 있습니다.  
  
 **곧 만료됨/만료됨** 상태 값은 임계값을 설정한 경우에만 표시됩니다. 임계값 설정에 대한 자세한 내용은 [복제 모니터에 임계값 및 경고 설정](monitor/set-thresholds-and-warnings-in-replication-monitor.md)을 참조하세요.  
  
 **구독**  
 각 구독의 이름으로 *SubscriberName: SubscriptionDatabaseName*형식입니다.  
  
 **게시**  
 구독을 동기화할 게시의 이름이며 *PublicationDatabaseName: PublicationName*형식입니다.  
  
 **마지막 동기화**  
 배포 에이전트가 마지막으로 실행된 시간입니다. 동기화가 진행 중인 경우 **진행 중** 이 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 모니터 시작](monitor/start-the-replication-monitor.md)   
 [복제 모니터를 사용하여 정보 보기 및 태스크 수행](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [복제 모니터링](monitoring-replication.md)  
  
  
