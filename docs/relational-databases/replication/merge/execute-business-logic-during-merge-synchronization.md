---
title: 병합 동기화 중 비즈니스 논리 실행 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- custom error resolution [SQL Server replication]
- custom change handling [SQL Server replication]
- errors [SQL Server replication], business logic handlers
- merge replication business logic handlers [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
- business logic handlers [SQL Server replication]
ms.assetid: 9d4da2ef-c17f-4a31-a1f6-5c3b7ca85f71
caps.latest.revision: 31
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ee583353ba4060d9ef48093e1db915c454d9040
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="execute-business-logic-during-merge-synchronization"></a>병합 동기화 중 비즈니스 논리 실행
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  비즈니스 논리 처리기 프레임워크를 사용하면 병합 동기화 과정 동안 호출되는 관리 코드 어셈블리를 작성할 수 있습니다. 이 어셈블리에는 동기화 중 데이터 변경, 충돌, 오류 등의 여러 상황에 응답할 수 있는 비즈니스 논리가 포함되어 있습니다. 비즈니스 논리 처리기 프레임워크에서 단순한 프로그래밍 모델을 제공하고 병합 프로세스에서 사용자 어셈블리에 ADO.NET 데이터 집합을 제공하므로 사용자는 소유 인터페이스를 새로 익히지 않고 ADO.NET에 대한 지식을 활용할 수 있습니다. 비즈니스 논리 처리기 프로그래밍에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   API(응용 프로그래밍 인터페이스) 참조: <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>  
  
-   비즈니스 논리 처리기 구현 방법: [병합 아티클에 대한 비즈니스 논리 처리기 구현](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
## <a name="uses-for-business-logic-handlers"></a>비즈니스 논리 처리기 용도  
 병합 동기화 프로세스는 비즈니스 논리 처리기를 호출하여 다음 작업을 수행할 수 있습니다.  
  
-   사용자 지정 변경 처리  
  
-   사용자 지정 충돌 해결  
  
-   사용자 지정 오류 해결  
  
> [!NOTE]  
>  사용자가 지정하는 비즈니스 논리 처리기는 동기화되는 모든 행에 대해 실행됩니다. 네트워크 서비스 또는 다른 응용 프로그램에 대한 호출과 복잡한 논리가 성능에 영향을 줄 수 있습니다.  
  
### <a name="custom-change-handling"></a>사용자 지정 변경 처리  
 비즈니스 논리 처리기는 충돌을 일으키지 않는 데이터 변경을 처리하는 중 호출할 수 있으며 다음 3가지 동작 중 하나를 수행할 수 있습니다.  
  
-   데이터 거부  
  
     이 작업은 지정된 구독자에서 변경 내용을 전파하지 않으려는 응용 프로그램에 유용합니다. 예를 들어 관리자는 구독자의 파티션에 속하지 않는 삽입을 필터링하거나 구독자에서 수행된 삭제를 거부할 수 있습니다. 또 다른 예로 재고가 없을 경우 응용 프로그램은 구독자에서 입력한 주문을 거부할 수 있습니다.  
  
-   데이터 적용  
  
     이 작업은 게시자 또는 구독자에서의 데이터 변경 내용을 전파하기 전에 확인할 필요가 있는 응용 프로그램에 유용합니다. 예를 들어 중간 계층 응용 프로그램이 현장에서 들어오는 새 주문을 검사하고 이를 중간 계층의 입고 워크플로 프로세스에 통합할 수 있습니다.  
  
-   사용자 지정 데이터 적용  
  
     이 작업은 특정 데이터 값 또는 작업을 재정의할 필요가 있는 응용 프로그램에 유용합니다. 예를 들어 응용 프로그램은 행의 **status** 열 값을 "deleted"로 설정한 다음 삭제를 수행하는 클라이언트 ID를 추적하는 특수 업데이트로 행 삭제를 변환할 수 있습니다. 이 방법은 감사 또는 워크플로에 유용할 수 있습니다.  
  
### <a name="custom-conflict-resolution"></a>사용자 지정 충돌 해결  
 사용자는 병합 복제에서 제공하는 충돌 감지 및 해결 기능을 사용하여 충돌에 대해 기본 해결 전략을 적용하거나 사용자 지정 해결을 선택할 수 있습니다. 자세한 내용은 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)에서 병합 아티클 해결 프로그램을 지정하는 방법에 대해 설명합니다. 비즈니스 논리 처리기는 충돌하는 데이터 변경을 처리하는 중 호출할 수 있으며 다음 두 가지 동작 중 하나를 수행할 수 있습니다.  
  
-   기본 해결 적용  
  
     이 작업은 충돌을 검토하고, 추가 동작을 수행하고, 사용자 지정 충돌 로그 메시지를 기록해야 하는 응용 프로그램에 유용합니다.  
  
-   사용자 지정 해결 수행  
  
     이 작업은 해당 비즈니스 논리와 관련된 데이터 값을 선택하고 동기화 프로세스에 이 사용자 지정 데이터 집합을 제공해야 하는 응용 프로그램에 유용합니다. 예를 들어 응용 프로그램은 게시자 데이터 집합의 값과 구독자 데이터 집합의 값을 결합하여 새 버전의 적용되는 행을 제공할 수 있습니다.  
  
### <a name="custom-error-resolution"></a>사용자 지정 오류 해결  
 오류를 일으키는 변경 내용을 전파하는 중 사용자 지정 논리를 호출할 수 있습니다. 사용자 지정 논리는 다음 두 동작 중 하나를 수행할 수 있습니다.  
  
-   기본 오류 해결 적용  
  
     이 작업은 오류를 검토하고, 추가 동작을 수행하고, 사용자 지정 오류 로그 메시지를 기록해야 하는 응용 프로그램에 유용합니다.  
  
-   사용자 지정 오류 해결 적용  
  
     이 작업은 해당 비즈니스 논리와 관련된 데이터 값을 선택하고 동기화 프로세스에 이 사용자 지정 데이터 집합을 제공해야 하는 응용 프로그램에 유용합니다. 예를 들어 복제 프로세스에서 중복 키 위반이 발생하면 비즈니스 논리 처리기는 키가 충돌하지 않는 새 버전의 데이터 변경 내용을 제공할 수 있습니다. 이렇게 하면 게시자 및 구독자에서 적용한 변경 내용이 데이터베이스에서 지속되며 복제 프로세스에서 삭제를 사용하여 실패한 삽입을 해결할 필요가 없습니다.  
  
## <a name="deployment-scenarios-for-business-logic-handlers"></a>비즈니스 논리 처리기의 배포 시나리오  
 비즈니스 논리 처리기는 다음에 배포할 수 있습니다.  
  
-   배포자 비즈니스 논리가 배포자에서 실행되도록 밀어넣기 구독을 사용합니다.  
  
-   구독자. 비즈니스 논리가 구독자에서 실행되도록 끌어오기 구독을 사용합니다.  
  
-   웹 동기화를 사용할 경우 인터넷 정보 서비스(IIS) 서버. 웹 동기화를 통해 동기화된 끌어오기 구독을 사용하며 이로 인해 비즈니스 논리 처리기가 IIS 서버에서 실행됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [병합 복제](../../../relational-databases/replication/merge/merge-replication.md)   
 [Subscribe to Publications](../../../relational-databases/replication/subscribe-to-publications.md)   
 [데이터 동기화](../../../relational-databases/replication/synchronize-data.md)   
 [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
