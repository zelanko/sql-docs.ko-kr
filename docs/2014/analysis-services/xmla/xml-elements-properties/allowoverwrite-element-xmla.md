---
title: AllowOverwrite 요소 (XMLA) | Microsoft Docs
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
- AllowOverwrite Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.allowoverwrite
- urn:schemas-microsoft-com:xml-analysis#EndSession
helpviewer_keywords:
- AllowOverwrite element
ms.assetid: e7e92481-5f29-47f2-9efd-4e5e60c002bb
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: b34b0becd78adca99e4052e142fc696c155f6e20
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079645"
---
# <a name="allowoverwrite-element-xmla"></a>AllowOverwrite 요소(XMLA)
  결정 여부 부모 [백업](../xml-elements-commands/backup-element-xmla.md) 또는 [복원](../xml-elements-commands/restore-element-xmla.md) 명령은 대상 파일이 나 데이터베이스를 덮어쓰려면 하려고 시도 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <AllowOverwrite>...</AllowOverwrite>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|False|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[백업](../xml-elements-commands/backup-element-xmla.md), [복원](../xml-elements-commands/restore-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Backup` 명령의 경우 `AllowOverwrite` 요소는 명령으로 `File` 요소에 지정된 백업 파일을 덮어쓸 수 있는지 여부를 결정합니다.  
  
 에 대 한 `Restore` 요소는 `AllowOverwrite` 요소 명령을 덮어쓸 수 있는지 여부를 결정은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에 지정 된 데이터베이스는 `DatabaseName` 요소입니다.  
  
## <a name="see-also"></a>관련 항목  
 [DatabaseName 요소 &#40;XMLA&#41;](name-element-xmla.md)   
 [파일 요소 &#40;XMLA&#41;](file-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  