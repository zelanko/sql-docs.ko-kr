---
title: ClrAssembly 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ClrAssembly Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ClrAssembly
helpviewer_keywords:
- ClrAssembly data type
ms.assetid: 3f5dc5a1-ebd6-41b8-ac04-91d4de137eb4
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e17992a5d15113ec0de5dd75978f932cb83d11c8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089655"
---
# <a name="clrassembly-data-type-assl"></a>ClrAssembly 데이터 형식(ASSL)
  나타내는 파생된 데이터 형식을 정의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 와 연결 된 어셈블리는 [데이터베이스](../objects/database-element-assl.md) 또는 [서버](../objects/server-element-assl.md) 요소  
  
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
|기본 데이터 형식|[어셈블리](../objects/assembly-element-assl.md)|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음(추상 형식)|  
|자식 요소|[파일](../collections/files-element-assl.md), [PermissionSet](../properties/permissionset-element-assl.md)|  
|파생 요소|참조 [어셈블리](../objects/assembly-element-assl.md) ([어셈블리](../collections/assemblies-element-assl.md) 컬렉션 [데이터베이스](../objects/database-element-assl.md) 또는 [서버](../objects/server-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 `ClrAssembly` 요소는 어셈블리를 실행하는 데 필요한 권한과 함께 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 또는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스의 특정 데이터베이스와 연결된 [!INCLUDE[ssAS](../../../includes/ssas-md.md)] 어셈블리를 다시 만들 때 필요한 파일을 포함합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ClrAssembly>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [파일 요소 &#40;ASSL&#41;](../objects/file-element-assl.md)   
 [ClrAssemblyFile 데이터 형식 &#40;ASSL&#41;](clrassemblyfile-data-type-assl.md)   
 [데이터 요소 &#40;ASSL&#41;](../objects/data-element-assl.md)   
 [DataBlock 데이터 형식 &#40;ASSL&#41;](datablock-data-type-assl.md)   
 [요소를 차단 &#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [요소를 차단 &#40;ASSL&#41;](../objects/block-element-assl.md)   
 [ComAssembly 데이터 형식 &#40;ASSL&#41;](assembly-data-type-assl.md)   
 [Analysis Services 스크립팅 언어 XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  