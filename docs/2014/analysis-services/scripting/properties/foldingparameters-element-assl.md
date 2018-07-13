---
title: FoldingParameters 요소 (ASSL) | Microsoft Docs
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
topic_type:
- apiref
f1_keywords:
- FoldIndex
- FoldCount
- MaxCases
- FoldingParameters
- FoldTargetAttribute
helpviewer_keywords:
- FoldingParameters element
ms.assetid: 5f5c5a3e-4aed-48fb-bca5-e67f421bef2f
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ac348aa326c53b1266edfff3396feadda6c80ea6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161144"
---
# <a name="foldingparameters-element-assl"></a>FoldingParameters 요소(ASSL)
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서버에서 마이닝 모델의 교차 유효성 검사를 수행할 때 사용하는 매개 변수를 지정합니다.  
  
> [!NOTE]  
>  이러한 매개 변수는 내부에서 사용하기 위한 것입니다. 여기에 제공된 정보는 참조용일 뿐입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningModel>  
   ...  
   <ddl100_100:FoldingParameters>...  
      <ddl100_100:FoldIndex>...</ddl100_100:FoldIndex>  
      <ddl100_100:FoldCount>...</ddl100_100:FoldCount>  
      <ddl100_100:MaxCases>...</ddl100_100:MAxCases>  
      <ddl100_100:FoldTargetAttribute>...</ddl100_100:FoldTargetAttribute  
...</ddl100_100:FoldingParameters>  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|*FoldIndex*|교차 유효성 검사에 사용되는 파티션의 시작 위치를 나타내는 정수입니다.|  
|*FoldCount*|교차 유효성 검사 후 모델에 있는 파티션 수를 나타내는 정수입니다.|  
|*MaxCases*|교차 유효성 검사에 사용되는 모델 사례 수를 나타내는 정수입니다.<br /><br /> 값 0은 모든 사례가 사용됨을 나타냅니다.|  
|*FoldTargetAttribute*|예측 가능한 특성이 포함된 모델 열의 ID를 나타내는 문자열입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningModel](../objects/miningmodel-element-assl.md)|  
|자식 요소|*FoldIndex*<br /><br /> *FoldCount*<br /><br /> *MaxCases*<br /><br /> *FoldTargetAttribute*|  
  
## <a name="remarks"></a>Remarks  
 이러한 속성은 내부에서 사용하기 위한 것이며 DDL 문에서 사용할 수 없습니다.  
  
 교차 유효성 검사를 사용 하는 방법에 대 한 자세한 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]를 참조 하세요 [교차 유효성 검사 보고서의 측정값](../../data-mining/measures-in-the-cross-validation-report.md)합니다.  
  
 사용 하 여 교차 유효성 검사를 수행 하는 방법에 대 한 자세한 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 저장 프로시저 [4788-9593-317b2826132d"&gt;data Mining Stored Procedures &#40;Analysis Services-Data Mining&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
