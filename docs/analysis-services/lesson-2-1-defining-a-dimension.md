---
title: 차원을 정의 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 38185df9928286acf184fbad21fd75839856d017
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="lesson-2-1---defining-a-dimension"></a>단원 2-1-차원 정의
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

다음 태스크에서는 차원 마법사를 사용하여 Date 차원을 구축합니다.  
  
> [!NOTE]  
> 이 단원을 수행하려면 1단원의 모든 절차를 완료해야 합니다.  
  
### <a name="to-define-a-dimension"></a>차원을 정의하려면  
  
1.  Microsoft Visual Studio의 오른쪽에 있는 솔루션 탐색기에서 **차원**을 마우스 오른쪽 단추로 클릭한 다음 **새 차원**을 클릭합니다. 차원 마법사가 표시됩니다.  
  
2.  **차원 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  **생성 방법 선택** 페이지에서 **기존 테이블 사용** 옵션이 선택되어 있는지 확인하고 **다음**을 클릭합니다.  
  
4.  **원본 정보 지정** 페이지에서 **Adventure Works DW 2012** 데이터 원본 뷰가 선택되어 있는지 확인합니다.  
  
5.  **주 테이블** 목록에서 **Date**를 선택합니다.  
  
6.  **다음**을 클릭합니다.  
  
7.  **차원 특성 선택** 페이지에서 다음 특성 옆에 있는 확인란을 선택합니다.  
  
    -   **Date Key**  
  
    -   **Full Date Alternate Key**  
  
    -   **English Month Name**  
  
    -   **Calendar Quarter**  
  
    -   **Calendar Year**  
  
    -   **Calendar Semester**  
  
8.  **Full Date Alternate Key** 특성의 **특성 유형** 열 설정을 **일반** 에서 **날짜**로 변경합니다. 이렇게 하려면 **특성 유형** 열에서 **일반** 을 클릭합니다. 그런 다음 화살표를 클릭하여 옵션을 확장합니다. **날짜** > **달력** > **날짜**를 클릭합니다. **확인**을 클릭합니다. 이 단계를 반복하여 특성의 특성 유형을 다음과 같이 변경합니다.  
  
    -   **English Month Name** to **Month**  
  
    -   **Calendar Quarter** to **Quarter**  
  
    -   **Calendar Year** to **Year**  
  
    -   **Calendar Semester** to **Half Year**  
  
9. **다음**을 클릭합니다.  
  
10. **마법사 완료** 페이지의 미리 보기 창에서 **Date** 차원 및 해당 특성을 볼 수 있습니다.  
  
11. **마침** 을 클릭하여 마법사를 완료합니다.  
  
    솔루션 탐색기의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 프로젝트에서 Date 차원은 **차원** 폴더에 표시됩니다. 차원 디자이너는 개별 환경의 가운데에 Date 차원을 표시합니다.  
  
12. **파일** 메뉴에서 **모두 저장**을 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[큐브 정의](../analysis-services/lesson-2-2-defining-a-cube.md)  
  
## <a name="see-also"></a>관련 항목:  
[다차원 모델의 차원](../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)  
[기존 테이블을 사용하여 차원 만들기](../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)  
[차원 마법사를 사용하여 차원 만들기](../analysis-services/multidimensional-models/create-a-dimension-using-the-dimension-wizard.md)  
  
  
  
