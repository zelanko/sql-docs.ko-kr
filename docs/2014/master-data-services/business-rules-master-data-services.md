---
title: 비즈니스 규칙(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], about business rules
- business rules [Master Data Services]
ms.assetid: a9f9e41a-2461-4845-b947-58b3a205543f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d6ad90fe277e76f98298f4e66fe8c652e64fd38d
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65483654"
---
# <a name="business-rules-master-data-services"></a>비즈니스 규칙(Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 비즈니스 규칙은 마스터 데이터의 품질과 정확성을 유지하는 데 사용되는 규칙입니다. 비즈니스 규칙을 사용하여 자동으로 데이터를 업데이트하거나, 전자 메일을 보내거나, 비즈니스 프로세스 또는 워크플로를 시작할 수 있습니다.  
  
## <a name="create-and-publish-business-rules"></a>비즈니스 규칙 만들기 및 게시  
 비즈니스 규칙은 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 만드는 `If/Then` 문입니다. 특성 값이 지정한 조건을 충족하는 경우 동작이 수행됩니다. 가능한 동작에는 기본값 설정이나 값 변경이 있습니다. 이러한 동작을 전자 메일 알림과 함께 사용할 수 있습니다.  
  
 비즈니스 규칙은 특성 값이 변경될 때(예: Color 특성 값 변경 시 동작 수행)나 특정 특성 값(예: Color=Blue일 경우 동작 수행)을 기반으로 할 수 있습니다. 비특정 변경 사항 추적에 대한 자세한 내용은 [변경 내용 추적&#40;Master Data Services&#41;](change-tracking-master-data-services.md)을 참조하세요.  
  
 비즈니스 규칙을 사용하려면 먼저 규칙을 만들어 게시한 다음 게시된 규칙을 데이터에 적용해야 합니다. 버전의 유효성을 검사하여 데이터의 하위 집합 또는 버전의 모든 데이터에 규칙을 적용할 수 있습니다. 모든 특성이 비즈니스 규칙 유효성 검사를 통과해야 버전이 커밋될 수 있습니다.  
  
 사용자가 비즈니스 규칙 유효성 검사에 통과하지 않은 특성 값을 추가하는 경우에도 해당 값이 저장될 수 있습니다. [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에 표시된 유효성 검사 문제를 검토 및 해결할 수 있습니다.  
  
 모델 배포 패키지를 만들 때 비즈니스 규칙을 포함하려면 버전의 데이터를 패키지에 포함해야 합니다.  
  
 **OR** 연산자를 사용하는 비즈니스 규칙을 만드는 경우 개별적으로 평가할 수 있는 각 조건 문에 대해 개별 규칙을 만들어야 합니다. 그런 다음 필요에 따라 규칙을 제외시키면 유연성이 향상되고 더 쉽게 문제를 해결할 수 있습니다.  
  
## <a name="how-business-rules-are-applied"></a>비즈니스 규칙을 적용하는 방법  
 규칙을 실행할 우선 순위를 설정할 수 있습니다. 그러나 우선 순위를 고려하기 전에 비즈니스 규칙은 규칙에서 수행하는 동작 유형에 따라 적용됩니다. 순서는 다음과 같습니다.  
  
1.  **기본값**  
  
2.  **값 변경**  
  
3.  **유효성 검사**  
  
4.  **외부 동작**  
  
 이 그룹 내에서 동작은 우선 순위가 낮은 것부터 적용됩니다. 따라서 예를 들면 네 개의 개별 규칙에 **기본값** 동작이 있을 수 있습니다. 먼저 발생하는 **기본값** 동작은 웹 UI에 지정된 우선 순위에 따라 달라집니다.  
  
 규칙을 적용하는 방법에 대한 기타 중요한 참고 사항은 다음과 같습니다.  
  
-   비즈니스 규칙이 제외되거나 **활성**상태로 게시되지 않는 경우에도 해당 규칙은 여전히 사용할 수 있지만 비즈니스 규칙 적용 시에 포함되지 않습니다.  
  
-   비즈니스 규칙은 모든 리프 멤버나 통합 멤버 중 하나의 특성 값에 적용됩니다.  
  
-   비즈니스 규칙은 **열림** 또는 **잠금**상태인 모델 버전에 적용될 수 있습니다.  
  
-   비즈니스 규칙을 적용할 때 데이터에 대해 변경된 내용은 트랜잭션으로 기록되지 않습니다.  
  
-   비즈니스 규칙은 **워크플로 시작** 동작을 두 개 이상 포함할 수 없습니다.  
  
## <a name="system-settings"></a>시스템 설정  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 에는 비즈니스 규칙에 영향을 주는 두 가지 설정이 있습니다. 이러한 설정은 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] 에서 조정하거나 시스템 설정 테이블에서 직접 조정할 수 있습니다. 자세한 내용은 [시스템 설정&#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|새 비즈니스 규칙을 만들어 게시합니다.|[비즈니스 규칙 만들기 및 게시&#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)|  
|비즈니스 규칙에 여러 조건을 추가합니다.|[비즈니스 규칙에 여러 조건 추가&#40;Master Data Services&#41;](../../2014/master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)|  
|특성에 값이 필요한 비즈니스 규칙을 만듭니다.|[특성 값 요구&#40;Master Data Services&#41;](../../2014/master-data-services/require-attribute-values-master-data-services.md)|  
|특성 값 변경 사항을 기반으로 동작을 수행하는 비즈니스 규칙을 만듭니다.|[특성 값 변경 기반 동작 시작&#40;Master Data Services&#41;](../../2014/master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)|  
|기존 비즈니스 규칙의 이름을 변경합니다.|[비즈니스 규칙 이름 변경&#40;Master Data Services&#41;](../../2014/master-data-services/change-a-business-rule-name-master-data-services.md)|  
|비즈니스 규칙이 적용될 때 알림을 보내도록 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 를 구성합니다.|[알림을 보내도록 비즈니스 규칙 구성&#40;Master Data Services&#41;](../../2014/master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
|특정 멤버에 비즈니스 규칙을 적용합니다.|[비즈니스 규칙에 대해 특정 멤버 유효성 검사&#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)|  
|비즈니스 규칙을 사용하지 않도록 제외합니다.|[비즈니스 규칙 제외&#40;Master Data Services&#41;](../../2014/master-data-services/exclude-a-business-rule-master-data-services.md)|  
|기존 비즈니스 규칙을 삭제합니다.|[비즈니스 규칙 삭제&#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-business-rule-master-data-services.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [Master Data Services 개요](master-data-services-overview-mds.md)  
  
-   [버전&#40;Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)  
  
-   [유효성 검사&#40;Master Data Services&#41;](../../2014/master-data-services/validation-master-data-services.md)  
  
-   [변경 내용 추적&#40;Master Data Services&#41;](change-tracking-master-data-services.md)  
  
  
