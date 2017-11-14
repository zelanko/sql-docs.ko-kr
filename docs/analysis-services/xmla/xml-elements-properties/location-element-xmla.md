---
title: "Location 요소 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Location Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.location
- urn:schemas-microsoft-com:xml-analysis#Location
- http://schemas.microsoft.com/analysisservices/2003/engine#Location
helpviewer_keywords:
- Location element
ms.assetid: cea5e776-f435-425a-9bce-812d727a2b71
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 57d724e1ed2aeae526077af50700e9fad504d29a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="location-element-xmla"></a>Location 요소(XMLA)
  부모에 대 한 원격 서버에 대 한 정보를 포함 [백업](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md), 또는 [동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) 명령입니다.  
  
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[백업](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md), [동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|  
|자식 요소|아래 표를 참조 합니다.|  
  
|상위 항목 또는 부모|자식 요소|  
|------------------------|-------------------|  
|[백업](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|[DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md), [파일](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)|  
|[복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|[ConnectionString](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md), [DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md), [DataSourceType](../../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md), [파일](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md), [폴더](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
|[동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|[ConnectionString](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md), [DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md), [DataSourceType](../../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md), [폴더](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 에 대 한 **백업** 명령에는 **위치** 의 원격 인스턴스에 대 한 원격 백업 파일 만들기에 대 한 정보를 제공 하는 요소 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
 에 대 한 **복원** 명령에는 **위치** 요소를 식별 하 고 원격에 연결 하는 방법에 대 한 정보를 제공 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 으로 인스턴스를 원격으로 복원 하는 데 사용 된 원격 백업 파일 해당 원격 인스턴스에서 파티션입니다.  
  
 **Synchronize** 명령의 경우 **Location** 요소는 부모 **DataSourceType** 명령의 **Synchronize** 요소 값에 따라 대상 인스턴스에서 사용할 데이터 원본 또는 대상 인스턴스와 동기화해야 하는 원본 인스턴스에 정의된 원격 인스턴스를 나타냅니다.  
  
 백업 및 원격 인스턴스를 복원 하는 방법에 대 한 자세한 내용은 참조 [백업 및 복원 Objects (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [BackupRemotePartitions 요소 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md)   
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

