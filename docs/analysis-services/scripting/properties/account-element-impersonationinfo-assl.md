---
title: "계정 요소 (ImpersonationInfo) (ASSL) | Microsoft Docs"
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
- Account Element (ImpersonationInfo)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Account element
ms.assetid: aa3a1281-e42a-4926-875b-e6b81f4599c3
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e99a3e4bd81c70fd1043465f59f76b2fab60e863
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="account-element-impersonationinfo-assl"></a>Account 요소(ImpersonationInfo)(ASSL)
  에 대 한 사용자 계정의 이름을 포함 된 [ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md) 데이터 형식입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Account>...</Account>  
   ...  
</Action>  
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
 값은 **계정** 의 값과 함께 요소는 [암호](../../../analysis-services/scripting/properties/password-element-assl.md) 요소를 경우 가장 용도로 사용 됩니다 값은 [ImpersonationMode](../../../analysis-services/scripting/properties/impersonationmode-element-assl.md) 요소에 대 한 파생 된 모든 요소는 **ImpersonationInfo** 데이터 유형이 설정 되어 *ImpersonateAccount*합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [DataSourceImpersonationInfo 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/datasourceimpersonationinfo-element-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

