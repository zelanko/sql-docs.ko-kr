---
title: 요소 (XMLA) 백업 | Microsoft Docs
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
- Backup Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Backup
- http://schemas.microsoft.com/analysisservices/2003/engine#Backup
- microsoft.xml.analysis.backup
helpviewer_keywords:
- Backup command
ms.assetid: 5bcbc14c-9db9-45b2-99de-f3a265bcb0c4
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a571681f52fb34e55df238229f659aa883bc84ac
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37215653"
---
# <a name="backup-element-xmla"></a>Backup 요소(XMLA)
  백업 된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스를 백업 파일입니다.  
  
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[AllowOverwrite](../xml-elements-properties/allowoverwrite-element-xmla.md), [ApplyCompression](../xml-elements-properties/applycompression-element-xmla.md)합니다 [BackupRemotePartitions](../xml-elements-properties/backupremotepartitions-element-xmla.md)를 [파일](../xml-elements-properties/file-element-xmla.md)를 [위치](../xml-elements-properties/locations-element-xmla.md), [ 개체](../xml-elements-properties/object-element-xmla.md)하십시오 [암호](../xml-elements-properties/password-element-xmla.md), [보안](../xml-elements-properties/security-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 합니다 `Backup` 명령은 백업 합니다 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에 지정 된 데이터베이스를 [개체](../xml-elements-properties/object-element-xmla.md) 백업 파일 및 필요에 따라 원격 파티션 원격 백업 파일을 백업 하는 요소입니다. `Object` 요소가 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스 이외의 개체를 참조하면 오류가 발생합니다.  
  
 정보는 `Backup` 명령 백업 데이터베이스의 개체에서 사용 되는 저장소 모드에 따라 달라 집니다. 다음 표에서는 사용하는 저장소 모드에 따라 백업되는 정보를 설명합니다.  
  
|저장소 모드|백업되는 정보|  
|------------------|-----------------------------------|  
|MOLAP(다차원 OLAP)|원본 데이터, 집계 및 메타데이터|  
|HOLAP(하이브리드 OLAP)|집계 및 메타데이터|  
|ROLAP(관계형 OLAP)|메타데이터|  
  
 중를 `Backup` 명령에 공유 잠금이 적용 되는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에 지정 된 데이터베이스는 `Object` 요소. 후에 공유 잠금이 해제 된 `Backup` 명령이 완료 되었습니다.  
  
 여러 `Backup` 명령에 포함 된 경우 명령을 병렬로 실행할 수 있습니다 합니다 [병렬](../xml-elements-properties/parallel-element-xmla.md) 컬렉션을 [일괄 처리](batch-element-xmla.md) 명령입니다. `Parallel` 컬렉션을 사용하면 데이터베이스를 여러 백업 파일에 동시에 백업할 수 있습니다.  
  
 백업 및 데이터베이스를 복원 하는 방법에 대 한 자세한 내용은 참조 하세요. [Backing Up, Restoring, and 데이터베이스 동기화 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
> [!IMPORTANT]  
>  백업 명령을 실행하는 사용자에게는 각 백업 파일에 대해 지정한 백업 위치에 쓸 수 있는 권한이 있어야 합니다. 또한 사용자는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버이거나 백업할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Restore 요소 &#40;XMLA&#41;](restore-element-xmla.md)   
 [Synchronize 요소 &#40;XMLA&#41;](synchronize-element-xmla.md)   
 [명령 &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
