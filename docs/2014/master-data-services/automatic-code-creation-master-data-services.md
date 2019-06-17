---
title: 코드 자동 생성(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9adbd5e1-f28c-4fb5-afa7-082de2831f3e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7ee7e06829f72ab44fd036766907be94c95b7d90
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483690"
---
# <a name="automatic-code-creation-master-data-services"></a>코드 자동 생성(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 코드 특성 또는 기타 숫자 특성에 대해 숫자 값을 자동으로 생성할 수 있습니다. 코드가 자동으로 생성될 때 코드에 다른 값을 입력할 수 없는 것은 아니지만 초기 값이 자동으로 설정됩니다.  
  
## <a name="generating-code-values"></a>코드 값 생성  
 관리자는 연결된 엔터티의 속성을 편집하여 코드 특성에 대한 자동 생성 값을 구성할 수 있습니다. 관리자가 초기 값을 지정할 수 있으며 이후의 각 값은 1씩 증가됩니다.  
  
 도구 중 하나를 사용하거나 준비 프로세스를 사용하여 코드 값을 MDS에 입력할 때 코드 값을 비워 둘 수 있으며 이 경우 코드 값이 자동으로 생성됩니다. 또는 원하는 코드 값을 지정할 수 있습니다.  
  
## <a name="generating-other-attribute-values"></a>다른 특성 값 생성  
 관리자는 비즈니스 규칙을 만들어 코드 외의 특성 값을 자동으로 생성할 수 있습니다. 초기 값을 지정할 수 있으며 이후의 각 값이 증가되는 수치를 지정할 수 있습니다.  
  
 도구 중 하나를 사용하거나 준비 프로세스를 사용하여 특성 값을 MDS에 입력할 때 특성 값을 비워 둘 수 있습니다. 비즈니스 규칙이 적용되면 가장 높은 기존 값을 기반으로 값이 증가됩니다. 예를 들어 규칙이 "1에서 시작하고 4씩 증가하는 생성된 값을 특성 기본값으로 설정"이고 특성의 가장 높은 현재 값이 700인 경우 추가되는 다음 멤버의 값은 704가 됩니다.  
  
## <a name="deleting-automatically-generated-values"></a>자동으로 생성된 값 삭제  
 관리자가 코드 특성에 대해 자동 생성 값을 설정한 후 사용자가 다시 사용하려는 코드 값이 포함된 멤버를 실수로 삭제할 수 있습니다. "멤버 코드가 이미 삭제 된 멤버가 사용 은" 오류 메시지가 표시 됩니다. 가능한 해결 방법으로는 다음 두 가지가 있습니다.  
  
-   **버전 관리** 기능 영역에서 관리자가 멤버가 삭제될 때 발생한 트랜잭션을 되돌릴 수 있습니다. 그러나이 경우 모든 이전 멤버의 특성 및 계층 및 컬렉션의 멤버 자격이 복원 됩니다. 자세한 내용은 [트랜잭션 되돌리기 &#40;Master Data Services&#41;](reverse-a-transaction-master-data-services.md)합니다.  
  
-   관리자는 준비 프로세스를 사용하여 멤버를 영구적으로 삭제할 수 있습니다. 자세한 내용은 [비활성화 하거나 준비 프로세스를 사용 하 여 멤버가 삭제 &#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)합니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|코드 특성 값 자동 생성|[코드 특성 값 자동 생성&#40;Master Data Services&#41;](../../2014/master-data-services/automatically-generate-code-attribute-values-master-data-services.md)|  
|다른 특성 값 자동 생성|[코드 외의 특성 값 자동 생성&#40;Master Data Services&#41;](../../2014/master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [Master Data Services 개요](master-data-services-overview-mds.md)  
  
-   [비즈니스 규칙&#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
-   [엔터티&#40;Master Data Services&#41;](../../2014/master-data-services/entities-master-data-services.md)  
  
  
