---
title: 색 선택 대화 상자 (보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.selectcolor.f1
- "10090"
helpviewer_keywords:
- Select Color dialog box
ms.assetid: ac7089a3-5c7b-4f53-8348-180610e86da2
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 882f7ba5aed75aec20d656c5ca49da66625ec6e6
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56293111"
---
# <a name="select-color-dialog-box-report-builder-and-ssrs"></a>색 선택 대화 상자(보고서 작성기 및 SSRS)
  **색 선택** 대화 상자를 사용하여 데이터 영역이나 입력란 내의 단일 셀 또는 여러 셀의 배경에 대한 색 옵션을 지정하거나 차트의 색 옵션을 지정할 수 있습니다.  
  
## <a name="options"></a>변수  
 **색 선택기**  
 세 가지 옵션 중 하나를 선택하여 색을 선택하는 데 사용할 방식을 지정합니다.  
  
-   **선택 - 색 원** HSB(색상/채도/명도) 색 값을 사용하여 색을 선택합니다.  
  
-   **선택 - 색 사각형** RGB(빨강/녹색/파랑) 색 값을 사용하여 색을 선택합니다.  
  
-   **색상표 - 표준 색** 미리 정의된 색 값의 목록에서 색을 선택합니다.  
  
 **색 원**  
 HSB 값은 원통형 좌표계에 매핑되므로 HSB 색에 사용합니다. 색상은 실제 색이고, 채도는 색의 순수한 정도이고, 명도는 밝음이나 어두움의 상대적인 정도입니다.  
  
 색을 선택하면 결정된 색이 원의 중앙에 표시됩니다. 색상을 변경하려면 색 슬라이더를 사용합니다. x 및 y 좌표는 각각 채도와 명도 값을 나타냅니다.  
  
 **사각형 색상표**  
 RGB 값은 데카르트 좌표계에 매핑되므로 RGB 색에 사용합니다. R은 빨강의 값, G는 녹색의 값, B는 파랑의 값입니다.  
  
 색을 선택하면 결정된 색이 사각형의 중앙에 나타납니다. 선택된 색의 범위를 변경하려면 색 슬라이더를 사용합니다. x 및 y 좌표는 다른 두 색을 나타냅니다. 예를 들어 녹색을 선택하면 슬라이더에 녹색 값의 범위가 표시되고 x 및 y 좌표는 각각 빨강 및 파랑 값을 나타냅니다.  
  
 **표준 색상표 색**  
 명명 된 색에 사용 된 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] `KnownColor` 열거형입니다.  
  
 **색 시스템**  
 RGB 또는 HSB 색을 지정합니다. 이 선택에 따라 RGB 또는 HSB 값을 표시하도록 디스플레이가 변경됩니다. RGB와 HSB 값은 **색 선택기**에서 색 원 또는 색 사각형을 사용할 때 대화형으로 업데이트됩니다.  
  
 **알파** 값은 색에 투명도 값이 포함될 수 있는 경우 일부 속성에 대해 표시됩니다. 예를 들어 차트 계열은 이 값이 표시됩니다. 투명도를 지원하지 않는 속성에 대해서는 이 값이 비활성화됩니다.  
  
 **빨강**  
 RGB 색의 빨강 부분을 나타내는 10진수 값입니다. 스핀 상자를 사용하여 값을 변경하거나 0에서 255 사이의 값을 입력합니다.  
  
 **녹색**  
 RGB 색의 녹색 부분을 나타내는 10진수 값입니다. 스핀 상자를 사용하여 값을 변경하거나 0에서 255 사이의 값을 입력합니다.  
  
 **Blue**  
 RGB 색의 파랑 부분을 나타내는 10진수 값입니다. 스핀 상자를 사용하여 값을 변경하거나 0에서 255 사이의 값을 입력합니다.  
  
 **Alpha**  
 색의 알파, 즉 투명도 부분을 나타내는 10진수 값입니다. 이 값이 활성화된 경우 슬라이더 스위치를 사용하여 투명도를 원하는 정도로 조정할 수 있습니다.  
  
 **색상**  
 HSB 색의 색상을 나타내는 10진수 값입니다. 스핀 상자를 사용하여 값을 변경하거나 0에서 255 사이의 값을 입력합니다.  
  
 **채도**  
 HSB 색의 채도를 나타내는 10진수 값입니다. 스핀 상자를 사용하여 값을 변경하거나 0에서 255 사이의 값을 입력합니다.  
  
 **밝기**  
 HSB 색의 명도를 나타내는 10진수 값입니다. 스핀 상자를 사용하여 값을 변경하거나 0에서 255 사이의 값을 입력합니다.  
  
 **색 보기**  
 창의 왼쪽 절반에 현재 색을 표시하고 사용자가 새로 선택하는 색을 창의 오른쪽 절반에 대화형으로 표시합니다. 기본 색이 없으면 창의 왼쪽 절반이 흰색으로 표시됩니다. 대부분의 RDL 속성에는 기본 색이 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 항목 서식 지정&#40;보고서 작성기 및 SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [텍스트 및 자리 표시자 서식 지정&#40;보고서 작성기 및 SSRS&#41;](report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)  
  
  
