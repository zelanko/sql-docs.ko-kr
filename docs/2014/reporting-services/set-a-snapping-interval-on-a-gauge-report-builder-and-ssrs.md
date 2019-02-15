---
title: 계기 (보고서 작성기 및 SSRS)의 맞춤 간격 설정 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 0ece7297-6e2f-47fb-835d-b9e9cce53fe2
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 56d1d5a5064c90719b1376460f51c928b4efb58b
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56284471"
---
# <a name="set-a-snapping-interval-on-a-gauge-report-builder-and-ssrs"></a>계기의 맞춤 간격 설정(보고서 작성기 및 SSRS)
  맞춤 간격은 값이 반올림되는 배수를 정의합니다. 기본적으로 계기는 데이터 창에서 지정한 필드의 정확한 값을 가리킵니다. 그러나 포인터가 미리 설정된 간격에 맞도록 정확한 값을 반올림하거나 내림할 수도 있습니다. 예를 들어 계기의 값이 34.2이고 맞춤 간격을 5로 지정한 경우에는 계기 포인터는 35를 가리킵니다. 계기의 값이 31.2이고 맞춤 간격을 5로 지정한 경우에는 계기 포인터가 30을 가리킵니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-a-snapping-interval-on-a-gauge"></a>계기의 맞춤 간격을 설정하려면  
  
1.  계기의 숫자를 아무 곳이나 클릭하여 눈금을 강조 표시합니다.  
  
2.  속성 창을 엽니다.  
  
    > [!NOTE]  
    >  속성 창에 표시 되지 않으면 클릭 합니다 **보기** 탭을 선택한 다음는 **속성** 확인란을 선택 합니다.  
  
3.  에 **포인터** 속성 (...) 단추를 클릭 합니다. Pointer 컬렉션 편집기가 열립니다.  
  
4.  설정 된 **SnappingEnabled** 속성을 `True`입니다.  
  
5.  설정 된 **SnappingInterval** 맞춤 간격을 나타내는 값입니다. 포인터가 지정한 값의 가장 근사한 반올림 배수로 맞춰집니다.  
  
## <a name="see-also"></a>관련 항목  
 [계기의 눈금 서식 지정&#40;보고서 작성기 및 SSRS&#41;](report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [계기의 포인터 서식 지정&#40;보고서 작성기 및 SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [계기&#40;보고서 작성기 및 SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)  
  
  
