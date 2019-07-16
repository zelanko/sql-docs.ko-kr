---
title: 복합 도메인 관리 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 47821eff-800b-4053-8d36-e42bbc267f54
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: fac57f53242fa7445820aaed5a39694a7277653c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935075"
---
# <a name="managing-a-composite-domain"></a>복합 도메인 관리

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )에서 복합 도메인을 사용하는 방법에 대해 설명합니다. 단일 도메인이 필드의 데이터를 충분히 표현하지 않아서 단일 도메인을 그룹화해야만 데이터를 표현할 수 있는 경우가 있습니다. 이 경우 복합 도메인을 만듭니다. 복합 도메인은 둘 이상의 단일 도메인으로 구성되며 구문 분석되지 않았지만 단일 복합 값에 포함되어 있는 여러 관련 용어로 구성된 데이터 필드에 매핑됩니다. 값의 각 용어는 다른 단일 값으로 표현됩니다. 단일 도메인을 복합 도메인에 포함한 후 복합 도메인을 데이터 필드에 매핑하고 나면 단일 도메인의 정보를 구축하여 해당 필드의 데이터에 대한 기술 자료의 정보를 구축할 수 있습니다. 복합 도메인은 단일 도메인과 마찬가지로 단일 데이터 필드의 데이터를 의미 체계에 따라 표현한 것입니다.  
  
 복합 도메인의 단일 도메인은 서로 공통된 정보 영역이 있어야 합니다. 예를 들어 우편 번호, 국가, 시/도, 구/군/시 및 번지 데이터가 있는 주소 필드가 있습니다. 이 필드에 있는 여러 용어의 데이터 형식은 서로 다를 수 있습니다. 이 문제를 해결하려면 해당 용어를 서로 다른 단일 도메인에 매핑합니다. 또 다른 예로 성, 중간 이름 및 이름 데이터가 있는 전체 이름 필드가 있습니다. 복합 도메인을 사용하려면 필드의 데이터를 서로 다른 단일 도메인으로 구문 분석한 후 해당 필드에 대한 복합 도메인과 필드의 각 부분에 대한 단일 도메인을 만들어야 합니다.  
  
 복합 도메인은 단일 도메인과 기능이 다릅니다. 복합 도메인에서는 단일 도메인처럼 값을 변경할 수 없습니다. 복합 도메인의 경우 도메인 간 규칙을 사용하여 복합 도메인의 단일 도메인에 있는 값을 테스트할 수 있습니다. 또한 복합 도메인에 있는 값 조합을 볼 수도 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 복합 도메인을 사용하면 다음과 같은 작업을 수행할 수 있습니다.  
  
|||  
|-|-|  
|구문 분석되지 않은 여러 관련 용어로 구성된 데이터 필드를 의미 체계에 따라 표현합니다.|[복합 도메인 만들기](../data-quality-services/create-a-composite-domain.md)|  
|복합 도메인에 복잡한 데이터를 매핑할 때 정보 기반 데이터를 구문 분석하고 구분 기호에 대해 구문 분석을 수행할 수 있습니다. DQS는 우선 단일 도메인에 대한 정보를 사용하여 복잡한 문자열의 각 부분이 단일 도메인에 어떻게 속해 있는지 확인합니다.|[복합 도메인 만들기](../data-quality-services/create-a-composite-domain.md)|  
|주소 데이터를 처리하는 서비스와 같은 참조 데이터 서비스를 복합 도메인에 연결합니다.|[참조 데이터에 도메인 또는 복합 도메인 연결](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|복합 도메인의 한 도메인 값이 다른 도메인의 값에 영향을 줄 경우 도메인 간 규칙을 만듭니다.|[도메인 간 규칙 만들기](../data-quality-services/create-a-cross-domain-rule.md)|  
|DQS가 빈도를 보고할 수 있도록 값 조합을 식별합니다.|[복합 도메인의 값 관계 사용](../data-quality-services/use-value-relations-in-a-composite-domain.md)|  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|기술 자료 검색을 실행하고 대화식으로 정보를 관리하여 기술 자료 구축|[기술 자료 구축](../data-quality-services/building-a-knowledge-base.md)|  
|기술 자료로 정보 가져오기 또는 기술 자료에서 정보 내보내기|[기술 자료 가져오기 및 내보내기](../data-quality-services/importing-and-exporting-knowledge.md)|  
|단일 도메인 만들기 및 단일 도메인에 정보 추가|[도메인 관리](../data-quality-services/managing-a-domain.md)|  
  
  
