---
title: "큐브 정의 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 8aa4ac2d-857f-4048-baa0-0f314e207cf6
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 16cc78325be6d6c2759d630740f54045b02f6bb3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-2-2---defining-a-cube"></a>단원 2-2-큐브를 정의 합니다.
큐브 마법사를 통해 큐브에 대한 측정값 그룹과 차원을 정의할 수 있습니다. 다음 태스크에서는 큐브 마법사를 사용하여 큐브를 만듭니다.  
  
### <a name="to-define-a-cube-and-its-properties"></a>큐브 및 해당 속성을 정의하려면  
  
1.  솔루션 탐색기에서 **큐브**를 마우스 오른쪽 단추로 클릭한 다음 **새 큐브**를 클릭합니다. 큐브 마법사가 나타납니다.  
  
2.  **큐브 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  **생성 방법 선택** 페이지에서 **기존 테이블 사용** 옵션이 선택되어 있는지 확인하고 **다음**을 클릭합니다.  
  
4.  **측정값 그룹 테이블 선택** 페이지에서 **Adventure Works DW 2012** 데이터 원본 뷰가 선택되어 있는지 확인합니다.  
  
5.  **제안** 을 클릭하여 측정값 그룹을 만드는 데 사용할 테이블을 큐브 마법사가 제안하도록 할 수 있습니다.  
  
    마법사는 테이블을 검사한 후 **InternetSales** 를 측정값 그룹 테이블로 제안합니다. 팩트 테이블이라고도 하는 측정값 그룹 테이블에는 판매된 단위의 수와 같이 사용자가 관심을 가지는 측정값이 포함됩니다.  
  
6.  **다음**을 클릭합니다.  
  
7.  **측정값 선택** 페이지에서 **Internet Sales** 측정값 그룹에서 선택한 측정값을 검토한 후 다음과 같은 측정값 확인란의 선택을 취소합니다.  
  
    -   **Promotion Key**  
  
    -   **Currency Key**  
  
    -   **Sales Territory Key**  
  
    -   **Revision Number**  
  
    기본적으로 마법사에서는 차원에 연결되지 않은 팩트 테이블의 모든 숫자 열을 측정값으로 선택합니다. 그러나 이러한 4개의 열은 실제 측정값이 아닙니다. 처음 3개 열은 이 큐브의 처음 버전에서 사용되지 않은 차원 테이블과 팩트 테이블을 연결하는 키 값입니다.  
  
8.  **다음**을 클릭합니다.  
  
9. **기존 차원 선택** 페이지에서 앞서 만든 **Date** 차원을 선택한 후 **다음**을 클릭합니다.  
  
10. **새 차원 선택** 페이지에서 새로 만들 차원을 선택합니다. 이렇게 하려면 **Customer**, **Geography**및 **Product** 확인란을 선택하고 **InternetSales** 확인란의 선택을 취소합니다.  
  
11. **다음**을 클릭합니다.  
  
12. **마법사 완료** 페이지에서 큐브 이름을 **Analysis Services Tutorial**로 변경합니다. 미리 보기 창에서 **InternetSales** 측정값 그룹 및 이 그룹의 측정값을 볼 수 있습니다. **Date**, **Customer** 및 **Product** 차원도 볼 수 있습니다.  
  
13. **마침** 을 클릭하여 마법사를 완료합니다.  
  
    솔루션 탐색기의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 프로젝트에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브는 **큐브** 폴더에 나타나고 Customer 및 Product 데이터베이스 차원은 **차원** 폴더에 나타납니다. 또한 개발 환경에서 가장 중요한 큐브 구조 탭에는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브가 표시됩니다.  
  
14. 큐브 구조 탭의 도구 모음에서 큐브의 차원 및 팩트 테이블을 보다 쉽게 볼 수 있도록 **확대/축소** 수준을 50%로 변경합니다. 팩트 테이블은 노란색, 차원 테이블은 파란색으로 표시됩니다.  
  
15. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[차원에 특성 추가](../analysis-services/lesson-2-3-adding-attributes-to-dimensions.md)  
  
## <a name="see-also"></a>참고 항목  
[다차원 모델의 큐브](../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
[다차원 모델의 차원](../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
  
