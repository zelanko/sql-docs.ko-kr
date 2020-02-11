---
title: 엔터티 트랜잭션 로그 유형 변경
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 75250b32-3384-43c2-9b5c-1607cc3aa7b3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: fde8e314462846088c7c673524d6e6d8d29ee631
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73729670"
---
# <a name="change-the-entity-transaction-log-type-master-data-services"></a>엔터티 트랜잭션 로그 유형 변경(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  엔터티의 트랜잭션 로그 유형을 특성, 멤버 또는 없음으로 변경할 수 있습니다.  
  
|트랜잭션 로그 유형|Description|  
|--------------------------|-----------------|  
|attribute|엔터티 변경 로그가 특성 수준에 저장됩니다.<br /><br /> 트랜잭션 로그는의 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]경우와 같이 저장 됩니다.|  
|멤버|엔터티 변경 로그가 행 수준에 저장됩니다.<br /><br /> 특성이 변경되면 새 행 수정이 트리거됩니다.<br /><br /> 행 트랜잭션 로그 유형을 사용할 때는 엔터티가 느리게 변경되는 차원 유형 4로 저장됩니다. 유형 2 구독 보기 및 유형 4(기록) 구독 뷰가 지원됩니다. 자세한 내용은 [구독 뷰 형식&#40;Master Data Services&#41;](../master-data-services/subscription-view-formats-master-data-services.md)을 참조하세요.<br /><br /> 더 나은 성능을 제공합니다.|  
|None|변경 로그가 저장되지 않습니다.<br /><br /> 최상의 성능을 제공합니다.|  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   시스템 관리 기능 영역에 액세스할 수 있는 권한이 있어야 합니다. 자세한 내용은 [기능 영역 권한&#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)을 참조하세요.  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
-   엔터티가 있어야 합니다. 자세한 내용은 [&#41;MDS(Master Data Services) 엔터티 &#40;만들기 ](../master-data-services/create-an-entity-master-data-services.md)를 참조 하세요.  
  
 **트랜잭션 로그 유형을 변경 하려면**  
  
1.  마스터 데이터 관리자에서 **시스템 관리**를 클릭합니다.  
  
2.  
  **모델 관리** 페이지에서 편집할 엔터티의 모델에 해당하는 행을 선택하고 **엔터티**를 클릭합니다.  
  
3.  
  **엔터티 관리** 페이지에서 업데이트할 엔터티에 해당하는 행을 선택하고 **편집**을 클릭합니다.  
  
4.  드롭다운 목록에서 트랜잭션 로그 유형을 선택합니다.  
  
5.  **저장**을 클릭합니다.  
  
  
