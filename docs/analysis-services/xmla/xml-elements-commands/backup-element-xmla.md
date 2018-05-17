---
title: 요소 (XMLA) 백업 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1c026adf2d5efaed3f4e21dcc1c4b84f8149d90
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="backup-element-xmla"></a>Backup 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스를 백업 파일에 백업합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Backup>  
      <Object>...</Object>  
      <File>...</File>  
      <Security>...</Security>  
      <ApplyCompression>...</ApplyCompression>  
      <AllowOverwrite>...</AllowOverwrite>  
      <Password>...</Password>  
      <BackupRemotePartitions>...</BackupRemotePartitions>  
      <Locations>...</Locations>  
   </Backup>  
</Command>  
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
|부모 요소|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[AllowOverwrite](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md), [ApplyCompression](../../../analysis-services/xmla/xml-elements-properties/applycompression-element-xmla.md), [BackupRemotePartitions](../../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md), [파일](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md), [위치](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md), [ 개체](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [암호](../../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md), [보안](../../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **백업** 명령은 백업는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에 지정 된 데이터베이스는 [개체](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) 요소를 백업 파일 및 필요에 따라 원격 파티션 원격 백업 파일에 백업 합니다. 경우는 **개체** 요소 이외의 다른 개체를 참조 한 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스 오류가 발생 합니다.  
  
 데이터베이스의 개체에서 사용하는 저장소 모드에 따라 **Backup** 명령으로 백업되는 정보가 달라집니다. 다음 표에서는 사용하는 저장소 모드에 따라 백업되는 정보를 설명합니다.  
  
|저장소 모드|백업되는 정보|  
|------------------|-----------------------------------|  
|MOLAP(다차원 OLAP)|원본 데이터, 집계 및 메타데이터|  
|HOLAP(하이브리드 OLAP)|집계 및 메타데이터|  
|ROLAP(관계형 OLAP)|메타데이터|  
  
 중는 **백업** 명령에 공유 잠금이 적용 되는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에 지정 된 데이터베이스는 **개체** 요소입니다. **Backup** 명령이 완료된 후에는 공유 잠금이 해제됩니다.  
  
 여러 **백업** 명령에 포함 된 경우 병렬로 명령을 실행할 수 있습니다는 [병렬](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md) 의 컬렉션을 [일괄 처리](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) 명령입니다. **Parallel** 컬렉션을 사용하면 데이터베이스를 여러 백업 파일에 동시에 백업할 수 있습니다.  
  
 데이터베이스 백업 및 복원 하는 방법에 대 한 자세한 내용은 참조 [Backing Up, Restoring, 및 데이터베이스 동기화 & #40; XMLA & #41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
> [!IMPORTANT]  
>  백업 명령을 실행하는 사용자에게는 각 백업 파일에 대해 지정한 백업 위치에 쓸 수 있는 권한이 있어야 합니다. 또한 사용자는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버이거나 백업할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [요소 & #40; 복원 XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [요소 & #40; 동기화 XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [명령 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
