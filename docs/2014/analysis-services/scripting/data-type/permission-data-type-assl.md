---
title: Permission 데이터 형식 (ASSL) | Microsoft Docs
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
- Permission Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Permission
helpviewer_keywords:
- Permission data type
ms.assetid: 5f309544-59f8-4432-b1eb-b7c1a049f8df
caps.latest.revision: 43
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c570ae1b3f2e2dbf65a4037f96e515d6667863a8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233953"
---
# <a name="permission-data-type-assl"></a>Permission 데이터 형식(ASSL)
  개별 사용 권한에 대한 정보를 나타내는 추상 기본 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Permission>  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreateTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <RoleID>...</RoleID>  
   <Description>...</Description>  
   <Process>...</Process>  
   <ReadDefinition>...</ReadDefinition>  
   <Read>...</Read>  
   <Write>...</Write>  
   <Annotations>...</Annotations>  
</Permission>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|InclusionThresholdSetting|  
|파생 데이터 형식|[CubePermission](../objects/cubepermission-element-assl.md), [DatabasePermission](../objects/databasepermission-element-assl.md)를 [DimensionPermission](permission-data-type-assl.md)하십시오 [MiningModelPermission](../objects/miningmodelpermission-element-assl.md), [MiningStructurePermission](../objects/miningstructurepermission-element-assl.md)|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[주석을](../collections/annotations-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [설명](../properties/description-element-assl.md)를 [ID](../properties/id-element-assl.md)를 [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [이름](../properties/name-element-assl.md), [프로세스](../properties/process-element-assl.md)를 [읽기](../properties/read-element-assl.md)를 [ReadDefinition](../properties/readdefinition-element-assl.md)를 [RoleID](../properties/roleid-element-assl.md), [작성](../properties/write-element-assl.md)|  
|파생 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Permission`은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에서 사용되는 많은 파생 사용 권한 유형에 대한 추상 기본 유형으로 사용됩니다.  
  
 이 데이터 형식은 DeploymentMode 값 2(테이블 형식 서버 모드)에서 다음과 같은 조건을 충족해야 합니다.  
  
-   *프로세스* 특성 기본 값 설정할지 `False`, 사용자에 게 경우를 제외 하 고는 **새로 고침** 권한. 사용자에 대 한 합니다 **새로 고침** 권한 합니다 *프로세스* 특성 값으로 설정 됩니다 `True`합니다.  
  
-   *ReadDefinition* 특성 값으로 설정 되어 `None`; 다른 값에 오류가 발생 합니다.  
  
-   *읽기* 특성 값으로 설정 됩니다 `Allowed` 사용자에 대 한 합니다 **사용자** 권한 및 `None` 사용자에 할당 된 경우를 **새로 고침** 권한; 사용자가 모두 **사용자** 하 고 **새로 고침** 로 설정 된 사용 권한을 다음 특성 `Allowed`합니다. 관리 권한을 가진 사용자의 경우 특성 값이 `Allowed`로 설정됩니다.  
  
-   *작성할* 특성 값으로 설정 되어 `None`; 다른 값에 오류가 발생 합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Permission>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [역할 요소 &#40;ASSL&#41;](../objects/role-element-assl.md)   
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
