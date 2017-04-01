---
title: "2단원: 데이터 보기 및 탐색(데이터 과학 종단 간 연습) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: d3835d6d-e68b-486d-81a0-81b717cc6134
caps.latest.revision: 32
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 26
---
# 2단원: 데이터 보기 및 탐색(데이터 과학 종단 간 연습)
데이터 탐색은 데이터 모델링의 중요한 부분이며 분석에 사용할 데이터 개체의 요약 및 데이터 시각화 검토를 포함합니다. 이 단원에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에 포함된 R 함수를 사용하여 데이터 개체를 살펴보고 그림을 생성합니다.  
  
그런 다음 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]과 함께 설치된 패키지에서 제공하는 새 함수를 사용하여 데이터를 시각화할 그림을 생성합니다.  
  
> [!TIP]  
> 이미 R을 잘 알고 있는 경우  
>   
> 모든 데이터를 다운로드하고 환경을 준비했으므로 RStudio 또는 다른 환경에서 전체 R 스크립트를 실행하고 직접 기능을 살펴볼 수 있습니다. RSQL_Walkthrough.R 파일을 열고 개별 줄을 강조 표시하여 실행하거나 전체 스크립트를 데모로 실행합니다.  
>   
> RevoScaleR 함수에 대한 추가 설명과 R에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 사용하기 위한 팁을 얻으려면 자습서를 계속 진행합니다. 정확히 동일한 스크립트를 사용합니다.  
  
## <a name="verify-downloaded-data-using-sql"></a>SQL을 사용하여 다운로드한 데이터 확인  
먼저 데이터가 올바르게 로드되었는지 확인합니다.  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
    다양한 도구를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 연결하고 확인할 수 있습니다.  
  
    -   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]    
    -   Visual Studio의 서버 탐색기  
  
2.  만든 데이터베이스를 확장합니다. 다음 그림에서는 **서버 탐색기**에 표시된 새 데이터베이스, 테이블 및 함수를 보여 줍니다.  
  
    ![new database objects created by script](../../advanced-analytics/r-services/media/rsql-e2e-ssms-newobjects.PNG "new database objects created by script")  
  
3.  데이터에 대해 간단한 쿼리를 실행할 수도 있습니다. 예를 들어 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 테이블을 마우스 오른쪽 단추로 클릭하고 **상위 1000개의 행 선택** 을 선택하여 이 쿼리를 생성 및 실행합니다.  
  
    ```  
    SELECT TOP 1000 * FROM [dbo].[nyctaxi_sample]  
    ```  
    테이블의 데이터가 보이지 않는 경우 이전 항목의 [문제 해결](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md) 섹션을 참조하세요.
      
4.  데이터의 스키마와 데이터 형식을 보려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 시스템 관리 뷰를 사용할 수 있습니다.  
  
    ```  
    SELECT TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME, COLUMN_DEFAULT  
    FROM [TaxiSample].INFORMATION_SCHEMA.COLUMNS  
    WHERE TABLE_NAME = N'nyctaxi_sample';  
    ```  
  
    > [!TIP]  
    > 데이터 테이블이 어떻게 만들어졌는지에 대한 세부 정보를 보기 위해 `create-db-tb-upload-data.sql`스크립트를 검토할 수도 있습니다.  
  
### <a name="generate-summaries-using-sql"></a>SQL을 사용하여 요약 생성  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 집합 기반 계산을 매우 빠르게 수행할 수 있기 때문에 R에서 사용하기에 적합합니다.  이 연습에서 테이블을 만든 코드를 [Columnstore 인덱스](../Topic/Columnstore%20Indexes%20Guide.md)에 적용하여 계산 속도를 높일 수 있습니다.   
  
```  
SELECT DISTINCT [passenger_count]  
    , ROUND (SUM ([fare_amount]),0) as TotalFares   
    , ROUND (AVG ([fare_amount]),0) as AvgFares  
FROM [dbo].[nyctaxi_sample]  
GROUP BY [passenger_count]   
ORDER BY  AvgFares desc  
```  

다음 단계에서는 SQL Server의 데이터를 사용하여 R을 통해 보다 정교한 요약과 그림을 생성합니다.  
  
## <a name="next-steps"></a>다음 단계  
[R을 사용하여 데이터 보기 및 요약&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/view-and-summarize-data-using-r-data-science-end-to-end-walkthrough.md)  
  
[R을 사용하여 그래프 및 그림 생성&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/create-graphs-and-plots-using-r-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>이전 단원  
[1단원: 데이터 준비&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
## <a name="see-also"></a>관련 항목:  
[Columnstore 인덱스 가이드](../Topic/Columnstore%20Indexes%20Guide.md)  
  
  
  
