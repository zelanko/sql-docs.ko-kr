---
title: 병합 아티클 간에 자동으로 조인 필터 생성 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
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
- automatic join filter generation
- join filters
ms.assetid: 7ef419f4-c17f-42a5-9068-174a3ec08941
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 70fc107aab8433822e5d674b39b8b4986ec32f4e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32963018"
---
# <a name="automatically-generate-join-filters-between-merge-articles"></a>병합 아티클 간에 자동으로 조인 필터 생성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<게시>** 대화 상자의 **행 필터** 페이지에서 자동으로 조인 필터 집합을 생성합니다. 마법사 사용 및 대화 상자 액세스에 대한 자세한 내용은 [게시 만들기](../../../relational-databases/replication/publish/create-a-publication.md) 및 [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
> [!NOTE]  
>  게시에 대한 구독이 초기화된 후 **게시 속성 - \<게시>** 대화 상자에서 조인 필터 집합을 자동으로 생성한 경우에는 변경 내용을 적용한 후에 새 스냅숏을 생성하고 모든 구독을 다시 초기화해야 합니다. 속성 변경 요구 사항에 대한 자세한 내용은 [게시 및 아티클 속성 변경](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)을 참조하세요.  
  
 테이블 집합에 대해 수동으로 조인 필터를 만들거나 테이블에 정의된 외래 키와 기본 키 간의 관계를 기반으로 복제에서 필터를 자동으로 생성할 수 있습니다. 조인 필터를 수동으로 만드는 방법에 대한 자세한 내용은 [병합 아티클 사이에서 조인 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)을 참조하세요.  
  
### <a name="to-automatically-generate-a-set-of-join-filters-between-merge-articles"></a>병합 아티클 간의 조인 필터 집합을 자동으로 생성하려면  
  
1.  새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<Publication>** 의 **행 필터** 페이지에서 **추가**를 클릭하고 **자동으로 필터 생성**을 클릭합니다.  
  
    > [!NOTE]  
    >  자동으로 필터를 생성하면 게시의 기존 행 필터나 조인 필터가 삭제됩니다. 필터 집합을 자동으로 생성한 후에 필터를 추가할 수 있습니다.  
  
2.  **필터 생성** 대화 상자의 프로세스를 따라 행 필터를 만듭니다. 그러면 기본 키와 외래 키 간의 관계를 통해 필터링된 테이블과 관련된 테이블로 행 필터가 확장됩니다.  
  
    1.  드롭다운 목록 상자에서 필터링할 테이블을 선택합니다.  
  
    2.  **필터 문** 입력란에서 필터 문을 만듭니다. 텍스트 영역에 직접 입력할 수도 있고 **열** 목록 상자에서 열을 끌어서 놓을 수도 있습니다.  
  
         **필터 문** 텍스트 영역에는 다음 형식의 기본 텍스트가 포함됩니다.  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
         기본 텍스트는 변경할 수 없습니다. 표준 SQL 구문을 사용하여 WHERE 키워드 다음에 정적 행 필터 또는 매개 변수가 있는 행 필터에 대한 필터 절을 입력합니다. 매개 변수가 있는 행 필터에 대한 전체 필터 절은 다음과 같습니다.  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         WHERE 절은 두 부분으로 구성된 이름을 사용해야 하며 세 부분 또는 네 부분으로 구성된 이름은 지원되지 않습니다.  
  
    3.  필터 옵션을 지정합니다.  
  
         **이 테이블의 행을 여러 구독으로 이동** 또는 **이 테이블의 행을 단일 구독으로 이동**중에서 구독자 간에 데이터를 공유하는 방식과 일치하는 옵션을 선택합니다. **이 테이블의 행을 단일 구독으로 이동**을 선택하면 병합 복제에서는 보다 작은 메타데이터를 저장하고 처리하여 성능을 최적화할 수 있습니다. 그러나 한 행이 둘 이상의 구독자로 복제될 수 없도록 데이터가 분할되어야 합니다. 자세한 내용은 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)항목의 "'partition options' 설정" 섹션을 참조하십시오.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     지정한 필터가 구문 분석되고 SELECT 절의 테이블에 대해 실행됩니다. 필터 문에 구문 오류나 기타 문제가 있으면 알림 메시지가 표시되며 이를 보고 필터 문을 편집할 수 있습니다.  
  
     문이 구문 분석된 후에 복제는 필요한 조인 필터를 만들고 **테이블 행 필터** 또는 **행 필터** 페이지의 **필터링된 테이블** 창에 이러한 필터를 표시합니다. 새 게시 마법사에서 필터를 생성할 때 이 마법사가 실행 중인 게시자에 대한 배포자를 아직 구성하지 않은 경우에는 구성을 요청하는 메시지가 표시됩니다.  
  
4.  **게시 속성 - \<게시>** 대화 상자에 있는 경우 **확인**을 클릭하여 대화 상자를 저장하고 닫습니다.  
  
### <a name="to-modify-a-filter-that-was-automatically-generated"></a>자동으로 생성된 필터를 수정하려면  
  
1.  새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<게시>** 대화 상자의 **행 필터** 페이지에 있는 **필터링된 테이블** 창에서 필터를 선택하고 **편집**을 클릭합니다.  
  
2.  **필터 편집** 또는 **조인 편집** 대화 상자에서 필터를 수정합니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-filter-that-was-automatically-generated"></a>자동으로 생성된 필터를 삭제하려면  
  
1.  새 게시 마법사의 **테이블 행 필터** 페이지 또는 **게시 속성 - \<게시>** 대화 상자의 **행 필터** 페이지에 있는 **필터링된 테이블** 창에서 필터를 선택하고 **삭제**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
