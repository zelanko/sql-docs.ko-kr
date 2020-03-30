---
title: 단위 설정 및 구성(보고서 작성기) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: a15a96c3-7d2c-433e-a440-4ea051e967a9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7651373c21b2e22d88a11d196e3f5c0322b07fe0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081016"
---
# <a name="set-and-configure-measurement-units-report-builder-and-ssrs"></a>단위 설정 및 구성(보고서 작성기 및 SSRS)
  [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 페이지를 매긴 보고서에서 표시기는 백분율과 숫자의 두 가지 측정 단위 중 하나를 사용합니다.   
    
  표시기는 기본적으로 백분율을 단위로 사용하도록 구성됩니다. 즉, 표시기 집합에서 각 아이콘에 할당되는 표시기 값은 백분율 범위로 결정됩니다. 백분율 범위는 표시기 집합의 아이콘에 대해 균등하게 분할됩니다. 각 아이콘은 표시기 상태를 나타냅니다. 다른 시작 백분율 및 끝 백분율을 지정하여 표시기 집합의 각 아이콘에 대한 백분율을 변경할 수 있습니다 또한 표시기는 데이터의 최소값 및 최대값을 자동으로 검색합니다.  
  
 측정 단위를 숫자 값이 되도록 변경할 수 있습니다. 이 경우에는 데이터의 최소값 및 최대값을 지정하지 않습니다. 대신 표시기에 사용되는 각 아이콘의 시작 값과 끝 값만 제공하면 됩니다.  
  
 식을 사용하여 단위 등의 옵션을 설정할 수 있습니다. 자세한 내용은 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="to-use-the-numeric-state-measurement-unit"></a>숫자 상태 단위를 사용하려면  
  
1.  변경할 표시기를 마우스 오른쪽 단추로 클릭하고 **표시기 속성**을 클릭합니다.  
  
2.  왼쪽 창에서 **값 및 상태** 를 클릭합니다.  
  
3.  **상태 단위** 목록에서 **숫자**를 클릭합니다.  
  
     필요한 경우 **식** (*fx*) 단추를 클릭하여 이 옵션의 값을 설정하는 식을 편집합니다.  
  
4.  표시기 집합의 각 아이콘에 대해 **시작** 및 **끝** 입력란의 값을 업데이트합니다.  
  
     필요한 경우 **식** (*fx*) 단추를 클릭하여 **시작** 및 **끝** 옵션의 값을 설정하는 식을 편집합니다.  
  
    > [!NOTE]  
    >  **시작** 및 **끝** 입력란의 값은 숫자여야 합니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-use-the-percentage-measurement-unit"></a>백분율 단위를 사용하려면  
  
1.  변경할 표시기를 마우스 오른쪽 단추로 클릭하고 **표시기 속성**을 클릭합니다.  
  
2.  왼쪽 창에서 **값 및 상태** 를 클릭합니다.  
  
3.  **상태 단위** 목록에서 **백분율**을 클릭합니다.  
  
     필요한 경우 **식** (*fx*) 단추를 클릭하여 이 옵션의 값을 설정하는 식을 편집합니다.  
  
4.  필요한 경우 **최소값** 및 **최대값** 옵션을 변경하여 표시기가 사용하는 데이터의 최소값 및 최대값을 자동으로 검색하는 대신 특정 값을 사용합니다. **최소값** 이 **최대값**보다 작아야 합니다.  
  
    > [!NOTE]  
    >  최소값 및 최대값을 명시적으로 설정하는 경우 데이터의 실제 최소값 및 최대값에 관계없이 표시기에서 해당 값 범위를 사용합니다. 즉, 최소값보다 작은 값과 최대값보다 큰 값은 보고서에 표시할 표시기 아이콘을 결정하는 평가에서 제외됩니다.  
  
     필요한 경우 **식** (*fx*) 단추를 클릭하여 이 옵션의 값을 설정하는 식을 편집합니다.  
  
5.  표시기 집합의 각 아이콘에 대해 **시작** 및 **끝** 입력란의 값을 업데이트합니다.  
  
     필요한 경우 **식** (*fx*) 단추를 클릭하여 **시작** 및 **끝** 옵션의 값을 설정하는 식을 편집합니다.  
  
    > [!NOTE]  
    >  **시작** 및 **끝** 입력란의 값은 숫자여야 합니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [표시기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
