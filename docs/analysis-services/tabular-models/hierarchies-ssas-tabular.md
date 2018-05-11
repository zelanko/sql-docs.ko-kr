---
title: 계층 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 68980b8c6207177696d1a9a30f7dfdd1dcc9464c
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="hierarchies"></a>계층 구조
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  테이블 형식 모델에서 계층은 테이블에서 두 개 이상의 열 간의 관계를 정의하는 메타데이터입니다. 계층은 보고 클라이언트 필드 목록에서 다른 열과는 별도로 표시되므로 클라이언트 사용자가 손쉽게 탐색하여 보고서에 포함할 수 있습니다.  
  
##  <a name="bkmk_benefits"></a> 이점  
 테이블에는 비정상적인 열 이름을 갖는 수십 또는 수백 개의 열이 일정한 순서 없이 포함될 수 있습니다. 따라서 보고 클라이언트 필드 목록이 순서 없이 표시되므로 사용자가 데이터를 찾아서 보고서에 포함하기가 어려울 수 있습니다. 계층을 통해 복잡한 데이터 구조를 간단하고 직관적으로 볼 수 있습니다.  
  
 예를 들어 날짜 테이블에서 달력 계층을 만들 수 있습니다. 이때 역년이 최상위 부모 수준으로 사용되고 월, 주 및 일은 자식 수준으로 포함됩니다(역년->월->주->일). 이 계층은 역년에서 일까지의 논리적 관계를 보여 줍니다. 클라이언트 사용자는 필드 목록에서 Calendar Year를 선택하여 피벗 테이블에 모든 수준을 포함하거나, 계층을 확장하고 피벗 테이블에 포함할 특정 수준만 선택할 수 있습니다.  
  
 계층의 각 수준은 테이블 열의 표현이므로 수준의 이름을 변경할 수 있습니다. 테이블 형식 모델에서 임의 열의 이름을 바꿀 수 있는 계층에만 국한되지 않고, 계층 수준의 이름을 바꾸면 사용자가 수준을 쉽게 찾아서 보고서에 포함할 수 있습니다. 수준의 이름을 변경해도 해당 수준이 참조하는 열의 이름은 바뀌지 않으며, 수준을 식별하기가 더 쉬워질 뿐입니다. 예를 들어 Calendar Year 계층의 데이터 뷰에 있는 데이터 테이블에서 CalendarYear, CalendarMonth, CalendarWeek 및 CalendarDay 열의 이름을 Calendar Year, Month, Week 및 Day로 변경하여 식별하기 쉽게 만들었습니다. 수준의 이름을 바꾸면 사용자가 피벗 테이블, 차트 등에서 열 이름을 읽기 쉽게 변경할 필요가 없기 때문에 보고서의 일관성이 유지되는 추가적인 이점이 있습니다.  
  
 계층은 큐브 뷰에 포함될 수 있습니다. 큐브 뷰는 모델을 비즈니스 또는 응용 프로그램 중심의 관점에서 파악할 수 있게 해주는 보기 가능한 모델 하위 집합을 정의합니다. 예를 들어 큐브 뷰에서는 특정 보고 요구 사항에 필요한 데이터 항목만으로 구성된 보기 목록(계층)을 제공할 수 있습니다. 자세한 내용은 참조 [큐브 뷰](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)합니다.  
  
 계층은 보안 수단이 아니라 보다 나은 사용자 환경을 제공하기 위한 도구입니다. 특정 계층에 대한 모든 보안은 기본 모델에서 상속됩니다. 계층에서 사용자에게 액세스 권한이 없는 모델 개체에 대한 액세스 권한을 부여할 수는 없습니다. 계층을 통해 모델의 개체에 대한 액세스를 제공하려면 먼저 model 데이터베이스에 대한 보안을 해결해야 합니다. 보안 역할을 사용하여 모델 메타데이터 및 데이터에 보안을 설정할 수 있습니다. 자세한 내용은 참조 [역할](../../analysis-services/tabular-models/roles-ssas-tabular.md)합니다.  
  
##  <a name="bkmk_define"></a> Defining hierarchies  
 다이어그램 뷰에서 모델 디자이너를 사용하여 계층을 만들고 관리합니다. 계층 만들기 및 관리는 데이터 뷰의 모델 디자이너에서는 지원되지 않습니다. 다이어그램 뷰에서 모델 디자이너를 보려면 **모델** 메뉴를 클릭하고 **모델 뷰**를 가리킨 다음 **다이어그램 뷰**를 클릭합니다.  
  
 계층을 만들려면 부모 수준으로 지정할 열을 마우스 오른쪽 단추로 클릭한 다음 **계층 만들기**를 클릭합니다. 단일 테이블에서 포함할 열을 다중 선택하거나, 나중에 열을 클릭한 후 부모 수준으로 끌어서 열을 자식 수준으로 추가할 수 있습니다. 여러 열을 선택하면 열이 카디널리티 기반 순서대로 자동으로 배치 됩니다. 열(수준)을 클릭한 후 다른 순서로 끌어 놓거나 상황에 맞는 메뉴에서 위로 및 아래로 탐색 컨트롤을 사용하여 순서를 변경할 수 있습니다. 열을 자식 수준으로 추가할 때 열을 부모 수준으로 끌어서 놓아 자동 검색을 사용할 수 있습니다.  
  
 열이 여러 계층에 나타날 수 있습니다. 계층은 측정값 또는 KPI 같은 비 열 개체를 포함할 수 없습니다. 계층은 단일 테이블 내에 있는 열만 기반으로 할 수 있습니다. 하나 이상의 열과 함께 측정값을 다중 선택하거나 여러 테이블의 열을 선택할 경우 상황에 맞는 메뉴에서 **계층 만들기** 명령이 비활성화됩니다. 다른 테이블의 열을 추가하려면 RELATED DAX 함수를 사용하여 관련 테이블의 열을 참조하는 계산 열을 추가합니다. 이 함수는 `=RELATED(TableName[ColumnName])`구문을 사용합니다. 자세한 내용은 RELATED 함수를 참조하십시오.  
  
 기본적으로 새 계층의 이름은 hierarchy1, hierarchy 2, 등으로 지정됩니다. 부모-자식 관계를 반영하여 클라이언트 사용자가 쉽게 식별할 수 있도록 계층 이름을 변경해야 합니다.  
  
 계층을 만든 후 Excel에서 분석 기능을 사용하여 효율성을 테스트할 수 있습니다. 자세한 내용은 참조 [Excel에서 분석](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)합니다.  
  
##  <a name="bkmk_related_tasks"></a> Related tasks  
  
|태스크|Description|  
|----------|-----------------|  
|[계층 만들기 및 관리](../../analysis-services/tabular-models/create-and-manage-hierarchies-ssas-tabular.md)|다이어그램 뷰에서 모델 디자이너를 사용하여 계층을 만들고 관리하는 방법에 대해 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 형식 모델 디자이너](../../analysis-services/tabular-models/tabular-model-designer-ssas.md)   
 [큐브 뷰](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
