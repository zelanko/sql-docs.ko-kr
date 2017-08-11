---
title: "필터 수식 예 (보고서 작성기 및 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filtering data [Reporting Services], filter equation examples
ms.assetid: 66bec93d-7c3b-4d4a-8cb6-7a7bb2f34ec6
caps.latest.revision: 18
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e6bbd95ac20afbeb00b331efa13492a0036fff20
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="filter-equation-examples-report-builder-and-ssrs"></a>필터 수식 예(보고서 작성기 및 SSRS)
  필터를 만들려면 하나 이상의 필터 수식을 지정해야 합니다. 필터 수식에는 식, 데이터 형식, 연산자 및 값이 포함됩니다. 이 항목에서는 일반적으로 사용되는 필터의 예를 제공합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="filter-examples"></a>필터 예  
 다음 표에서는 다양한 데이터 형식 및 연산자를 사용하는 필터 수식의 예를 보여 줍니다. 비교 범위는 필터가 정의된 보고서 항목에 따라 결정됩니다. 예를 들어 데이터 집합에 대해 정의된 필터의 경우 **TOP % 10** 은 데이터 집합의 상위 10% 값이며 그룹에 대해 정의된 필터의 경우 **TOP % 10** 은 그룹의 상위 10% 값입니다.  
  
|간단한 식|데이터 형식|연산자|Value|Description|  
|-----------------------|---------------|--------------|-----------|-----------------|  
|`[SUM(Quantity)]`|**정수**|**>**|`7`|7보다 큰 데이터 값을 포함합니다.|  
|`[SUM(Quantity)]`|**정수**|**TOP N**|`10`|상위 10개 데이터 값을 포함합니다.|  
|`[SUM(Quantity)]`|**정수**|**TOP %**|`20`|데이터 값의 상위 20%를 포함합니다.|  
|`[Sales]`|**텍스트**|**>**|`=CDec(100)`|$100보다 큰 System.Decimal 형식(SQL "money" 데이터 형식)의 모든 값을 포함합니다.|  
|`[OrderDate]`|**DateTime**|**>**|`2008-01-01`|2008년 1월 1일부터 현재 날짜까지의 모든 날짜를 포함합니다.|  
|`[OrderDate]`|**DateTime**|**BETWEEN**|`2008-01-01`<br /><br /> `2008-02-01`|2008년 1월 1일부터 2008년 2월 1일까지의 날짜를 포함합니다.|  
|`[Territory]`|**텍스트**|**LIKE**|`*east`|"east"로 끝나는 모든 지역 이름입니다.|  
|`[Territory]`|**텍스트**|**LIKE**|`%o%th*`|이름의 시작 부분에 North와 South를 포함하는 모든 지역 이름입니다.|  
|`=LEFT(Fields!Subcat.Value,1)`|**텍스트**|**IN**|`B, C, T`|B, C 또는 T 문자로 시작하는 모든 하위 범주 값입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 매개 변수 사용 &#40; 보고서 작성기 및 보고서 디자이너 &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [데이터 집합 필터, 데이터 영역 필터 및 그룹 필터 &#40; 추가 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [식 &#40;의 데이터 형식 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [보고서 &#40;에 사용 되는 식 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [식 예 &#40; 보고서 작성기 및 SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
