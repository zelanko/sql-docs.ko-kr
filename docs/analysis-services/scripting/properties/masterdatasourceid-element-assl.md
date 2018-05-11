---
title: MasterDatasourceID 요소 (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: dfa3ee83ddd643577c56dd5569eccb65c67bab78
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="masterdatasourceid-element-assl"></a>MasterDatasourceID 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  에 대 한 마스터 데이터 원본 식별자 (ID)를 포함 한 [데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Database>  
   ...  
   <MasterDatasourceID>...</MasterDatasourceID>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[데이터베이스](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 원격 인스턴스에서 데이터베이스에 대 한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 원격 파티션을 포함 하는 **MasterDatasourceID** 요소는 데이터 원본의 ID 마스터를 식별 하는 데 데이터 원본 포함 인스턴스 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 원격 파티션을 관리 하는 합니다.  
  
 부모에 해당 하는 요소 **MasterDatasourceID** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Database>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
