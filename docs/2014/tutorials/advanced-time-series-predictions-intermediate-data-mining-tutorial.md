---
title: 고급 시계열 예측 (중급 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b614ebdb-07ca-44af-a0ff-893364bd4b71
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2d26b05a6d6929947054cd1546b46a976aa2dc2c
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312921"
---
# <a name="advanced-time-series-predictions-intermediate-data-mining-tutorial"></a>고급 시계열 예측(중급 데이터 마이닝 자습서)
  예측 모델 탐색을 통해 대부분 지역의 판매는 유사한 패턴을 따르지만 태평양 지역의 M200 모델과 같이 특정 지역 및 모델은 서로 매우 다른 추세를 보여 준다는 사실을 알았습니다. 이는 놀라운 일이 아니고 알려진 바와 같이 지역 간 차이는 일반적인 것이며 마케팅 홍보, 정확하지 않은 보고 또는 지정학적 사건과 같은 많은 요인으로 인해 발생할 수 있습니다.  
  
 그러나 사용자가 전 세계에 적용될 수 있는 모델을 요청할 수도 있습니다. 따라서 개별적인 요인이 예측에 끼치는 영향을 최소화하기 위해 전 세계 판매의 집계 측정값을 기반으로 하는 모델을 작성하기로 합니다. 그런 다음 이 모델을 사용하여 각 개별 지역에 대해 예측할 수 있습니다.  
  
 이 태스크에서는 고급 예측 태스크를 수행하는 데 필요한 모든 데이터 원본을 작성합니다. 예측 쿼리에 대한 입력으로 사용할 데이터 원본 뷰 두 개와 새 모델을 만드는 데 사용할 데이터 원본 뷰 하나를 만듭니다.  
  
 **단계**  
  
1.  [확장된 판매 데이터 준비 (예측) 용](#bkmk_newExtendData)  
  
2.  [집계 된 데이터 (모델 작성용) 준비](#bkmk_newReplaceData)  
  
3.  [계열 데이터 준비 (교차 예측) 용](#bkmk_CrossData2)  
  
4.  [EXTEND를 사용한 예측](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
5.  [교차 예측 모델 만들기](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
6.  [REPLACE를 사용한 예측](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
7.  [새 예측 검토](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
##  <a name="bkmk_newExtendData"></a> 새로운 확장된 판매 데이터 생성  
 판매 데이터를 업데이트하려면 최신 판매 수치가 필요합니다. 신규 매장에 대한 관심을 불러일으키고 해당 제품의 인지도를 높이기 위해 지역 판매 홍보를 실시한 태평양 지역 내 데이터는 특히 중요합니다.  
  
 이 시나리오에서는 두 군데 지역에 대한 3개월 동안의 신규 데이터가 들어 있는 Excel 통합 문서에서 데이터를 가져온 것으로 가정합니다. Transact-SQL 스크립트를 사용하는 데이터용 테이블을 만든 다음 예측에 사용할 데이터 원본 뷰를 정의합니다.  
  
#### <a name="create-the-table-with-new-sales-data"></a>새 판매 데이터가 있는 테이블 만들기  
  
1.  Transact-SQL 쿼리 창에서 다음 문을 실행하여 판매 데이터를 AdventureWorksDW 데이터베이스 또는 기타 데이터베이스에 추가합니다.  
  
    ```  
    USE [database name];  
    GO  
    IF OBJECT_ID ([dbo].[NewSalesData]) IS NOT NULL   
        DROP TABLE [dbo].[NewSalesData];  
    GO  
    CREATE TABLE [dbo].[NewSalesData]([Series] [nvarchar](255) NULL,  
    [NewDate] [datetime] NULL,  
    [NewQty] [float] NULL,  
    [NewAmount] [money] NULL) ON [PRIMARY]  
  
    GO  
    ```  
  
2.  다음 스크립트를 사용하여 새 값을 삽입합니다.  
  
    ```  
    INSERT INTO [NewSalesData]  
    (Series,NewDate,NewQty,NewAmount)  
    VALUES('T1000 Pacific', '7/25/08', 55, '$130,170.22'),  
    ('T1000 Pacific', '8/25/08', 50, '$114,435.36 '),  
    ('T1000 Pacific', '9/25/08', 50, '$117,296.24 '),  
    ('T1000 Europe', '7/25/08', 37, '$88,210.00 '),  
    ('T1000 Europe', '8/25/08', 41, '$97,746.00 '),  
    ('T1000 Europe', '9/25/08', 37, '$88,210.00 '),  
    ('T1000 North America', '7/25/08', 69, '$164,500.00 '),  
    ('T1000 North America', '8/25/08', 66, '$157,348.00 '),  
    ('T1000 North America', '9/25/08', 58, '$138,276.00 '),  
    ('M200 Pacific', '7/25/08', 65, '$149,824.35'),  
    ('M200 Pacific', '8/25/08', 54,  '$124,619.46'),  
    ('M200 Pacific', '9/25/08', 61, '$141,143.39'),  
    ('M200 Europe', '7/25/08', 75, '$173,026.00'),  
    ('M200 Europe', '8/25/08', 76, '$175,212.00'),  
    ('M200 Europe', '9/25/08', 84, '$193,731.00'),  
    ('M200 North America', '7/25/08', 94, '$216,916.00'),  
    ('M200 North America', '8/25/08', 94, '$216,891.00'),  
    ('M200 North America', '9/25/08', 91,'$209,943.00');  
    ```  
  
    > [!WARNING]  
    >  쉼표 구분 기호 및 통화 기호 사용 시 발생하는 문제를 방지하기 위해 따옴표가 통화 값에 사용됩니다. 이 서식에 통화 값에 전달할 수 있습니다. `130170.22`  
    >   
    >  예제 데이터베이스에 사용된 날짜가 이 릴리스에 맞게 변경되었습니다. 이전 버전의 AdventureWorks를 사용하는 경우에는 이에 따라 삽입된 날짜를 조정해야 할 수 있습니다.  
  
###  <a name="bkmk_newReplaceData"></a> 새 판매 데이터를 사용 하 여 데이터 원본 뷰 만들기  
  
1.  **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **데이터 원본 뷰**를 선택한 후 **새 데이터 원본 뷰**합니다.  
  
2.  데이터 원본 뷰 마법사에서 다음을 선택합니다.  
  
     **데이터 원본**: [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]  
  
     **테이블 및 뷰 선택**: NewSalesData 만들어지면 방금 테이블을 선택 합니다.  
  
3.  **마침**을 클릭합니다.  
  
4.  데이터 원본 뷰 디자인 화면에서 NewSalesData를 마우스 오른쪽 단추로 클릭 한 다음 선택 **데이터 탐색** 데이터를 확인 하려면.  
  
> [!WARNING]  
>  이 데이터는 예측에만 사용하므로 데이터는 불완전해도 상관없습니다.  
  
##  <a name="bkmk_CrossData2"></a> 교차 예측 모델에 대 한 데이터 만들기  
 원래에서 사용 된 데이터는 여러 자전거 모델이 더 적은 수의 범주를 축소 하 고 개별 국가의 결과가 영역에 병합 vTimeSeries 뷰에 의해 일부 그룹화 예측 모델은 이미 있습니다. 전 세계 예측에 사용할 수 있는 모델을 만들기 위해 데이터 원본 뷰 디자이너에서 직접 추가 단순 집계를 생성합니다. 새 데이터 원본 뷰에는 전 지역의 모든 제품 판매에 대한 합계와 평균만 포함됩니다.  
  
 모델에 사용할 데이터 원본을 만든 후에는 예측에 사용할 새 데이터 원본 뷰를 만들어야 합니다. 예를 들어, 새로운 전 세계 모델을 사용하여 유럽 지역의 판매를 예측하려는 경우 유럽 지역의 데이터만 넣어야 합니다. 따라서 원래 데이터를 필터링하는 새 데이터 원본 뷰를 설정하고 각 예측 쿼리 집합에 대한 필터 조건을 변경합니다.  
  
#### <a name="to-create-the-model-data-using-a-custom-data-source-view"></a>사용자 지정 데이터 원본 뷰를 사용하여 모델 데이터를 만들려면  
  
1.  **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **데이터 원본 뷰**를 선택한 후 **새 데이터 원본 뷰**합니다.  
  
2.  마법사 시작 페이지에서 **다음**을 클릭합니다.  
  
3.  에 **데이터 원본 선택** 페이지 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)], 클릭 하 고 **다음**합니다.  
  
4.  **테이블 및 뷰 선택**페이지에서 테이블을 추가하지 않고 **다음**을 클릭합니다.  
  
5.  페이지에서 **마법사 완료**를 이름을 입력 `AllRegions`, 클릭 하 고 **마침**합니다.  
  
6.  다음으로 빈 데이터 원본 뷰 디자인 화면을 마우스 오른쪽 단추로 클릭 한 다음 선택 **새 명명 된 쿼리**합니다.  
  
7.  에 **명명 된 쿼리 만들기** 대화 상자에 대 한 **이름**, 형식 `AllRegions`, 및에 대 한 **설명**, 형식 **합계 및 모든 모델에 대 한 판매의 평균 및 영역**합니다.  
  
8.  SQL 텍스트 창에 다음 문을 입력한 다음 확인을 클릭합니다.  
  
    ```  
    SELECT ReportingDate,   
    SUM([Quantity]) as SumQty, AVG([Quantity]) as AvgQty,  
    SUM([Amount]) AS SumAmt, AVG([Amount]) AS AvgAmt,  
    'All Regions' as [Region]  
    FROM dbo.vTimeSeries   
    GROUP BY ReportingDate  
    ```  
  
9. 마우스 오른쪽 단추로 클릭는 `AllRegions` 테이블을 선택한 다음 **데이터 탐색**합니다.  
  
###  <a name="bkmk_CrossData"></a> 교차 예측 용 계열 데이터를 만들려면  
  
1.  **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **데이터 원본 뷰**를 선택한 후 **새 데이터 원본 뷰**합니다.  
  
2.  데이터 원본 뷰 마법사에서 다음을 선택합니다.  
  
     **데이터 원본**: [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]  
  
     **테이블 및 뷰 선택**: 어떤 테이블도 선택하지 않습니다.  
  
     **이름**: `T1000 Pacific Region`  
  
3.  **마침**을 클릭합니다.  
  
4.  에 대 한 빈 디자인 화면을 마우스 오른쪽 단추로 클릭 **T1000 Pacific Region.dsv**를 선택한 후 **새 명명 된 쿼리**합니다.  
  
     **명명된 쿼리 만들기** 대화 상자가 나타납니다. 이름을 다시 입력한 후 설명을 추가합니다.  
  
     **이름**: `T1000 Pacific Region`  
  
     **설명**: **필터`vTimeSeries`지역과 모델 별로**  
  
5.  텍스트 창에 다음 쿼리를 입력한 다음 확인을 클릭합니다.  
  
    ```  
    SELECT ReportingDate, ModelRegion, Quantity, Amount  
    FROM dbo.vTimeSeries  
    WHERE (ModelRegion = N'T1000 Pacific')  
    ```  
  
    > [!NOTE]  
    >  각 계열에 대한 예측을 개별적으로 생성해야 할 수 있으므로 다른 데이터 계열에 다시 사용할 수 있도록 쿼리 텍스트를 복사하고 텍스트 파일에 저장할 수도 있습니다.  
  
6.  데이터 원본 뷰 디자인 화면에서 T1000 Pacific을 마우스 오른쪽 단추로 클릭 한 다음 선택 **데이터 탐색** 데이터가 올바르게 필터링 되었는지 확인 합니다.  
  
     교차 예측 쿼리를 생성할 때 이 데이터를 모델에 대한 입력으로 사용합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [업데이트 된 데이터를 사용 하 여 시계열 예측 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 시계열 알고리즘](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Microsoft 시계열 알고리즘 기술 참조](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [다차원 모델의 데이터 원본 뷰](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  