---
title: 필터 생성 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.generatefilters.f1
ms.assetid: be28515c-5d6d-467b-b933-d7c8d97a45b4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 14ccac181a4b76f8fc0423d6e00b20f91f8ea9cc
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67581357"
---
# <a name="generate-filters"></a>필터 생성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **필터 생성** 대화 상자를 사용하여 병합 게시의 테이블에 행 필터를 정의할 수 있습니다. 그러면 복제에서 외래 키 관계를 통해 관련된 다른 테이블로 해당 필터를 확장합니다. 예를 들어 프랑스 고객에 대한 데이터만 포함되도록 고객 테이블에 필터를 정의하면 복제에서는 관련된 주문 및 주문 세부 정보 테이블에 프랑스 고객과 관련된 정보만 포함되도록 해당 필터를 확장합니다.  
  
## <a name="options"></a>옵션  
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

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] and later versions only. Merge replication allows you to specify the type of partitions that are best suited to your data and application. If you select **A row from this table will go to only one subscription**, merge replication sets the nonoverlapping partitions option. Nonoverlapping partitions work in conjunction with precomputed partitions to improve performance, with nonoverlapping partitions minimizing the upload cost associated with precomputed partitions. The performance benefit of nonoverlapping partitions is more noticeable when the parameterized filters and join filters used are more complex. If you select this option, you must ensure that the data is partitioned in such a way that a row cannot be replicated to more than one Subscriber. For more information, see the section "Setting 'partition options'" in the topic [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 필터를 추가한 후에는 **확인** 을 클릭하여 대화 상자를 닫습니다. 지정한 필터가 구문 분석되고 SELECT 절의 테이블에 대해 실행됩니다. 필터 문에 구문 오류나 기타 문제가 있으면 알림 메시지가 표시되며 이를 보고 필터 문을 편집할 수 있습니다.  
  
 문이 구문 분석되면 복제에서는 필요한 조인 필터를 만듭니다. 이 마법사가 실행 중인 게시자에 대해 배포자를 아직 구성하지 않은 경우 배포자를 구성하라는 메시지가 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [게시된 데이터 필터링](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
