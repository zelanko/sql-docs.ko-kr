---
title: 변경 집합
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: f227c49a-ed46-4e0f-8992-83093456cf94
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c6b91f1d0b4fbfff3294502b0953462f97efc707
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85811625"
---
# <a name="changesets-master-data-services"></a>변경 집합(Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 에서는 이제 엔터티에 대해 보류 중인 모든 변경 내용을 변경 집합으로 저장하는 기능을 지원합니다. 이 기능의 두 가지 사용 시나리오가 있습니다.  
  
-   **엔터티 관리자가 "승인 필요"를 켠 경우의 변경 내용**  
  
     엔터티 관리자가 지정된 엔터티의 변경 내용을 커밋하기 전에 승인이 필요하도록 지정할 경우 엔터티에 대한 모든 변경 내용을 새 변경 집합이나 기존 변경 집합에 저장해야 승인을 위해 제출할 수 있습니다.  자세한 내용은 [승인 필요&#40;Master Data Services&#41;](../master-data-services/approval-required-master-data-services.md)를 참조하세요.  
  
     다음 워크플로를 따릅니다.  
  
    1.  변경 집합을 만듭니다. 변경 집합은 열림 상태입니다. [Create a Changeset &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)  
  
    2.  변경 집합을 적용하고 일부 변경 내용을 변경 집합에 추가합니다. [변경 집합 적용 및 업데이트&#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)를 참조하세요.  
  
    3.  승인을 위해 엔터티 관리자에게 변경 집합을 제출합니다. 변경 집합은 보류 중 상태입니다. [변경 집합 커밋 또는 제출&#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)을 참조하세요.  
  
    4.  엔터티 관리자가 변경 집합이 승인 대기 중이라는 메일 알림을 받습니다. 엔터티 관리자가 변경 집합을 승인할 경우 변경 집합은 승인됨 상태입니다. [변경 집합 승인 또는 거부&#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)를 참조하세요.  
  
    5.  승인된 변경 집합은 자동으로 커밋됩니다. 변경 내용이 성공적으로 커밋되면 변경 집합은 커밋됨 상태입니다.  
  
-   **로컬 사용자 변경 내용**  
  
     나중에 사용하거나 검색할 수 있도록 단순히 로컬 변경 내용을 저장하려는 경우 변경 집합을 사용할 수 있습니다.  
  
     다음 워크플로를 따릅니다.  
  
    1.  변경 집합을 만듭니다. 변경 집합은 열림 상태입니다. [Create a Changeset &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)  
  
    2.  변경 집합을 적용하고 일부 변경 내용을 변경 집합에 추가합니다. [변경 집합 적용 및 업데이트&#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)를 참조하세요.  
  
    3.  준비가 되면 변경 집합을 커밋합니다. [변경 집합 커밋 또는 제출&#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [변경 집합 &#40;MDS(Master Data Services)를 만듭니다&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [변경 집합 &#40;MDS(Master Data Services) 적용 및 업데이트&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [MDS(Master Data Services)&#41;&#40;변경 집합 커밋 또는 제출](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)   
 [변경 집합 &#40;MDS(Master Data Services) 승인 또는 거부&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)   
 [변경 집합 관리&#40;Master Data Services&#41;](../master-data-services/manage-changesets-master-data-services.md)  
  
  
