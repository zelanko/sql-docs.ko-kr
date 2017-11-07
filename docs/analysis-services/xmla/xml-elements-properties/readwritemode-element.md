---
title: "ReadWriteMode 요소 | Microsoft Docs"
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
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ReadWriteMode command
ms.assetid: 379bcaca-bb7e-4934-a9e7-21f8ede2fdc7
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3075b7834f7e24004811ce3802dd5fcb55b56f6c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="readwritemode-element"></a>ReadWriteMode 요소
  **ReadWriteMode** 데이터베이스 속성은 데이터베이스가 **ReadWrite** 모드에 있는지 또는 **ReadOnly** 모드에 있는지를 지정합니다. 이 속성 값은 두 가지만 가능합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Database>  
...  
   <ddlns_100_0:ReadWriteMode>...</ddlns_100_0:ReadWriteMode>  
...  
</Database>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|ReadWrite|  
|카디널리티|0-1: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[데이터베이스](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **ReadWrite** 모드에서만 데이터베이스를 만들 수 있으며 **ReadOnly** 모드에서는 데이터베이스를 만들 수 없습니다.  
  
 **ReadWriteMode** 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*읽기 전용*|데이터베이스에 변경 또는 업데이트를 적용할 수 없습니다.|  
|*ReadWrite*|데이터베이스에 변경 또는 업데이트를 적용할 수 있습니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [Attach 요소](../../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [Analysis Services 데이터베이스 연결 및 분리](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Analysis Services 데이터베이스 이동](../../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [Readwritemode 데이터베이스](../../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [ReadOnly 및 ReadWrite 모드 간 Analysis Services 데이터베이스 전환](../../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  

