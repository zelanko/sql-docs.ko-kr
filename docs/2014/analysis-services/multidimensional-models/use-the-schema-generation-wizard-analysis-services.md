---
title: 스키마 생성 마법사 사용 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Schema Generation Wizard, steps
- relational schema [Analysis Services], Schema Generation Wizard
ms.assetid: 8c710745-d41d-4c31-b6a2-2956229df75a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e434493813f0237533ca2e50ff089974f3556f34
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66072651"
---
# <a name="use-the-schema-generation-wizard-analysis-services"></a>스키마 생성 마법사 사용(Analysis Services)
  스키마 생성 마법사는 스키마를 생성하는 동안 제한된 정보만 사용합니다. 스키마 생성 마법사가 관계형 스키마를 생성하기 위해 필요한 대부분의 정보는 프로젝트에서 이미 만들었던 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 큐브와 차원으로부터 추출됩니다. 또한 주제 영역 데이터베이스 스키마가 생성되는 방법과 스키마의 개체 이름이 지정되는 방법을 사용자 지정할 수 있습니다.  
  
## <a name="start-the-wizard"></a>마법사 시작  
 
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 몇 가지 방법으로 스키마 생성 마법사를 열 수 있습니다.  
  
-   
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 개체를 마우스 오른쪽 단추로 클릭한 다음 상황에 맞는 메뉴에서 **관계형 스키마 생성** 을 클릭합니다.  
  
-   
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 개체를 클릭한 다음 **데이터베이스** 메뉴에서 **관계형 스키마 생성** 을 클릭합니다.  
  
-   마법사의 마지막 페이지에서 **지금 스키마 생성** 확인란을 클릭하여 차원 마법사 내에서 마법사를 시작합니다.  
  
## <a name="step-1-specify-targets"></a>1단계: 대상 지정  
 스키마 생성 마법사에서 주제 영역 데이터베이스에 대한 스키마를 생성할 데이터 원본 뷰(DSV)를 지정해야 합니다. 기존 DSV를 선택할 수 있지만 일반적으로 데이터 원본을 기반으로 새 데이터 원본을 만듭니다. 기존 또는 새 연결을 기반으로 하거나 다른 개체를 기반으로 하여 데이터 원본을 만들 수 있습니다. 스키마 생성 마법사는 데이터 원본이 참조하는 데이터베이스와 데이터 원본 뷰 모두에서 주제 영역 데이터베이스에 대한 스키마를 생성합니다. 스키마 생성 마법사가 주제 영역 데이터베이스를 만들지는 않으며 대신 사용자가 지정한 기존 데이터베이스의 큐브와 차원을 지원하는 관계형 스키마를 생성합니다.  
  
 스키마 생성 마법사는 기본 개체를 생성할 때 데이터 원본 뷰 스타일의 바인딩을 통해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 차원과 큐브를 생성된 테이블과 열에 바인딩합니다.  
  
> [!NOTE]  
>  이전에 생성된 개체에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 차원과 큐브의 바인딩을 해제하려면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 큐브와 차원이 바인딩된 데이터 원본 뷰를 삭제한 다음 스키마 생성 마법사를 사용하여 큐브와 차원에 대해 새 데이터 원본 뷰를 정의합니다.  
  
## <a name="step-3-specify-schema-options-for-the-subject-area-database"></a>3단계: 주제 영역 데이터베이스에 대한 스키마 옵션 지정  
 스키마 생성 마법사는 주제 영역 데이터베이스에 대해 생성되는 스키마를 정의하는 데 사용할 수 있는 많은 옵션을 제공합니다. 마법사의 **주제 영역 데이터베이스 스키마 옵션** 페이지에서 이러한 옵션을 지정할 수 있습니다.  
  
### <a name="specifying-the-schema-owner"></a>스키마 소유자 지정  
 
  **소유 스키마** 의 값을 유효한 문자열로 설정하여 스키마 소유자를 지정할 수 있습니다. 스키마의 기본 소유자는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트이지만 원하는 스키마 소유자를 지정할 수도 있습니다.  
  
### <a name="specifying-primary-keys-indexes-and-constraints"></a>기본 키, 인덱스 및 제약 조건 지정  
 스키마 생성 마법사는 기본적으로 주제 영역 데이터베이스의 각 차원 테이블에 기본 키 제약 조건을 생성합니다. 기본 키는 연관된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 차원에서 키 특성으로 지정된 특성에 해당합니다. 이 제약 조건은 대부분의 환경에서 최소한의 비용으로 처리 성능을 높입니다. 주제 영역 데이터베이스에서 기본 키를 만들지 않도록 선택한 경우에도 논리적 기본 키는 항상 데이터 원본 뷰에서 생성됩니다. 차원 테이블에 기본 키 제약 조건을 정의하려면 **차원 테이블에 기본 키 만들기**를 선택합니다.  
  
 기본적으로 마법사는 각 팩트 테이블의 외래 키 열에 대해서도 인덱스를 만듭니다. 이러한 인덱스는 대부분의 환경에서 처리 성능을 향상시킵니다. 대개 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 주제 영역 데이터베이스에서 새 데이터를 검색하기 위해 생성하는 처리 쿼리에는 팩트 테이블과 차원 테이블 간의 조인 문이 상당수 포함되기 때문에 성능이 향상됩니다. 각 팩트 테이블의 외래 키 열에 인덱스를 정의하려면 **인덱스 만들기**를 선택합니다.  
  
 마지막으로, 마법사는 팩트 테이블과 각 차원 테이블 간에 참조 무결성을 적용합니다. 참조 무결성을 적용하지 않도록 선택하면 스키마 생성 마법사가 데이터베이스와 데이터 원본 뷰에서 팩트 테이블과 각 차원 테이블 간의 관계를 만듭니다. 참조 무결성을 적용하려면 **참조 무결성 적용**을 선택합니다.  
  
### <a name="preserving-data-for-incremental-generation"></a>증분 생성을 위해 데이터 유지  
 스키마 생성 마법사는 기본적으로 데이터베이스 스키마가 다시 생성될 때 데이터를 유지합니다. 스키마 변경으로 인해 스키마 생성 마법사가 행을 삭제해야 하는 경우에는 행을 삭제하기 전에 경고 메시지를 표시합니다. 예를 들어 차원을 삭제했기 때문에 참조 무결성 문제를 해결하기 위해 행을 삭제하거나, 차원 특성을 변경할 때 데이터 형식이 변경되어 행을 삭제해야 하는 경우가 있습니다. 데이터베이스 스키마가 다시 생성될 때 데이터를 유지하려면 **다시 생성 시 데이터 유지**를 선택합니다.  
  
## <a name="step-4-specify-naming-conventions"></a>4단계: 명명 규칙 지정  
 스키마 생성 마법사가 주제 영역 데이터베이스에서 개체를 생성할 때 사용할 명명 규칙은 마법사의 **명명 규칙 지정** 페이지에서 정의할 수 있습니다. 
  **명명 규칙 지정** 페이지에서 사용할 수 있는 옵션에 대한 자세한 내용은 [명명 규칙 지정&#40;스키마 생성 마법사&#41;&#40;Analysis Services - 다차원 데이터&#41;](../specify-naming-conventions-schema-generation-analysis-services-multidimensional-data.md)을 참조하세요.  
  
  
