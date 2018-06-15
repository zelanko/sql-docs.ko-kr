---
title: 디자인 모드에서 DirectQuery 모델에 샘플 데이터 추가 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ca4c4c2a00eed80e709602084cf5de427134977
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34041637"
---
# <a name="add-sample-data-to-a-directquery-model-in-design-mode"></a>디자인 모드에서 DirectQuery 모델에 샘플 데이터 추가
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
 DirectQuery 모드에서는 모델링 디자인 중에 사용하는 샘플 데이터 하위 집합을 만들거나 전체 데이터 뷰의 대안을 만들기 위해 테이블 파티션을 사용합니다.
 
 DirectQuery 테이블 형식 모델을 배포하는 경우 테이블당 파티션 한 개만 허용되며 해당 파티션은 전체 데이터 뷰여야 합니다. 추가 파티션은 전체 데이터 뷰 또는 샘플 데이터를 대체합니다. 이 항목에서는 데이터 하위 집합을 사용하여 샘플 파티션을 만드는 방법을 설명합니다.
 
 기본적으로 SSDT에서 DirectQuery 모드로 테이블 형식 모델을 디자인하는 경우 모델의 작업 데이터베이스에 데이터가 포함되지 않습니다. 각 테이블마다 하나의 기본 파티션이 있으며, 이 파티션이 모든 쿼리를 데이터 원본으로 보냅니다. 
  
그러나 디자인 타임에 사용하기 위해 모델의 작업 데이터베이스에 소량의 샘플 데이터를 추가할 수 있습니다. 샘플 데이터는 디자인 중에만 사용되는 샘플 파티션에 대한 쿼리를 통해 지정됩니다. 해당 데이터는 모델과 함께 메모리에 캐시됩니다. 이렇게 하면 작업을 진행하면서 데이터 원본에 영향을 주지 않고 모델링 결정의 유효성을 검사하는 데 도움이 됩니다. SSDT(SQL Server Data Tools)의 **Excel에서 분석** 을 사용할 때 또는 작업 영역 데이터베이스에 연결하는 다른 클라이언트 응용 프로그램에서 샘플 데이터 집합으로 모델링 결정을 테스트할 수 있습니다.  
  
> [!TIP]  
>  빈 모델의 DirectQuery 모드에서도 항상 각 테이블에 대해 작은 기본 제공 행 집합이 표시됩니다. 50행 데이터 집합을 보려면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 **테이블** > **테이블 속성** 을 클릭합니다.  
  
## <a name="create-a-sample-partition"></a>샘플 파티션 만들기
 이러한 지침은 테이블 형식 모델에서 만들거나 호환성 수준 1200 이상으로 업그레이드 됩니다. 더 낮은 호환성 수준의 모델은 다른 속성을 사용하여 캐시된 데이터를 가져옵니다. 속성 설명은 [SSMS에서 DirectQuery 모드 사용](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md) 을 참조하세요.  
  
1.  SQL Server Data Tools, 다이어그램 또는 데이터 뷰에서 팩트 테이블을 클릭하여 해당 속성 페이지를 엽니다. 팩트 테이블은 모델의 집계된 수치 데이터 및 측정값을 제공합니다. 두 개 이상을 가질 수 있습니다.  
  
2.  **테이블** > **속성** 을 클릭하여 파티션 관리 대화 상자를 엽니다.  
  
    기본 파티션에 **(Direct Query) \<테이블 이름 >** 합니다. 전체 데이터 뷰입니다. 이 파티션을 삭제하지 마세요. 이 파티션은 모델을 배포할 때 사용됩니다.  
  
4.  파티션을 선택하고 **복사**를 클릭합니다.  

    기본 파티션의 복사본이 생성됩니다. 그러나 이 복사본에는 쿼리에서 지정한 샘플 데이터가 포함됩니다. 예를 들어:
  
     ![ssas_tabularproject_copypartition](../../analysis-services/tabular-models/media/ssas-tabularproject-copypartition.jpg "ssas_tabularproject_copypartition")  
  
5.  복사된 파티션을 선택한 다음 **SQL 쿼리 편집기** 단추를 클릭하여 필터를 추가합니다. 모델을 작성하는 동안 샘플 데이터 크기를 줄입니다. 예를 들어 AdventureWorksDW에서 **FactInternetSales** 를 선택한 경우 필터는 다음과 같습니다.  
  
    ```  
    SELECT [dbo].[FactInternetSales].* FROM [dbo].[FactInternetSales]  
    JOIN DimSalesTerritory as ST  
    ON ST.SalesTerritoryKey = FactInternetSales.SalesTerritoryKey  
    WHERE ST.SalesTerritoryGroup='North America';  
    ```  
  
6.  **유효성 검사** 를 클릭하여 구문 오류를 검사합니다.  
  
     DirectQuery 모드에는 파티션 대화 상자의 **새로 만들기** , **복사**및 **삭제** 단추 외에도 **샘플로 설정** 또는 **DirectQuery로 설정**으로 번갈아 표시되는 토글 단추도 있습니다.  
  
     파티션 한 개만이 DirectQuery 파티션일 수 있습니다. 테이블에 대해 정의된 파티션을 선택하고 **샘플로 설정**을 클릭하여 이를 제어할 수 있습니다.  
  
7.  테이블을 처리합니다.  
  


  
  
