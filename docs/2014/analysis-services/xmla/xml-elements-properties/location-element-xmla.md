---
title: Location 요소 (XMLA) | Microsoft Docs
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
- Location Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.location
- urn:schemas-microsoft-com:xml-analysis#Location
- http://schemas.microsoft.com/analysisservices/2003/engine#Location
helpviewer_keywords:
- Location element
ms.assetid: cea5e776-f435-425a-9bce-812d727a2b71
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 51b0838b9843658b4081f9464c63274631ed74be
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184787"
---
# <a name="location-element-xmla"></a>Location 요소(XMLA)
  부모에 대 한 원격 서버에 대 한 정보를 포함 [백업](../xml-elements-commands/backup-element-xmla.md), [복원](../xml-elements-commands/restore-element-xmla.md), 또는 [동기화](../xml-elements-commands/synchronize-element-xmla.md) 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Location>  
```  
  
```  
  
<File>...</File> <!-- for Backup and Restore only -->  
<DataSourceID>...</DataSourceID>  
<DataSourceType>...</DataSourceType> <!-- for Restore and Synchronize only -->  
<ConnectionString>...</ConnectionString> <!-- for Restore and Synchronize only -->  
<Folders>...</Folders> <!-- for Restore and Synchronize only -->  
```  
  
```  
  
   </Location>  
   ...  
</Backup>  
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
|부모 요소|[백업](../xml-elements-commands/backup-element-xmla.md), [복원](../xml-elements-commands/restore-element-xmla.md), [동기화](../xml-elements-commands/synchronize-element-xmla.md)|  
  
## <a name="child-elements"></a>자식 요소  
  
|상위 항목 또는 부모|자식 요소|  
|------------------------|-------------------|  
|[백업](id-element-xmla.md), [파일](file-element-xmla.md)|  
|[복원](connectionstring-element-xmla.md), [DataSourceID](datasourceid-element-xmla.md), [DataSourceType](type-element-xmla.md), [파일](file-element-xmla.md), [폴더](folders-element-xmla.md)|  
|[동기화](../xml-elements-commands/synchronize-element-xmla.md)|[ConnectionString](connectionstring-element-xmla.md), [DataSourceID](datasourceid-element-xmla.md), [DataSourceType](type-element-xmla.md), [폴더](folders-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 `Backup` 명령에는 `Location` 의 원격 인스턴스에 대 한 원격 백업 파일 만들기에 대 한 정보를 제공 하는 요소 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
 `Restore` 명령의 경우 `Location` 요소는 원격 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스를 식별하고 연결하는 방법 및 해당 원격 인스턴스에서 원격 파티션을 복원하는 데 사용하는 원격 백업 파일에 대한 정보를 제공합니다.  
  
 `Synchronize` 명령의 경우 `Location` 요소는 부모 `DataSourceType` 명령의 `Synchronize` 요소 값에 따라 대상 인스턴스에서 사용할 데이터 원본 또는 대상 인스턴스와 동기화해야 하는 원본 인스턴스에 정의된 원격 인스턴스를 나타냅니다.  
  
 백업 및 원격 인스턴스를 복원 하는 방법에 대 한 자세한 내용은 참조 [백업 및 복원 Objects (XMLA)](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [BackupRemotePartitions 요소 &#40;XMLA&#41;](backupremotepartitions-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  