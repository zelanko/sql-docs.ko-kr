---
title: Restore 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Restore Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Restore
- urn:schemas-microsoft-com:xml-analysis#Restore
- microsoft.xml.analysis.restore
helpviewer_keywords:
- Restore command
ms.assetid: bb5a0c92-3927-4fa4-975b-6e4d79e0a912
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: df3e4814b0dafadd8ba7a5c6f572fba7d48e6d4a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094663"
---
# <a name="restore-element-xmla"></a>Restore 요소(XMLA)
  복원 된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 백업 파일에서 데이터베이스입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Restore>  
      <DatabaseName>...</DatabaseName>  
      <DatabaseID>...</DatabaseID>  
      <File>...</File>  
      <Security>...</Security>  
      <AllowOverwrite>...</AllowOverwrite>  
      <Password>...</Password>  
      <Locations>...</Locations>  
      <DbStorageLocation>...</DbStorageLocation>  
   </Restore>  
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
|자식 요소|[AllowOverwrite](../xml-elements-properties/allowoverwrite-element-xmla.md), [DatabaseName](../xml-elements-properties/name-element-xmla.md)를 [DatabaseID](../xml-elements-properties/id-element-xmla.md)를 [파일](../xml-elements-properties/file-element-xmla.md)를 [위치](../xml-elements-properties/locations-element-xmla.md), [암호](../xml-elements-properties/password-element-xmla.md)하십시오 [security](../xml-elements-properties/security-element-xmla.md), [DbStorageLocation](../xml-elements-properties/dbstoragelocation-element.md)|  
  
## <a name="remarks"></a>Remarks  
 합니다 `Restore` 명령를 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에 지정 된 데이터베이스는 `DatabaseName` 백업 파일 및 필요에 따라 복원 원격 파티션을 원격 백업 파일에서 요소입니다.  
  
 백업 파일에 저장 된 개체에서 사용 하는 저장소 모드에 따라는 `Restore` 명령은 다음 표에 나열 된 대로 정보를 복원 합니다.  
  
|저장소 모드|정보|  
|------------------|-----------------|  
|MOLAP(다차원 OLAP)|원본 데이터, 집계 및 메타데이터|  
|HOLAP(하이브리드 OLAP)|집계 및 메타데이터|  
|ROLAP(관계형 OLAP)|메타데이터|  
  
 중를 `Restore` 명령에 배타적 잠금이 적용 되는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 에 지정 된 데이터베이스는 `DatabaseName` 요소입니다. 뒤에 잠금이 해제 되는 `Restore` 명령이 완료 되었습니다.  
  
 백업 및 데이터베이스를 복원 하는 방법에 대 한 자세한 내용은 참조 하세요. [Backing Up, Restoring, and 데이터베이스 동기화 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
> [!IMPORTANT]  
>  복원 명령을 실행하는 사용자는 각 백업 파일에 대해 지정한 백업 위치에서 읽을 수 있는 권한을 가져야 합니다. 서버에 설치되지 않은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스를 복원하려면 사용자도 해당 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버여야 합니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스를 덮어쓰려면 사용자가 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버이거나 복원할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버여야 합니다.  
  
> [!NOTE]  
>  기존 데이터베이스를 복원한 다음에는 해당 데이터베이스를 복원한 사용자가 보유하고 있는 복원된 데이터베이스 액세스 권한이 손실될 수 있습니다. 이러한 액세스 권한 손실은 백업 수행 당시에 사용자가 서버 역할의 멤버가 아니었거나 모든 권한(관리자)이 있는 데이터베이스 역할의 멤버가 아니었던 경우 발생할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소를 백업 &#40;XMLA&#41;](backup-element-xmla.md)   
 [요소를 일괄 처리 &#40;XMLA&#41;](batch-element-xmla.md)   
 [병렬 요소 &#40;XMLA&#41;](../xml-elements-properties/parallel-element-xmla.md)   
 [Synchronize 요소 &#40;XMLA&#41;](synchronize-element-xmla.md)   
 [명령 &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
