---
title: 달력 선택 (차원 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.dimensionwizard.serverSpecialCalendars.f1
ms.assetid: 6e28a020-2586-4b13-9333-b499fb1b33af
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6796c7c3064adc65982b1d5aaec005249e224cae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090255"
---
# <a name="select-calendars-dimension-wizard"></a>달력 선택(차원 마법사)
  **달력 선택** 페이지를 사용하여 시간 차원에 대한 회계 달력, 보고 달력, 제조 달력 또는 ISO(International Standards Organization) 8601 달력을 나타내는 추가 계층을 만들 수 있습니다.  
  
> [!NOTE]  
>  이 페이지는 **차원 유형 선택** 페이지에서 **서버 시간 차원** 을 선택했거나 **차원 정의** 페이지에서 **데이터 원본을 사용하지 않고 차원 생성** 을 선택한 다음 **차원 유형 선택** 페이지에서 **시간 차원** 을 선택한 경우에만 표시됩니다.  
  
## <a name="options"></a>변수  
 **회계 달력**  
 회계 달력을 기반으로 시간 계층을 만들려면 선택합니다.  
  
 **시작 일 및 월**  
 회계 달력의 시작 일 및 월을 선택합니다.  
  
> [!NOTE]  
>  이 옵션은 **회계 달력** 을 선택한 경우에만 사용할 수 있습니다.  
  
 **회계 달력 명명 규칙**  
 회계 달력에 사용할 명명 규칙을 선택합니다. **역년 이름** 또는 **역년 이름 + 1**을 선택합니다.  
  
> [!NOTE]  
>  이 옵션은 **회계 달력** 을 선택한 경우에만 사용할 수 있습니다.  
  
 **보고 / 마케팅 달력**  
 보고 달력을 기반으로 시간 계층을 만들려면 선택합니다.  
  
 **시작 주 및 월**  
 보고 달력의 시작 주 및 월을 선택합니다.  
  
> [!NOTE]  
>  이 옵션은 **보고/마케팅 달력** 을 선택한 경우에만 사용할 수 있습니다.  
  
 **월간 주 패턴**  
 보고 달력에 사용할 월간 주 패턴을 선택합니다.  
  
> [!NOTE]  
>  이 옵션은 **보고/마케팅 달력** 을 선택한 경우에만 사용할 수 있습니다.  
  
 다음 표에서는 월간 주 패턴에 사용할 수 있는 옵션을 나열합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**주 445**|사분기의 첫 번째 달에 4주, 두 번째 달에 4주, 세 번째 달에 5주가 있습니다.|  
|**주 454**|사분기의 첫 번째 달에 4주, 두 번째 달에 5주, 세 번째 달에 4주가 있습니다.|  
|**주 544**|사분기의 첫 번째 달에 5주, 두 번째 달에 4주, 세 번째 달에 4주가 있습니다.|  
  
 **제조 달력**  
 제조 달력을 기반으로 시간 계층을 만들려면 선택합니다.  
  
 **시작 주 및 월**  
 제조 달력의 시작 주 및 월을 선택합니다.  
  
> [!NOTE]  
>  이 옵션은 **제조 달력** 을 선택한 경우에만 사용할 수 있습니다.  
  
 **추가 기간이 있는 사분기**  
 추가 기간이 포함될 사분기를 선택하거나 입력합니다.  
  
> [!NOTE]  
>  이 옵션은 **제조 달력** 을 선택한 경우에만 사용할 수 있습니다.  
  
 **ISO 8601 달력**  
 ISO 8601 달력을 기반으로 계층을 만들려면 선택합니다.  
  
## <a name="see-also"></a>관련 항목  
 [차원 마법사 F1 도움말](dimension-wizard-f1-help.md)   
 [차원 &#40;Analysis Services-다차원 데이터&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [다차원 모델의 차원](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  