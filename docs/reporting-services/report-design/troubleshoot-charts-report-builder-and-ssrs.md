---
title: 차트 문제 해결(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 01/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 65dac70a2b3eebc090cf282d650aff3840d00e89
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47738673"
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>차트 문제 해결(보고서 작성기 및 SSRS)
  다음은 차트로 작업할 때 도움이 되는 문제 관련 정보입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>차트에서 값 축에 있는 값의 합이 표시되어야 하는데 개수가 표시되는 이유  
 대부분의 차트 종류는 일반적으로 y축인 값 축에 숫자 값이 있어야 올바르게 그려집니다. 값 필드의 데이터 형식이 **String**이면 필드에 숫자가 있더라도 차트에서 숫자 값을 표시할 수 없습니다. 대신 차트는 해당 필드에 값이 포함되어 있는 행의 총 개수를 표시합니다. 이러한 현상을 방지하려면 값 계열에 사용하는 필드에 형식이 지정된 문자가 포함된 문자열이 아니라 숫자 데이터 형식이 포함되도록 해야 합니다.  

## <a name="need-more-help"></a>도움이 더 필요하세요?  
   
  다음을 사용해 보세요.  
 * Stack Overflow의 [SQL Server Reporting Services](https://stackoverflow.com/questions/tagged/reporting-services)  
 * [Microsoft SQL Server UserVoice](https://feedback.azure.com/forums/908035-sql-server)에서 문제 또는 제안 기록  
  
## <a name="see-also"></a>참고 항목  
 [차트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
