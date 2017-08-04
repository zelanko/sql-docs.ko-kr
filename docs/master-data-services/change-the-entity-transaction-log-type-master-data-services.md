---
title: "(Master Data Services) 엔터티 트랜잭션 로그 유형 변경 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 75250b32-3384-43c2-9b5c-1607cc3aa7b3
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d3f5998073b5a4ddf596e241a52db6bbd49f3a2d
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="change-the-entity-transaction-log-type-master-data-services"></a>엔터티 트랜잭션 로그 유형 변경(Master Data Services)
  엔터티의 트랜잭션 로그 유형을 특성, 멤버 또는 없음으로 변경할 수 있습니다.  
  
|트랜잭션 로그 유형|Description|  
|--------------------------|-----------------|  
|Attribute|엔터티 변경 로그가 특성 수준에 저장됩니다.<br /><br /> 트랜잭션 로그는 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서와 같이 저장됩니다.|  
|멤버|엔터티 변경 로그가 행 수준에 저장됩니다.<br /><br /> 특성이 변경되면 새 행 수정이 트리거됩니다.<br /><br /> 행 트랜잭션 로그 유형을 사용할 때는 엔터티가 느리게 변경되는 차원 유형 4로 저장됩니다. 유형 2 구독 보기 및 유형 4(기록) 구독 뷰가 지원됩니다. 자세한 내용은 [구독 뷰 형식&#40;Master Data Services&#41;](../master-data-services/subscription-view-formats-master-data-services.md)을 참조하세요.<br /><br /> 더 나은 성능을 제공합니다.|  
|없음|변경 로그가 저장되지 않습니다.<br /><br /> 최상의 성능을 제공합니다.|  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   시스템 관리 기능 영역에 액세스할 수 있는 권한이 있어야 합니다. 자세한 내용은 [기능 영역 권한&#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)을 참조하세요.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
-   엔터티가 있어야 합니다. 자세한 내용은 [엔터티 만들기&#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)를 참조하세요.  
  
 **트랜잭션 로그 유형을 변경하려면**  
  
1.  마스터 데이터 관리자에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 관리** 페이지에서 편집할 엔터티의 모델에 해당하는 행을 선택하고 **엔터티**를 클릭합니다.  
  
3.  **엔터티 관리** 페이지에서 업데이트할 엔터티에 해당하는 행을 선택하고 **편집**을 클릭합니다.  
  
4.  드롭다운 목록에서 트랜잭션 로그 유형을 선택합니다.  
  
5.  **저장**을 클릭합니다.  
  
  
