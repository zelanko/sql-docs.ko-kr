---
title: 차트에 이동 평균 추가(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 166cf9c1-0750-4866-8381-542e4fbfe65a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 016eeebb679ee16e07a99e44a3740efaae413483
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106825"
---
# <a name="add-a-moving-average-to-a-chart-report-builder-and-ssrs"></a>차트에 이동 평균 추가(보고서 작성기 및 SSRS)
  이동 평균은 정의된 기간 동안 계산되는 계열 데이터의 평균입니다. 이동 평균은 차트에서 중요한 추세를 파악하는 데 사용될 수 있습니다.  
  
 이동 평균 수식은 기술 분석에서 사용되는 가장 일반적인 가격 표시기입니다. 평균값, 중앙값 및 표준 편차를 비롯한 다른 많은 수식들도 차트의 계열에서 파생될 수 있습니다. 이동 평균을 지정할 때 각 수식은 하나 이상의 필수 매개 변수를 가질 수 있습니다.  
  
 디자인 모드에서 이동 평균 수식을 추가할 때 유일한 시각적 자리 표시자는 추가되는 선 계열입니다. 차트는 보고서 처리 중에 각 수식에 대한 데이터 요소를 계산합니다.  
  
 추세 선에 대한 기본 지원은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 제공되지 않습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-calculated-moving-average-to-a-series-on-the-chart"></a>계산된 이동 평균을 차트의 계열에 추가하려면  
  
1.  **값** 영역에서 필드를 마우스 오른쪽 단추로 클릭하고 **계산된 계열 추가**를 클릭합니다. **계산된 계열 속성** 대화 상자가 열립니다.  
  
2.  **수식** 드롭다운 목록에서 **이동 평균** 옵션을 선택합니다.  
  
3.  이동 평균의 기간을 나타내는 정수 값을 **기간** 에 지정합니다.  
  
    > [!NOTE]  
    >  기간은 이동 평균을 계산하는 데 사용되는 일 수입니다. x축에 날짜/시간 값이 지정되지 않으면 이동 평균을 계산하는 데 사용되는 데이터 요소의 수에 따라 기간이 표시됩니다. 데이터 요소가 한 개뿐이면 이동 평균 수식이 계산되지 않습니다. 이동 평균은 두 번째 요소부터 계산됩니다. **첫 번째 요소에서 시작** 옵션을 지정할 경우 차트에서 이동 평균이 첫 번째 요소에서부터 시작됩니다. 데이터 요소가 한 개뿐이면 계산된 이동 평균의 요소는 원본 계열의 첫 번째 요소와 동일합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 작성기 및 SSRS&#41;&#40;차트 서식 지정](formatting-a-chart-report-builder-and-ssrs.md)   
 [차트 &#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [차트 &#40;보고서 작성기 및 SSRS에 빈 요소를 추가&#41;](add-empty-points-to-a-chart-report-builder-and-ssrs.md)  
  
  
