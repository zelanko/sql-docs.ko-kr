---
title: 데이터 영역 렌더링(보고서 작성기) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4f3b2c7d-3669-457f-899b-b758d1db3426
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 06eb5ee05e045a2cb6e902030714ebb2f824becc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "77077007"
---
# <a name="rendering-data-regions-report-builder-and-ssrs"></a>데이터 영역 렌더링(보고서 작성기 및 SSRS)
  모든 보고서 항목에 적용되는 일반적인 렌더링 동작 이외에도 데이터 영역에는 고유한 페이지 매김 및 렌더링 동작이 추가로 적용됩니다. 데이터 영역과 관련된 렌더링 규칙에는 데이터 영역을 늘리는 방법, 모퉁이 셀이나 머리글 셀 같은 특수 셀의 렌더링 방법, 오른쪽에서 왼쪽으로 읽어야 하는 자료에 대한 데이터 영역의 렌더링 방법 등이 포함됩니다. 이 항목에서는 데이터 영역의 여러 부분이 어떻게 렌더링되는지 설명합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="tablix-data-regions"></a>테이블릭스 데이터 영역  
 테이블, 행렬 및 목록을 만드는 데 사용할 수 있는 테이블릭스 데이터 영역은 열과 행으로 이루어진 표로 렌더링됩니다. 행과 열이 교차하는 지점이 셀입니다. 보고서를 렌더링할 때 이 셀에는 데이터를 비롯하여 이미지, 사각형, 입력란, 하위 보고서 등과 같은 다른 보고서 항목이 포함될 수 있습니다. 테이블릭스 데이터 영역은 가로 및/또는 세로로 크기를 늘릴 수 있습니다. 또한 해당 내용을 기준으로 모퉁이 셀, 데이터 영역 머리글 셀 및 데이터 영역 본문 셀의 크기를 늘릴 수도 있습니다. 데이터 영역이 여러 페이지에 걸쳐 있는 경우 데이터 영역과 함께 반복하여 표시하도록 설정된 보고서 항목은 데이터 영역이 표시되는 각 페이지에 렌더링됩니다. 자세한 내용은 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)를 참조하세요.  
  
### <a name="right-to-left"></a>오른쪽에서 왼쪽  
 오른쪽에서 왼쪽으로 표시하도록 설정된 테이블릭스 데이터 영역은 이를 왼쪽에서 오른쪽으로 렌더링했을 때의 데이터 영역 이미지를 거울에 비춰 뒤집은 것과 같은 구조로 렌더링됩니다. 이 경우 데이터 영역의 모퉁이가 오른쪽 위 모퉁이에 표시됩니다. 보고서에 동적 열이 있으면 그 확장 방향이 왼쪽을 향합니다. 오른쪽에서 왼쪽 설정은 데이터 영역에 있는 데이터의 순서에는 영향을 주지 않습니다. 단지 열을 배치하는 순서가 바뀔 뿐입니다.  
  
### <a name="tablix-headers"></a>테이블릭스 머리글  
 테이블릭스 머리글은 머리글 셀이 행 그룹 계층에 표시되는지 열 그룹 계층에 표시되는지에 따라 행 머리글이나 열 머리글로 렌더링됩니다. 머리글의 셀 내용 안에 논리적 페이지 나누기가 있는 경우 이는 렌더링되지 않습니다. 열 그룹의 논리적 페이지 나누기는 무시됩니다.  
  
 그룹에 논리적 페이지 나누기가 있어도 바깥쪽 그룹 머리글이 나눠지지는 않습니다. 예를 들어 바깥쪽 그룹에 국가를 지정하고 안쪽 그룹에 행정 구역을 지정한 보고서가 있다고 가정해 봅시다. 행정 구역 그룹의 인스턴스 사이에 논리적 페이지 나누기가 있더라도 바깥쪽 그룹인 국가 그룹은 보고서의 각 페이지에 모두 표시됩니다.  
  
#### <a name="repeated-tablix-headers"></a>반복되는 테이블릭스 머리글  
 **속성** 창에서 RepeatWith 속성을 설정한 경우 열 머리글 같이 데이터 영역 내에서 바뀌지 않는 항목은 데이터 영역의 해당 부분을 렌더링하는 각 페이지에 반복하여 표시됩니다. 예를 들어 데이터 한 줄을 다음 페이지에 표시해야 하는 경우 RepeatWith 속성이 설정되어 있으면 렌더링되는 다음 페이지에도 열 머리글이 표시됩니다.  
  
### <a name="tablix-corner"></a>테이블릭스 모퉁이  
 왼쪽 위 모퉁이를 테이블릭스 모퉁이라고 합니다. 테이블릭스 모퉁이에는 다른 보고서 항목이 포함될 수 있지만 모퉁이에 논리적 페이지 나누기를 삽입한 경우 이러한 페이지 나누기는 테이블릭스 데이터 영역을 렌더링할 때 무시됩니다.  
  
### <a name="tablix-body"></a>테이블릭스 본문  
 테이블릭스 본문은 테이블릭스 셀로 구성됩니다. 테이블릭스 본문은 페이지 매김 규칙과 보고서 항목의 렌더링 동작을 기준으로 렌더링됩니다. 자세한 내용은 [보고서 항목 렌더링&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="chart-gauge-and-map-data-regions"></a>차트, 계기 및 지도 데이터 영역  
 차트, 계기 및 지도 데이터 영역은 이를 렌더링하고 보고서 본문에 표시할 때 이미지와 같은 방식으로 동작합니다. 다른 보고서에 연결하거나 책갈피로 이동하는 것과 같은 동작을 데이터 영역 내의 값에 연결할 수 있고, 렌더러가 지원하는 경우 이러한 동작도 함께 렌더링할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [여러 보고서 렌더링 확장 프로그램의 대화형 기능&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [보고서 항목 렌더링&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [테이블, 행렬 및 목록&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [계기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
