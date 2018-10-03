---
title: Member 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Member Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Member
- microsoft.xml.analysis.member
- http://schemas.microsoft.com/analysisservices/2003/engine#Member
helpviewer_keywords:
- Member element
ms.assetid: 5cc33a1f-192e-4821-a4ef-9a5f2bb7a9f0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8ab24b02a46a5e6416018d9f77c733b0d3de7153
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168973"
---
# <a name="member-element-xmla"></a>Member 요소(XMLA)
  부모 [Members](members-element-xmla.md) 또는 [Tuple](tuple-element-xmla.md) 요소의 단일 멤버를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Members>  
   ...  
   <Member>  
      <UName>...</UName>  
      <Caption>...</Caption>  
      <LName>...</LName>  
      <LNum>...</LNum>  
      <DisplayInfo>...</DisplayInfo>  
   </Member>  
   ...  
</Members>  
<!-- or -->  
<Tuple>  
   ...  
   <Member Hierarchy="string">  
      <UName>...</UName>  
      <Caption>...</Caption>  
      <LName>...</LName>  
      <LNum>...</LNum>  
      <DisplayInfo>...</DisplayInfo>  
   </Member>  
   ...  
</Tuple>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Members](members-element-xmla.md), [Tuple](tuple-element-xmla.md)|  
|자식 요소|[Caption](caption-element-xmla.md), [DisplayInfo](displayinfo-element-xmla.md), [LName](name-element-xmla.md), [LNum](lnum-element-xmla.md), [UName](uname-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|계층|필수 `String` 특성입니다(부모 `Tuple` 요소에만 해당). `Member` 요소가 나타내는 멤버가 속하는 계층의 이름입니다.|  
  
## <a name="remarks"></a>Remarks  
 `Member` 요소는 지정된 계층 내에서 멤버를 식별하고 표시하는 데 필요한 정보를 포함합니다. 부모 `Members` 요소의 경우 계층은 부모 요소의 `Hierarchy` 특성에 의해 이미 지정되어 있습니다. 부모 `Tuple` 요소의 경우 계층은 `Hierarchy` 요소의 `Member` 특성을 사용하여 지정됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
