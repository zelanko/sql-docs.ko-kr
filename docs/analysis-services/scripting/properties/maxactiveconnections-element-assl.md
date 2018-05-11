---
title: MaxActiveConnections 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 48bddf07cfb4904fc40e4c663657fcf2914367eb
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="maxactiveconnections-element-assl"></a>MaxActiveConnections 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  파생 된 요소에 의해 허용 되는 동시 연결의 최대 수를 포함 된 [DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md) 데이터 형식입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DataSource>  
   ...  
   <MaxActiveConnections>...</MaxActiveConnections>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|정수|  
|기본값|**10**|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값이 0으로 설정된 경우 최대 동시 연결 수는 데이터 원본에 액세스하는 데 사용되는 데이터 카트리지에 의해 결정됩니다. 이 요소의 값이 음수 값으로 설정된 경우 최대 동시 연결 수에는 제한이 없습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
