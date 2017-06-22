---
title: "(보고서 작성기 및 SSRS) 차트에 3D 효과 추가 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab9625d8-6557-4a4d-8123-eefa7c066ff5
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 7170699a3f0cbb26dd2376a8805978fe792223f0
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="chart-effects---add-3d-effects-report-builder"></a>차트-효과 (보고서 작성기) 3D 효과 추가
  3D(3차원) 효과를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 페이지가 매겨진 보고서의 차트에 깊이를 더하고 시각적 효과를 강화할 수 있습니다. 예를 들어 쪼개진 원형 차트에서 특정 조각을 강조하려는 경우 차트를 돌려 원근감을 변경함으로써 해당 조각이 가장 먼저 보이도록 할 수 있습니다. 차트에 3D 효과를 적용할 경우 모든 그라데이션 색과 해칭 스타일이 해제됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-apply-3d-effects-to-a-range-area-line-scatter-or-polar-chart"></a>범위형, 영역형, 꺾은선형, 분산형 또는 극좌표형 차트에 3D 효과를 적용하려면  
  
1.  차트 영역의 아무 위치나 마우스 오른쪽 단추로 클릭하고 **3D 효과**를 선택합니다. **차트 영역 속성** 대화 상자가 나타납니다.  
  
2.  **3D 옵션**에서 **3D 사용** 옵션을 선택합니다.  
  
3.  (옵션) **3D 옵션**에서 3D 각도 및 장면 옵션과 관련된 다양한 속성을 설정할 수 있습니다. 이러한 속성에 대한 자세한 내용은 [차트의 3D, 빗면 및 기타 효과&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-effects-3d-bevel-and-other-report-builder.md)를 선택합니다.  
  
4.  **확인**을 클릭합니다.  
  
## <a name="to-apply-3d-effects-to-a-funnel-chart"></a>깔때기형 차트에 3D 효과를 적용하려면  
  
1.  차트 영역의 아무 위치나 마우스 오른쪽 단추로 클릭하고 **3D 효과**를 선택합니다. **차트 영역 속성** 대화 상자가 나타납니다.  
  
2.  **3D 옵션**에서 **3D 사용** 옵션을 선택합니다. **확인**을 클릭합니다.  
  
3.  (옵션) 깔때기형 차트의 시각적 모양을 사용자 지정하려면 속성 창으로 이동하여 깔때기형 차트에 관련된 속성을 변경합니다.  
  
    1.  속성 창을 엽니다.  
  
    2.  디자인 화면에서 깔때기형 차트의 아무 곳이나 클릭합니다. 깔때기형 차트의 계열에 대한 속성이 속성 창에 표시됩니다.  
  
    3.  **일반** 섹션에서 **CustomAttributes** 노드를 확장합니다.  
  
    4.  **Funnel3DDrawingStyle** 속성에서 깔때기형 차트를 원형으로 표시할지 사각형으로 표시할지 선택합니다.  
  
    5.  **Funnel3DRotationAngle** 속성에 대해 -10에서 10 사이의 값을 설정합니다. 이 값은 3D 깔때기형 차트에 표시될 기울기 정도를 결정합니다.  
  
## <a name="to-apply-3d-effects-to-a-pie-chart"></a>원형 차트에 3D 효과를 적용하려면  
  
1.  차트 영역의 아무 위치나 마우스 오른쪽 단추로 클릭하고 3D 효과를 선택합니다. **차트 영역 속성** 대화 상자가 나타납니다.  
  
2.  **3D 옵션**에서 **3D 사용** 옵션을 선택합니다. **확인**을 클릭합니다.  
  
3.  (옵션) **회전**에 원형 차트의 수평 회전을 나타내는 정수 값을 입력합니다.  
  
4.  (옵션) **기울기**에 원형 차트의 수직 기울기 회전을 나타내는 정수 값을 입력합니다.  
  
5.  **확인**을 클릭합니다.  
  
## <a name="to-apply-3d-effects-to-a-bar-or-column-chart"></a>가로 막대형 또는 세로 막대형 차트에 3D 효과를 적용하려면  
  
1.  차트 영역의 아무 위치나 마우스 오른쪽 단추로 클릭하고 **3D 효과**를 선택합니다. **차트 영역 속성** 대화 상자가 나타납니다.  
  
2.  **3D 사용** 옵션을 선택합니다. **확인**을 클릭합니다.  
  
3.  (옵션) **계열 클러스터링 사용** 옵션을 선택합니다. 차트에 여러 개의 가로 막대형 또는 세로 막대형 차트 계열이 포함되어 있는 경우 이 옵션을 선택하면 계열이 클러스터형으로 표시됩니다. 기본적으로 여러 개의 가로 막대형 또는 세로 막대형 계열이 나란히 표시됩니다.  
  
4.  **확인**을 클릭합니다.  
  
5.  (옵션) 가로 막대형 또는 세로 막대형 차트에 원통형 효과를 추가하려면 다음 단계를 수행합니다.  
  
    1.  속성 창을 엽니다.  
  
    2.  디자인 화면에서 계열의 가로 막대 중 아무 것이나 클릭합니다. 계열의 속성이 속성 창에 표시됩니다.  
  
    3.  **일반** 섹션에서 **CustomAttributes** 노드를 확장합니다.  
  
    4.  **DrawingStyle** 속성에서 **Cylinder** 값을 지정합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [차트의 3D, 빗면 및 기타 효과&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-effects-3d-bevel-and-other-report-builder.md)   
 [차트 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
