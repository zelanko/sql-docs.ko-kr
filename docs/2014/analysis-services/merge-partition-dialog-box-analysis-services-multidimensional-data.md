---
title: 병합 파티션 대화 상자 (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.mergepartition.f1
ms.assetid: 1c94e250-ee18-4f98-b112-985f6346102a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26751f2cc00330716f160c115d0e839cc6d9527a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66077825"
---
# <a name="merge-partition-dialog-box-analysis-services---multidimensional-data"></a>병합 파티션 대화 상자(Analysis Services - 다차원 데이터)
  **SQL Server Management Studio** 의 **파티션 병합** 대화 상자를 사용하여 큐브에 있는 측정값 그룹의 파티션을 병합할 수 있습니다. **개체 탐색기** 에서 파티션 폴더 또는 파티션을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **파티션 병합** 을 선택하면 **파티션 병합** 대화 상자를 표시할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **Server**  
 대상 파티션이 포함된 Analysis Services 인스턴스 이름을 선택합니다.  
  
 **이름**  
 대상 파티션으로 사용할 기존 파티션의 이름을 선택합니다.  
  
 **폴더**  
 이름에서 선택한 파티션이 Analysis Services 인스턴스에 대한 기본 폴더를 사용하지 않는 경우 대상 파티션이 포함된 폴더의 이름을 표시합니다.  
  
 **원본 파티션**  
 대상 파티션에 병합할 수 있는 원본 파티션이 포함된 표를 표시합니다.  
  
> [!NOTE]  
>  동일한 집계 디자인을 공유하는 같은 측정값 그룹의 파티션만 병합할 수 있습니다.  
  
 표에는 다음 열이 있습니다.  
  
|열|Description|  
|------------|-----------------|  
|**결합**|원본 파티션을 대상 파티션에 병합하려면 선택합니다.|  
|**파티션 이름**|원본 파티션 이름을 표시합니다.|  
|**마지막 처리**|원본 파티션을 마지막으로 처리한 날짜와 시간을 표시합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [파티션 &#40;Analysis Services 다차원 데이터&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Analysis Services의 파티션 병합&#40;SSAS - 다차원 데이터&#41;](multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  
