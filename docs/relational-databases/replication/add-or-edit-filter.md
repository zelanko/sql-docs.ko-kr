---
title: 필터 추가 또는 편집 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
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
f1_keywords:
- sql13.rep.newpubwizard.addeditfilter.f1
ms.assetid: bdd7c71d-1c59-4044-bfe8-c85f908345bb
caps.latest.revision: 27
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 332d02a43291257c567b93a4d689e932d67e7a8f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="add-or-edit-filter"></a>필터 추가 또는 편집
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **필터 추가** 및 **필터 편집** 대화 상자를 사용하여 정적 행 필터 및 매개 변수가 있는 행 필터를 추가 및 편집할 수 있습니다.  
  
> [!NOTE]  
>  기존 게시에서 필터를 편집하려면 해당 게시에 대한 새 스냅숏이 필요합니다. 게시에 구독이 있으면 해당 구독을 다시 초기화해야 합니다. 속성 변경에 대한 자세한 내용은 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)을 참조하세요.  
  
 모든 게시 유형은 정적 필터를 포함할 수 있습니다. 또한 병합 게시는 매개 변수가 있는 필터를 포함할 수 있습니다. 정적 필터는 게시가 생성될 때 평가됩니다. 즉, 해당 게시에 대한 모든 구독자는 같은 데이터를 받습니다. 매개 변수가 있는 필터는 복제 동기화 중에 평가됩니다. 즉, 서로 다른 구독자는 각 구독자의 로그인 또는 컴퓨터 이름에 따라 다른 데이터 파티션을 받을 수 있습니다. 대화 상자에서 **예문** 링크를 클릭하여 필터의 각 유형에 대한 예를 볼 수 있습니다. 필터링 옵션에 대한 자세한 내용은 [게시된 데이터 필터링](../../relational-databases/replication/publish/filter-published-data.md)을 참조하세요.  
  
 행 필터를 사용하여 게시할 행의 하위 집합을 테이블로부터 지정할 수 있습니다. 중요한 정보 또는 비밀 정보가 포함된 행과 같이 사용자가 보지 말아야 하는 행을 삭제하거나 서로 다른 구독자에 전달할 서로 다른 데이터 파티션을 만드는 데 행 필터를 사용할 수 있습니다. 서로 다른 데이터 파티션을 서로 다른 구독자로 게시하면 여러 구독자에서 동일한 데이터를 업데이트함으로써 발생할 수 있는 충돌을 방지할 수 있습니다.  
  
## <a name="options"></a>변수  
 이 대화 상자는 2단계로 이루어진 트랜잭션 및 스냅숏 게시 처리 과정과 3단계로 이루어진 병합 게시 처리 과정으로 구성되어 있습니다. 모든 게시 유형에 대해 필터링할 테이블과 필터에 포함할 하나 이상의 열을 선택해야 합니다. 필터는 표준 WHERE 절로 정의합니다.  
  
1.  **필터링할 테이블을 선택하십시오.**  
  
     기존 필터를 편집하는 경우 테이블을 변경할 수 없습니다. 새 필터를 추가하는 경우 드롭다운 목록 상자에서 테이블을 선택합니다. **아티클** 페이지에서 선택한 테이블 중 아직 행 필터가 없는 테이블만 목록 상자에 표시됩니다. 테이블에 행 필터가 있지만 새 필터를 정의하려면 다음을 수행하십시오.  
  
    1.  **필터 추가** 대화 상자에서 **취소** 를 클릭합니다.  
  
    2.  **테이블 행 필터** 페이지의 필터 창에서 테이블을 선택하고 **편집**을 클릭합니다.  
  
    3.  **필터 편집** 대화 상자에서 기존 필터를 편집합니다.  
  
2.  **구독자가 받을 테이블 행을 식별하는 필터 문을 작성하십시오.**  
  
     새 필터 문을 정의하거나 기존 필터 문을 편집합니다. **열** 목록 상자는 **필터링할 테이블을 선택하십시오**에서 선택한 테이블에서 게시 중인 열을 모두 나열합니다. **필터 문** 텍스트 영역에는 다음 형식의 기본 텍스트가 포함됩니다.  
  
     `SELECT <published_columns> FROM [schema].[tablename] WHERE`  
  
     이 텍스트는 변경할 수 없습니다. 표준 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문을 사용하여 WHERE 키워드 뒤에 필터 절을 입력합니다. 게시자가 Oracle 게시자인 경우 WHERE 절은 Oracle 쿼리 구문과 호환되어야 합니다. 가능하면 복잡한 필터를 사용하지 마십시오. 정적 필터 및 매개 변수가 있는 필터는 모두 게시 처리 시간을 증가시키므로 필터 문을 최대한 단순하게 유지해야 합니다.  
  
    > [!IMPORTANT]  
    >  성능상의 이유로 `LEFT([MyColumn]) = SUSER_SNAME()`과 같이 병합 게시에 대한 매개 변수가 있는 행 필터 절의 열 이름에는 함수를 적용하지 않는 것이 좋습니다. 필터 절에 HOST_NAME을 사용하고 HOST_NAME 값을 재지정할 경우 CONVERT를 사용하여 데이터 형식을 변환해야 할 수 있습니다. 이를 위한 최선의 구현 방법은 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)항목의 "HOST_NAME() 값 재정의" 섹션을 참조하십시오.  
  
3.  **이 테이블의 데이터를 받을 구독 수를 지정하십시오.**  
  
     [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전만 해당하며 병합 게시만 사용할 수 있습니다. 병합 복제를 사용하면 데이터 및 응용 프로그램에 가장 적합한 파티션 유형을 지정할 수 있습니다. **이 테이블의 행을 단일 구독으로 이동**을 선택하면 병합 복제에서 겹치지 않는 파티션 옵션을 설정합니다. 겹치지 않는 파티션을 사전 계산 파티션과 함께 사용하면 겹치지 않는 파티션이 사전 계산 파티션과 연관된 업로드 비용을 최소화하므로 성능을 향상시킬 수 있습니다. 사용하는 매개 변수가 있는 필터와 조인 필터가 복잡할수록 겹치지 않는 파티션의 성능상 이점이 더욱 분명하게 드러납니다. 이 옵션을 선택하면 행을 둘 이상의 구독자에 복제할 수 없는 방식으로 데이터를 분할해야 합니다. 자세한 내용은 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)항목의 "'partition options' 설정" 섹션을 참조하십시오.  
  
 필터를 추가 또는 편집한 후에는 **확인** 을 클릭하여 변경 내용을 저장하고 대화 상자를 닫습니다. 지정한 필터가 구문 분석되고 SELECT 절의 테이블에 대해 실행됩니다. 필터 문에 구문 오류나 기타 문제가 있으면 알림 메시지가 표시되며 이를 보고 필터 문을 편집할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [게시된 데이터 필터링](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
