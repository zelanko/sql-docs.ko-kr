---
title: DMX를 사용 하 여 드릴스루 쿼리 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 42c896ee-e5ee-4017-b66e-31d1fe66d369
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2ff75840ba60d8ab93a3adeeeef949263e607b35
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722705"
---
# <a name="create-drillthrough-queries-using-dmx"></a>DMX를 사용하여 드릴스루 쿼리 만들기
  드릴스루를 지원하는 모든 모델의 경우 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 DMX를 지원하는 다른 모든 클라이언트에서 DMX 쿼리를 만들어 사례 데이터 및 구조 데이터를 검색할 수 있습니다.  
  
> [!WARNING]  
>  데이터를 보려면 드릴스루를 사용하도록 설정되었으며 필요한 사용 권한이 있어야 합니다.  
  
## <a name="specifying-drillthrough-options"></a>드릴스루 옵션 지정  
 모델 사례 및 구조 사례를 검색하는 일반 구문은 다음과 같습니다.  
  
```  
SELECT <model column list>, StructureColumn('<structure column name') FROM <modelname>.CASES  
```  
  
 DMX 쿼리를 사용하여 사례 데이터를 반환하는 방법에 대한 자세한 내용은 [SELECT FROM &#60;model&#62;.CASES&#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx) 및 [SELECT FROM &#60;structure&#62;.CASES](/sql/dmx/select-from-structure-cases)를 참조하세요.  
  
## <a name="examples"></a>예  
 다음 DMX 쿼리는 시계열 모델의 특정 제품 계열에 대한 사례 데이터를 반환합니다. 또한 이 쿼리는 모델에 사용되지 않았지만 마이닝 구조에서는 사용할 수 있는 `Amount` 열도 반환합니다.  
  
```  
SELECT [DateSeries], [Model Region], Quantity, StructureColumn('Amount') AS [M200 Pacific Amount]  
FROM Forecasting.CASES  
WHERE [Model Region] = 'M200 Pacific'  
```  
  
 이 예에서는 별칭을 사용하여 구조 열의 이름을 바꾸었습니다. 구조 열에 별칭을 할당하지 않는 경우 열은 'Expression'이라는 이름으로 반환됩니다. 이 동작은 명명되지 않은 모든 열의 기본 동작입니다.  
  
## <a name="see-also"></a>관련 항목  
 [드릴스루 쿼리&#40;데이터 마이닝&#41;](drillthrough-queries-data-mining.md)   
 [마이닝 구조에 대한 드릴스루](drillthrough-on-mining-structures.md)  
  
  
