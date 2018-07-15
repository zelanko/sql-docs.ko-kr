---
title: ConnectionString 요소 (XMLA) | Microsoft Docs
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
- ConnectionString Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.connectionstring
- urn:schemas-microsoft-com:xml-analysis#ConnectionString
- http://schemas.microsoft.com/analysisservices/2003/engine#ConnectionString
helpviewer_keywords:
- ConnectionString element
ms.assetid: 3b0575aa-79ed-4f14-ae7e-dd587af4cdb1
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e7345d2a35d80a2ce4d72875c4afb082b57ec1a4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37293213"
---
# <a name="connectionstring-element-xmla"></a>ConnectionString 요소(XMLA)
  부모에서 사용 하는 연결 문자열을 포함 [위치](location-element-xmla.md) 하거나 [원본](source-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Location> <!-- or Source -->  
   ...  
   <ConnectionString>...</ConnectionString>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티-상위 항목 또는 부모|카디널리티|  
|[위치](location-element-xmla.md)|1-1: 한 번만 나타나는 필수 요소입니다.|  
|[원본](source-element-xmla.md)|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[위치](location-element-xmla.md), [원본](source-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Location` 요소의 경우 `ConnectionString` 요소는 `Restore` 또는 `Synchronize` 명령이 로컬 데이터 원본을 업데이트하거나 원격 인스턴스에 연결하는 데 사용하는 연결 문자열을 포함합니다.  
  
 `Source` 요소의 경우 `ConnectionString` 요소는 `Synchronize` 명령이 원본 인스턴스에 연결하는 데 사용하는 연결 문자열을 포함합니다.  
  
 백업 및 복원 하는 개체에 대 한 자세한 내용은 참조 하세요. [Backing Up, Restoring, and 데이터베이스 동기화 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Restore 요소 &#40;XMLA&#41;](../xml-elements-commands/restore-element-xmla.md)   
 [Synchronize 요소 &#40;XMLA&#41;](../xml-elements-commands/synchronize-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
