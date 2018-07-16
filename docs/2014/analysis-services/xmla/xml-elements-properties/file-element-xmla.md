---
title: 파일 요소 (XMLA) | Microsoft Docs
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
- File Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.file
- http://schemas.microsoft.com/analysisservices/2003/engine#File
- urn:schemas-microsoft-com:xml-analysis#File
helpviewer_keywords:
- File element
ms.assetid: 3dfd0e9b-746b-4ce5-8a95-610d2e573739
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b75a261f4a86d5a227e1018ad96a40d91db7b6c7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319223"
---
# <a name="file-element-xmla"></a>File 요소(XMLA)
  부모에서 사용할 파일 식별 [Backup](../xml-elements-commands/backup-element-xmla.md) 또는 [복원](../xml-elements-commands/restore-element-xmla.md) 명령이 나 부모 [위치](location-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <File>...</File>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Backup](../xml-elements-commands/backup-element-xmla.md)하십시오 [위치](location-element-xmla.md), [복원](../xml-elements-commands/restore-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `File` 요소는 UNC 파일 이름을 포함하고 부모 요소가 `File` 요소의 사용 여부를 결정합니다.  
  
 `Backup` 명령의 경우 `File` 요소는 `Backup` 명령으로 만들어지는 백업 파일의 이름을 결정합니다. 파일 이름에 경로가 지정되지 않은 경우 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스의 `BackupDir` 구성 속성에 지정된 경로가 사용됩니다. 지정된 파일이 이미 있는 경우 부모 `AllowOverwrite` 명령의 `Backup` 요소를 `True`로 설정하지 않으면 오류가 발생합니다.  
  
 `Restore` 명령의 경우 `File` 요소는 `Restore` 명령으로 복원되는 백업 파일의 이름을 결정합니다.  
  
 `Location` 요소의 경우 `File` 요소는 원격 파티션을 포함하는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 대한 원격 백업 파일을 설명합니다. 백업 및 원격 파티션을 복원 하는 방법에 대 한 자세한 내용은 참조 하세요. [Backing Up, Restoring, and 데이터베이스 동기화 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [AllowOverwrite 요소 &#40;XMLA&#41;](allowoverwrite-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
