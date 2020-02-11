---
title: 코드 자동 생성
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9adbd5e1-f28c-4fb5-afa7-082de2831f3e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: abf900f8eea0e64ed8e541ee7cd94c63834fbb48
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73729749"
---
# <a name="automatic-code-creation-master-data-services"></a>코드 자동 생성(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서는 코드 특성 또는 기타 숫자 특성에 대해 숫자 값을 자동으로 생성할 수 있습니다. 코드가 자동으로 생성될 때 코드에 다른 값을 입력할 수 없는 것은 아니지만 초기 값이 자동으로 설정됩니다.  
  
## <a name="generating-code-values"></a>코드 값 생성  
 관리자는 연결된 엔터티의 속성을 편집하여 코드 특성에 대한 자동 생성 값을 구성할 수 있습니다. 관리자가 초기 값을 지정할 수 있으며 이후의 각 값은 1씩 증가됩니다.  
  
 도구 중 하나를 사용하거나 준비 프로세스를 사용하여 코드 값을 MDS에 입력할 때 코드 값을 비워 둘 수 있으며 이 경우 코드 값이 자동으로 생성됩니다. 또는 원하는 코드 값을 지정할 수 있습니다.  
  
## <a name="generating-other-attribute-values"></a>다른 특성 값 생성  
 관리자는 비즈니스 규칙을 만들어 코드 외의 특성 값을 자동으로 생성할 수 있습니다. 초기 값을 지정할 수 있으며 이후의 각 값이 증가되는 수치를 지정할 수 있습니다.  
  
 도구 중 하나를 사용하거나 준비 프로세스를 사용하여 특성 값을 MDS에 입력할 때 특성 값을 비워 둘 수 있습니다. 비즈니스 규칙이 적용되면 가장 높은 기존 값을 기반으로 값이 증가됩니다. 예를 들어 규칙이 "1에서 시작하고 4씩 증가하는 생성된 값을 특성 기본값으로 설정"이고 특성의 가장 높은 현재 값이 700인 경우 추가되는 다음 멤버의 값은 704가 됩니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|코드 특성 값 자동 생성|[MDS(Master Data Services) &#40;코드 특성 값을 자동으로 생성&#41;](../master-data-services/automatically-generate-code-attribute-values-master-data-services.md)|  
|다른 특성 값 자동 생성|[코드 &#40;MDS(Master Data Services) 이외의 특성 값을 자동으로 생성&#41;](../master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [MDS&#41;&#40;MDS(Master Data Services) 개요](../master-data-services/master-data-services-overview-mds.md)  
  
-   [비즈니스 규칙 &#40;MDS(Master Data Services)&#41;](../master-data-services/business-rules-master-data-services.md)  
  
-   [엔터티 &#40;MDS(Master Data Services)&#41;](../master-data-services/entities-master-data-services.md)  
  
  
