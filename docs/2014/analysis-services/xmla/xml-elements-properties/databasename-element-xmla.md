---
title: DatabaseName 요소 (XMLA) | Microsoft Docs
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
- DatabaseName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.databasename
- http://schemas.microsoft.com/analysisservices/2003/engine#DatabaseName
- urn:schemas-microsoft-com:xml-analysis#DatabaseName
helpviewer_keywords:
- DatabaseName element
ms.assetid: 5cfd9a1f-da53-497a-b677-c51be4641bd0
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: fbfff4e4389406496cf5df467ad044b6fa847727
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181169"
---
# <a name="databasename-element-xmla"></a>DatabaseName 요소(XMLA)
  식별 된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 부모 복원할 데이터베이스 [복원](../xml-elements-commands/restore-element-xmla.md) 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Restore>  
   ...  
   <DatabaseName>...</DatabaseName>  
   ...  
</Restore>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[복원](../xml-elements-commands/restore-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `DatabaseName` 요소는 `Restore` 명령으로 백업 파일을 복원하는 데이터베이스를 식별합니다. 이 요소를 지정하지 않았거나 빈 문자열을 포함하는 경우 백업 파일에 포함된 데이터베이스의 이름이 사용됩니다.  
  
 데이터베이스가 대상 인스턴스에 이미 있는 경우 부모 `AllowOverwrite` 명령에 대한 `Restore` 요소를 `True`로 설정하지 않으면 오류가 발생합니다.  
  
## <a name="see-also"></a>관련 항목  
 [AllowOverwrite 요소 &#40;XMLA&#41;](allowoverwrite-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  