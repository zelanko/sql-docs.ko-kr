---
title: 셀 데이터에 대 한 사용자 지정 액세스 권한 부여 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.celldata.f1
helpviewer_keywords:
- user access rights [Analysis Services], cell data
- permissions [Analysis Services], cells
- read contingent permissions
- read permissions
- cells [Analysis Services]
- custom cell data access [Analysis Services]
ms.assetid: 3b13a4ae-f3df-4523-bd30-b3fdf71e95cf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5db12886384089afe87ffb5fa659c34b09a9fe23
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074975"
---
# <a name="grant-custom-access-to-cell-data-analysis-services"></a>셀 데이터에 대한 사용자 지정 액세스 부여(Analysis Services)
  셀 보안은 큐브 내 측정값 데이터에 대한 액세스를 허용하거나 거부하는 데 사용됩니다. 다음 그림은 특정 측정값에 대한 액세스만 허용된 사용자로 연결했을 때 피벗 테이블에서 허용된 측정값과 거부된 측정값의 조합을 보여 줍니다. 이 예제에서 **재판매인 판매액** 및 **재판매인 총 제품 원가** 는 이 역할을 통해 사용할 수 있는 유일한 측정값입니다. 다른 모든 측정값은 암시적으로 거부됩니다. 이 결과를 얻는 데 사용한 단계는 아래의 다음 섹션인 "특정 측정값에 대한 액세스 허용"에 나와 있습니다.  
  
 ![허용된 셀 및 거부된 셀을 보여 주는 피벗 테이블](../media/ssas-permscellsallowed.png "허용된 셀 및 거부된 셀을 보여 주는 피벗 테이블")  
  
 셀 사용 권한은 셀 내부의 데이터에 적용되며, 메타데이터에는 적용되지 않습니다. 셀이 쿼리 결과에 여전히 나타나며 실제 셀 값 대신 `#N/A` 값을 표시하는 방식을 살펴보세요. 클라이언트 `#N/A` 응용 프로그램에서 값을 변환 하거나 연결 문자열에서 보안 셀 값 속성을 설정 하 여 다른 값을 지정 하지 않으면 셀에 값이 표시 됩니다.  
  
 셀을 완전히 숨기려면 볼 수 있는 멤버 차원, 차원 특성 및 차원 특성 멤버를 제한 해야 합니다. 자세한 내용은 [차원 데이터에 대한 사용자 지정 액세스 권한 부여&#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md)를 참조하세요.  
  
 관리자는 구성원이 큐브 내 셀에 대한 읽기, 불확정 읽기 또는 읽기/쓰기 권한을 갖는지 여부를 지정할 수 있습니다. 셀에 대한 사용 권한 부여는 허용된 가장 낮은 보안 수준이므로 이 수준에서 사용 권한 적용을 시작하기 전에 다음과 같은 사항에 유의하세요.  
  
-   셀 수준 보안은 더 높은 수준에서 제한된 권한을 확장할 수 없습니다. 예제: 한 역할에서 차원 데이터에 대한 액세스를 거부한 경우 셀 수준 보안이 거부된 집합을 재정의할 수 없습니다. 또 다른 예: 큐브에 대 한 `Read` 사용 권한이 있는 역할 및 셀에 대 한 **읽기/쓰기** 권한 권한은 셀 데이터 권한이 **읽기/쓰기가**되지 않습니다. 이는 `Read`입니다.  
  
-   사용자 지정 사용 권한은 보통 차원 구성원과 동일한 역할 내 셀 간에 조정해야 합니다. 예를 들어 다양한 조합의 재판매인에 대해 몇 가지 할인 관련 측정값에 대한 액세스를 거부하려는 경우를 가정해 보겠습니다. 차원 데이터로 **Resellers** , 측정값으로 **Discount Amount** 를 고려할 때 이 항목의 지침을 사용하여 차원 구성원은 물론 두 측정값에 대한 사용 권한을 동일한 역할 내에서 조합해야 합니다. 차원 권한을 설정하는 방법에 대한 자세한 내용은 [차원 데이터에 대한 사용자 지정 액세스 권한 부여&#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) 를 참조하세요.  
  
 셀 수준 보안은 MDX 식을 통해 지정합니다. 셀이 튜플(즉, 잠재적인 다중 차원과 측정값에 걸친 교차점)이므로 MDX를 사용하여 특정 셀을 확인할 필요가 있습니다.  
  
## <a name="allow-access-to-specific-measures"></a>특정 측정값에 대한 액세스 허용  
 셀 보안을 사용하여 사용 가능한 측정값을 명시적으로 선택할 수 있습니다. 허용되는 구성원을 명확하게 식별한 후 다른 모든 구성원은 사용할 수 없게 됩니다. 이 방법은 아래 단계에 설명된 대로 MDX 스크립트를 통해 구현할 수 있는 가장 간단한 시나리오일 것입니다.  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 인스턴스에 연결하고, 데이터베이스를 선택하고, **역할** 폴더를 연 후 데이터베이스 역할을 클릭하거나 새로운 데이터베이스 역할을 만듭니다. 멤버 자격이 이미 지정되어 있어야 하며, 해당 역할에 큐브에 대한 `Read` 권한이 있어야 합니다. 자세한 내용은 [큐브 또는 모델 권한 부여&#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md) 를 참조하세요.  
  
2.  **셀 데이터**에서 큐브 선택을 점검하여 올바른 항목을 선택했는지 확인한 후 **읽기 권한 설정**을 선택합니다.  
  
     이 확인란만 선택하고 MDX 식을 지정하지 않은 경우 큐브의 모든 셀에 대한 액세스를 거부한 것과 동일한 결과를 얻게 됩니다. 이는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 큐브 셀의 하위 집합을 확인할 때마다 기본적으로 허용되는 집합이 빈 집합이기 때문입니다.  
  
3.  다음 MDX 식을 입력합니다.  
  
    ```  
    (Measures.CurrentMember IS [Measures].[Reseller Sales Amount]) OR (Measures.CurrentMember IS [Measures].[Reseller Total Product Cost])  
    ```  
  
     이 식은 사용자가 볼 수 있는 측정값을 명시적으로 식별합니다. 다른 측정값은 이 역할을 통해 연결된 사용자가 사용할 수 없습니다. [CurrentMember&#40;MDX&#41;](/sql/mdx/current-mdx)에서 컨텍스트를 설정한 다음 허용된 측정값이 표시됩니다. 이 식의 결과로 현재 구성원에 **재판매인 판매액** 또는 **재판매인 총 제품 원가**가 포함된 경우 해당 값이 표시됩니다. 그렇지 않으면 액세스가 거부됩니다. 이 식에는 각각 괄호로 묶인 부분이 여러 개 있습니다. `OR` 연산자는 여러 측정값을 지정하는 데 사용됩니다.  
  
## <a name="deny-access-to-specific-measures"></a>특정 측정값에 대한 액세스 거부  
 **역할** | 만들기**셀 데이터** | **큐브 내용을 읽을 수**있습니다에도 지정 된 다음 MDX 식은 그 반대의 영향을 받아 특정 측정값을 사용할 수 없게 됩니다. `NOT` 이 예에서는 및 `AND` 연산자를 사용 하 여 **할인 금액** 및 **할인율** 을 사용할 수 없습니다. 다른 모든 측정값은 이 역할을 통해 연결된 사용자가 볼 수 있습니다.  
  
```  
(NOT Measures.CurrentMember IS [Measures].[Discount Amount]) AND (NOT Measures.CurrentMember IS [Measures].[Discount Percentage])  
```  
  
 Excel에서 셀 보안은 다음 그림과 같이 명확합니다.  
  
 ![셀을 사용할 수 없음으로 표시하는 Excel 열](../media/ssas-permscellshidemeasure.png "셀을 사용할 수 없음으로 표시하는 Excel 열")  
  
## <a name="set-read-permissions-on-calculated-measures"></a>계산된 측정값에 대한 읽기 권한 설정  
 계산된 측정값에 대한 사용 권한은 해당 구성 요소와는 별도로 설정할 수 있습니다. 계산된 측정값과 종속 측정값 사이에 사용 권한을 조정하려는 경우에는 불확정 읽기에 대한 다음 섹션으로 건너뛰세요.  
  
 읽기 권한이 계산된 측정값에 어떻게 작용하는지 이해하려면 AdventureWorks의 **Reseller Gross Profit** 을 살펴보세요. 이 측정값은 **Reseller Sales Amount** 및 **Reseller Total Product Cost** 측정값에서 파생됩니다. 역할에 **Reseller Gross Profit** 셀에 대한 읽기 권한이 있는 한 다른 측정값에서 사용 권한이 명시적으로 거부되는 경우에도 이 측정값은 볼 수 있습니다. 데모용으로 다음 MDX 식을 **역할** | 만들기**셀 데이터** | 를 사용 하 여**큐브 내용을 읽을 수**있습니다.  
  
```  
(NOT Measures.CurrentMember IS [Measures].[Reseller Sales Amount])  
AND (NOT Measures.CurrentMember IS [Measures].[Reseller Total Product Cost])  
```  
  
 Excel에서 현재 역할을 사용하여 큐브에 연결하고 세 가지 측정값을 모두 선택하여 셀 보안 결과를 살펴보세요. 거부된 집합의 측정값은 사용할 수 없지만 계산된 측정값은 사용자에게 표시됩니다.  
  
 ![사용 가능한 셀 및 사용 불가능한 셀이 있는 Excel 테이블](../media/ssas-permscalculatedcells.png "사용 가능한 셀 및 사용 불가능한 셀이 있는 Excel 테이블")  
  
## <a name="set-read-contingent-permissions-on-calculated-measures"></a>계산된 측정값에 대한 불확정 읽기 권한 설정  
 셀 보안에서는 계산에 포함되는 관련 셀에 대한 사용 권한을 설정하는 데 대체 권한인 불확정 읽기를 제공합니다. **Reseller Gross Profit** 예제를 다시 생각해 보세요. 이전 섹션에서 제공 된 것과 동일한 MDX 식을 입력 하는 경우이 시간을 **역할** | **셀 데이터** 만들기 대화 상자의 두 번째 텍스트 영역 ( **셀 보안에 따라 셀 내용을 읽을 수**있습니다. 아래 텍스트 영역)에 배치 하면 Excel에서 볼 때 결과가 표시 됩니다. **Reseller Gross Profit** 이 **Reseller Sales Amount** 및 **Reseller Total Product Cost**에 따라 달라지기 때문에 이제 해당 구성 요소에 액세스할 수 없으므로 매출 총 이익에도 액세스할 수 없습니다.  
  
> [!NOTE]  
>  동일한 역할 내 특정 셀에 대해 읽기와 불확정 읽기 권한을 둘 다 설정하는 경우 어떻게 됩니까? 역할에 셀에 대한 읽기 권한은 있지만, 불확정 읽기 권한은 없습니다.  
  
 **불확정 읽기 권한 설정** 확인란만 선택하고 MDX 식을 지정하지 않으면 큐브의 모든 셀에 대한 액세스가 거부된다는 앞의 섹션 내용을 상기해 보세요. 이는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 큐브 셀의 하위 집합을 확인할 때마다 기본적으로 허용되는 집합이 빈 집합이기 때문입니다.  
  
## <a name="set-readwrite-permissions-on-a-cell"></a>셀에 대한 읽기/쓰기 권한 설정  
 구성원에게 큐브 자체에 대한 읽기/쓰기 권한이 있다면 셀에 대한 읽기/쓰기 권한은 쓰기 저장을 사용하도록 설정하는 데 사용됩니다. 셀 수준에서 부여되는 사용 권한은 큐브 수준에서 부여되는 사용 권한보다 클 수 없습니다. 자세한 내용은 [Set Partition Writeback](set-partition-writeback.md) 를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [MDX 작성기 &#40;Analysis Services 다차원 데이터&#41;](../mdx-builder-analysis-services-multidimensional-data.md)   
 [MDX &#40;기본 MDX 스크립트&#41;](mdx/the-basic-mdx-script-mdx.md)   
 [Analysis Services&#41;&#40;처리 권한 부여](grant-process-permissions-analysis-services.md)   
 [차원 &#40;Analysis Services&#41;에 대 한 권한을 부여 합니다.](grant-permissions-on-a-dimension-analysis-services.md)   
 [차원 데이터 &#40;Analysis Services&#41;에 대 한 사용자 지정 액세스 권한 부여](grant-custom-access-to-dimension-data-analysis-services.md)   
 [큐브 또는 모델 권한 부여&#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)  
  
  
