---
title: "사용 되지 않는 Master Data Services 기능 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d8506bda-66dd-45a4-bfc9-3a10fa665acc
caps.latest.revision: 18
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e4d9b433e72c916ae6611520498b0eb8fa85c8f6
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="deprecated-master-data-services-features"></a>사용되지 않는 Master Data Services 기능
  이 항목에서는 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 에서 계속 제공되지만 더 이상 사용되지 않는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]기능에 대해 설명합니다. 이러한 기능은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 이후 릴리스에서 제거될 예정입니다. 새 응용 프로그램에는 이러한 기능을 사용하면 안 됩니다.  
  
## <a name="explicit-hierarchies-collections-and-related-components"></a>명시적 계층, 컬렉션 및 관련 구성 요소  
 명시적 계층, 컬렉션 및 관련 구성 요소는 사용되지 않습니다. 이전에는 통합 멤버 유형(명시적 계층 부모) 및 컬렉션 멤버 유형으로 모델링되었던 멤버는 파생 계층의 리프 멤버로 모델링됩니다. 아래의 새로운 기능을 통해 파생 계층을 명시적 계층 대신 사용할 수 있습니다.  
  
-   이제는 재귀 파생 계층을 사용하여 멤버 보안 권한을 할당할 수 있습니다.  
  
     명시적 계층은 재귀 수준 아래에 비재귀 수준 하나가 포함되어 있는 재귀 파생 계층과 동일합니다. 재귀 수준 아래 및/또는 위에 수준을 포함하여 재귀 파생 계층을 복합 계층으로 만들 수 있습니다.  
  
-   이제는 탐색기에서 파생 계층 페이지에 각 계층 구조 수준의 할당되지 않은(사용되지 않는) 멤버가 표시됩니다. 사용되지 않는 노드는 계층 구조 수준별로 그룹화됩니다. 끌어서 놓기 또는 잘라내기와 붙여넣기를 통해 사용 안 함 노드와 루트 노드 간에 멤버를 이동할 수 있습니다.  
  
     시스템 관리에서 사용되지 않는 노드는 **미리 보기** 창에 표시됩니다. 보안에서 사용되지 않는 노드는 **계층 멤버 권한** 창에 표시됩니다. 위치( **루트** 노드 아래 또는 **사용 안 함** 노드 아래)에 관계없이 모든 멤버에 권한을 할당할 수 있습니다. **루트**, **사용 안 함**및 **사용 안 함** 의사 멤버에도 권한을 할당할 수 있습니다.  
  
-   mdm.udpConvertCollectionAndConsolidatedMembersToLeaf 저장 프로시저는 명시적 계층을 재귀 파생 계층으로 변환하고 통합 및 컬렉션 멤버를 리프 멤버로 변환합니다.  
  
     명시적 계층 및 통합/컬렉션 멤버 유형은 계속 지원되므로 필요에 따라 저장 프로시저를 실행할 수 있습니다. 그러나 이러한 항목은 더 이상 사용되지 않으므로 사용 시에는 저장 프로시저를 실행하는 것이 좋습니다.  
  
 명시적 계층, 컬렉션 및 통합 멤버에 대한 자세한 내용은 다음 항목을 참조하세요.  
  
-   [명시적 계층&#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [컬렉션&#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
-   [멤버&#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)  
  
## <a name="attribute-entity-transaction-log-type"></a>특성 엔터티 트랜잭션 로그 유형  
엔터티 트랜잭션 로그 유형 "특성"은 더 이상 사용되지 않습니다. "멤버" 엔터티 트랜잭션 로그 유형으로 마이그레이션하세요. 엔터티 트랜잭션 로그 유형에 대한 자세한 내용은 다음 항목을 참조하세요.
* [엔터티 트랜잭션 로그 유형 변경(Master Data Services)](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)
* [멤버 수정 기록](../master-data-services/member-revision-history-master-data-services.md)
  
## <a name="external-resources"></a>외부 리소스  
 msdn.com의 블로그 게시물 [사용되지 않음: 명시적 계층 및 컬렉션](http://go.microsoft.com/fwlink/p/?LinkId=615373)  
  
## <a name="see-also"></a>참고 항목  
 [지원되지 않는 MDS(Master Data Services) 기능](../master-data-services/discontinued-master-data-services-features.md)  
  
  
