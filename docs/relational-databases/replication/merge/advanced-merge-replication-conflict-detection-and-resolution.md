---
title: "고급 병합 복제 충돌 감지 및 해결 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], about conflict resolution
- default conflict resolver
- column-level conflict tracking
- row-level conflict tracking
- viewing merge replication conflicts
- resolving merge replication conflicts
- logical record-level conflict tracking [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 063d3d9c-ccb5-4fab-9d0c-c675997428b4
caps.latest.revision: 46
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: be8f8a4e1df903cc70191dc582ce2aef19e7e7aa
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="advanced-merge-replication---conflict-detection-and-resolution"></a>고급 병합 복제 - 충돌 감지 및 해결
  게시자와 구독자가 연결되고 동기화가 이루어지면 병합 에이전트는 충돌이 있는지 감지합니다. 충돌이 감지되면 병합 에이전트는 게시에 아티클을 추가할 때 지정한 충돌 해결 프로그램을 사용해서 수락하여 다른 사이트로 전파할 데이터를 확인합니다.  
  
> [!NOTE]  
>  구독자와 게시자가 동기화되는 경우에도 충돌은 대체로 구독자 및 게시자에서 수행되는 업데이트가 아닌 여러 구독자에서 수행되는 업데이트 사이에서 발생합니다.  
  
 충돌 감지 및 해결 동작은 다음 옵션에 따라 결정됩니다.  
  
-   열 수준 추적, 행 수준 추적 또는 논리적 레코드 수준 추적 지정  
  
-   기본 우선 순위 기반 해결 메커니즘 또는 아티클 해결 프로그램 지정. 아티클 해결 프로그램은 다음 중 하나일 수 있습니다.  
  
    -   관리 코드로 작성된 *비즈니스 논리 처리기*  
  
    -   COM 기반 *사용자 지정 해결 프로그램*  
  
    -   [!INCLUDE[msCoName](../../../includes/msconame-md.md)]에서 제공하는 COM 기반 해결 프로그램  
  
     기본 해결 메커니즘을 사용하는 경우 구독 유형이 클라이언트인지 또는 서버인지에 따라 동작이 추가로 결정됩니다.  
  
## <a name="conflict-detection"></a>충돌 감지  
 데이터 변경의 충돌 여부는 아티클에 대해 설정한 충돌 추적 유형에 따라 결정됩니다.  
  
-   열 수준 충돌 추적을 선택하면 둘 이상의 복제 노드에서 동일한 행의 동일한 열이 변경되는 경우 충돌로 간주됩니다.  
  
-   행 수준 추적을 선택하면 둘 이상의 복제 노드에서 동일한 행의 임의 열이 변경되는 경우 충돌로 간주됩니다. 해당 행에서 영향을 받는 열이 동일할 필요는 없습니다.  
  
-   논리적 레코드 수준 추적을 선택하면 둘 이상의 복제 노드에서 동일한 논리적 레코드의 임의 행이 변경되는 경우 충돌로 간주됩니다. 해당 행에서 영향을 받는 열이 동일할 필요는 없습니다.  
  
 자세한 내용은 [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)을 참조하세요.  
  
 아티클의 충돌 추적 및 해결 수준을 지정하려면 [병합 아티클에 대 한 충돌 추적 및 해결 수준 지정](../../../relational-databases/replication/publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md)을 참조하십시오.  
  
## <a name="conflict-resolution"></a>충돌 해결  
 충돌이 감지되면 병합 에이전트는 선택한 충돌 해결 프로그램을 시작하고 해결 프로그램을 사용하여 충돌 시 적용되는 내용을 확인합니다. 적용되는 행이 게시자 및 구독자에서 적용되며 무시되는 행의 데이터는 충돌 테이블에 기록됩니다. 대화형으로 충돌을 해결하도록 선택하지 않으면 해결 프로그램이 실행된 후 즉시 충돌이 해결됩니다.  
  
### <a name="resolver-types"></a>해결 프로그램 유형  
 병합 복제에서 충돌 해결은 아티클 수준에서 수행됩니다. 여러 아티클로 구성된 게시의 경우 아티클별로 서로 다른 충돌 해결 프로그램을 사용할 수도 있고 게시를 구성하는 모든 아티클, 여러 아티클 또는 하나의 아티클에 대해 같은 충돌 해결 프로그램을 사용할 수도 있습니다.  
  
 기본 우선 순위 기반 충돌 해결 프로그램을 사용할 경우에는 아티클의 해결 프로그램 속성을 설정할 필요가 없습니다. 기본 해결 프로그램 대신 아티클 해결 프로그램을 사용하려면 게시자에서 사용 가능한 해결 프로그램을 선택하여 해당 해결 프로그램이 사용될 아티클에 대해 해결 프로그램 속성을 설정해야 합니다. 해결 프로그램으로 전달되어야 하는 모든 특정 정보는 해결 프로그램 정보 속성에서 지정할 수도 있습니다.  
  
 병합 복제는 다음 4가지 유형의 충돌 해결 프로그램을 제공합니다.  
  
-   기본 우선 순위 기반 충돌 해결 프로그램  
  
     기본 해결 메커니즘은 구독이 클라이언트 구독인지 서버 구독인지에 따라 다르게 동작합니다. 서버 구독을 사용하는 개별 구독자에게 우선 순위 값을 할당하며 우선 순위가 가장 높은 노드의 변경 내용이 충돌 시 적용됩니다. 클라이언트 구독의 경우 게시자에 작성된 첫 번째 변경 내용이 충돌 시 적용됩니다.  
  
     구독을 만든 후에는 해당 유형을 변경할 수 없습니다.  
  
-   비즈니스 논리 처리기  
  
     비즈니스 논리 처리기 프레임워크를 사용하면 병합 동기화 과정 동안 호출되는 관리 코드 어셈블리를 작성할 수 있습니다. 이 어셈블리에는 동기화 중에 충돌과 다른 많은 조건에 응답할 수 있는 비즈니스 논리가 포함됩니다. 자세한 내용은 [병합 동기화 중 비즈니스 논리 실행](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)을 참조하세요.  
  
-   COM 기반 사용자 지정 해결 프로그램  
  
     병합 복제는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vcprvc](../../../includes/vcprvc-md.md)] 또는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]과 같은 언어를 사용하여 해결 프로그램을 COM 개체로 작성하기 위한 API를 제공합니다. 자세한 내용은 [COM-Based Custom Resolvers](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)을(를) 참조하세요.  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)]에서 제공하는 COM 기반 해결 프로그램  
  
     [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] includes a number of COM-based resolvers. 자세한 내용은 [Microsoft COM-Based Resolvers](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)을(를) 참조하세요.  
  
 적절한 유형의 해결 프로그램을 선택하는 방법에 대한 자세한 내용은 [해결 프로그램 선택](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-choose-a-resolver.md)을 참조하세요.  
  
