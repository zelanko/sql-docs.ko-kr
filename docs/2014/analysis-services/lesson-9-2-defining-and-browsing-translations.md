---
title: 번역 정의 및 찾아보기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0e60be99-3768-499c-a22c-a4ec37e61887
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f9a254f685f83e97b14c78c7d6c4c21e2737b636
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "69493786"
---
# <a name="defining-and-browsing-translations"></a>번역 정의 및 찾아보기
  번역은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체의 이름을 특정 언어로 나타내는 것을 말합니다. 개체에는 측정값 그룹, 측정값, 차원, 특성, 계층, KPI, 동작 및 계산 멤버가 포함됩니다. 번역은 여러 언어를 지원할 수 있는 클라이언트 애플리케이션에 대한 서버 지원을 제공합니다. 클라이언트는 이러한 클라이언트를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스에 LCID(로캘 식별자)를 전달합니다. 그러면 해당 Analysis Services 인스턴스는 LCID를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체에 대한 메타데이터를 제공할 때 사용할 번역 집합을 결정합니다. 
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 개체에 해당 언어에 대한 번역이나 지정된 개체에 대한 번역이 없을 경우 기본 언어가 개체 메타데이터를 클라이언트에게 다시 반환하는 데 사용됩니다. 예를 들어 프랑스의 비즈니스 사용자가 프랑스어로 로캘이 설정된 워크스테이션에서 큐브에 액세스하는 경우 프랑스어 번역이 있다면 이 비즈니스 사용자에게는 멤버 캡션과 멤버 속성 값이 프랑스어로 표시됩니다. 그러나 독일의 비즈니스 사용자가 독일어로 로캘이 설정된 워크스테이션에서 동일한 큐브에 액세스하면 해당 캡션 이름과 멤버 속성 값이 독일어로 표시됩니다. 자세한 내용은 [차원 번역](multidimensional-models-olap-logical-dimension-objects/dimension-translations.md), [큐브 번역](multidimensional-models-olap-logical-cube-objects/cube-translations.md), [번역 &#40;Analysis Services&#41;](translations-analysis-services.md)를 참조 하세요.  
  
 이 항목의 태스크에서는 Date 차원의 제한된 차원 개체 집합 및 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브의 큐브 개체에 대한 메타데이터 번역을 정의합니다. 그런 후 이러한 차원 및 큐브 개체를 검색하여 메타데이터 번역을 검토합니다.  
  
## <a name="specifying-translations-for-the-date-dimension-metadata"></a>Date 차원 메타데이터에 대한 번역 지정  
  
1.  
  **Date** 차원에 대한 차원 디자이너를 연 다음 **번역** 탭을 클릭합니다.  
  
     각 차원 개체에 대한 메타데이터가 기본 언어로 표시됩니다. 
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브의 기본 언어는 영어입니다.  
  
2.  
  **번역** 탭의 도구 모음에서 **새 번역** 단추를 클릭합니다.  
  
     언어 목록이 **언어 선택** 대화 상자에 표시됩니다.  
  
3.  
  **스페인어(스페인)** 를 클릭한 후 **확인**을 클릭합니다.  
  
     번역할 메타데이터 개체를 스페인어로 번역하도록 정의할 수 있는 새 열이 나타납니다. 이 자습서에서는 진행 과정을 보여 주기 위해 몇 개의 개체만 번역해 보겠습니다.  
  
4.  
  **번역** 탭의 도구 모음에서 **새 번역** 단추를 클릭하고 **언어 선택** 대화 상자에서 **프랑스어(프랑스)** 를 클릭한 후 **확인**을 클릭합니다.  
  
     프랑스어 번역을 정의할 수 있는 또 다른 언어 열이 나타납니다.  
  
5.  **Date** 차원에 대 한 **Caption** 개체의 행에서 **스페인어 (스페인)** 번역 열과 `Temps` **프랑스어 (프랑스)** 번역 열에을 입력 `Fecha` 합니다.  
  
6.  **Month Name** 특성에 대 한 **Caption** 개체의 행에서 **스페인어 (스페인)** 번역 열을 입력 하 고 `Mois d'Année` **프랑스어 (프랑스)** 번역 열에을 입력 `Mes del Año` 합니다.  
  
     이러한 번역을 입력 하면 줄임표 (**...**)가 나타납니다. 이 줄임표를 클릭하면 특성 계층의 각 멤버에 대한 번역을 제공하는 기본 테이블의 열을 지정할 수 있습니다.  
  
7.  **Month Name** 특성의 **스페인어 (스페인)** 번역에 대 한 줄임표 (**...**)를 클릭 합니다.  
  
     
  **특성 데이터 번역** 대화 상자가 표시됩니다.  
  
8.  다음 그림에 표시된 것처럼 **번역 열** 목록에서 **SpanishMonthName**을 선택합니다.  
  
     ![특성 데이터 번역 대화 상자](../../2014/tutorials/media/l9-translations-4.gif "특성 데이터 번역 대화 상자")  
  
9. **확인**을 클릭 한 다음 **Month Name** 특성의 **프랑스어 (프랑스)** 번역에 대 한 줄임표 (**...**)를 클릭 합니다.  
  
10. 
  **번역 열** 목록에서 **FrenchMonthName**을 선택한 다음 **확인**을 클릭합니다.  
  
     이 절차의 단계는 차원 개체 및 멤버에 대한 메타데이터 번역을 정의하는 과정을 보여 줍니다.  
  
## <a name="specifying-translations-for-the-analysis-services-tutorial-cube-metadata"></a>Analysis Services Tutorial 큐브 메타데이터에 대한 번역 지정  
  
1.  
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브에 대한 큐브 디자이너로 전환한 후 **번역** 탭으로 전환합니다.  
  
     다음 그림에 표시된 것처럼 각 큐브 개체에 대한 메타데이터가 기본 언어로 표시됩니다. 
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브의 기본 언어는 영어입니다.  
  
     ![번역 탭의 기본 언어](../../2014/tutorials/media/l9-translations-5.gif "번역 탭의 기본 언어")  
  
2.  
  **번역** 탭의 도구 모음에서 **새 번역** 단추를 클릭합니다.  
  
     언어 목록이 **언어 선택** 대화 상자에 표시됩니다.  
  
3.  
  **스페인어(스페인)** 를 선택한 후 **확인**을 클릭합니다.  
  
     번역할 메타데이터 개체를 스페인어로 번역하도록 정의할 수 있는 새 열이 나타납니다. 이 자습서에서는 진행 과정을 보여 주기 위해 몇 개의 개체만 번역해 보겠습니다.  
  
4.  
  **번역** 탭의 도구 모음에서 **새 번역** 단추를 클릭하고 **언어 선택** 대화 상자에서 **프랑스어(프랑스)** 를 선택한 후 **확인**을 클릭합니다.  
  
     프랑스어 번역을 정의할 수 있는 또 다른 언어 열이 나타납니다.  
  
5.  **Date** 차원에 대 한 **Caption** 개체의 행에서 **스페인어 (스페인)** 번역 열과 `Temps` **프랑스어 (프랑스)** 번역 열에을 입력 `Fecha` 합니다.  
  
6.  **Internet Sales** 측정값 그룹에 대 한 **Caption** 개체의 행에서 **스페인어 (스페인)** 번역 열과 `Ventes D'Internet` **프랑스어 (프랑스)** 번역 열을 입력 `Ventas del lnternet` 합니다.  
  
7.  Internet Sales-Sales Amount 측정값에 대 한 **Caption** 개체의 행에서 **스페인어 (스페인)** 번역 열과 `Quantité de Ventes d'Internet` **프랑스어 (프랑스)** 번역 열을 입력 `Cantidad de las Ventas del Internet` 합니다.  
  
     이 절차의 단계는 큐브 개체에 대한 메타데이터 번역을 정의하는 과정을 보여 줍니다.  
  
## <a name="browsing-the-cube-by-using-translations"></a>번역을 사용하여 큐브 찾아보기  
  
1.  
  **빌드** 메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
2.  배포가 성공적으로 완료되면 **브라우저** 탭으로 전환한 다음 **다시 연결**을 클릭합니다.  
  
3.  
  **데이터** 창에서 모든 계층 및 측정값을 제거하고 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 큐브 뷰 **목록에서** Tutorial을 선택합니다.  
  
4.  메타데이터 창에서 **Measures** 를 확장한 후 **Internet Sales**를 확장합니다.  
  
     이 측정값 그룹에 **Internet Sales-Sales Amount** 측정값이 영어로 나타납니다.  
  
5.  도구 모음의 **언어** 목록에서 **스페인어(스페인)** 를 선택합니다.  
  
     메타데이터 창의 항목이 다시 채워집니다. 메타데이터 창의 항목이 다시 채워지면 인터넷 판매 표시 폴더에 Internet Sales-Sales Amount 측정값이 더 이상 나타나지 않습니다. 대신, 다음 이미지에 표시 된 것 처럼 이라는 `Ventas del lnternet`새 표시 폴더에 스페인어로 표시 됩니다.  
  
     ![다시 채워진 메타데이터 창](../../2014/tutorials/media/l9-translations-6.gif "다시 채워진 메타데이터 창")  
  
6.  메타 데이터 창에서를 마우스 오른쪽 단추로 `Cantidad de las Ventas del Internet` 클릭 하 고 **쿼리에 추가를**선택 합니다.  
  
7.  메타 데이터 `Fecha`창에서 **Fecha**를 확장 하 고 **Fecha**를 마우스 오른쪽 단추로 클릭 한 다음 **필터에 추가**를 선택 합니다.  
  
8.  
  **필터** 창에서 **CY 2007** 을 필터 식으로 선택합니다.  
  
9. 메타데이터 창에서 **Mes del Ano** 를 마우스 오른쪽 단추로 클릭하고 **쿼리에 추가**를 선택합니다.  
  
     다음 그림에 표시된 것처럼 월 이름이 스페인어로 표시됩니다.  
  
     ![데이터 창에 스페인어로 표시된 월 이름](../../2014/tutorials/media/l9-translations-7.gif "데이터 창에 스페인어로 표시된 월 이름")  
  
10. 도구 모음의 **언어** 목록에서 **프랑스어(프랑스)** 를 선택합니다.  
  
     이제 월 이름과 측정값 이름이 프랑스어로 표시됩니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [10단원: 관리자 역할 정의](lesson-10-defining-administrative-roles.md)  
  
## <a name="see-also"></a>참고 항목  
 [차원 번역](multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [큐브 번역](multidimensional-models-olap-logical-cube-objects/cube-translations.md)   
 [번역 &#40;Analysis Services&#41;](translations-analysis-services.md)  
  
  
