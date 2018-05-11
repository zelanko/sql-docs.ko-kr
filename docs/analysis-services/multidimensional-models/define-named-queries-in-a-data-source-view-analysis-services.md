---
title: 데이터 원본 뷰 (Analysis Services)에서 명명 된 쿼리 정의 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: da72dd5023307a5207b9082b8adf8234d77aeac0
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="define-named-queries-in-a-data-source-view-analysis-services"></a>데이터 원본 뷰에서 명명된 쿼리 정의(Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  명명된 쿼리는 테이블로 표현된 SQL 식입니다. 명명된 쿼리에 SQL 식을 지정하여 하나 이상의 데이터 원본에 있는 하나 이상의 테이블에서 반환된 행 및 열을 선택할 수 있습니다. 식을 기반으로 한다는 점을 제외하면 명명된 쿼리는 관계 및 행이 있는 데이터 원본 뷰(DSV)의 다른 테이블과 같습니다.  
  
 명명된 쿼리를 사용하면 기본 데이터 원본을 수정하지 않고 DSV에 있는 기존 테이블의 관계형 스키마를 확장할 수 있습니다. 예를 들어 일련의 명명된 쿼리를 사용하여 복잡한 차원 테이블을 데이터베이스 차원에서 사용할 수 있도록 더 작고 간단한 차원 테이블로 분할할 수 있습니다. 명명된 쿼리를 사용하여 하나 이상의 데이터 원본의 여러 데이터베이스 테이블을 하나의 데이터 원본 뷰 테이블로 조인할 수도 있습니다.  
  
## <a name="creating-a-named-query"></a>명명된 쿼리 만들기  
  
> [!NOTE]  
>  명명된 계산을 명명된 쿼리에 추가할 수 없으며 명명된 계산이 포함된 테이블을 명명된 쿼리의 기반으로 할 수 없습니다.  
  
 명명된 쿼리를 만들 때는 테이블의 열과 데이터를 반환하는 SQL 쿼리 및 쿼리의 이름을 지정하고 필요에 따라 명명된 쿼리에 대한 설명을 지정합니다. SQL 식은 데이터 원본 뷰에서 다른 테이블을 참조할 수 있습니다. 명명된 쿼리를 정의하면 명명된 쿼리의 SQL 쿼리가 데이터 원본의 공급자에게 전송되어 유효성이 전체적으로 검사됩니다. 공급자가 SQL 쿼리에서 오류를 찾을 수 없으면 해당 열이 테이블에 추가됩니다.  
  
 SQL 쿼리에서 참조되는 테이블 및 열은 한정되어서는 안 되며 한정할 경우 테이블 이름으로만 한정해야 합니다. 예를 들어 테이블의 SaleAmount 열을 참조하려면 `SaleAmount` 나 `Sales.SaleAmount` 는 유효하지만 `dbo.Sales.SaleAmount` 는 오류를 생성합니다.  
  
 **참고**   [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 데이터 원본을 쿼리하는 명명된 쿼리를 정의할 때 상관 하위 쿼리 및 GROUP BY 절을 포함하는 명명된 쿼리는 실패합니다. 자세한 내용은 [기술 문서에서](http://support.microsoft.com/kb/274729) 버그: 상관 하위 쿼리 및 GROUP BY를 포함하는 SELECT 문의 내부 오류(BUG: Internal Error with SELECT Statement Containing Correlated Subquery and GROUP BY) [!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 참조하십시오.  
  
## <a name="add-or-edit-a-named-query"></a>명명된 쿼리 추가 또는 편집  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 명명된 쿼리를 추가할 데이터 원본 뷰가 포함된 프로젝트를 열거나 데이터베이스에 연결합니다.  
  
2.  솔루션 탐색기에서 **데이터 원본 뷰** 폴더를 확장한 다음 해당 데이터 원본 뷰를 두 번 클릭합니다.  
  
3.  **테이블** 또는 **다이어그램** 창에서 열린 영역을 마우스 오른쪽 단추로 클릭한 다음 **새 명명된 쿼리**를 클릭합니다.  
  
4.  **명명된 쿼리 만들기** 대화 상자에서 다음을 수행하십시오.  
  
    1.  **이름** 입력란에 쿼리 이름을 입력합니다.  
  
    2.  필요에 따라 **설명** 입력란에 쿼리에 대한 설명을 입력합니다.  
  
    3.  **데이터 원본** 목록 상자에서 명명된 쿼리가 실행될 데이터 원본을 선택합니다.  
  
    4.  아래쪽 창에 쿼리를 입력하거나 그래픽 쿼리 작성 도구를 사용하여 쿼리를 만듭니다.  
  
    > [!NOTE]  
    >  쿼리 작성 UI(사용자 인터페이스)는 데이터 원본에 따라 달라집니다. 그래픽 UI가 아닌 텍스트 기반의 일반 UI가 표시될 수 있습니다. 이렇게 다른 UI를 사용해도 같은 작업을 수행할 수 있지만 수행 방식은 서로 다릅니다. 자세한 내용은 [명명된 쿼리 만들기 또는 편집 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](http://msdn.microsoft.com/library/8e192ad6-a0b1-4e21-bb3f-087c93e62941)를 참조하세요.  
  
5.  **확인**을 클릭합니다. 테이블이 명명된 쿼리로 바뀌었음을 나타내기 위해 겹치는 두 개의 테이블을 표시하는 아이콘이 테이블 머리글에 나타납니다.  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델의 데이터 원본 뷰](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [데이터 원본 뷰 & #40; 명명 된 계산을 정의 합니다. Analysis Services & #41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
