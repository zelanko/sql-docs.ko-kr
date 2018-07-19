---
title: Location 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4953981e7657706a986e9a2407f6786ff676a854
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38004495"
---
# <a name="location-element-xmla"></a>Location 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모에 대 한 원격 서버에 대 한 정보가 [Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)를 [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md), 또는 [동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element relationships table -->  
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
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)하십시오 [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md), [동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|  
|자식 요소|아래 표를 참조하세요.|  
  
|상위 항목 또는 부모|자식 요소|  
|------------------------|-------------------|  
|[백업](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|[DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md), [파일](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)|  
|[복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|[ConnectionString](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md), [DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md)를 [DataSourceType](../../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md)하십시오 [파일](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md), [폴더](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
|[동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|[ConnectionString](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md)하십시오 [DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md)합니다 [DataSourceType](../../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md), [폴더](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 **백업** 명령에는 **위치** 요소 Analysis Services의 원격 인스턴스에 대해 원격 백업 파일을 만드는 방법에 대 한 정보를 제공 합니다.  
  
 에 대 한 **복원** 명령에는 **위치** 식별 하 고 원격 연결에 대 한 정보를 제공 하는 요소 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 원격 복원 하는 데 사용 된 원격 백업 파일 뿐만 아니라 인스턴스 해당 원격 인스턴스에서 파티션입니다.  
  
 **Synchronize** 명령의 경우 **Location** 요소는 부모 **DataSourceType** 명령의 **Synchronize** 요소 값에 따라 대상 인스턴스에서 사용할 데이터 원본 또는 대상 인스턴스와 동기화해야 하는 원본 인스턴스에 정의된 원격 인스턴스를 나타냅니다.  
  
 백업 및 원격 인스턴스를 복원 하는 방법에 대 한 자세한 내용은 참조 하세요. [백업 및 복원 Objects (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>참고자료
 [BackupRemotePartitions 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md)   
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
