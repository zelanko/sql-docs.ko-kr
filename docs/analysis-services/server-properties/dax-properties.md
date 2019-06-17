---
title: Analysis Services DAX 속성 | Microsoft Docs
ms.date: 10/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 20a6df833f8c525c24abdf3bb51278d0067db951
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62509661"
---
# <a name="dax-properties"></a>DAX 속성
[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

   Msmdsrv.ini의 DAX 섹션에는 DAX 쿼리 결과 집합에서 반환 된 행 수의 상한값 같은 Analysis Services에서 특정 쿼리 동작을 제어 하는 데 사용 하는 설정을 포함 합니다.

  DirectQuery 모델에서 반환된 행 집합과 같이 매우 큰 행 집합의 경우 기본값 백만 개의 행은 부족할 수 있습니다. 도이 오류가 발생할 경우 조정 해야 하는지 여부를 알 수 있습니다. "외부 데이터 원본에 대 한 쿼리 결과 집합의 허용 된 최대 크기인 '1000000' 행을 초과 했습니다."

상한값을 늘리려면 **MaxIntermediateRowSize** 구성 설정을 지정합니다. 구성 파일의 DAX 섹션에 전체 요소를 수동으로 추가해야 합니다. 이 설정은 추가한 다음에야 파일에 표시됩니다.

## <a name="configuration-snippet"></a>구성 코드 조각

```
<ConfigurationSettings>
. . .
<DAX>
  <PredicateCheckSpoolCardinalityThreshold>5000
  </PredicateCheckSpoolCardinalityThreshold>
  <DQ>
     <MaxIntermediateRowsetSize>1000000
     </MaxIntermediateRowsetSize>
  </DQ>
</DAX>
. . .
```

## <a name="property-descriptions"></a>속성 설명

설정 |값 |Description
--------|-------|-----------
MaxIntermediateRowsetSize | 1000000 | DAX 쿼리에서 반환된 최대 행 수입니다. 이 항목을 msmdsrv.ini 파일에 수동으로 추가하고 기본값이 너무 낮은 경우 값을 늘리세요.
PredicateCheckSpoolCardinalityThreshold| 5000 | Microsoft 지원의 지침에 따라 변경하는 경우를 제외하고 변경하면 안 되는 고급 속성입니다.

추가 서버 속성 및 해당 속성 설정 방법에 대한 자세한 내용은 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)을 참조하세요.
