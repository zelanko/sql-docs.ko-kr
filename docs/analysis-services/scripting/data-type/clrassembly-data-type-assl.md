---
title: ClrAssembly 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ClrAssembly Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ClrAssembly
helpviewer_keywords:
- ClrAssembly data type
ms.assetid: 3f5dc5a1-ebd6-41b8-ac04-91d4de137eb4
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: aefbbf4ed85773ddf29993b35ddf6d3cfa2c482f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="clrassembly-data-type-assl"></a>ClrAssembly 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]나타내는 파생된 데이터 형식을 정의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 와 연결 된 어셈블리는 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 또는 [서버](../../../analysis-services/scripting/objects/server-element-assl.md) 요소  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ClrAssembly>  
      <!-- The following elements extend Assembly -->  
   <Files>...</Files>  
      <PermissionSet>...</PermissionSet>  
</ClrAssembly>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[어셈블리](../../../analysis-services/scripting/objects/assembly-element-assl.md)|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음(추상 형식)|  
|자식 요소|[파일](../../../analysis-services/scripting/collections/files-element-assl.md), [PermissionSet](../../../analysis-services/scripting/properties/permissionset-element-assl.md)|  
|파생 요소|참조 [어셈블리](../../../analysis-services/scripting/objects/assembly-element-assl.md) ([어셈블리](../../../analysis-services/scripting/collections/assemblies-element-assl.md) 컬렉션 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 또는 [서버](../../../analysis-services/scripting/objects/server-element-assl.md))|  
  
## <a name="remarks"></a>주의  
 **ClrAssembly** 다시 만드는 데 필요한 파일을 포함 하는 요소는 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 어셈블리를 연결 된 인스턴스의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 또는 인스턴스의특정데이터베이스와[!INCLUDE[ssAS](../../../includes/ssas-md.md)]는 어셈블리를 실행 하는 데 필요한 사용 권한과 함께 합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ClrAssembly>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [File 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/file-element-assl.md)   
 [ClrAssemblyFile 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)   
 [데이터 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/data-element-assl.md)   
 [DataBlock 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)   
 [Blocks 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/blocks-element-assl.md)   
 [Block 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/block-element-assl.md)   
 [ComAssembly 데이터 형식 &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)   
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
