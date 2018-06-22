---
title: 요소를 연결 | Microsoft Docs
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
- Attach command
ms.assetid: a315d1f1-e220-4296-97cb-6d35606b9640
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 0052882eec86aeb74dca98a21ebf236d1b0a65e1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089627"
---
# <a name="attach-element"></a>Attach 요소
  이전에 현재 서버 인스턴스 또는 다른 인스턴스로부터 분리된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스를 현재 서버 인스턴스에 연결합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Attach>  
      <Folder>...</Folder>  
            <ReadWriteMode>...</ReadWriteMode>  
            <Password>...</Password>  
   </Attach>  
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
|자식 요소|[Folder](../xml-elements-properties/folder-element-xmla.md)<br /><br /> [ReadWriteMode](../xml-elements-properties/readwritemode-element.md)<br /><br /> [암호](../xml-elements-properties/password-element-xmla.md)|  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Detach 요소](detach-element.md)   
 [Analysis Services 데이터베이스 연결 및 분리](../../multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Analysis Services 데이터베이스 이동](../../multidimensional-models/move-an-analysis-services-database.md)   
 [Readwritemode 데이터베이스](../../multidimensional-models/database-readwritemodes.md)   
 [ReadOnly 및 ReadWrite 모드 간 Analysis Services 데이터베이스 전환](../../multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  