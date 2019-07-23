---
title: 테이블 행 필터 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.filtertablerows.f1
ms.assetid: 005f5c71-0401-490e-8823-adc54a2e9675
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6974e8c3d07bd1da5fd48a4bbbc8e49c86e2d314
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128094"
---
# <a name="filter-table-rows"></a>테이블 행 필터
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **테이블 행 필터** 페이지를 사용하여 다음 작업을 수행할 수 있습니다.  
  
-   스냅샷, 트랜잭션 및 병합 게시의 테이블 아티클에 정적 행 필터를 적용합니다.  
  
-   병합 게시의 테이블 아티클에 매개 변수가 있는 행 필터를 적용합니다.  
  
-   조인 필터를 사용하여 병합 테이블 아티클의 필터를 관련 테이블 아티클로 확장할 수 있습니다.  
  
 필터링 옵션에 대한 자세한 내용은 [게시된 데이터 필터링](../../relational-databases/replication/publish/filter-published-data.md)을 참조하세요. **게시 속성** 대화 상자의 **행 필터** 페이지에서 필터링을 변경할 수 있습니다.  
  
 애플리케이션 성능을 최대화하고 필요한 원격 스토리지를 줄이거나 특정 구독자가 사용할 수 있는 데이터를 제한하려면 필요한 데이터만 게시해야 합니다. 게시에는 필터링되지 않은 테이블과 필터링된 테이블이 모두 포함될 수 있습니다. 예를 들어 필터링되지 않은 전체 회사 제품 테이블을 포함할 수도 있고 행 필터를 사용하여 특정 영역으로 필터링된 고객 테이블을 제공할 수 있습니다. 게시된 데이터를 필터링하여 다음 작업을 수행할 수 있습니다.  
  
-   네트워크로 보내지는 데이터 양을 최소화합니다.  
  
-   구독자에 필요한 스토리지 공간을 줄입니다.  
  
-   개별 구독자 요구 사항에 기초하여 게시 및 애플리케이션을 사용자 지정합니다.  
  
-   서로 다른 구독자에 서로 다른 데이터 파티션을 보낼 수 있으므로 구독자가 데이터를 업데이트할 때 충돌을 방지하거나 충돌 횟수를 줄일 수 있습니다. 즉, 두 개의 구독자가 같은 데이터 값을 업데이트하지 않게 됩니다.  
  
-   중요한 데이터를 전송하지 못하게 할 수 있습니다. 행 필터와 열 필터를 사용하여 구독자의 데이터 액세스를 제한할 수 있습니다. 병합 복제에서 HOST_NAME()을 포함하는 매개 변수가 있는 필터를 사용할 경우 보안 고려 사항이 있습니다. 자세한 내용은 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)의 "HOST_NAME()으로 필터링" 섹션을 참조하십시오.  
  
 필터는 행 식별을 위해 복제에 사용된 **rowguidcol** 을 포함하지 않아야 합니다. 기본적으로 이 열은 병합 복제를 설정할 때 추가된 열이며 이름은 **rowguid**입니다.  
  
## <a name="options"></a>옵션  
 **필터링된 테이블**  
 이 창은 게시의 테이블 아티클에 필터를 추가하면 추가된 필터로 채워집니다. 행 필터가 있는 테이블은 창에서 최상위 노드로 표시됩니다. 병합 게시의 경우 조인 필터를 통해 필터링이 확장된 테이블은 자식 노드로 표시됩니다.  
  
 **추가**  
 **추가** 를 클릭하면 테이블 아티클을 필터링할 수 있는 대화 상자가 시작됩니다. 스냅샷 또는 트랜잭션 게시에 대해 **추가** 를 클릭하면 대화 상자가 바로 시작됩니다. 병합 게시에 대해 **추가**를 클릭하면 **필터 추가**, **선택한 필터 확장을 위해 조인 추가**, **자동으로 필터 생성**의 세 가지 선택 사항이 표시됩니다.  
  
