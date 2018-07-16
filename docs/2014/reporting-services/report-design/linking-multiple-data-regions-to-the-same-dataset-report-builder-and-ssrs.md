---
title: 동일한 데이터 집합에 여러 데이터 영역 연결(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 90c94a91-8fb2-42cb-b998-563691f30d2d
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: c17a66cff53551f9bb4aa6687b8529c45e7f42e4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37301763"
---
# <a name="linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs"></a>동일한 데이터 집합에 여러 데이터 영역 연결(보고서 작성기 및 SSRS)
  여러 데이터 영역을 보고서에 추가하면 동일한 보고서 데이터 집합의 데이터를 여러 가지 방식으로 표시할 수 있습니다. 예를 들어 데이터를 테이블에 표시하고 차트로도 표시하려는 경우 해당 필터 식, 정렬 식 및 그룹 식에 동일한 식과 범위를 사용해야 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 차트와 테이블 또는 행렬을 사용하여 동일한 데이터를 표시하려면 테이블과 셰이프 차트, 행렬과 영역, 가로 막대형 및 세로 막대형 차트 간의 유사성을 충분히 파악해야 합니다. 행 그룹이 하나인 테이블은 쉽게 원형 차트로 표시할 수 있습니다. 행 그룹을 여러 개 추가한 경우에는 중첩된 그룹을 표시하는 데 적합한 여러 가지 차트 유형을 선택할 수 있습니다. 원형 차트에 중첩된 행 그룹을 추가하면 원형 차트 내의 조각 수가 늘어납니다. 따라서 부모 그룹과 자식 그룹의 인스턴스 수가 하나의 원형 차트에 표시하기에 너무 많지는 않은지 확인해야 합니다. 필요한 경우 원형 차트에서 작은 조각으로 표시되는 여러 개의 그룹 값에 대해 속성을 설정하여 특정 임계값 미만의 모든 값은 하나의 조각으로 표시되도록 할 수 있습니다. 자세한 내용은 [원형 차트에서 작은 조각 수집&#40;보고서 작성기 및 SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)을 참조하세요.  
  
 행 그룹이 여러 개인 테이블은 범주 그룹이 여러 개인 세로 막대형 차트로 표시할 수 있습니다. 자세한 내용은 [행렬 및 차트에 같은 데이터 표시&#40;보고서 작성기&#41;](display-the-same-data-on-a-matrix-and-a-chart-report-builder.md)를 참조하세요. 동일한 보고서 데이터 집합을 여러 가지 방식으로 표시하는 테이블 및 차트의 예를 보려면 AdventureWorks 보고서 예제의 Product Line Sales 보고서를 참조하십시오. 이 보고서에서는 테이블과 차트가 같은 데이터 집합에 연결되기 때문에, Top Employees 테이블 정렬에서 Employee Name에 대한 대화형 정렬 단추를 클릭하면 Top Employees 차트도 자동으로 새로 정렬됩니다. 이 샘플 보고서 및 기타 보고서를 다운로드하는 방법은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][보고서 작성기 및 보고서 디자이너 샘플 보고서](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
 행과 열 그룹이 여러 개인 행렬은 범주와 계열 그룹이 모두 있는 영역, 가로 막대 또는 세로 막대 차트를 사용하여 표시하기에 적합합니다. 차트의 행렬 및 범주 그룹의 열 그룹에 대해 동일한 그룹 식을 사용하고 차트의 행렬 및 계열 그룹의 행 그룹에 대해 동일한 그룹 식을 사용합니다. 그룹 인스턴스의 수가 많아지면 차트를 쉽게 알아볼 수 없다는 점에 유의해야 합니다. 범위 값을 기반으로 그룹을 정의하면 보고서의 그룹 인스턴스 수를 줄일 수 있습니다. 자세한 내용은 [그룹 식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [차트&#40;보고서 작성기 및 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [목록&#40;보고서 작성기 및 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [중첩 된 데이터 영역 &#40;보고서 작성기 및 SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md)  
  
  
