---
title: 비즈니스 규칙 조건
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d2e0a8c3-4c2e-407c-856e-68d95ebda9ed
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ab2b632307f966a0f8e37d290c3cc12d52cda064
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728725"
---
# <a name="business-rule-conditions-master-data-services"></a>비즈니스 규칙 조건(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]의 비즈니스 규칙 조건은 True일 때만 하나 이상의 동작이 수행되는 조건을 결정합니다.  
  
> [!NOTE]  
>  조건은 선택 사항입니다. 조건을 지정하지 않는 경우 비즈니스 규칙에 대해 데이터의 유효성 검사가 실행되면 동작이 수행됩니다.  
  
## <a name="business-rule-conditions"></a>비즈니스 규칙 조건  
  
|조건 이름|설명|  
|--------------------|-----------------|  
|**같음**|선택한 특성이 특정 특성 또는 특정 특성 값과 **같거나** , 비어 있습니다.<br /><br /> 이 조건은 텍스트, 숫자, 날짜 및 링크 값에 유효합니다.|  
|**같지 않음**|선택한 특성이 특정 특성 또는 특정 특성 값과 **같지 않거나** , 비어 있습니다.<br /><br /> 이 조건은 텍스트, 숫자, 날짜 및 링크 값에 유효합니다.|  
|**보다 큼**|선택한 특성이 특정 특성 또는 특정 특성 값보다 **크거나** , 비어 있습니다.<br /><br /> 이 조건은 텍스트, 숫자 및 날짜 값에 유효합니다.|  
|**크거나 같음**|선택한 특성이 특정 특성 또는 특정 특성 값보다 **크거나 같거나** , 비어 있습니다.<br /><br /> 이 조건은 텍스트, 숫자 및 날짜 값에 유효합니다.|  
|**보다 작음**|선택한 특성이 특정 특성 또는 특정 특성 값보다 **작거나** , 비어 있습니다.<br /><br /> 이 조건은 텍스트, 숫자 및 날짜 값에 유효합니다.|  
|**작거나 같음**|선택한 특성이 특정 특성 또는 특정 특성 값보다 **작거나 같거나** , 비어 있습니다.<br /><br /> 이 조건은 텍스트, 숫자 및 날짜 값에 유효합니다.|  
|**시작 문자**|선택한 특성이 특정 특성 또는 특정 특성 값으로 **시작되거나** , 비어 있습니다.<br /><br /> 이 조건은 텍스트 및 링크 값에 유효합니다.|  
|**제외할 시작 문자**|선택한 특성이 특정 특성 또는 특정 특성 값으로 **시작되지 않거나** , 비어 있습니다.<br /><br /> 이 조건은 텍스트 및 링크 값에 유효합니다.|  
|**끝 문자**|선택한 특성이 특정 특성 또는 특정 특성 값으로 **끝나거나** , 비어 있습니다.<br /><br /> 이 조건은 텍스트 및 링크 값에 유효합니다.|  
|**제외할 끝 문자**|선택한 특성이 특정 특성 또는 특정 특성 값으로 **끝나지 않거나** , 비어 있습니다.<br /><br /> 이 조건은 텍스트 및 링크 값에 유효합니다.|  
|**contains**|선택한 특성이 특정 특성 또는 특정 특성 값을 **포함하거나** , 비어 있습니다.<br /><br /> 이 조건은 텍스트 및 링크 값에 유효합니다.|  
|**포함하지 않음**|선택한 특성이 특정 특성 또는 특정 특성 값을 **포함하지 않거나** , 비어 있습니다.<br /><br /> 이 조건은 텍스트 및 링크 값에 유효합니다.|  
|**패턴 포함**|선택한 특성이 특정 특성 또는 특정 특성 값의 **패턴을 포함하거나** , 비어 있습니다. 패턴은 .NET Framework 정규식을 사용하여 지정할 수 있습니다.<br /><br /> 정규식에 대한 자세한 내용은 MSDN Library의 [정규식 언어 요소](https://go.microsoft.com/fwlink/?LinkId=164401) 를 참조하십시오.<br /><br /> 이 조건은 텍스트 및 링크 값에 유효합니다.|  
|**제외할 패턴**|선택한 특성이 특정 특성 또는 특정 특성 값의 **패턴을 포함하지 않거나** , 비어 있습니다. 패턴은 .NET Framework 정규식을 사용하여 지정할 수 있습니다.<br /><br /> 정규식에 대한 자세한 내용은 MSDN Library의 [정규식 언어 요소](https://go.microsoft.com/fwlink/?LinkId=164401) 를 참조하십시오.<br /><br /> 이 조건은 텍스트 및 링크 값에 유효합니다.|  
|**하위 집합 포함**|선택한 특성이 특정 특성 또는 특정 특성 값의 **하위 집합을 포함** 합니다. 검색 시작 지점을 지정해야 합니다. 예를 들어 1은 첫 번째 문자에서 검색을 시작함을 나타냅니다.<br /><br /> 이 조건은 텍스트 및 링크 값에 유효합니다.|  
|**제외할 하위 집합**|선택한 특성이 특정 특성 또는 특정 특성 값의 **하위 집합을 포함하지 않습니다** . 검색 시작 지점을 지정해야 합니다. 예를 들어 1은 첫 번째 문자에서 검색을 시작함을 나타냅니다.<br /><br /> 이 조건은 텍스트 및 링크 값에 유효합니다.|  
|**변경된 경우**|비즈니스 규칙을 마지막으로 멤버에 적용한 이후 선택한 특성이 **변경된 경우** 입니다. 특성이 멤버로 속한 변경 그룹을 지정해야 합니다.<br /><br /> 변경 내용 추적 그룹에 대한 자세한 내용은 [변경 내용 추적 그룹에 특성 추가&#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)를 참조하세요.<br /><br /> 이 조건은 텍스트, 숫자, 날짜 및 링크 값에 유효합니다.|  
|**변경되지 않음**|비즈니스 규칙을 마지막으로 멤버에 적용한 이후 선택한 특성이 **변경되지 않은 경우** 입니다. 특성이 멤버로 속한 변경 그룹을 지정해야 합니다.<br /><br /> 변경 내용 추적 그룹에 대한 자세한 내용은 [변경 내용 추적 그룹에 특성 추가&#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)를 참조하세요.<br /><br /> 이 조건은 텍스트, 숫자, 날짜 및 링크 값에 유효합니다.|  
|**사이**|선택한 특성이 특정 특성 값 두 개의 **사이** 에 속합니다.<br /><br /> 이 조건은 텍스트, 숫자 및 날짜 값에 유효합니다.|  
|**제외 범위**|선택한 특성이 특정 특성 값 두 개의 **사이에 속하지 않습니다** .<br /><br /> 이 조건은 텍스트, 숫자 및 날짜 값에 유효합니다.|  
  
> [!NOTE]  
>  비즈니스 규칙에 두 값을 비교하는 조건이 포함되었고 두 값이 모두 Null인 멤버에 대해 이 규칙을 적용할 경우 해당 멤버의 유효성 검사가 실패합니다.  
  
## <a name="see-also"></a>참고 항목  
 [비즈니스 규칙 동작&#40;Master Data Services&#41;](../master-data-services/business-rule-actions-master-data-services.md)   
 [비즈니스 규칙&#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [비즈니스 규칙 만들기 및 게시&#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)  
  
  
