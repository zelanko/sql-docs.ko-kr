---
title: 데이터 원본 뷰 (Analysis Services)에서 논리적 관계 정의 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- adding relationships
- relationships [Analysis Services], data source views
- data source views [Analysis Services], relationships
ms.assetid: a20d6dae-e769-4131-8a59-7ef56f174220
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6ce3e78493e9e8e3f24cc7a146b2ad4afb9bfebc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36183724"
---
# <a name="define-logical-relationships-in-a-data-source-view-analysis-services"></a>데이터 원본 뷰에서 논리적 관계 정의(Analysis Services)
  데이터 원본 뷰 마법사와 데이터 원본 뷰 디자이너에서는 기본 데이터베이스 관계 또는 지정한 이름 일치 조건을 기반으로 데이터 원본 뷰(DSV)에 추가된 테이블 간의 관계를 자동으로 정의합니다.  
  
 여러 데이터 원본의 데이터를 사용하여 작업할 경우 자동으로 정의되는 관계를 보완하기 위해 DSV에서 수동으로 논리적 관계를 정의해야 할 수도 있습니다. 관계는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 팩트 테이블과 차원 테이블을 식별하고, 기본 데이터 원본에서 데이터 및 메타데이터를 검색할 쿼리를 작성하며, 고급 비즈니스 인텔리전스 기능을 사용하는 데 필요합니다.  
  
 데이터 원본 뷰 디자이너에서는 다음과 같은 유형의 관계를 정의할 수 있습니다.  
  
-   같은 데이터 원본의 서로 다른 테이블 간 관계  
  
-   부모-자식 관계처럼 테이블과 테이블 자신 간 관계  
  
-   서로 다른 데이터 원본의 테이블 간 관계  
  
> [!NOTE]  
>  데이터 원본 뷰에 정의된 관계는 논리적이므로 기본 DSV에 정의된 실제 관계에 반영되지 않을 수 있습니다. 데이터 원본 뷰 디자이너에서 기본 데이터 원본에 없는 관계를 만들고 기본 데이터 원본의 기존 외래 키 관계에서 데이터 원본 뷰 디자이너를 사용하여 만든 관계를 제거할 수 있습니다.  
  
 관계의 방향이 지정됩니다. 원본 열의 모든 값은 대상 열에 해당 값이 있습니다. **다이어그램** 창에 표시되는 다이어그램처럼 데이터 원본 뷰 다이어그램에서 두 테이블 사이의 선에 있는 화살표는 관계의 방향을 나타냅니다.  
  
 이 항목은 다음과 같은 섹션으로 구성됩니다.  
  
 [테이블, 명명된 쿼리 또는 뷰 간의 관계를 추가하려면](#bkmk_addRel)  
  
 [다이어그램 창에서 관계를 보거나 수정하려면](#bkmk_diagrampane)  
  
 [테이블 창에서 관계를 보거나 수정하려면](#bkmk_tablespane)  
  
##  <a name="bkmk_addRel"></a> 테이블, 명명된 쿼리 또는 뷰 간의 관계를 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 논리적 관계를 추가할 데이터 원본 뷰가 포함된 프로젝트를 열거나 데이터베이스에 연결합니다.  
  
2.  솔루션 탐색기에서 **데이터 원본 뷰** 폴더를 확장하고 데이터 원본 뷰를 두 번 클릭하여 **데이터 원본 뷰 디자이너**에서 엽니다.  
  
3.  **테이블** 창에서 관계를 추가할 테이블, 명명된 쿼리 또는 뷰를 마우스 오른쪽 단추로 클릭한 다음 **새 관계**를 클릭합니다.  
  
    > [!NOTE]  
    >  테이블, 뷰 또는 명명된 쿼리를 찾으려면 **데이터 원본 뷰** 메뉴를 클릭하거나 **테이블** 또는 **다이어그램** 창의 열린 영역을 마우스 오른쪽 단추로 클릭하여 **테이블 찾기** 옵션을 사용할 수 있습니다.  
  
4.  **관계 지정** 대화 상자에서 다음 작업을 수행합니다.  
  
    1.  **원본(외래 키) 테이블** 목록에서 해당 테이블, 명명된 쿼리 또는 뷰를 선택합니다.  
  
    2.  **대상(기본 키) 테이블** 목록에서 해당 테이블, 명명된 쿼리 또는 뷰를 선택합니다.  
  
    3.  **원본 열** 및 **대상 열** 목록에서 열을 선택하여 두 테이블 간의 관계를 만듭니다.  
  
         [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 기본 테이블, 뷰 또는 명명된 쿼리의 데이터를 샘플링하여 잘못된 방향(외래 키에서 기본 키로의 방향이 아닌 기본 키에서 외래 키로의 방향)으로 관계가 정의된 것을 감지하면 순서를 반대로 바꾸라는 메시지가 표시됩니다. 신속하게 순서를 반대로 바꾸려면 **반대로**를 클릭합니다.  
  
         [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 선택한 열에 대한 관계가 이미 있음을 감지하면 메시지가 표시됩니다. 중복 관계는 정의할 수 없습니다.  
  
    4.  필요에 따라 **설명** 입력란에 관계에 대한 설명을 입력합니다.  
  
##  <a name="bkmk_diagrampane"></a> 다이어그램 창에서 관계를 보거나 수정하려면  
  
-   **데이터 원본 뷰 디자이너** 의 **다이어그램**창에서 보려는 관계를 마우스 오른쪽 단추로 클릭한 다음 **관계 편집** 을 클릭하거나 간단하게 관계 화살표를 두 번 클릭합니다.  **관계 편집** 대화 상자를 사용하여 관계를 수정합니다.  
  
##  <a name="bkmk_tablespane"></a> 테이블 창에서 관계를 보거나 수정하려면  
  
1.  **데이터 원본 뷰 디자이너** 의 **테이블**창에서 관계를 보거나 수정하려는 테이블, 뷰 또는 명명된 쿼리를 찾아 확장합니다.  
  
2.  **관계** 폴더를 확장합니다.  선택한 테이블, 뷰 또는 명명된 쿼리와 다른 테이블, 뷰 및 명명된 쿼리 간의 관계가 표시되고 관계 열이 나열됩니다.  
  
3.  수정하려는 관계를 마우스 오른쪽 단추로 클릭한 다음 **관계 편집**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [다차원 모델의 데이터 원본 뷰](data-source-views-in-multidimensional-models.md)  
  
  