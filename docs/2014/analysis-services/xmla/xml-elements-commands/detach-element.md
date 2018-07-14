---
title: Detach 요소 | Microsoft Docs
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
helpviewer_keywords:
- Detach command
ms.assetid: adbc7920-2a4a-4842-9e6f-37006fa19ff8
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4da654dd7b6af196f8ca2ac9c3efeb6e0b23ed45
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37217953"
---
# <a name="detach-element"></a>Detach 요소
  현재 서버 인스턴스에서 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스를 분리합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Detach>  
      <Object>...</Object>  
      <Password>...</Password>  
   </Detach>  
</Command>  
  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[개체](../xml-elements-properties/object-element-xmla.md)<br /><br /> [암호](../xml-elements-properties/password-element-xmla.md)|  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Attach 요소](attach-element.md)   
 [Analysis Services 데이터베이스 연결 및 분리](../../multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Analysis Services 데이터베이스 이동](../../multidimensional-models/move-an-analysis-services-database.md)   
 [Readwritemode 데이터베이스](../../multidimensional-models/database-readwritemodes.md)   
 [ReadOnly 및 ReadWrite 모드 간 Analysis Services 데이터베이스 전환](../../multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  