-   **필터 추가** 를 선택하면 **필터 추가** 대화 상자가 시작됩니다. 이 대화 상자를 사용하여 테이블 아티클에 행 필터를 적용할 수 있습니다. 예를 들어 **필터 추가** 대화 상자에서 고객 데이터가 들어 있는 테이블을 구독자로 복제할 때 프랑스 고객의 데이터만 포함되도록 지정할 수 있습니다.  
  
-   **선택한 필터 확장을 위해 조인 추가** 를 선택하면 **조인 추가** 대화 상자가 시작됩니다. **조인 추가** 대화 상자를 사용하여 행 필터가 있는 테이블과 관련된 테이블의 데이터를 필터링하도록 행 필터를 확장할 수 있습니다. 예를 들어 프랑스 고객의 데이터만 포함하도록 고객 테이블을 필터링하고 고객 주문과 관련된 테이블이 있으면 주문 테이블에 프랑스 고객의 주문만 포함되도록 두 테이블 간 조인을 정의할 수 있습니다.  
  
    > [!NOTE]  
    >  이 옵션을 사용하려면 먼저 필터 창에서 조인의 기본 테이블을 선택해야 합니다.  
  
-   **자동으로 필터 생성** 을 선택하면 **필터 생성** 대화 상자가 시작됩니다. 이 대화 상자를 사용하여 외래 키 관계를 통해 관련된 다른 테이블로 복제가 자동으로 확장되는 병합 게시의 한 테이블에 행 필터를 정의할 수 있습니다. 예를 들어 게시에 고객 테이블, 고객 테이블에 대한 외래 키가 있는 주문 테이블, 주문 테이블에 대한 외래 키가 있는 주문 세부 정보 테이블 등 3개의 테이블이 있을 수 있습니다. 고객 테이블에 행 필터를 정의하면 복제가 해당 필터를 다른 테이블로 확장합니다.  
  
    > [!NOTE]  
    >  복제 시 필터가 자동으로 생성되면 게시의 기존 필터는 모두 삭제됩니다. 자동으로 생성된 필터와 수동으로 지정한 필터를 모두 포함하려면 먼저 필터를 생성합니다. 각 게시에 대해 자동으로 생성된 필터 집합을 하나만 지정할 수 있습니다.  
  
 **편집**  
 필터 창에서 행 필터 또는 조인 필터를 선택하고 **편집** 을 클릭하면 **필터 편집** 또는 **조인 편집** 대화 상자가 시작됩니다.  
  
 **Delete**  
 필터 창에서 행 필터 또는 조인 필터를 선택하고 **삭제** 를 클릭하면 필터가 삭제됩니다.  
  
 **테이블 찾기**  
 조인 필터만 사용하여 게시를 병합합니다. **테이블 찾기** 를 클릭하여 복잡한 필터 트리에서 테이블을 찾을 수 있습니다. 관계가 복잡하게 설정된 데이터베이스에서는 한 테이블이 여러 테이블에 조인될 수 있으므로 필터 트리에서 두 개 이상의 위치에 표시될 수 있습니다.  
  
 실제 테이블은 트리의 한 위치에만 표시되고 나머지 위치에서는 바로 가기로 표시됩니다. 테이블 바로 가기는 테이블에 대한 참조일 뿐이므로 해당 테이블의 자식 노드는 표시되지 않습니다. 바로 가기 노드는 바로 가기 화살표로 표시되며 해당 노드를 확장하면 **\<tablename>에 대한 테이블을 보려면 [테이블 찾기]를 클릭하십시오.** 라는 텍스트가 표시됩니다.  
  
 창에서 바로 가기 노드를 선택하고 **테이블 찾기**를 클릭합니다. 창이 확장되고 해당 테이블이 강조 표시됩니다. 바로 가기 노드를 선택하지 않고 **테이블 찾기** 를 클릭하면 **테이블 찾기** 대화 상자가 시작됩니다.  
  
 **Assert**  
 필터 창에서 선택한 필터의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 정의를 포함합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [게시된 데이터 필터링](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
