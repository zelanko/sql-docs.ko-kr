---
title: 여러 셰이프 차트에 일관된 색 지정-보고서 작성기-SSRS | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d52f68e9-2ba7-4bff-9053-4089e5164ab4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d9e7b846d17fd6ad86edc45ff7dd4251c098ae1a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65578453"
---
# <a name="specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs"></a>여러 셰이프 차트에 일관된 색 지정(보고서 작성기 및 SSRS)
  페이지를 매긴 보고서의 셰이프가 아닌 차트에서 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 는 차트 내 계열의 인덱스를 기반으로 색상표에서 새로운 색을 선택합니다. 예를 들어 차트의 첫 번째 계열은 색상표의 첫 번째 색에 매핑됩니다. 그러나 셰이프 차트의 경우 다르게 동작합니다. 셰이프 차트에서 색상표의 각 색은 데이터 세트의 데이터 요소와 매핑됩니다. 즉 데이터 요소 1은 색상표의 첫 번째 색과 매핑되며 데이터 요소 2는 두 번째 색 등의 형태로 매핑됩니다.  
  
 데이터 요소에 값이 없는 경우 셰이프 차트에 표시되지 않습니다. 즉, 데이터 요소에 색이 지정되는 과정이 생략됩니다. 예를 들어 요소 2에 값 0이 있는 경우 요소 1은 색상표의 첫 번째 색에 매핑되고 요소 3은 색상표의 두 번째 색에 매핑됩니다. 이러한 방법을 사용하면 원형 차트의 데이터 세트에서 비어 있는 요소에 대해 불필요하게 색상표 색을 사용하지 않아도 되므로 비어 있는 요소를 그리지 않아도 되는 경우 유용합니다.  
  
 그러나 여러 개의 원형 차트가 보고서에 표시되는 경우 동일한 범주 그룹에 있는 데이터 요소가 다른 색으로 표시될 수 있다는 단점이 있습니다. 이 문제를 해결하려면 개별 데이터 값 대신 범주 그룹에 매핑되는 색을 각각 정의해야 합니다. 이 방법은 셰이프 차트가 테이블 또는 행렬의 스파크라인인지 아니면 보고서 자체의 셰이프 차트인지에 따라 달라집니다.  
  
 범례는 계열과 연결되므로 계열에 대해 지정한 색이 범례에 자동으로 표시됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-specify-consistent-colors-across-multiple-sparkline-shape-charts-in-a-table-or-matrix"></a>테이블 또는 행렬에서 여러 스파크라인 셰이프 차트에 일관된 색을 지정하려면  
  
1.  차트를 클릭하여 차트 데이터 창을 표시합니다.  
  
2.  **범주 그룹** 영역에서 범주를 마우스 오른쪽 단추로 클릭한 다음 **범주 그룹 속성**을 클릭합니다.  
  
3.  일반 탭의 **다음 위치의 그룹 동기화** 상자에서 색을 동기화할 범주의 이름을 클릭하고 **확인**을 클릭합니다.  
  
## <a name="to-specify-consistent-colors-across-multiple-shape-charts"></a>여러 셰이프 차트에 일관된 색을 지정하려면  
  
1.  보고서 본문 바깥쪽을 마우스 오른쪽 단추로 클릭하고 **보고서 속성**을 선택합니다.  
  
2.  **코드**에서 입력란에 다음 코드를 입력합니다.  
  
    ```  
    Private colorPalette As String() = {"Color1", "Color2", "Color3"}  
    Private count As Integer = 0  
    Private mapping As New System.Collections.Hashtable()  
    Public Function GetColor(ByVal groupingValue As String) As String  
        If mapping.ContainsKey(groupingValue) Then  
            Return mapping(groupingValue)  
        End If  
        Dim c As String = colorPalette(count Mod colorPalette.Length)  
        count = count + 1  
        mapping.Add(groupingValue, c)  
        Return c  
    End Function  
    ```  
  
    > [!NOTE]  
    >  "Color1" 문자열을 원하는 식으로 바꾸어야 합니다. "Red"와 같은 명명된 색을 사용하거나 색을 나타내는 6자리 16진수 값(예: 검정의 경우 "#FFFFFF")을 사용할 수도 있습니다. 4가지 이상의 색을 정의한 경우 배열에 있는 색 수가 셰이프 차트의 요소 수와 일치하도록 색 배열을 확장해야 합니다. 명명된 색이나 16진수 색 표현이 포함된 쉼표로 구분된 문자열 값 목록을 지정하여 배열에 새로운 색을 추가할 수 있습니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  셰이프 차트를 마우스 오른쪽 단추로 클릭하고 **계열 속성**을 선택합니다.  
  
5.  **채우기**에서 **식** (*fx*) 단추를 클릭하여 **색** 속성에 대한 식을 편집합니다.  
  
6.  다음 식을 입력합니다. 여기서 "MyCategoryField"는 **범주 그룹** 영역에 표시되는 필드입니다.  
  
    ```  
    =Code.GetColor(Fields!MyCategoryField)  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [차트에서 계열 색 서식 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [차트에 3D 가장자리, 볼록 및 질감 스타일 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [색상표를 사용하여 차트에 대한 색 정의&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [차트에 빈 요소 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md)   
 [셰이프 차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)   
 [동일한 데이터 세트에 여러 데이터 영역 연결&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [중첩된 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)   
 [스파크라인 및 데이터 막대&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
