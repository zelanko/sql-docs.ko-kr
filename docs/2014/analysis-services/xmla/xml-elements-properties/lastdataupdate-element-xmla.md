---
title: LastDataUpdate 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- LastDataUpdate Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.lastdataupdate
- http://schemas.microsoft.com/analysisservices/2003/engine#LastDataUpdate
- urn:schemas-microsoft-com:xml-analysis#LastDataUpdate
helpviewer_keywords:
- LastDataUpdate element
ms.assetid: 66e43b17-844f-4ec2-bd1d-35608e7b6524
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2ad5b16a02a8f88699d0a92011955797eb1897aa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055823"
---
# <a name="lastdataupdate-element-xmla"></a>LastDataUpdate 요소(XMLA)
  부모 [Cube](cube-element-olapinfo-xmla.md) 요소가 나타내는 큐브의 데이터가 마지막으로 업데이트된 날짜 및 시간을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cube>  
   ...  
   <LastDataUpdate>...</LastDataUpdate>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|dateTime|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Cube](cube-element-olapinfo-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
