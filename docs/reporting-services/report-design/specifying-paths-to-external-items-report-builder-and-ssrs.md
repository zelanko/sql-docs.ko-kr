---
title: 외부 항목에 대한 경로 지정(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4fe513da-f3c5-479c-9fec-8662b91a0d6d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ce654cc4724a71be36e49be71bdaf64994812567
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56293482"
---
# <a name="specifying-paths-to-external-items-report-builder-and-ssrs"></a>외부 항목에 대한 경로 지정(보고서 작성기 및 SSRS)
  드릴스루 보고서, 하위 보고서 및 이미지 파일과 같이 보고서 서버에 저장되어 있고 보고서 정의 파일 외부에 있는 항목을 참조하기 위해 보고서 항목 속성에 경로를 지정할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
> [!NOTE]  
>  보고서 작성기에서 항목 경로는 보고서 서버의 항목을 지정해야 합니다. 파일 시스템에 있는 항목의 경로는 지원되지 않습니다. 항목이 있는 보고서 서버에 연결된 경우에만 해당 항목을 사용하는 보고서를 미리 볼 수 있습니다.  
  
 동작, 하위 보고서 또는 이미지에 대한 대화 상자에서 외부 항목에 대한 경로를 지정할 때는 직접 보고서 서버를 찾아서 항목을 선택할 수 있습니다. 드릴스루 보고서 또는 하위 보고서를 지정할 때는 직접 항목을 찾아서 선택하는 것이 좋습니다. 이 방식을 사용할 경우 보고서 또는 하위 보고서 매개 변수를 지정할 때 드롭다운 목록에 올바른 매개 변수 이름이 표시됩니다. 항목 경로를 다른 항목에 대한 경로로 변경할 때는 필요에 따라 올바른 매개 변수 이름과 값을 수동으로 업데이트해야 합니다.  
  
 기본 모드로 구성된 보고서 서버의 경우 .rdl 파일 확장명 없이 드릴스루 보고서 이름을 지정합니다.  
  
 SharePoint 통합 모드로 구성된 보고서 서버의 경우 파일 확장명 .rdl을 포함해야 합니다. 경로는 다음 중 하나일 수 있습니다.  
  
-   **주 보고서에서 항목에 대한 상대 경로.** 예를 들면 ../AllSubreports/Subreport1과 같은 형태입니다. 이 예에서 **..** 는 주 보고서가 있는 폴더의 상위 폴더를 나타냅니다.  
  
    > [!NOTE]  
    >  보고서가 보고서 작성기 안에서 실행될 때는 상대 경로가 지원되지 않습니다. 외부 항목에 대한 상대 경로를 사용하는 보고서를 보려면 보고서를 보고서 서버에 저장하고 이 위치에서 보고서를 실행하십시오.  
  
-   **항목에 대한 전체 경로.**  
  
    -   **보고서 서버:** 경로는 홈 폴더인 **/** 에서 시작합니다. 예를 들면 /Reports/AllSubreports/Subreport1과 같은 형태입니다.  
  
    -   **SharePoint 사이트:** 항목의 전체 URL 및 파일 확장명 .rdl과 함께 보고서 이름을 식에 지정해야 합니다. `="https://server/site/library/folder/Report1.rdl"`)을 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
 [외부 이미지 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-an-external-image-report-builder-and-ssrs.md)   
 [하위 보고서 및 매개 변수 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-subreport-and-parameters-report-builder-and-ssrs.md)   
 [보고서에 드릴스루 동작 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)  
  
  
