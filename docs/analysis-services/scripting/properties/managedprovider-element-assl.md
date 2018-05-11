---
title: ManagedProvider 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b0ef8d8bcd692231ac65c4bc8e2c5b773544ada3
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="managedprovider-element-assl"></a>ManagedProvider 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  파생 된 요소에 의해 사용 되는 관리 되는 공급자의 이름을 포함 된 [DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md) 데이터 형식입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DataSource>  
   ...  
   <ManagedProvider>...</ManagedProvider>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 데이터 원본에서 관리 공급자를 사용하는 경우 **ManagedProvider** 요소에 관리 공급자의 이름이 포함됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Name 요소 &#40;ASSL&#41;](../../../analysis-services/scripting/properties/name-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
