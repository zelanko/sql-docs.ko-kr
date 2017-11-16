---
title: "11 단원: 파티션 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 92eb21a8-5fc4-4999-ad37-1332ce26431d
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 57ed4f364bcc7ca144c6e963c7b550a5dcc1831d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-10-create-partitions"></a>10단원: 파티션 만들기
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

이 단원에서는 파티션을 만듭니다 FactInternetSales 테이블 처리할 수 있는 더 작은 논리적 부분으로 나누는 데 (새로 고침) 다른 파티션과 별개로 합니다. 기본적으로 모델에 포함하는 각 테이블에는 테이블의 열과 행이 모두 들어 있는 파티션이 하나씩 포함되어 있습니다. 연도별; 데이터를 분할할 원하는 FactInternetSales 테이블에 대 한 각 테이블의 5 년에 대해 하나의 파티션을 합니다. 이렇게 하면 각 파티션을 독립적으로 처리할 수 있습니다. 자세한 내용은 [파티션](../analysis-services/tabular-models/partitions-ssas-tabular.md)을 참조하세요.  
  
이 단원에 소요되는 예상 시간: **15분**  
  
## <a name="prerequisites"></a>필수 구성 요소  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [9 단원: 계층 구조 만들기](../analysis-services/lesson-9-create-hierarchies.md)합니다.  
  
## <a name="create-partitions"></a>파티션 만들기  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a>FactInternetSales 테이블에서 파티션을 만들려면  
  
1.  테이블 형식 모델 탐색기에서 확장 **테이블**를 마우스 오른쪽 단추로 클릭 **FactInternetSales** > **파티션을**합니다.  
  
2.  파티션 관리자 대화 상자에서 클릭 **복사**합니다.  
  
3.  **파티션 이름**, 이름을 **FactInternetSales2010**합니다.  
  
    > [!TIP]  
    > 테이블 미리 보기 창에 열 이름 표시 (확인란 선택)의 열 이름 원본에서으로 모델 테이블에 포함 된 해당 열을 볼 수 있습니다. 이는 테이블 미리 보기 창에 모델 테이블의 열이 아니라 원본 테이블의 열이 표시되기 때문입니다.  
  
4.  선택 된 **SQL** 바로 SQL 문을 편집기를 열려면 미리 보기 창의 오른쪽 위에 있는 단추입니다.  
  
    파티션에 특정 기간에 해당하는 행만 포함하려고 하므로 WHERE 절을 포함해야 합니다. WHERE 절은 SQL 문을 사용해서만 만들 수 있습니다.  
  
5.  에 **SQL 문을** 필드에서 복사한 다음 문을 붙여 넣어 기존 문을 바꿉니다.  
  
    ```  
    SELECT   
    [dbo].[FactInternetSales].[ProductKey],  
    [dbo].[FactInternetSales].[CustomerKey],  
    [dbo].[FactInternetSales].[PromotionKey],  
    [dbo].[FactInternetSales].[CurrencyKey],  
    [dbo].[FactInternetSales].[SalesTerritoryKey],  
    [dbo].[FactInternetSales].[SalesOrderNumber],  
    [dbo].[FactInternetSales].[SalesOrderLineNumber],  
    [dbo].[FactInternetSales].[RevisionNumber],  
    [dbo].[FactInternetSales].[OrderQuantity],  
    [dbo].[FactInternetSales].[UnitPrice],  
    [dbo].[FactInternetSales].[ExtendedAmount],  
    [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
    [dbo].[FactInternetSales].[DiscountAmount],  
    [dbo].[FactInternetSales].[ProductStandardCost],  
    [dbo].[FactInternetSales].[TotalProductCost],  
    [dbo].[FactInternetSales].[SalesAmount],  
    [dbo].[FactInternetSales].[TaxAmt],  
    [dbo].[FactInternetSales].[Freight],  
    [dbo].[FactInternetSales].[CarrierTrackingNumber],  
    [dbo].[FactInternetSales].[CustomerPONumber],  
    [dbo].[FactInternetSales].[OrderDate],  
    [dbo].[FactInternetSales].[DueDate],  
    [dbo].[FactInternetSales].[ShipDate]   
    FROM [dbo].[FactInternetSales]  
    WHERE (([OrderDate] >= N'2010-01-01 00:00:00') AND ([OrderDate] < N'2011-01-01 00:00:00'))  
    ```  
  
    이 문은 WHERE 절에 지정된 대로 OrderDate가 2010년인 행의 데이터를 모두 파티션에 포함하도록 지정합니다.  
  
