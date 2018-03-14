---
title: "필터 생성 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newpubwizard.generatefilters.f1
ms.assetid: be28515c-5d6d-467b-b933-d7c8d97a45b4
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8261d1194ea4f1786fbe19088cdde66ef2cc3f30
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="generate-filters"></a>필터 생성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **필터 생성** 대화 상자를 사용하여 병합 게시의 테이블에 행 필터를 정의할 수 있습니다. 그러면 복제에서 외래 키 관계를 통해 관련된 다른 테이블로 해당 필터를 확장합니다. 예를 들어 프랑스 고객에 대한 데이터만 포함되도록 고객 테이블에 필터를 정의하면 복제에서는 관련된 주문 및 주문 세부 정보 테이블에 프랑스 고객과 관련된 정보만 포함되도록 해당 필터를 확장합니다.  
  
## <a name="options"></a>변수  
 이 대화 상자에서는 3단계로 이루어진 프로세스를 통해 테이블에 행 필터를 만듭니다. 그러면 기본 키와 외래 키 간의 관계를 통해 필터링된 테이블과 관련된 테이블로 필터가 확장됩니다. 예를 들어 **Customer**, **SalesOrderHeader**및 **SalesOrderDetail**테이블이 있는데 **Customer** 와 **SalesOrderHeader**간에 관계가 있고 **SalesOrderHeader** 와 **SalesOrderDetail**간에 관계가 있을 때 **Customer**에 행 필터를 적용하면 복제에서는 해당 필터를 **SalesOrderHeader** 및 **SalesOrderDetail**로 확장합니다.  
  
1.  **필터링할 테이블을 선택하십시오.**  
  
     드롭다운 목록 상자에서 테이블을 선택합니다. **아티클** 페이지에서 선택한 테이블만 목록 상자에 표시됩니다.  
  
2.  **구독자가 받을 테이블 행을 식별하는 필터 문을 작성하십시오.**  
  
     새 필터 문을 정의합니다. **열** 목록 상자는 **필터링할 테이블을 선택하십시오**에서 선택한 테이블에서 게시 중인 열을 모두 나열합니다. **필터 문** 텍스트 영역에는 다음 형식의 기본 텍스트가 포함됩니다.  
  
     `SELECT <published_columns> FROM [tableowner].[tablename] WHERE`  
  
     이 텍스트는 변경할 수 없습니다. 표준 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문을 사용하여 WHERE 키워드 뒤에 필터 절을 입력합니다.  
  
    > [!IMPORTANT]  
    >  성능상의 이유로 `LEFT([MyColumn]) = SUSER_SNAME()`과 같은 매개 변수가 있는 행 필터 절의 열 이름에는 함수를 적용하지 않는 것이 좋습니다. 필터 절에 HOST_NAME을 사용하고 HOST_NAME 값을 재지정할 경우 CONVERT를 사용하여 데이터 형식을 변환해야 할 수 있습니다. 이를 위한 최선의 구현 방법은 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)로 확장합니다.  
  
3.  **이 테이블의 데이터를 받을 구독 수를 지정하십시오.**  
  
     [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에만 해당됩니다. 병합 복제를 사용하면 데이터 및 응용 프로그램에 가장 적합한 파티션 유형을 지정할 수 있습니다. **이 테이블의 행을 단일 구독으로 이동**을 선택하면 병합 복제에서 겹치지 않는 파티션 옵션을 설정합니다. 겹치지 않는 파티션을 사전 계산 파티션과 함께 사용하면 겹치지 않는 파티션이 사전 계산 파티션과 연관된 업로드 비용을 최소화하므로 성능을 향상시킬 수 있습니다. 사용하는 매개 변수가 있는 필터와 조인 필터가 복잡할수록 겹치지 않는 파티션의 성능상 이점이 더욱 분명하게 드러납니다. 이 옵션을 선택하면 행을 둘 이상의 구독자에 복제할 수 없는 방식으로 데이터를 분할해야 합니다. 자세한 내용은 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)항목의 "'partition options' 설정" 섹션을 참조하십시오.  
  
 필터를 추가한 후에는 **확인** 을 클릭하여 대화 상자를 닫습니다. 지정한 필터가 구문 분석되고 SELECT 절의 테이블에 대해 실행됩니다. 필터 문에 구문 오류나 기타 문제가 있으면 알림 메시지가 표시되며 이를 보고 필터 문을 편집할 수 있습니다.  
  
 문이 구문 분석되면 복제에서는 필요한 조인 필터를 만듭니다. 이 마법사가 실행 중인 게시자에 대해 배포자를 아직 구성하지 않은 경우 배포자를 구성하라는 메시지가 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [게시된 데이터 필터링](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
