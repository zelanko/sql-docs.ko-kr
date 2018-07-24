---
title: 조건부 삭제 추적으로 병합 복제 성능 최적화 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- conditional delete tracking [SQL Server replication]
- merge replication [SQL Server replication], conditional delete tracking
- articles [SQL Server replication], conditional delete tracking
ms.assetid: 58f120a3-ea3a-4e97-93f0-0eb4e580ecf2
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c90fa044fb810de8e269d875643c7eb415c1de2a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37987465"
---
# <a name="optimize-merge-replication-performance-with-conditional-delete-tracking"></a>조건부 삭제 추적으로 병합 복제 성능 최적화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 병합 복제를 사용하여 하나 이상의 아티클에 대한 삭제를 복제 트리거 및 시스템 테이블에서 추적할 수 없도록 지정할 수 있습니다. 아티클에 대해 이 옵션을 지정하면 게시자나 구독자에서 삭제가 추적되거나 복제되지 않습니다. 이 옵션은 다양한 응용 프로그램 시나리오를 지원하며 삭제를 복제할 필요가 없거나 삭제를 복제하는 것이 바람직하지 않은 상황에 대해 최적화된 성능을 제공합니다. 성능을 향상시키는 방법으로는 삭제에 대한 메타데이터를 저장하지 않는 방법, 동기화 중 삭제를 열거하지 않는 방법, 삭제가 구독자에 복제 및 적용되지 않게 하는 방법의 3가지가 있습니다.  
  
> [!NOTE]  
>  다운로드 전용 아티클을 사용하려면 게시의 호환성 수준이 적어도 90RTM 이상이어야 합니다.  
  
 옵션은 게시 생성 시 지정할 수 있으며 응용 프로그램에서 일부 삭제 내용은 복제하고 나머지 삭제 내용은 복제하지 않아야 하는 경우(예: 일괄 삭제) 옵션을 설정 또는 해제할 수 있습니다. 다음 예에서는 응용 프로그램에서 이 옵션을 사용하는 방법을 설명합니다.  
  
-   이동이 잦은 영업 사원이 사용하는 응용 프로그램에는 일반적으로 **SalesOrderHeader**, **SalesOrderDetail** 및 **Product**와 같은 테이블이 있습니다. 구독자에서 입력한 주문은 게시자로 복제되고 게시자에서는 이 데이터를 주문 수행 시스템에 제공합니다. 이동이 잦은 영업 사원 중 많은 수가 저장소가 제한된 핸드헬드 장치를 사용하므로 게시자에서 주문을 받으면 해당 주문을 구독자에서 삭제할 수 있습니다. 해당 주문은 시스템 내에서 계속 활성 상태이므로 삭제가 게시자에 전파되지 않습니다.  
  
     이 시나리오에서 **SalesOrderHeader** 및 **SalesOrderDetail** 테이블에 대해 삭제를 추적할 수 없습니다. 제품이 게시자에서 삭제되면 제품 목록을 최신 내용으로 유지할 수 있게 삭제 내용을 구독자로 보내야 하므로 **Product** 테이블에 대한 삭제는 추적할 수 있습니다.  
  
-   응용 프로그램에서는 1년을 초과하는 레코드를 주기적으로 제거하는 **TransactionHistory**와 같은 테이블에 기록 데이터를 저장할 수 있습니다. 이 테이블을 구독자가 현재 달의 트랜잭션에 있는 데이터만 받도록 필터링할 수 있습니다. 이전 데이터를 제거하는 게시자에서 매월 수행하는 일괄 삭제는 구독자와 아무 관련이 없지만 기본적으로 이 삭제를 계속 추적하고 열거합니다.  
  
     이 시나리오에서는 일괄 처리가 발생하기 전에 시스템에서 작업을 중지할 수 있으며 응용 프로그램에서 삭제 추적을 해제할 수 있습니다. 처리가 완료되면 추적을 다시 설정할 수 있습니다.  
  
> [!IMPORTANT]  
>  게시자에서 다른 작업이 계속되는 경우 삭제 추적이 해제되어 있는 동안은 구독자로 전파되어야 하는 삭제가 발생하지 않도록 합니다.  
  
 **삭제가 추적되지 않게 지정하려면**  
  
-   복제 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 프로그래밍: [병합 아티클에 대해 삭제가 추적되지 않도록 지정&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/publish/specify-that-deletes-should-not-be-tracked-for-merge-articles.md)  
  
## <a name="see-also"></a>참고 항목  
 [병합 복제를 위한 아티클 옵션](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [다운로드 전용 아티클로 병합 복제 성능 최적화](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)  
  
  
