---
title: "ImpersonationMode 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ImpersonationMode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ImpersonateMode
helpviewer_keywords:
- ImpersonateMode element
ms.assetid: 160fdcb2-ac9f-4c5a-a0eb-a5f7669166b9
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 92091cdbdb14462629c18cc065f780b24d97b057
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="impersonationmode-element-assl"></a>ImpersonationMode 요소(ASSL)
  파생 된 요소에 대 한 가장 방법을 나타내는 값이 포함 된 [ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md) 데이터 형식입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ImpersonationInfo>  
   ...  
   <ImpersonationMode>...</ImpersonationMode>  
  
</ImpersonationInfo>...  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*기본값*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*기본값*|부모가 가장이 사용되는 컨텍스트에 대해 가장 적합한 가장 방법을 사용합니다.|  
|*ImpersonateAccount*|부모가 부모 요소에 지정된 사용자 계정의 자격 증명을 사용합니다.|  
|*ImpersonateAnonymous*|부모가 익명 사용자의 자격 증명을 사용합니다.|  
|*ImpersonateCurrentUser*|부모가 현재 사용자의 자격 증명을 사용합니다.|  
|*ImpersonateServiceAccount*|인스턴스에 연결 된 서비스 계정의 자격 증명을 사용 하는 부모 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **ImpersonationMode** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ImpersonationLevel>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

