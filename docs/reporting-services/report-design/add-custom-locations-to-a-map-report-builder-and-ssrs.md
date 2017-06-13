---
title: "지도 (보고서 작성기 및 SSRS)에 사용자 지정 위치 추가 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- MICROSOFT.REPORTDESIGNER.MAPPOINT.POINTTEMPLATE
ms.assetid: 7d36faae-5bcc-446a-9eba-f42349cafacb
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c78f99c32d37e36986c4ea8bac20c12f87d4d568
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="add-custom-locations-to-a-map-report-builder-and-ssrs"></a>지도에 사용자 지정 위치 추가(보고서 작성기 및 SSRS)
  페이지가 매겨진 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 보고서에 지도를 추가한 후 점 위치를 추가할 수 있습니다.  
  
 계층의 모든 점에 대한 표시 속성은 계층의 점 속성에 대한 옵션을 설정하여 제어됩니다. 선택한 포함된 점의 경우 표시 속성을 무시할 수 있습니다.  
  
> [!NOTE]  
>  포함된 점에 대한 계층 표시 속성을 무시할 때 변경한 내용은 되돌릴 수 없습니다.  
  
 자세한 내용은 [규칙 및 분석 데이터를 사용하여 다각형, 선 및 점 표시 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-point-layer"></a>점 계층을 추가하려면  
  
1.  보고서 디자인 화면에서 지도를 클릭해 선택하여 지도 창을 표시합니다.  
  
2.  도구 모음에서 **계층 추가**를 클릭합니다.  
  
3.  드롭다운 목록에서 **점 계층 추가**를 클릭합니다. 점이 포함되지 않은 점 계층이 지도에 추가됩니다. 기본적으로 이 점 계층은 포함된 점을 사용할 준비가 됩니다.  
  
## <a name="to-add-a-custom-point"></a>사용자 지정 점을 추가하려면  
  
1.  보고서 디자인 화면에서 지도를 클릭해 선택하여 지도 창을 표시합니다.  
  
2.  지도 창에서 **포함**유형인 점 계층을 마우스 오른쪽 단추로 클릭한 다음 **점 추가**를 클릭합니다. 커서가 십자 기호로 변경됩니다.  
  
3.  점을 추가하려면 지도에서 위치를 클릭합니다. 포함된 점이 클릭한 위치의 선택한 계층에 추가됩니다.  
  
## <a name="to-customize-the-display-for-an-embedded-point"></a>포함된 점의 표시를 사용자 지정하려면  
  
1.  점을 마우스 오른쪽 단추로 클릭한 다음 **점 속성**을 클릭합니다. **지도 포함 점 속성** 대화 상자가 열립니다.  
  
2.  **이 계층의 점 옵션 무시**를 클릭합니다. 여러 속성 페이지가 왼쪽 창에 나타납니다.  
  
3.  페이지를 클릭하고 이 점에 적용할 표시 속성을 설정합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [지도&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [규칙 및 분석 데이터를 사용하여 다각형, 선 및 점 표시 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  
  
