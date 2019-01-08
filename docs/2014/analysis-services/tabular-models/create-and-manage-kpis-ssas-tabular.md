---
title: Kpi (SSAS 테이블 형식) 만들기 및 관리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.kpi.f1
ms.assetid: c96026c2-4394-4c3c-986b-4c95a4421900
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dde3d1c12dd4f5b037d24030ae9ec96ae9f97dd0
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52405148"
---
# <a name="create-and-manage-kpis-ssas-tabular"></a>KPI 만들기 및 관리(SSAS 테이블 형식)
  이 항목에서는 테이블 형식 모델에서 KPI(핵심 성과 지표)를 만들거나 편집하거나 삭제하는 방법을 설명합니다. KPI를 만들려면 KPI의 기본 값으로 계산 되는 측정값을 선택 합니다. 그런 후 핵심 성과 지표 대화 상자를 사용해서 대상 값으로 평가되는 두 번째 측정값 또는 절대값을 선택합니다. 그리고 기본 및 대상 측정값 사이의 성능을 측정하는 상태 임계값을 정의할 수 있습니다.  
  
 이 항목에는 다음 태스크가 포함됩니다.  
  
-   [KPI 만들기](#bkmk_create_KPI)  
  
-   [KPI 편집](#bkmk_edit_KPI)  
  
-   [KPI 및 기본 측정값 삭제](#bkmk_delete)  
  
-   [KPI를 삭제하고 기본 측정값 유지](#bkmk_delete_KPI)  
  
## <a name="tasks"></a>태스크  
  
> [!IMPORTANT]  
>  KPI를 만들려면 먼저 값으로 계산되는 기본 측정값을 만들어야 합니다. 그런 다음 기본 측정값을 KPI로 확장합니다. 측정값을 만드는 방법은 다른 항목 [측정값 만들기 및 관리&#40;SSAS 테이블 형식&#41;](measures-ssas-tabular.md)에서 설명합니다. KPI에는 대상 값도 필요합니다. 이 값은 미리 정의된 다른 측정값이나 절대값에서 얻을 수 있습니다. 기본 측정값을 KPI로 확장한 후 핵심 성과 지표 대화 상자에서 대상 값을 선택하고 상태 임계값을 정의할 수 있습니다.  
  
###  <a name="bkmk_create_KPI"></a> KPI 만들기  
  
1.  측정값 표에서 기본 측정값(값)으로 사용할 측정값을 마우스 오른쪽 단추로 클릭하고 **KPI 만들기**를 클릭합니다.  
  
2.  **핵심 성과 지표** 대화 상자의 **대상 값 정의**에서 다음 중 하나를 선택합니다.  
  
     **측정값**을 선택하고 목록 상자에서 대상 측정값을 선택합니다.  
  
     **절대값**을 선택하고 숫자 값을 입력합니다.  
  
3.  **상태 임계값 정의**에서 낮은 임계값과 높은 임계값을 클릭한 후 이동합니다.  
  
4.  **아이콘 스타일 선택**에서 이미지 유형을 클릭합니다.  
  
5.  **설명**을 클릭하고 KPI, 값, 상태 및 대상에 대한 설명을 입력합니다.  
  
> [!TIP]  
>  Excel에서 분석 기능을 사용하여 KPI를 테스트할 수 있습니다. 자세한 내용은 [Excel에서 분석&#40;SSAS 테이블 형식&#41;](analyze-in-excel-ssas-tabular.md)을 참조하세요.  
  
###  <a name="bkmk_edit_KPI"></a> KPI 편집  
  
-   측정값 표에서 KPI의 기본 측정값(값)으로 사용할 측정값을 마우스 오른쪽 단추로 클릭하고 **KPI 설정 편집**을 클릭합니다.  
  
###  <a name="bkmk_delete"></a> KPI 및 기본 측정값 삭제  
  
-   측정값 표에서 KPI의 기본 측정값(값)으로 사용할 측정값을 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.  
  
###  <a name="bkmk_delete_KPI"></a> KPI를 삭제하고 기본 측정값 유지  
  
-   측정값 표에서 KPI의 기본 측정값(값)으로 사용할 측정값을 마우스 오른쪽 단추로 클릭하고 **KPI 삭제**를 클릭합니다.  
  
## <a name="alt-shortcuts"></a>Alt 바로 가기  
  
|UI 섹션|키 명령|  
|----------------|-----------------|  
|KPI 기본 측정값|Alt+B|  
|KPI 상태|Alt+S|  
|이름|Alt+M|  
|절대값|Alt+A|  
|상태 임계값 정의|Alt+U|  
|아이콘 스타일 선택|Alt+I|  
|추세|Alt+T|  
|설명|Alt+D|  
|추세|Alt+T|  
  
## <a name="see-also"></a>관련 항목  
 [KPI&#40;SSAS 테이블 형식&#41;](kpis-ssas-tabular.md)   
 [측정값&#40;SSAS 테이블 형식&#41;](measures-ssas-tabular.md)   
 [측정값 만들기 및 관리&#40;SSAS 테이블 형식&#41;](create-and-manage-measures-ssas-tabular.md)  
  
  
