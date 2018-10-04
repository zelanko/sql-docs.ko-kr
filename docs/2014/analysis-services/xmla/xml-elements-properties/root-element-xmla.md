---
title: root 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Root Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#root
- urn:schemas-microsoft-com:xml-analysis#root
- microsoft.xml.analysis.root
helpviewer_keywords:
- root element
ms.assetid: ecd9d6e8-b16c-4d62-9a87-107c413a0056
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 610ef2a3b332ec59e6ddf31d7f30acfe418549e5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48110253"
---
# <a name="root-element-xmla"></a>root 요소(XMLA)
  반환 된 결과 포함 합니다 [검색](../xml-elements-methods-discover.md) 메서드 또는 XML for Analysis (XMLA) 명령 사용 하 여 실행 합니다 [Execute](../xml-elements-methods-execute.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<return> <!-- or results-->  
   ...  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">...</root> <!-- for Execute method only -->  
   <!-- or -->  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">...</root>  
   <!-- or -->  
   <root xmlns= xmlns="urn:schemas-microsoft-com:xml-analysis:empty">...</root>  
   ...  
</return>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본값|없음|  
|카디널리티|1-n: 두 번 이상 나타날 수 있는 필수 요소입니다.|  
  
## <a name="data-type-and-length"></a>데이터 형식 및 길이  
  
|상위 항목|데이터 형식|  
|--------------|---------------|  
|[DiscoverResponse](../xml-data-types/rowset-data-type-xmla.md), [olapxmla_EmptyResult](../xml-data-types/emptyresult-data-type-xmla.md)|  
|[ExecuteResponse](../xml-data-types/mddataset-data-type-xmla.md)하십시오 [행 집합](../xml-data-types/rowset-data-type-xmla.md), [olapxmla_EmptyResult](../xml-data-types/emptyresult-data-type-xmla.md)|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[결과](results-element-xmla.md), [반환](return-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 `root` 요소에서 반환 된 정보를 포함 합니다 [DiscoverResponse](../xml-elements-objects-discoverresponse.md) 단일에서 반환한 요소 `Discover` 메서드 호출 또는 합니다 [ExecuteResponse](../xml-elements-objects-executeresponse.md) 요소 단일 실행 된 단일 XMLA 명령에서 반환 된 `Execute` 메서드를 호출 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
