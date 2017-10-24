---
title: "Permission 데이터 형식 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Permission Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Permission
helpviewer_keywords:
- Permission data type
ms.assetid: 5f309544-59f8-4432-b1eb-b7c1a049f8df
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 56534a2dfba72ed8f620da5b7e8959ccb3f04d24
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

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
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|없음|  
|파생 데이터 형식|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md), [DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md), [DimensionPermission](../../../analysis-services/scripting/data-type/dimensionpermission-data-type-assl.md), [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md), [MiningStructurePermission](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[주석](../../../analysis-services/scripting/collections/annotations-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [설명](../../../analysis-services/scripting/properties/description-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [이름](../../../analysis-services/scripting/properties/name-element-assl.md), [프로세스](../../../analysis-services/scripting/properties/process-element-assl.md), [읽기](../../../analysis-services/scripting/properties/read-element-assl.md), [ReadDefinition](../../../analysis-services/scripting/properties/readdefinition-element-assl.md), [RoleID](../../../analysis-services/scripting/properties/roleid-element-assl.md), [쓰기](../../../analysis-services/scripting/properties/write-element-assl.md)|  
|파생 요소|없음|  
  
## <a name="remarks"></a>주의  
 **사용 권한** 역할의 인스턴스에 사용 되는 파생된 사용 권한 유형 수에 대 한 추상 기본 유형을 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
 이 데이터 형식은 DeploymentMode 값 2(테이블 형식 서버 모드)에서 다음과 같은 조건을 충족해야 합니다.  
  
-   *프로세스* 특성 기본값 설정은 **False**, 사용자에 게 경우를 제외 하 고는 **새로 고침** 권한. 사용자에 대 한는 **새로 고침** 권한은 *프로세스* 특성 값으로 설정 되어 **True**합니다.  
  
-   *ReadDefinition* 특성 값으로 설정 되어 **None**; 다른 모든 값에 오류가 발생 합니다.  
  
-   *읽기* 특성 값으로 설정 되어 **허용** 있는 사용자를 위해는 **사용자** 권한 및 **없음** 에 사용자 할당 때는  **새로 고침** permission; 사용자가 모두 **사용자** 및 **새로 고침** 로 설정 된 사용 권한을 다음 특성 **허용**합니다. 관리자 권한이 있는 사용자에 대 한 특성 값으로 설정 됩니다 **허용**합니다.  
  
-   *쓰기* 특성 값으로 설정 되어 **None**; 다른 모든 값에 오류가 발생 합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Permission>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Role 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

