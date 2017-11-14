---
title: "계산된 테이블 (SSAS 테이블 형식) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3d7ff98a-82a9-4333-a7d3-7a95a6f2caf7
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9e7db92207b2a518c3d697b997a22ed7c076cd0b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-calculated-table-ssas-tabular"></a>계산 테이블 만들기(SSAS 테이블 형식)
  *계산 테이블* 은 DAX 쿼리 또는 식을 기반으로 계산된 개체이며 같은 모델에 포함된 다른 테이블의 전체 또는 일부에서 파생됩니다.  
  
 계산 테이블이 해결할 수 있는 일반적인 디자인 문제는 클라이언트 응용 프로그램의 쿼리 구조로 노출할 수 있도록 특정 컨텍스트에서 롤플레잉 차원을 겉으로 드러내는 것입니다.  롤플레잉 차원은 여러 컨텍스트에 표면화되는 테이블입니다. 전형적인 예에는 외래 키 관계에 따라서 OrderDate, ShipDate, 또는 DueDate으로 표시되는 날짜 테이블이 있습니다. ShipDate의 계산 테이블을 명시적으로 만들면, 쿼리에 사용할 수 있는 다른 테이블처럼 완벽하게 작동되는 독립 실행형 테이블을 갖게 됩니다.  
  
 계산 테이블의 두 번째 용도에는 기존의 다른 테이블에서 필터링된 행 집합이나 열의 하위 집합 또는 상위 집합을 구성하는 작업이 포함됩니다. 이렇게 하면 특정 시나리오를 지원하기 위해 테이블의 변형을 생성하더라도 원래 테이블을 그대로 유지할 수 있습니다.  
  
 계산 테이블을 최대한 활용하려면 적어도 몇 가지 DAX를 알아야 합니다. 테이블의 식으로 작업할 때, 계산 테이블에 (식이 DAX 식인) DAXSource 단일 파티션이 포함된다는 것을 아는 것이 유용할 수 있습니다.  
식에 의해 반환되는 각 열에는 하나의 CalculatedTableColumn이 있으며, SourceColumn은 반환된 열의 이름입니다(비 계산 테이블의 DataColumns과 유사).  
  
## <a name="how-to-create-a-calculated-table"></a>계산 테이블을 만드는 방법  
  
1.  첫째, 테이블 형식 모델에 호환성 수준이 1200 이상일 확인 합니다. SSDT의 모델에서 **호환성 수준** 속성을 확인할 수 있습니다.  
  
2.  데이터 뷰로 전환합니다. 다이어그램 뷰에서는 계산 테이블을 만들 수 없습니다.  
  
3.  **테이블** > **새 계산 테이블**을 선택합니다.  
  
4.  DAX 식을 입력하거나 붙여넣습니다(아래 참조).  
  
5.  테이블 이름을 지정합니다.  
  
6.  모델의 다른 테이블과 관계를 만듭니다. 이 단계에 대한 도움이 필요하면 [두 테이블 간에 관계 만들기&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)를 참조하세요.  
  
7.  모델의 계산 또는 식에 포함된 테이블을 참조하거나 임시 데이터 탐색을 위해 **Excel에서 분석** 을 사용합니다.  
  
### <a name="replicate-a-role-playing-dimension"></a>롤플레잉 차원 복제  
 수식 입력줄에 다른 테이블의 사본을 가져오도록 하는 DAX 수식을 입력합니다. 계산 테이블이 채워진 후에 설명하는 이름을 지정한 다음 특정 역할에 대한 외래 키를 사용하는 관계를 설정합니다. 예를 들어, Adventure Works 데이터베이스에서 Due Date의 계산 테이블을 만들고 DueDateKey를 팩트 테이블에 대한 관계의 기반으로 사용할 수 있습니다.  
  
```  
=DimDate  
```  
  
### <a name="summarized-or-filtered-dataset"></a>요약 또는 필터링된 데이터 집합  
 수식 입력 줄에 원하는 행을 포함하도록 데이터 집합을 조작하거나, 필터링하거나 요약하는 DAX 식을 입력합니다. 이 예는 판매, 색상, 화폐별 그룹이 형성됩니다.  
  
```  
=SUMMARIZECOLUMNS(DimProduct[Color]  
, DimCurrency[CurrencyName]   
, "Sales" , SUM(FactInternetSales[SalesAmount])  
)  
```  
  
### <a name="superset-using-columns-from-multiple-tables"></a>여러 테이블의 열을 사용한 상위 집합  
 수식 입력줄에 여러 테이블의 열을 결합하는 DAX 식을 입력합니다. 이 경우, 쿼리는 각 화폐에 대한 제품 범주 목록을 출력합니다.  
  
```  
=CROSSJOIN(DimProductCategory, DimCurrency)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis services에서 테이블 형식 모델에 대한 호환성 수준](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [데이터 분석 식 &#40; DAX &#41; Analysis Services에서](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5)   
 [테이블 형식 모델의 DAX 이해&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)  
  
  

