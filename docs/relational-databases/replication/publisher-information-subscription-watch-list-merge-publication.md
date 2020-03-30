---
title: 구독 조사 목록(병합 - SSMS)
description: SSMS(SQL Server Management Studio) 복제 모니터의 ‘구독 조사 목록’ 탭을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publisherinfo.subscriptionssummary.merge.f1
ms.assetid: 4ec956bf-5cef-4377-a1d1-8c7f0107a6cb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 39c036c354716118fc4df791084f9838c6af5fea
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75320638"
---
# <a name="publisher-information-subscription-watch-list-merge-publication"></a>게시자 정보, 구독 조사 목록(병합 게시)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **구독 조사 목록** 탭은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전을 실행하는 배포자에 대해 사용할 수 있으며 선택한 게시자에서 사용 가능한 모든 게시의 구독 정보를 표시합니다. 구독 목록을 필터링하여 오류, 경고 및 성능이 저조한 구독을 볼 수 있습니다. 이 탭에서는 관리자가 게시자에서의 모든 복제 작업을 모니터링할 수 있는 단일 위치를 제공합니다. 복제 모니터는 선택한 복제 유형과 **표시** 드롭다운 목록 상자에서 선택한 옵션에 기반하여 주의가 필요한 모든 구독을 표시합니다. 이 탭에 표시되는 항목은 현재 상태와 성능에 기반하기 때문에 현재 **표시** 목록 상자의 옵션과 일치하는 구독만 이 페이지에 표시됩니다.  
  
## <a name="options"></a>옵션  
 자세한 내용 및 구독과 관련된 태스크를 보려면 해당 구독에 대한 행을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 옵션을 클릭합니다. 표에서 데이터를 표시하는 방식을 변경하려면 표를 마우스 오른쪽 단추로 클릭한 후 다음 옵션 중 하나를 클릭합니다.  
  
-   **정렬**: **열 정렬** 대화 상자에서 한 개 이상의 열에 대해 정렬합니다.  
  
-   **표시할 열 선택**: **열 선택** 대화 상자에서 표시할 열 및 해당 열이 표시되는 순서를 선택합니다.  
  
-   **필터**: **필터 설정** 대화 상자의 열 값에 따라 표의 행을 필터링합니다.  
  
-   **필터 지우기**: 표에 대한 모든 필터 설정을 지웁니다.  
  
 필터 설정은 각 표에 대해 지정됩니다. 열 선택 및 정렬은 각 게시자에 대한 게시 표와 같이 동일한 유형의 모든 표에 적용됩니다.  
  
 **병합 구독 표시**  
 선택한 게시자에 대해 표시할 구독 유형(트랜잭션, 스냅샷 또는 병합)을 선택합니다.  
  
 **표시**  
 선택한 구독 유형에 대해 표시할 구독 상태를 선택합니다. 예를 들어 오류가 있는 구독만 표시하도록 선택할 수 있습니다.  
  
 **상태**  
 병합 에이전트의 상태에 의해 결정되는 각 구독의 상태입니다.  
  
 기본적으로 구독 정보가 들어 있는 표는 **상태** 열을 기준으로 정렬한 다음 상태가 같은 구독을 **성능** 열을 기준으로 정렬합니다. 다음 목록에서는 가능한 상태 값 및 값 정렬 순서를 보여 줍니다. 예를 들어 오류는 항상 표의 맨 위에 표시됩니다.  
  
-   Error  
  
-   성능 심각  
  
-   장기 실행 트랜잭션 병합  
  
-   곧 만료됨/만료됨  
  
-   초기화되지 않은 구독  
  
-   실패한 명령 다시 시도 중  
  
-   동기화 중  
  
