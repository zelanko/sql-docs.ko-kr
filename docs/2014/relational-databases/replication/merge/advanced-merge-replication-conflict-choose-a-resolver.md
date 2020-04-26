---
title: 해결 프로그램 선택 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- default conflict resolver
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: b7dec3fa-d9d9-409d-b946-f9b9a3202829
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 17c751898aee25fa98bfeb6c2a7e1f1143bc61ae
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62931623"
---
# <a name="choose-a-resolver"></a>해결 프로그램 선택
  해결 프로그램을 선택할 때는 애플리케이션에서 충돌 해결의 중요성을 고려하고 우선 순위를 기반으로 하는 기본 충돌 해결 프로그램을 사용할 수 있는지 또는 아티클 해결 프로그램을 사용해야 하는지 여부를 고려해야 합니다.  
  
 같은 파티션에 기록하는 여러 사용자가 없는 상황에서 데이터가 분할되고 복제 토폴로지가 상대적으로 간단한 경우에는(단일 게시자 및 소수의 구독자) 충돌이 드물게 발생하거나 아예 발생하지 않을 것입니다. 이러한 환경에서는 복잡한 충돌 해결 전략이 필요하지 않습니다. 따라서 충돌 해결에 기본 설정을 사용하는 전략과 클라이언트 구독자 및 최초 변경 내용을 적용하는 정책을 사용하는 것이 좋습니다. 토폴로지가 재게시 구독자를 사용하는 경우와 같이 복잡한 경우에는 서버 구독에 우선 순위를 지정하는 것이 더 적합할 수 있습니다.  
  
 비즈니스에 기본 해결 프로그램에서 제공하는 것 보다 더 세밀하게 조정된 솔루션이 필요한 경우에는 아티클 해결 프로그램을 사용하는 것이 좋습니다. 아티클 해결 프로그램을 사용할 때는 비즈니스 논리 처리기를 사용하는 것이 좋습니다. 자세한 내용은 [병합 동기화 중 비즈니스 논리 실행](execute-business-logic-during-merge-synchronization.md)을 참조하세요.  
  
 따라서 기본 해결 프로그램을 사용할지 또는 아티클 해결 프로그램을 사용할지 여부는 데이터와 애플리케이션의 비즈니스 논리 필요 사항을 기반으로 합니다. 예를 들어 다양한 작업 범주(지점장, 라인 관리자 및 판매 담당자)에 걸쳐 있는 여러 직원이 서로 다른 구독자에 있는 분할되지 않은 테이블 집합에 고객 순위 데이터를 입력하고 작업 범주에 의해 데이터의 우선 순위가 결정되는 경우를 고려해 봅시다. 이 경우 충돌 발생 시 변경 내용을 적용할 항목을 결정하는 데 아티클의 작업 범주 데이터를 사용하는 아티클 해결 프로그램을 작성할 수 있습니다.  
  
 충돌이 자주 발생할 것으로 예측되면 충돌 해결 전략을 구현할 때 다음과 같은 매우 중요한 사항을 고려하십시오.  
  
|충돌 해결 문제|권장|  
|-------------------------------|--------------------|  
|서로 다른 사용자 범주에 다른 우선 순위 값이 필요합니다.|기본 해결 프로그램을 사용하고 다른 우선 순위 값을 가진 서버 구독을 만듭니다.<br /><br /> -또는-<br /><br /> 아티클의 권한 값 열을 인식하여 충돌 해결을 돕는 아티클 해결 프로그램을 사용합니다.|  
|최초 변경 내용을 적용하는 충돌 솔루션이 필요합니다.|기본 해결 프로그램을 사용하고 클라이언트 구독을 만듭니다.|  
|같은 열에 충돌하는 변경 내용을 적용하지 않는 한 여러 사용자가 같은 데이터 행을 변경할 수 있도록 허용합니다.|기본 해결 프로그램 또는 열 수준 추적을 설정한 아티클 해결 프로그램을 사용합니다.|  
|행 값의 여러 변경 내용을 충돌로 플래그 지정합니다.|기본 해결 프로그램 또는 행 수준 추적을 설정한 아티클 해결 프로그램을 사용합니다.|  
|논리적 레코드 값의 여러 변경 내용을 충돌로 플래그 지정합니다.|논리적 레코드 수준 추적을 설정한 기본 해결 프로그램을 사용합니다. 논리적 레코드 기능은 사용자 지정 해결 프로그램 또는 비즈니스 논리 처리기를 지원하지 않습니다.|  
|충돌 결과 데이터가 원본 충돌 데이터와 달라야 합니다.|새 값을 계산하는 아티클 해결 프로그램을 사용합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Detecting and Resolving Conflicts in Logical Records](advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [Advanced Merge Replication Conflict Detection and Resolution](advanced-merge-replication-conflict-detection-and-resolution.md)   
 [데이터 다시 게시](../republish-data.md)  
  
  
