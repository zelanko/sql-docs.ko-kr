---
title: 측정값 만들기 및 관리 | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: edc1a4b2-96d3-4f34-bb70-6cacec79e819
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6a695bdc842c7495beee2b6c09f98cd8205e892b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="create-and-manage-measures"></a>측정값 만들기 및 관리 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  측정값은 보고서나 Excel 피벗 테이블 또는 피벗 차트에 사용하기 위해 만드는 수식입니다. COUNT 또는 SUM과 같은 표준 집계 함수를 기반으로 측정값을 만들거나 DAX를 사용하여 고유한 수식을 정의할 수 있습니다. 이 항목의 태스크에서는 테이블의 측정값 표를 사용하여 측정값을 만들고 관리하는 방법을 설명합니다.  
  
## <a name="tasks"></a>태스크  
 측정값을 만들고 관리하려면 테이블의 측정값 표를 사용합니다. 모델 디자이너의 데이터 뷰에서만 테이블에 대한 측정값 표를 볼 수 있습니다. 다이어그램 뷰에서는 측정값을 만들거나 측정값 표를 볼 수 없지만 기존 측정값을 볼 수는 있습니다. 테이블의 측정값 표를 보려면 **테이블** 메뉴를 클릭한 다음 **측정값 표 표시**를 클릭합니다.  
  
###  <a name="bkmk_create_stand"></a> 표준 집계 수식을 사용하여 측정값을 만들려면  
  
-   측정값을 만들 열을 클릭한 후 **열** 메뉴를 클릭하고 **자동 합계**를 가리킨 다음 집계 유형을 클릭합니다.  
  
     기본 이름 뒤에 측정값 표의 해당 열 바로 아래에 있는 첫 번째 셀의 수식이 추가되어 측정값이 자동으로 만들어집니다.  
  
###  <a name="bkmk_create_custom"></a> 사용자 지정 수식을 사용하여 측정값을 만들려면  
  
-   측정값 표에서 측정값을 만들려는 열 아래의 셀을 클릭한 다음 수식 표시줄에 이름과 콜론(:), 등호(=) 및 수식을 차례로 입력합니다. Enter 키를 눌러 수식을 적용합니다.  
  
###  <a name="bkmk_edit"></a> 측정값을 편집하려면  
  
-   측정값 표에서 측정값을 클릭한 다음 **속성** 창에서 다른 속성 값을 입력하거나 선택합니다.  
  
###  <a name="bkmk_rename"></a> 측정값의 이름을 바꾸려면  
  
-   측정값 표에서 측정값을 클릭한 다음 **속성** 창의 **측정값 이름**에 새 이름을 입력하고 Enter 키를 누릅니다.  
  
     수식 입력줄에서 측정값 이름을 바꿀 수도 있습니다. 수식 앞에 측정값 이름이 표시되고 그 뒤에 콜론이 표시됩니다.  
  
###  <a name="bkmk_delete"></a> 측정값을 삭제하려면  
  
-   측정값 표에서 측정값을 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [측정값](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [Kpi](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [계산 된 열](../../analysis-services/tabular-models/ssas-calculated-columns.md)  
  
  
