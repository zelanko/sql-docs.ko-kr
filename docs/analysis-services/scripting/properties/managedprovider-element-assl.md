---
title: ManagedProvider 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ManagedProvider Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ManagedProvider element
ms.assetid: ed5a1077-20a4-40b9-b62d-0db0d53b9624
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7d4e720aa2aa3071b02209e00e4abcbda8d6ab6f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
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
  
  
