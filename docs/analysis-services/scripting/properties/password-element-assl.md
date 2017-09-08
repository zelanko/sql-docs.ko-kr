---
title: "Password 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Password Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Password element
ms.assetid: ee756b01-fb08-4a9a-8c2a-7c04af0f8658
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d83c0cccfaf1c4a50b2c10efead1f923012e6e0d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="password-element-assl"></a>Password 요소(ASSL)
  에 대 한 사용자 계정의 암호를 포함 된 [ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Password>...</Password>  
   ...  
</ImpersonationInfo>  
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
|부모 요소|[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 값은 **암호** 의 값과 함께 요소는 [계정](../../../analysis-services/scripting/properties/account-element-impersonationinfo-assl.md) 요소를 경우 가장 용도로 사용 됩니다 값은 [ImpersonationMode](../../../analysis-services/scripting/properties/impersonationmode-element-assl.md) 요소에 대 한 파생 된 모든 요소는 **ImpersonationInfo** 데이터 유형이 설정 되어 *ImpersonateAccount*합니다.  
  
 에 대 한 서버 관리자 역할의 구성원만는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 대 한 빈 값을 제공할 수는 **암호** 요소  
  
## <a name="see-also"></a>관련 항목:  
 [DataSourceImpersonationInfo 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/datasourceimpersonationinfo-element-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
