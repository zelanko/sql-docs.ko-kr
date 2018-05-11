---
title: 다운로드 전용 아티클로 병합 복제 성능 최적화 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], download-only articles
- articles [SQL Server replication], download-only
- download-only articles
ms.assetid: 8851faa6-e6df-4ea5-a6ea-2a3471680fa3
caps.latest.revision: 37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e3b8384afc96be2b71a1f2c51bbfbbd35920562e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="optimize-merge-replication-performance-with-download-only-articles"></a>다운로드 전용 아티클로 병합 복제 성능 최적화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  병합 복제에서는 다양한 응용 프로그램의 요구 사항을 해결할 수 있도록 두 가지 아티클 유형을 제공합니다. 게시에는 이러한 아티클 유형 중 해당 응용 프로그램에 적합한 하나 이상의 아티클 유형이 포함될 수 있습니다.  
  
-   표준 아티클  
  
-   다운로드 전용 아티클  
  
 적절한 상황에서 다운로드 전용 아티클을 사용하면 표준 아티클과 비교하여 성능상의 이점이 있습니다.  
  
> [!NOTE]  
>  다운로드 전용 아티클을 사용하려면 게시의 호환성 수준이 적어도 90RTM 이상이어야 합니다.  
  
## <a name="standard-articles"></a>표준 아티클  
 기본값인 표준 아티클은 뛰어난 충돌 감지 및 해결 기능을 비롯하여 병합 복제의 모든 기능을 제공합니다. 표준 아티클은 여러 구독자가 업데이트하는 테이블에 적합하며 저장 프로시저 및 뷰와 같은 테이블 이외의 개체는 항상 표준 아티클로 게시됩니다.  
  
## <a name="download-only-articles"></a>다운로드 전용 아티클  
 다운로드 전용 아티클은 제품 카탈로그에 포함된 아티클 집합처럼 구독자에서 업데이트되지 않는 데이터가 있는 응용 프로그램에 적합하게 디자인되었습니다. 일반적으로 제품 카탈로그는 게시자에서는 업데이트되지만 구독자에서는 업데이트되지 않습니다. 다운로드 전용 아티클은 구독자에서 업데이트할 수 없으므로 추적 메타데이터가 구독자로 전송되지 않습니다. 이로 인해 구독자의 저장소 용량 및 성능상 이점이 줄어들 수 있으며 특히 네트워크 연결 속도가 느릴 경우 더욱 그렇습니다.  
  
 다운로드 전용 아티클은 클라이언트 구독과 함께 작동합니다. 아티클을 다운로드 전용으로 지정할 경우 해당 아티클에 대한 행은 클라이언트 구독을 사용하는 구독자에 삽입, 업데이트 또는 삭제할 수 없습니다. 서버 구독 유형을 사용하는 게시자와 구독자(일반적으로 데이터를 다른 구독자로 다시 게시하는 구독자)는 데이터를 삽입, 업데이트 및 삭제할 수 있습니다. 클라이언트 구독에 대한 자세한 내용은 [게시 구독](../../../relational-databases/replication/subscribe-to-publications.md)을 참조하세요.  
  
 아티클을 다운로드 전용으로 지정하려면 [Specify That a Merge Table Article is Download-Only](../../../relational-databases/replication/publish/specify-that-a-merge-table-article-is-download-only.md)을 참조하십시오.  
  
## <a name="using-different-article-types-in-your-applications"></a>응용 프로그램에서 다른 아티클 유형 사용  
 응용 프로그램의 요구 사항을 이해하면 최대 유연성과 최적 성능 간 균형을 유지할 수 있습니다. 예를 들어 게시자와 구독자에서 충돌이 자주 발생하고 내용이 자주 변경되는 응용 프로그램의 경우 표준 아티클로 구성된 응용 프로그램을 사용합니다. SFA(Sales Force Automation) 응용 프로그램과 같은 일부 응용 프로그램에는 충돌 가능성이 있는 아티클과 다운로드 전용으로 지정할 수 있는 조회 테이블의 기능을 하는 다른 아티클이 있을 수 있습니다. POS(Point of Sale) 시스템 및 FFA(Field Force Automation) 응용 프로그램과 같은 데이터 항목 응용 프로그램은 충돌을 제거하고 한 구독자의 데이터가 다른 구독자로 이동하지 않는 방식으로 데이터를 엄격하게 분할하는 경우가 많습니다. 이러한 경우 겹치지 않는 파티션, 다운로드 전용 아티클 및 사전 계산 파티션을 잘 조합하여 성능과 확장성을 최적화할 수 있습니다. 겹치지 않는 파티션 및 사전 계산 파티션에 대한 자세한 내용은 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [병합 복제를 위한 아티클 옵션](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [조건부 삭제 추적으로 병합 복제 성능 최적화](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  
