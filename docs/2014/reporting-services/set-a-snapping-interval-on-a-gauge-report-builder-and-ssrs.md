---
title: 계기의 맞춤 간격 설정 (보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 0ece7297-6e2f-47fb-835d-b9e9cce53fe2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3e2a35e4d6fefb6830774ffd7b2c3bc13a5e097c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101373"
---
# <a name="set-a-snapping-interval-on-a-gauge-report-builder-and-ssrs"></a>계기의 맞춤 간격 설정(보고서 작성기 및 SSRS)
  맞춤 간격은 값이 반올림되는 배수를 정의합니다. 기본적으로 계기는 데이터 창에서 지정한 필드의 정확한 값을 가리킵니다. 그러나 포인터가 미리 설정된 간격에 맞도록 정확한 값을 반올림하거나 내림할 수도 있습니다. 예를 들어 계기의 값이 34.2이고 맞춤 간격을 5로 지정한 경우에는 계기 포인터는 35를 가리킵니다. 계기의 값이 31.2이고 맞춤 간격을 5로 지정한 경우에는 계기 포인터가 30을 가리킵니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-a-snapping-interval-on-a-gauge"></a>계기의 맞춤 간격을 설정하려면  
  
1.  계기의 숫자를 아무 곳이나 클릭하여 눈금을 강조 표시합니다.  
  
2.  속성 창을 엽니다.  
  
    > [!NOTE]  
    >  속성 창이 표시 되지 않으면 **보기** 탭을 클릭 한 다음 **속성** 확인란을 선택 합니다.  
  
3.  **포인터** 속성에서 (...) 단추를 클릭 합니다. Pointer 컬렉션 편집기가 열립니다.  
  
4.  **SnappingEnabled** 속성을로 `True`설정 합니다.  
  
5.  맞춤 간격을 나타내는 값으로 **SnappingInterval** 을 설정 합니다. 포인터가 지정한 값의 가장 근사한 반올림 배수로 맞춰집니다.  
  
## <a name="see-also"></a>참고 항목  
 [계기의 눈금 서식 지정 &#40;보고서 작성기 및 SSRS&#41;](report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [계기 &#40;보고서 작성기 및 SSRS에 대 한 형식 지정&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [계기&#40;보고서 작성기 및 SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)  
  
  
