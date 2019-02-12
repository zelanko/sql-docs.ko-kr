---
title: 지도 색 규칙 대화 상자, 일반 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10541"
- sql12.rtp.rptdesigner.shared.mapcolorrulesgeneral.f1
ms.assetid: 14ff5fc1-4cf8-4a45-9d98-47a1bf1c52c4
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 6c1d4289f9785d6975c6bba85e8215f208a3c537
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56018255"
---
# <a name="map-color-rules-dialog-box-general"></a>지도 색 규칙 대화 상자, 일반
  **색 규칙 속성** 대화 상자에서 **일반** 을 선택하여 이 계층의 지도 요소에 대한 색 옵션을 정의할 수 있습니다. 지도 요소에는 다각형, 선 및 점이 포함됩니다. 공간 데이터 기반의 지도 요소와 데이터 세트 필드 또는 공간 데이터 원본 필드의 분석 데이터 간 관계를 만든 경우 색 규칙을 적용할 수 있습니다.  
  
 서로 다른 기본 색과 보조 색으로 장식 그라데이션을 지정하여 계층의 모든 지도 요소를 표시하려면 지도 다각형 속성 대화 상자의 **채우기** 페이지를 사용합니다. 색 규칙은 계층의 표시 속성보다 우선합니다. 자세한 내용은 [지도 또는 지도 계층의 데이터 및 표시 사용자 지정&#40;보고서 작성기 및 SSRS&#41;](report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **템플릿 스타일 적용**  
 마법사에서 선택하거나 다각형, 선 또는 점 계층 속성에서 설정한 테마에 따라 색을 사용하려면 이 옵션을 선택합니다. 테마에 따라 지도의 색, 글꼴 및 테두리에 대한 기본 옵션이 설정됩니다. 이 옵션의 경우 각 지도 요소에 색을 할당하기 위해 규칙이 적용되지 않습니다.  
  
 **색상표를 사용 하 여 데이터 시각화**  
 특정 색상표에서 색을 사용하여 분석 데이터를 시각화하려면 이 옵션을 선택합니다.  
  
 **색 범위를 사용 하 여 데이터 시각화**  
 각 지도 요소에 색 범위를 사용하여 분석 데이터를 시각화하려면 이 옵션을 선택합니다. 예를 들어 빨강을 시작 색으로, 노랑을 중간 색으로, 녹색을 마지막 색으로 지정하는 경우 하위 범위의 값은 빨강이고, 중간 범위의 값은 노랑이고, 상위 범위의 값은 녹색입니다.  
  
 **사용자 지정 색을 사용 하 여 데이터 시각화**  
 색 목록을 직접 지정하여 분석 데이터를 시각화하려면 이 옵션을 선택합니다.  
  
 **데이터 필드**  
 이 옵션은 **데이터 시각화** 옵션 중 하나를 선택하면 나타납니다.  
  
 드롭다운 목록에서 사용할 분석 데이터 필드를 선택합니다. 공간 데이터의 원본에 따라 목록에는 공간 데이터 원본의 필드와 공간 데이터와 분석 데이터 간의 관계가 있는 보고서 데이터 세트의 필드가 표시됩니다. 이러한 관계를 만들려면 선택된 지도 계층에 대한 분석 데이터 페이지에서 데이터 옵션을 설정합니다.  
  
 **색상표**  
 색상표의 이름을 입력하거나 선택합니다.  
  
 **시작 색**  
 데이터 범위의 하위에 있는 데이터에 사용할 색을 지정합니다.  
  
 **중간 색**  
 데이터 범위의 중간에 있는 데이터에 사용할 색을 지정합니다. 이 범위를 제거하려면 **색 없음** 을 선택합니다.  
  
 **마지막 색**  
 데이터 범위의 상위에 있는 데이터에 사용할 색을 지정합니다.  
  
 **추가**  
 색 규칙의 색을 직접 지정하려면 **추가** 를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [지도&#40;보고서 작성기 및 SSRS&#41;](report-design/maps-report-builder-and-ssrs.md)   
 [지도 범례, 색 눈금 및 관련 규칙 변경&#40;보고서 작성기 및 SSRS&#41;](report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)  
  
  
