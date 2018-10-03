---
title: 큐브 및 차원 속성 검토 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: dda922b8-6d75-4662-b09e-8a317c6a1c70
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b4db6133a486e77369630dc717fab02b3be7f8e2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196273"
---
# <a name="reviewing-cube-and-dimension-properties"></a>큐브 및 차원 속성 검토
  큐브를 정의한 후에는 큐브 디자이너를 사용하여 결과를 검토할 수 있습니다. 다음 태스크에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 프로젝트의 큐브 구조를 검토합니다.  
  
### <a name="to-review-cube-and-dimension-properties-in-cube-designer"></a>큐브 디자이너에서 큐브 및 차원 속성을 검토하려면  
  
1.  큐브 디자이너를 열려면 솔루션 탐색기의 **큐브** 노드에서 **Analysis Services Tutorial** 큐브를 두 번 클릭합니다.  
  
2.  큐브 디자이너에 있는 **큐브 구조** 탭의 **측정값** 창에서 **Internet Sales** 측정값 그룹을 확장하여 정의된 측정값을 확인합니다.  
  
     해당 측정값을 원하는 순서로 끌어서 정렬 순서를 바꿀 수 있습니다. 순서를 만들면 이 순서는 특정 클라이언트 응용 프로그램에서 이러한 측정값을 정렬하는 방법에 영향을 미칩니다. 측정값 그룹과 여기에 포함된 각 측정값은 속성을 갖고 있으며 이러한 속성은 속성 창에서 편집할 수 있습니다.  
  
3.  큐브 디자이너에 있는 **큐브 구조** 탭의 **차원** 창에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브의 큐브 차원을 검토합니다.  
  
     솔루션 탐색기에서 볼 수 있듯이 데이터베이스 수준에서는 차원이 3개만 만들어졌지만 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에는 5개의 큐브 차원이 있습니다. Date 데이터베이스 차원이 팩트 테이블의 다른 날짜 관련 팩트를 기반으로 세 개의 개별 날짜 관련 큐브 차원에 대한 기초로 사용되므로 큐브에는 데이터베이스보다 차원이 많이 있습니다. 이러한 날짜 관련 차원을 *롤플레잉 차원*이라고 합니다. 세 개의 날짜 관련 큐브 차원을 사용하여 각 제품 판매와 관련된 세 개의 개별 팩트 즉, 제품 주문 날짜, 주문 이행 기한 및 주문 출하 날짜에 따라 큐브의 차원을 지정할 수 있습니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 여러 큐브 차원에 단일 데이터베이스 차원을 다시 사용하여 간단하게 차원을 관리하고, 디스크 공간을 덜 사용하고, 전체 처리 시간을 줄일 수 있습니다.  
  
4.  **큐브 구조** 탭의 **차원** 창에서 **Customer**를 확장한 후 **Customer 편집** 을 클릭하여 차원 디자이너에서 이 차원을 엽니다.  
  
     차원 디자이너에는 **차원 구조**, **특성 관계**, **번역**및 **브라우저**탭이 있습니다. **차원 구조** 탭에는 **특성**, **계층**및 **데이터 원본 뷰**창이 있습니다. 차원에 포함된 특성은 **특성** 창에 나타납니다. 자세한 내용은 [차원 특성 속성 참조](multidimensional-models/dimension-attribute-properties-reference.md)를 [사용자 정의 계층 만들기](multidimensional-models/user-defined-hierarchies-create.md)합니다.  
  
5.  큐브 디자이너로 전환하려면 솔루션 탐색기에서 **큐브** 노드의 **Analysis Services Tutorial** 큐브를 마우스 오른쪽 단추로 클릭하고 **디자이너 보기**를 클릭합니다.  
  
6.  큐브 디자이너에서 **차원 용도** 탭을 클릭합니다.  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브의 이 뷰에 Internet Sales 측정값 그룹에서 사용하는 큐브 차원이 나타납니다. 또한 각 차원과 해당 차원이 사용되는 각 측정값 그룹 간의 관계 유형도 정의할 수 있습니다.  
  
7.  **파티션** 탭을 클릭합니다.  
  
     큐브 마법사에서 집계가 없는 다차원 온라인 분석 처리 저장소 모드를 사용하여 큐브에 대해 단일 파티션을 정의합니다. MOLAP을 사용하면 최대 성능을 위해 모든 리프 수준 데이터와 모든 집계가 해당 큐브 내에 저장됩니다. 집계는 질문이 이루어지기 전에 응답을 준비 상태로 만들어 쿼리 응답 시간을 빠르게 하기 위해 미리 계산된 데이터 요약입니다. **파티션** 탭에서 추가로 파티션, 저장소 설정 및 쓰기 저장(writeback) 설정을 정의할 수 있습니다. 자세한 내용은 [파티션&#40;Analysis Services - 다차원 데이터&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md), [집계 및 집계 디자인](multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)을 참조하세요.  
  
8.  **브라우저** 탭을 클릭합니다.  
  
     큐브를 아직 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 인스턴스에 배포하지 않았기 때문에 큐브를 검색할 수 없습니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 프로젝트에서 큐브를 정의했으므로 이제 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 인스턴스에 배포할 수 있습니다. 큐브를 배포 및 처리할 때는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 의 인스턴스에서 정의된 개체를 만들고 기본 데이터 원본에서 가져온 데이터로 이 개체를 채웁니다.  
  
9. 솔루션 탐색기의 **큐브** 노드에서 **Analysis Services Tutorial** 을 마우스 오른쪽 단추로 클릭한 다음 **코드 보기**를 클릭합니다. 기다려야 할 수도 있습니다.  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial.cube [XML] **[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 탭에** Tutorial 큐브에 대한 XML 코드가 표시됩니다. 이 코드는 배포하는 동안 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 인스턴스에서 큐브를 만드는 데 사용되는 실제 코드입니다. 자세한 내용은 [Analysis Services 프로젝트에 대한 XML 보기&#40;SSDT&#41;](multidimensional-models/view-the-xml-for-an-analysis-services-project-ssdt.md)를 참조하세요.  
  
10. XML 코드 탭을 닫습니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [Analysis Services 프로젝트 배포](lesson-2-5-deploying-an-analysis-services-project.md)  
  
## <a name="see-also"></a>관련 항목  
 [차원 디자이너에서 차원 데이터 찾아보기](multidimensional-models/database-dimensions-browse-dimension-data-in-dimension-designer.md)  
  
  
