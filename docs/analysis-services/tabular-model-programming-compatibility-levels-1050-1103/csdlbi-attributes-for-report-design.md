---
title: 보고서 디자인의 CSDLBI 특성 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ed1b2b8830bbf4bdb380cf1d469641621039a566
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/08/2018
---
# <a name="csdlbi-attributes-for-report-design"></a>보고서 디자인의 CSDLBI 특성
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  이 섹션에서는 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 쿼리 디자인에 영향을 주는 테이블 형식 모델링의 CSDL 확장에 있는 특성에 대해 설명합니다.  
  
## <a name="model-attributes"></a>Model Attributes  
 이러한 특성은 CSDL [EntityContainer](http://msdn.microsoft.com/library/bb399169.aspx) 요소의 하위 요소에 정의됩니다.  
  
|특성 이름|데이터 형식|Description|  
|--------------------|---------------|-----------------|  
|Culture|텍스트|통화 형식에 사용되는 culture를 나타냅니다. 생략하면 EN-US가 사용됩니다.|  
|IsRightToLeft|Boolean|텍스트 필드 값을 기본적으로 오른쪽에서 왼쪽으로 읽어야 하는지 여부를 나타냅니다.|  
  
## <a name="entity-attributes"></a>엔터티 특성  
 이러한 특성은 CSDL EntitySet 또는 EntityType 요소의 하위 요소에 정의됩니다.  
  
|특성 이름|데이터 형식|Description|  
|--------------------|---------------|-----------------|  
|**ReferenceName**|텍스트|DAX 쿼리에서 이 엔터티를 참조하는 데 사용되는 식별자입니다. 생략하면 이름이 사용됩니다.|  
|**캡션**|텍스트|엔터티의 표시 이름입니다.|  
|**설명서**|텍스트|비즈니스 사용자가 데이터의 의미를 이해하는 데 도움을 주는 설명 텍스트입니다.|  
|**숨김**|Boolean|엔터티를 표시해야 하는지 여부를 나타냅니다. 기본값은 **false**입니다.|  
|**CollectionCaption**|텍스트|엔터티의 인스턴스 집합을 참조하기 위한 복수 이름입니다. 생략하면 Caption 특성이 사용됩니다.|  
|**DisplayKey**|MemberRef[]|비즈니스 사용자가 엔터티 인스턴스를 식별하는 데 사용하는 필드의 정렬된 목록입니다. 참조는 인스턴스 속성 및 탐색 속성을 포함할 수 있습니다. 탐색 속성을 참조하면 대상 엔터티의 **DisplayKey** 가 표시됩니다. **DisplayKey** 값을 생략하면 키 필드가 사용됩니다.|  
|**DefaultImage**|MemberRef|비즈니스 사용자가 엔터티 인스턴스를 시각적으로 식별하는 데 사용하는 이미지가 포함된 필드에 대한 참조입니다. 생략하면 엔터티의 첫 번째 이미지 필드가 사용됩니다(있는 경우).|  
|**DefaultDetails**|MemberRef[]|엔터티 인스턴스에 대해 비즈니스 사용자에게 표시하는 기본 세부 정보 집합을 나타내는 필드의 정렬된 목록입니다. 생략하면 엔터티의 처음 5개 필드가 사용됩니다. 이때 **Key**, **DisplayKey**또는 **DefaultImage**에서 이미 참조하는 필드는 제외됩니다.|  
|**SortProperties**|MemberRef[]|엔터티 인스턴스가 일반적으로 정렬될 때 기준이 되는 필드의 정렬된 목록입니다. 이러한 필드를 정렬할 때는 각 필드에 지정된 **SortDirection** 이 사용됩니다. 생략하면 **DisplayKey** 필드가 사용됩니다.|  
|**DefaultMeasure**|MemberRef|측정값 또는 필드를 엔터티의 여러 인스턴스에 대한 기본 표현으로 사용해야 함을 나타내기 위해 모델에 정의된 측정값이나 기본 집계 함수가 있는 숫자 필드에 대한 참조입니다. 생략하면 엔터티 인스턴스 수가 사용됩니다.|  
|**DefaultLocation**|MemberRef|필드 값이 엔터티 인스턴스에 연결된 기본 위치를 나타내는 필드에 대한 참조입니다. 생략하면 엔터티의 첫 번째 위치 필드가 사용됩니다(있는 경우).|  
  
## <a name="field-attributes"></a>필드 특성  
 이러한 특성은 CSDL 속성 또는 [NavigationProperty](http://msdn.microsoft.com/library/bb387104.aspx) 요소의 하위 요소에 정의됩니다.  
  
|특성 이름|데이터 형식|Description|  
|--------------------|---------------|-----------------|  
|**ReferenceName**|텍스트|DAX 쿼리에서 이 엔터티를 참조하는 데 사용되는 식별자입니다. 생략하면 필드 이름이 사용됩니다.|  
|**캡션**|텍스트|엔터티의 표시 이름입니다. 생략하면 필드의 **ReferenceName** 이 사용됩니다.|  
|**설명서**|텍스트|비즈니스 사용자가 필드의 의미를 이해하는 데 도움을 주는 설명 텍스트입니다.|  
|**숨김**|Boolean|필드를 표시해야 하는지 여부를 나타냅니다. 기본값은 **false**이며 필드가 표시됨을 의미합니다.|  
|**DisplayFolder**|텍스트|이 필드가 표시되는 폴더의 이름(전체 경로)입니다. 생략하면 필드가 모델 루트에 표시됩니다.|  
|**ContextualNameRule**|Enum|속성 이름을 해당 이름이 사용되는 컨텍스트를 기반으로 수정할지 여부와 수정 방법을 나타내는 값입니다. 가능한 값은  **None**,  **Role**,  **Merge**입니다.|  
|**맞춤**|Enum|테이블 형식 프레젠테이션에서 필드 값을 정렬하는 방법을 나타내는 값입니다. 가능한 값은 **Default**, **Center**, **Left**, **Right**입니다. 생략하면 기본값이 필드의 데이터 형식에 따라 맞춤을 결정합니다.|  
|**FormatString**|텍스트|기본적으로 필드 값의 서식을 지정하는 방법을 나타내는 .NET 형식입니다. 생략하면 다음 형식이 사용됩니다.<br /><br /> -날짜/시간 필드: 국가별 짧은 날짜 또는 "d"<br /><br /> -집계 함수 부동 소수점 필드 및 기본 정수 필드: 국가별 숫자 또는 "n"<br /><br /> -집계 함수가 없는 기본 정수: 국가별 10 진수 또는 "d"<br /><br /> 다른 모든 유형의 필드에는 형식 문자열이 적용되지 않습니다.|  
|**단위**|텍스트|단위를 표현하기 위해 필드 값에 적용되는 기호입니다. 생략하면 단위는 알 수 없는 것으로 간주됩니다.|  
|**너비**|정수|테이블 형식 프레젠테이션에서 필드 값을 표시하기 위해 예약해야 하는 기본 설정 너비(문자 수)입니다. 생략하면 기본 너비는 필드의 데이터 형식을 기반으로 합니다.|  
|**SortDirection**|Enum|필드 값이 일반적으로 정렬되는 방법을 나타내는 값입니다. 가능한 값은 **Default**, **Ascending**, **Descending**입니다. 생략하면 정렬 방향을 할당하는 기본값은 필드의 데이터 형식을 기반으로 합니다.|  
|**IsRightToLeft**|Boolean|필드에 오른쪽에서 왼쪽으로 읽어야 하는 텍스트가 포함되는지 여부를 나타냅니다. 생략하면 모델 설정이 사용됩니다.|  
|**OrderBy**|MemberRef|이 필드 값의 정렬 순서를 정의하는 모델 내 다른 필드에 대한 참조입니다. 두 필드의 값이 1:1 매핑을 가지거나 정렬 동작이 정의되지 않습니다. 생략하면 필드는 필드 고유 값에 따라 정렬됩니다.|  
|**내용**|Enum|필드의 하위 형식 또는 내용을 설명하는 열거형입니다. 생략하면 필드의 데이터 형식이 Binary가 아닌 경우 특정 하위 형식이 사용되지 않고 이미지가 사용됩니다. 지원되는 내용 유형의 전체 목록을 보려면 AMO 설명서를 참조하십시오.|  
|**DefaultAggregateFunction**|Enum|일반적으로 이 필드를 집계하는 데 사용되는 기본 함수를 나타내는 값입니다(있는 경우). 가능한 값은 **None**, **Sum**, **Average**, **Count**, **Min**, **Max**입니다. 생략하면 숫자 필드에는 **Sum** 이 사용되고, 다른 모든 필드에는 **None** 이 사용됩니다.|  
|**IsSimpleMeasure**|Boolean|측정값이 단순히 숫자 필드의 간단한 집계인지 여부를 나타냅니다. 이러한 집계는 필요한 경우 쿼리에 쉽게 정의할 수 있으므로 성능 향상을 위해 모델 정의에서 생략해야 합니다. 생략하면 **false** 가 사용됩니다.|  
|**Kpi**<br /><br /> **KpiGoal**<br /><br /> **KpiStatus**|하위 요소|측정값 요소가 KPI로 사용됨을 나타냅니다. KPI 하위 요소는 KpiGoal 및 KpiStauts 요소를 사용하여 관련된 표시 이미지 및 대상 범위를 정의합니다.|  
  
  
