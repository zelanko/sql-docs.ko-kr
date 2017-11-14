---
title: "PendingValue 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- PendingValue Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- PendingValue
helpviewer_keywords:
- PendingValue element
ms.assetid: 386b2ec6-3d83-42d2-b83a-83e375fbdcbd
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5f52fd24820bf616cf82fb6e322329a9bdeb5bea
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="pendingvalue-element-assl"></a>PendingValue 요소(ASSL)
  값의 연결 된 보류 중인 읽기 전용 포함 [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ServerProperty>  
   ...  
   <PendingValue>...</PendingValue>  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|모든 simpleType|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 값을 포함 하는이 요소는 **ServerProperty** 사용 되는의 현재 인스턴스를 다음에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 시작 됩니다. 일반적으로 이 값은 서버 속성에 대한 값이 저장된 위치(초기화 파일, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 레지스트리 또는 다른 저장 메커니즘)에서 검색됩니다.  
  
 부모에 해당 하는 요소 **PendingValue** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ServerProperty>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ServerProperties 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)   
 [Server 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

