---
title: 요소 연결 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- Attach command
ms.assetid: a315d1f1-e220-4296-97cb-6d35606b9640
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eda22adcd9760fbeb01e009b0a8d9692f7e5d333
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105403"
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
|데이터 형식 및 길이|없음|  
|기본값|없음|  
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
  
  
