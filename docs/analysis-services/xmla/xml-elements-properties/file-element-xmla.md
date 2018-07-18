---
title: 파일 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb80a091c9b9585a6efc29088d15139db7033efb
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37970001"
---
# <a name="file-element-xmla"></a>File 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모에서 사용할 파일 식별 [Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) 또는 [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) 명령이 나 부모 [위치](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element relationships table -->  
   ...  
   <File>...</File>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)하십시오 [위치](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md), [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 합니다 **파일** 요소는 UNC 파일 이름을 포함 하 고 부모 요소의 사용 여부를 결정 합니다 **파일** 요소입니다.  
  
 에 대 한 **백업** 명령 합니다 **파일** 요소에서 만든 백업 파일의 이름을 결정 합니다 **백업** 명령. 경로에 지정 된 경로 파일 이름의 일부로 지정 하지 않으면 합니다 **BackupDir** Analysis Services 인스턴스의 구성 속성을 사용 합니다. 지정 된 파일이 이미 있으면 오류가 발생 하지 않으면 합니다 **AllowOverwrite** 부모 요소의 **백업** 명령은 설정 됩니다 **True**합니다.  
  
 에 대 한 **복원** 명령에는 **파일** 하 여 복원할 백업 파일의 이름을 확인 하는 요소는 **복원** 명령입니다.  
  
 에 대 한 **위치** 요소를 **파일** 요소에 대 한 원격 백업 파일에 설명 합니다는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 원격 파티션을 포함 하는 인스턴스. 백업 및 원격 파티션을 복원 하는 방법에 대 한 자세한 내용은 참조 하세요. [Backing Up, Restoring, and 데이터베이스 동기화 &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
## <a name="see-also"></a>참고자료
 [AllowOverwrite 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md)   
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