6.  **유효성 검사**를 클릭합니다.  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a>2011년에 대한 파티션을 만들려면  
  
1.  파티션 목록에서 클릭 된 **FactInternetSales2010** 방금 만든 파티션을 만들고 클릭 **복사**합니다.  
  
2.  **파티션 이름**, 형식 **FactInternetSales2011**합니다.  
  
3.  2011년에 해당하는 행만 파티션에 포함되도록 SQL 문에서 WHERE 절을 다음과 같이 바꿉니다.  
  
    ```  
    WHERE (([OrderDate] >= N'2011-01-01 00:00:00') AND ([OrderDate] < N'2012-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2012-year"></a>2012년에 대한 파티션을 만들려면  
  
- 다음과 같은 WHERE 절을 사용 하 여 위의 단계를 따르세요. 
  
    ```  
    WHERE (([OrderDate] >= N'2012-01-01 00:00:00') AND ([OrderDate] < N'2013-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2013-year"></a>2013년에 대한 파티션을 만들려면  
  
- 다음과 같은 WHERE 절을 사용 하 여 위의 단계를 따르세요. 
  
    ```  
    WHERE (([OrderDate] >= N'2013-01-01 00:00:00') AND ([OrderDate] < N'2014-01-01 00:00:00'))  
    ```  
  
#### <a name="to-create-a-partition-for-the-2014-year"></a>2014 년에 대 한 파티션을 만들려면  
  
- 다음과 같은 WHERE 절을 사용 하 여 위의 단계를 따르세요. 
  
    ```  
    WHERE (([OrderDate] >= N'2014-01-01 00:00:00') AND ([OrderDate] < N'2015-01-01 00:00:00'))  
    ```  

## <a name="delete-the-factinternetsales-partition"></a>FactInternetSales 파티션을 삭제합니다
각 연도 대 한 파티션을가지고 FactInternetSales 파티션을 삭제할 수 있습니다. 파티션을 처리할 때 모든 프로세스를 선택 하는 경우 중첩을 하지 않습니다.
#### <a name="to-delete-the-factinternetsales-partition"></a>FactInternetSales 파티션을 삭제 하려면
-  FactInternetSales 파티션을 클릭 한 다음 클릭 **삭제**합니다.



## <a name="process-partitions"></a>파티션 처리  
파티션 관리자에서 확인 된 **마지막 처리** 새 각각에 대 한 열 파티션 이러한 파티션을 처리 되지 않은 방금 만든된 보여 줍니다. 새 파티션을 만들면 파티션 처리 또는 테이블 처리 작업을 실행하여 해당 파티션의 데이터를 새로 고쳐야 합니다.  
  
#### <a name="to-process-the-factinternetsales-partitions"></a>FactInternetSales 파티션을 처리 하려면  
  
1.  클릭 **확인** 파티션 관리자 대화 상자를 닫습니다.  
  
2.  클릭는 **FactInternetSales** 테이블을 클릭는 **모델** 메뉴 > **프로세스** > **파티션 처리**합니다.  
  
3.  파티션 처리 대화 상자에서 확인 **모드** 로 설정 된 **기본값 처리**합니다.  
  
4.  방금 만든 5개의 파티션 각각에 대해 **처리** 열에서 확인란을 선택한 다음 **확인**을 클릭합니다.  

    ![로-테이블 형식-10 단원에서는--파티션 처리](../analysis-services/media/as-tabular-lesson10-process-partitions.png)
  
    가장 자격 증명을 묻는 Windows 사용자 이름 및 2 단원에서에서 지정한 암호를 입력 합니다.  
  
    그러면 **데이터 처리** 대화 상자가 나타나고 각 파티션에 대한 처리 정보가 표시됩니다. 파티션마다 서로 다른 개수의 행이 전송되었음을 확인할 수 있습니다. 이는 각 파티션에 해당 SQL 문의 WHERE 절에 지정된 연도의 행만 포함되어 있기 때문입니다. 처리가 완료되면 계속해서 데이터 처리 대화 상자를 닫습니다.  
  
    ![-테이블 형식-10 단원에서는-프로세스-완료](../analysis-services/media/as-tabular-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>다음 단계
다음 단원으로 이동: [11 단원: 역할 만들기](../analysis-services/lesson-11-create-roles.md)합니다. 

