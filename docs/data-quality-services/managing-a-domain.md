---
title: 도메인 관리 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
ms.assetid: c5ab71a3-0dac-45b1-be8e-93bf7e0e03ce
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2730c37ba3afd24a0bbc29dece7a25dd15496bac
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51700891"
---
# <a name="managing-a-domain"></a>도메인 관리

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )에서 도메인을 사용하는 방법에 대해 설명합니다. 도메인은 분석할 데이터 원본의 특정 필드에 있는 데이터를 의미 체계에 따라 표현한 것입니다. 도메인은 사용자가 데이터 원본에 대해 만드는 기술 자료의 일부이며, 샘플 데이터 원본을 분석하거나 데이터를 가져와 구축한 정보는 기술 자료에 정의된 도메인에 추가됩니다. 이러한 도메인의 정보는 나중에 데이터 품질 프로젝트에서 정리 및 일치를 수행할 때 사용됩니다. 도메인은 Data Quality Services에서 모든 작업의 핵심에 있습니다.  
  
 도메인은 데이터 원본 필드에 매핑되고 기술 자료 검색, 도메인 관리 및 일치 작업에서 채워집니다. 데이터 원본의 데이터와 보고서의 출력 데이터를 로드하는 방법은 도메인 속성에 정의됩니다. 참조 데이터 공급자를 사용하여 데이터를 정리할 경우 단일 도메인이나 복합 도메인에 참조 데이터 서비스를 연결합니다. 도메인의 데이터에 적용할 규칙을 만들고 도메인의 용어 기반 관계를 만들 수 있습니다. 도메인의 데이터를 보고 수정할 수 있습니다.  
  
 또한 각각 공통 데이터에 대한 정보가 포함된 두 개 이상의 개별 도메인으로 구성되는 복합 도메인을 만들 수도 있습니다. 자세한 내용은 [복합 도메인 관리](../data-quality-services/managing-a-composite-domain.md)를 참조하세요.  
  
## <a name="domain-properties"></a>도메인 속성  
 도메인을 만들 때 원본 데이터에서 도메인을 채우는 방법과 도메인 값을 출력하는 방법에 대해 다음과 같은 옵션을 사용할 수 있습니다. 자세한 내용은 [도메인 속성 설정](../data-quality-services/set-domain-properties.md)을 참조하세요.  
  
-   도메인을 채우는 데 사용할 데이터 형식을 선택합니다. 각 도메인 데이터 형식에 대해 지원되는 데이터 형식에 대한 자세한 내용은 [DQS 도메인에 대해 지원되는 SQL Server 및 SSIS 데이터 형식](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md)을 참조하십시오.  
  
-   동의어가 아닌 선행 값만 도메인에서 출력되도록 지정합니다.  
  
-   도메인 값이 데이터 형식에 따라 특정 형식으로 출력되도록 지정합니다.  
  
-   데이터 형식이 문자열인 경우 데이터 원본에서 도메인으로 문자열이 로드될 때 특수 문자를 제거하여 문자열을 정규화할 수 있습니다.  
  
-   데이터 형식이 문자열인 경우 DQS 맞춤법 검사기를 실행하여 문자열의 구문, 맞춤법 및 문장 구조를 검사하고 잠재적 오류가 있으면 **도메인 관리** 의 **도메인 값**페이지에 표시할 수 있습니다. 여기에는 맞춤법 검사기가 실행될 때 사용할 언어를 지정하는 과정이 포함됩니다.  
  
-   데이터 형식이 문자열인 경우 문자열에서 구문 오류가 발생하지 않을 것이라 판단되면 DQS에서 구문 오류를 식별하지 않도록 지정할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 도메인을 사용하면 다음과 같은 작업을 수행할 수 있습니다.  
  
|||  
|-|-|  
|특정 데이터 형식의 데이터 필드를 의미 체계에 따라 표현, 도메인을 채우는 방법 지정, 도메인의 출력 형식 지정|[도메인 만들기](../data-quality-services/create-a-domain.md)|  
|도메인을 다른 도메인에 연결하여 동일한 설정 및 값 공유|[연결된 도메인 만들기](../data-quality-services/create-a-linked-domain.md)|  
|단일 또는 복합 도메인에 참조 데이터 서비스 연결|[참조 데이터에 도메인 또는 복합 도메인 연결](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|기술 자료의 값 변경 또는 보강|[도메인 값 변경](../data-quality-services/change-domain-values.md)|  
|유효성 검사 및 표준화 규칙 사용|[도메인 규칙 만들기](../data-quality-services/create-a-domain-rule.md)|  
|관계를 사용하여 도메인 값에 포함된 용어 수정|[용어 기반 관계 만들기](../data-quality-services/create-term-based-relations.md)|  
|도메인 관리 작업 완료, 닫기 또는 취소|[도메인 관리 작업 종료](https://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)|  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|기술 자료 검색을 실행하고 대화식으로 정보를 관리하여 기술 자료 구축|[기술 자료 구축](../data-quality-services/building-a-knowledge-base.md)|  
|기술 자료로 정보 가져오기 또는 기술 자료에서 정보 내보내기|[기술 자료 가져오기 및 내보내기](../data-quality-services/importing-and-exporting-knowledge.md)|  
|복합 도메인 만들기 및 단일 도메인에 정보 추가|[복합 도메인 관리](../data-quality-services/managing-a-composite-domain.md)|  
  
  
