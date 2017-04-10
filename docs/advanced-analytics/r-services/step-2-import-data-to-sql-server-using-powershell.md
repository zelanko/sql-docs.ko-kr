---
title: "2단계: PowerShell을 사용하여 SQL Server로 데이터 가져오기(데이터베이스 내 고급 분석 자습서) | Microsoft Docs"
ms.custom: ""
ms.date: "08/05/2016"
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
  - "TSQL"
ms.assetid: 3c5b5145-fa57-455a-b153-0400fc062dc0
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 2단계: PowerShell을 사용하여 SQL Server로 데이터 가져오기(데이터베이스 내 고급 분석 자습서)
이 단계에서는 다운로드한 스크립트 중 하나를 실행하여 연습에 필요한 데이터베이스 개체를 만듭니다. 또한 스크립트는 사용할 대부분의 저장 프로시저를 만들고 지정한 데이터베이스의 테이블에 샘플 데이터를 업로드합니다.  
  
## 스크립트를 실행하여 SQL 개체 만들기  
다운로드한 파일 중에 PowerShell 스크립트가 있어야 합니다. 연습을 위한 환경을 준비하려면 이 스크립트를 실행합니다.  
  
스크립트에서 수행하는 작업은 다음과 같습니다.  
  
-   아직 설치되지 않은 경우 SQL Native Client 및 SQL 명령줄 유틸리티 설치. 이 유틸리티는 **bcp**를 사용하여 데이터베이스에 데이터를 대량 로드하는 데 필요합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 데이터베이스 및 테이블 만들기, 테이블에 데이터 대량 삽입  
  
-   여러 SQL 함수 및 저장 프로시저 만들기  
  
#### 스크립트를 실행하려면  
1.  관리자 권한으로 PowerShell 명령 프롬프트를 열고 다음 명령을 실행합니다.  
  
    ```  
    .\RunSQL_SQL_Walkthrough.ps1  
    ```  
  
    다음 정보를 입력하라는 메시지가 표시됩니다.  
  
    -   [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]이 설치된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스의 이름 또는 주소  
  
    -   인스턴스의 계정에 대한 사용자 이름 및 암호. 사용하는 계정이 데이터베이스를 만들고, 테이블 및 저장 프로시저를 만들고, 테이블에 데이터를 업로드할 수 있어야 합니다.  
  
    -   방금 다운로드한 샘플 데이터 파일의 경로 및 파일 이름. 예를 들어  
  
        `C:\tempRSQL\nyctaxi1pct.csv`  
  
2.  이 단계의 일부로, 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트가 자리 표시자를 스크립트 입력으로 제공한 데이터베이스 이름 및 사용자 이름으로 대체하도록 수정됩니다.  
  
    스크립트를 통해 생성된 저장 프로시저 및 함수를 검토합니다.  
  
    |||  
    |-|-|  
    |**SQL 스크립트 파일 이름**|**함수**|  
    |create-db-tb-upload-data.sql|데이터베이스와 다음 두 개의 테이블을 만듭니다.<br /><br />nyctaxi_sample: 주 NYC Taxi 데이터 집합을 포함합니다. 저장소 및 쿼리 성능 향상을 위해 클러스터형 columnstore 인덱스가 테이블에 추가됩니다. NYC Taxi 데이터 집합의 1% 샘플이 이 테이블에 삽입됩니다.<br /><br />nyc_taxi_models: 학습된 고급 분석 모델을 저장하는 데 사용됩니다.|  
    |fnCalculateDistance.sql|승하차 위치 사이의 직접 거리를 계산하는 스칼라 반환 함수를 만듭니다.|  
    |fnEngineerFeatures.sql|모델 학습을 위한 새로운 데이터 기능을 만드는 테이블 반환 함수를 만듭니다.|  
    |PersistModel.sql|모델을 저장하기 위해 호출할 수 있는 저장 프로시저를 만듭니다. 저장 프로시저는 varbinary 데이터 형식으로 직렬화된 모델을 사용하고 지정된 테이블에 씁니다.|  
    |PredictTipBatchMode.sql|학습된 모델을 호출하여 모델을 사용해서 예측을 만드는 저장 프로시저를 만듭니다. 저장 프로시저는 쿼리를 입력 매개 변수로 사용하고 입력된 행에 대한 점수를 포함하는 숫자 값 열을 반환합니다.|  
    |PredictTipSingleMode.sql|학습된 모델을 호출하여 모델을 사용해서 예측을 만드는 저장 프로시저를 만듭니다. 이 저장 프로시저는 새 관찰을 개별 기능 값이 인라인 매개 변수로 전달되는 입력으로 사용하고 새 관찰의 결과를 예측하는 값을 반환합니다.|  
  
    이 연습의 뒷부분에서는 몇 개의 저장 프로시저를 추가로 만듭니다.  
  
    |||  
    |-|-|  
    |**SQL 스크립트 파일 이름**|**함수**|  
    |PlotHistogram.sql|데이터 탐색을 위한 저장 프로시저를 만듭니다. 이 저장 프로시저는 R 함수를 호출하여 변수 히스토그램을 그린 다음 그림을 이진 개체로 반환합니다.|  
    |PlotInOutputFiles.sql|데이터 탐색을 위한 저장 프로시저를 만듭니다. 이 저장 프로시저는 R 함수를 사용하여 그래픽을 만든 다음 출력을 로컬 PDF 파일로 저장합니다.|  
    |TrainTipPredictionModel.sql|R 패키지를 호출하여 로지스틱 회귀 모델을 학습하는 저장 프로시저를 만듭니다. 모델은 tipped 열의 값을 예측하며 임의로 선택된 70%의 데이터를 사용하여 학습됩니다. 저장 프로시저의 출력은 nyc_taxi_models 테이블에 저장된 학습된 모델입니다.|  
  
3.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 지정한 로그인으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 로그인하여 생성된 데이터베이스, 테이블, 함수 및 저장 프로시저를 볼 수 있는지 확인합니다.  
  
    ![rsql_devtut_BrowseTables](../../advanced-analytics/r-services/media/rsql-devtut-browsetables.PNG "rsql_devtut_BrowseTables")  
  
    > [!NOTE]  
    > 데이터베이스 개체가 이미 있는 경우에는 다시 만들 수 없습니다.  
    >   
    > 테이블이 이미 있는 경우 데이터가 추가되며 덮어쓰지 않습니다. 따라서 스크립트를 실행하기 전에 기존 개체를 모두 삭제해야 합니다.  
  
## 다음 단계  
[3단계: 데이터 탐색 및 시각화](../../advanced-analytics/r-services/step-3-explore-and-visualize-the-data-in-database-advanced-analytics-tutorial.md)  
  
## 이전 단계  
[1단계: 샘플 데이터 다운로드](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md)  
  
## 관련 항목:  
[SQL 개발자를 위한 데이터베이스 내 고급 분석&#40;자습서&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[SQL Server R Services 자습서](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