-   비동기화 중  
  
 정렬 순서는 지정한 구독의 상태가 두 가지 이상일 경우에 표시할 값도 결정합니다. 예를 들어 구독에 오류가 있고 곧 만료될 예정이면 **상태** 열에 **오류**가 표시됩니다.  
  
 **성능 심각**, **장기 실행 트랜잭션 병합**, **곧 만료됨/만료됨**및 **초기화되지 않은 구독** 상태 값은 경고입니다. 경고를 표시할 때 **상태** 열은 에이전트가 동기화 중인지 여부도 표시합니다. 예를 들어 상태가 **동기화 중, 성능 심각**과 같이 표시될 수 있습니다.  
  
 **곧 만료됨/만료됨** 및 **장기 실행 트랜잭션 병합** 상태 값은 임계값이 설정된 경우에만 표시할 수 있습니다. 상태 값 **성능 심각** 은 동일한 연결 유형(전화 접속 또는 LAN)으로 구독을 5회 동기화한 후에만 표시할 수 있습니다. 성능 측정 및 임계값 설정에 대한 자세한 내용은 [복제 모니터로 성능 모니터링](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) 및 [복제 모니터에 임계값 및 경고 설정](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)을 참조하세요.  
  
 **구독**  
 각 구독의 이름으로, 형식은*SubscriberName: SubscriptionDatabaseName*입니다.  
  
 **이름**  
 각 구독에 대한 설명입니다. 설명은 **구독 속성** 대화 상자에서 입력하거나 `@description`sp_addmergesubscription[ 또는 ](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)sp_addmergepullsubscription[의 ](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md) 매개 변수를 사용하여 지정합니다. 설명을 구독의 "이름" 또는 애칭으로 사용하기도 합니다.  
  
 **게시**  
 구독을 동기화할 게시의 이름이며 *PublicationDatabaseName: PublicationName*형식입니다.  
  
 **성능**  
 복제 모니터에서 측정한 가장 최근의 배달 속도 측정값을 기반으로 하는 각 구독의 성능 등급입니다. 등급은 개별 구독 성능과 게시에 대한 구독(연결 유형이 전화 접속 또는 LAN 등으로 동일한 구독)의 평균 기록 성능을 비교하여 결정됩니다. 복제 모니터는 같은 유형의 연결별로 50개 이상의 변경 사항을 5번 동기화한 후에 값을 표시합니다. 50개 이상의 변경 사항에 대해 동기화가 5번 미만으로 수행되었거나 가장 최근에 동기화가 수행된 변경 사항이 50개 미만인 경우에는 이 열이 비어 있습니다.  
  
> [!NOTE]  
>  성능은 **연결** 열에 표시된 연결 유형을 기준으로 하기 때문에 느린 연결을 통해 첫 번째 구독을 동기화할 경우 배달 속도가 느린 구독이 다른 구독보다 성능 등급이 높게 표시될 수 있습니다.  
  
 성능 등급은 다음 값 중 하나입니다.  
  
-   최고  
  
-   좋음  
  
-   보통  
  
-   나쁨  
  
 성능 등급 정의 방법 및 성능 임계값 설정 방법은 [복제 모니터로 성능 모니터링](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)을 참조하세요.  
  
 **배달 속도**  
 병합 에이전트에서 처리하는 초당 행 수입니다.  
  
 **마지막 동기화**  
 병합 에이전트가 마지막으로 실행된 시간입니다. 마지막 동기화 중에 변경 내용이 처리될 수도 있고 처리되지 않을 수도 있습니다. 동기화가 진행 중이면 백분율로 진행 상황을 표시합니다.  
  
 **Duration**  
 마지막 동기화 중에 병합 에이전트가 실행된 시간입니다. 병합 에이전트가 현재 동기화 중이면 이 시간은 경과된 시간을 나타내고 병합 에이전트가 이전에 동기화된 경우에는 총 시간을 나타냅니다.  
  
 **연결**  
 구독자와 게시자 간의 연결 유형입니다. 가능한 값은 **LAN**, **전화 접속**및 **인터넷**입니다. **인터넷** 값은 구독에서 웹 동기화를 사용하는 경우에 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [게시자에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [복제 모니터링](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [병합 복제에 대한 웹 동기화](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
