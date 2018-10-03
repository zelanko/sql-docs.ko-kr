---
title: 차트 문제 해결(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 043246a90567bbd0cc2d084e1b2844ef2b79c346
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48162063"
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>차트 문제 해결(보고서 작성기 및 SSRS)
  다음은 차트로 작업할 때 도움이 되는 문제 관련 정보입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>차트에서 값 축에 있는 값의 합이 표시되어야 하는데 개수가 표시되는 이유  
 대부분의 차트 종류는 일반적으로 y축인 값 축에 숫자 값이 있어야 올바르게 그려집니다. 값 필드의 데이터 형식이 경우 `String`, 필드에 숫자가 있더라도 차트에서 숫자 값을 표시할 수 없습니다. 대신 차트는 해당 필드에 값이 포함되어 있는 행의 총 개수를 표시합니다. 이러한 현상을 방지하려면 값 계열에 사용하는 필드에 형식이 지정된 문자가 포함된 문자열이 아니라 숫자 데이터 형식이 포함되도록 해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [차트 &#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