> [!NOTE]  
>  일부 아티클 해결 프로그램은 특정 작업에 대해서만 충돌을 처리하도록 작성됩니다. 예를 들어 특정 해결 프로그램은 삽입 또는 삭제는 처리하지 않고 업데이트만 처리할 수 있습니다. 기본 우선 순위 기반 충돌 해결 프로그램은 아티클 해결 프로그램이 처리하지 못한 모든 충돌을 처리합니다.  
  
 병합 구독 유형 및 충돌 해결 우선 순위를 지정하려면 다음을 참조하십시오.  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Specify a Merge Subscription Type and Conflict Resolution Priority &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md)  
  
-   복제 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 복제 프로그래밍 및 RMO(복제 관리 개체) 프로그래밍: [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md) 및 [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md)  
  
### <a name="interactive-resolver"></a>대화형 해결 프로그램  
 복제는 기본 우선 순위 기반 충돌 해결 프로그램이나 아티클 해결 프로그램과 함께 사용할 수 있는 대화형 해결 프로그램 사용자 인터페이스를 제공합니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 동기화 관리자를 통해 요청 시 동기화를 수행할 때 대화형 해결 프로그램은 런타임 시 충돌 데이터를 표시하고 충돌 해결 방법을 선택할 수 있습니다. 대화형 해결 기능 설정 방법 및 대화형 해결 프로그램 시작 방법은 [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)을 참조하십시오.  
  
## <a name="viewing-conflicts"></a>충돌 보기  
 가장 간단한 방법으로 충돌을 보려면 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 에서 제공하는 복제 충돌 뷰어를 사용합니다.[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 충돌 테이블을 쿼리할 저장 프로시저도 제공합니다. 충돌 뷰어와 대화형 해결 프로그램은 유사한 도구이지만, 대화형 해결 프로그램은 동기화가 이루어지는 동안 충돌을 해결하는데 사용하는 반면 충돌 뷰어는 충돌이 해결된 후 충돌을 보는 데 사용합니다. 시스템 테이블에서 충돌 메타데이터를 사용할 수 있는 경우(충돌 메타데이터는 기본적으로 14일 동안 유지됨) 충돌 뷰어에서 충돌 해결 결과를 무시할 수 있지만 정기적으로 직접적인 사용자 작업이 필요한 경우 대화형 해결 프로그램을 사용합니다.  
  
> [!NOTE]  
>  논리적 레코드와 관련된 충돌은 충돌 뷰어에 표시되지 않습니다. 이러한 충돌에 대한 정보를 보려면 복제 저장 프로시저를 사용합니다. 자세한 내용은 [병합 게시에 대한 충돌 정보 보기&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)을 참조하세요.  
  
 충돌 뷰어는 3개의 시스템 테이블에 대한 정보를 표시합니다.  
  
-   복제는 병합 아티클의 각 테이블에 대해 **MSmerge_conflict_\<PublicationName>_\<ArticleName>** 형식의 이름으로 충돌 테이블을 만듭니다.  
  
     충돌 테이블의 구조는 기준이 되는 테이블의 구조와 동일합니다. 이 테이블 중 한 테이블의 행은 충돌 행의 삭제된 버전으로 구성되어 있습니다. 행의 적용되는 버전은 실제 사용자 테이블에 있습니다.  
  
-   **MSmerge_conflicts_info** 테이블은 충돌 유형을 포함하여 각 충돌에 대한 정보를 제공합니다.  
  
-   **sysmergearticles** 테이블은 충돌 테이블이 있는 사용자 테이블을 식별하고 충돌 테이블에 대한 정보를 제공합니다.  
  
 기본적으로 충돌 정보는 다음 위치에 저장됩니다.  
  
-   게시 호환성 수준이 90RTM 이상일 경우 게시자 및 구독자.  
  
-   게시 호환성 수준이 80RTM 미만일 경우 게시자  
  
-   구독자가 [!INCLUDE[ssEW](../../../includes/ssew-md.md)]을 실행하는 경우 게시자. 충돌 데이터는 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 구독자에 저장할 수 없습니다.  
  
 **충돌을 보려면**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [View and Resolve Data Conflicts for Merge Publications &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   복제 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 프로그래밍: [병합 게시에 대한 충돌 정보 보기&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 동기화](../../../relational-databases/replication/synchronize-data.md)  
  
  
