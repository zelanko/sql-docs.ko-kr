---
title: 드릴다운 작업(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "10249"
- "10186"
- "10092"
- "10167"
- "10174"
- sql13.rtp.rptdesigner.charttitleproperties.visibility.f1
- "10155"
- sql13.rtp.rptdesigner.chartproperties.visibility.f1
- sql13.rtp.rptdesigner.pictureproperties.visibility.f1
- sql13.rtp.rptdesigner.majorgridlineproperties.visibility.f1
- "10123"
- "10425"
- sql13.rtp.rptdesigner.axisproperties.visibility.f1
- "10217"
- "10161"
- "10215"
- sql13.rtp.rptdesigner.legendproperties.visibility.f1
- "10258"
- "10144"
- sql13.rtp.rptdesigner.subreportproperties.visibility.f1
- sql13.rtp.rptdesigner.textboxproperties.visibility.f1
- "10062"
- sql13.rtp.rptdesigner.serieslabelproperties.visibility.f1
- sql13.rtp.rptdesigner.rectangleproperties.visibility.f1
- sql13.rtp.rptdesigner.calculatedseriesproperties.visibility.f1
- sql13.rtp.rptdesigner.chartareaproperties.visibility.f1
- "10053"
- sql13.rtp.rptdesigner.minorgridlineproperties.visibility.f1
- sql13.rtp.rptdesigner.seriesproperties.visibility.f1
ms.assetid: 1f8d1ef2-0daf-40c6-9ba7-3b391249bcd4
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1250e47366e8beab3cdee5f07e6d17e76827a597
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34550714"
---
# <a name="drilldown-action-report-builder-and-ssrs"></a>드릴다운 동작(보고서 작성기 및 SSRS)
입력란에 더하기 및 빼기 아이콘을 제공하면 사용자가 항목을 대화식으로 숨기거나 표시할 수 있습니다. 이를 *드릴다운* 동작이라고 합니다. 테이블 또는 행렬에 대해서는 정적 행과 열 또는 그룹과 연결된 행과 열을 표시하거나 숨길 수 있습니다.  
  
 ![rs_drilldown](../../reporting-services/report-design/media/rs-drilldown.gif "rs_drilldown")  
  
 이 그림에서 사용자는 보고서에서 더하기 기호(+)를 클릭하여 세부 데이터를 표시합니다.  
  
 예를 들어 처음에는 행 그룹이 있는 테이블의 외부 그룹 요약 행을 제외한 모든 행을 숨길 수 있습니다. 세부 정보 그룹이 포함된 각 내부 그룹의 경우 포함 그룹의 그룹화 셀에 확장/축소 아이콘을 추가합니다. 보고서가 렌더링되면 사용자가 입력란을 클릭하여 세부 데이터를 확장하거나 축소할 수 있습니다. 자세한 내용은 [테이블&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)을 참조하세요.  
  
 사용자가 항목을 확장 또는 축소할 수 있도록 하려면 해당 항목에 표시 유형 속성을 설정합니다.  
  
> [!NOTE]  
>  드릴다운 동작이 있는 보고서를 만드는 경우에는 표시 유형 정보를 행이나 열의 단일 입력란이 아닌 숨기려는 그룹,  열 또는 행에서 설정해야 합니다. 또한 토글에 사용하는 입력란은 표시하거나 숨기려는 항목을 제어하는 포함 범위에 있어야 합니다.  
>   
>  예를 들어 중첩된 그룹에 연결된 행을 숨기려면 입력란이 포함 계층 구조에서 부모 그룹 이상의 그룹과 연결된 행에 있어야 합니다.  
>   
>  그룹, 열 또는 행의 가시 정보 설정에 대한 자세한 내용은 [항목에 확장 또는 축소 동작 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)를 참조하세요.  
  
 보고서 항목을 숨기는 방법에 대한 자세한 내용은 [항목 숨기기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/hide-an-item-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="comparing-drilldown-and-drillthrough-reports"></a>드릴다운 및 드릴스루 보고서 비교  
 드릴다운 보고서에서 사용자는 더하기 또는 빼기 단추를 클릭하여 보고서의 섹션을 확장 또는 축소함으로써 해당 위치의 세부 데이터를 표시합니다. 드릴스루 보고서에서 사용자는 요약 값 링크를 클릭하여 별도의 관련 보고서를 열고 세부 데이터를 볼 수 있습니다. 세부 데이터는 세부 정보 보고서가 실행될 때만 검색됩니다. 일반적으로 드릴스루 보고서는 드릴다운 보고서보다 필요한 리소스가 적습니다. 자세한 내용은 [드릴스루, 드릴다운, 하위 보고서 및 중첩 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)을 참조하세요.  
  
## <a name="rendering-extension-support-for-hidden-report-items"></a>숨겨진 보고서 항목에 대한 렌더링 확장 프로그램별 지원 기능  
 보고서 항목의 표시/숨기기 토글 기능은 사용자 상호 작용을 지원하는 렌더링 확장 프로그램(예: 보고서 작성기 및 웹 포털에서 보고서를 실행할 때 사용되는 HTML 렌더링 확장 프로그램)에서만 지원합니다. 다른 렌더링 확장 프로그램은 숨겨진 항목을 표시합니다. 아래에서는 조건부 표시 유형이 적용된 보고서 항목에 대한 지원을 설명합니다.  
  
-   HTML에서 숨겨진 항목은 HTML  원본에 표시되지 않습니다.  
  
-   XML  렌더링 확장 프로그램은 숨김 여부에 관계없이 모든 보고서 항목을 표시합니다.  
  
-   Excel  렌더링 확장 프로그램은 테이블,  행렬 또는 목록에 대해 숨겨진 행과 열을 표시하고 확장합니다. 행과 열이 모두 표시됩니다.  
  
 자세한 내용은 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [드릴스루, 드릴다운, 하위 보고서 및 중첩 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)   
 [대화형 정렬, 문서 구조 및 링크&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
