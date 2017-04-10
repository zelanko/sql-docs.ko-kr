---
title: "데이터 과학 시나리오 및 솔루션 템플릿 | Microsoft Docs"
ms.custom: ""
ms.date: "04/18/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 49e54fa9-9b28-44ba-b256-06dad4e8dece
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# 데이터 과학 시나리오 및 솔루션 템플릿
템플릿은 모범 사례를 보여 주고 솔루션을 더 빠르게 구현할 수 있도록 구성 요소를 제공하는 샘플 솔루션입니다. 각 템플릿은 특정 문제를 해결하도록 작성되었으며 샘플 데이터, R 코드(Microsoft R Server), SQL 저장 프로시저를 포함합니다. 각 템플릿의 작업은 데이터 준비 및 기능 엔지니어링에서 모델 학습 및 점수 매기기까지 확장됩니다. SQL Server에서 계산을 수행하거나 SQL Server management Studio 등의 SQL 클라이언트 도구를 사용하여 R IDE에서 코드를 실행할 수 있습니다.  
  
이러한 템플릿을 사용하여 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]의 작동 방식을 알아보고, 고유한 시나리오에 맞게 템플릿을 사용자 지정하여 고유한 솔루션을 빌드 및 배포할 수 있습니다.  
  
다운로드 및 설치 지침은 이 항목의 끝에 있는 [템플릿 사용 방법](#bkmk_HowTo)을 참조하세요.  
  
## 사기 검색  
[온라인 사기 검색 템플릿(SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)  
  
온라인 비즈니스에 중요한 작업 중 하나는 지불 거절 손실을 줄이기 위해 사기성 거래를 검색하고 도난당한 결제 방법이나 자격 증명을 통한 거래를 식별하는 것입니다. 사기성 거래가 발견되면 비즈니스는 일반적으로 추가 손실을 방지하기 위해 조치를 취하여 특정 계정을 최대한 빨리 차단합니다. 이 시나리오에서는 온라인 구매 거래의 데이터를 사용하여 가능한 사기 행위를 식별하는 방법을 알아봅니다. 이 방법론은 다른 도메인의 사기 검색에도 쉽게 적용할 수 있습니다.  
  
이 템플릿에서는 온라인 구매 거래의 데이터를 사용하여 가능한 사기 행위를 식별하는 방법을 알아봅니다. 사기 검색은 이진 분류 문제로 해결됩니다. 이 템플릿에서 사용되는 방법론은 다른 도메인의 사기 검색에도 쉽게 적용할 수 있습니다.    
  
## 고객 이탈  
[고객 이탈 예측 템플릿(SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)  
  
고객 이탈을 분석하고 예측하는 일은 경쟁 업체에 빼앗기는 고객을 관리하고 차단해야 하는 금융업, 이동통신업, 소매업 등의 모든 업계에서 중요합니다. 이탈 분석의 목표는 이탈 가능성이 있는 고객을 확인한 다음 적절한 조치를 취하여 해당 고객을 보존하고 비즈니스를 유지하는 것입니다.  
  
이 템플릿은 이탈 문제를 **이진 분류** 문제로 작성하여 이탈 방지를 시작하게 합니다. 고객 인구 통계와 고객 거래의 두 원본에 있는 샘플 데이터를 사용하여 고객을 이탈 가능성이 있거나 없는 것으로 분류합니다.   
  
## 예측 유지 관리  
[예측 유지 관리 템플릿(SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/Introduction.md)  
  
"데이터 기반" 예측 유지 관리의 목표는 이전 오류를 캡처하고 해당 정보를 사용하여 장치에서 오류가 발생할 수 있는 시기나 위치를 예측함으로써 유지 관리 작업의 효율성을 높이는 것입니다. 장치 노후화를 예측하는 능력은 IoT(사물 인터넷)의 예와 같이 분산 데이터 또는 센서를 사용하는 응용 프로그램에 특히 중요합니다.  
  
이 템플릿은 "서비스 중인 컴퓨터에서 언제 오류가 발생하나요?"란 질문에 대한 답변에 중점을 둡니다. 입력 데이터는 항공기 엔진에 대해 시뮬레이트된 센서 측정값을 나타냅니다. 현재 작업 주기, 설정, 센서 측정값 등 엔진의 현재 작동 상태를 모니터링하여 얻은 데이터를 사용하여 다음 세 가지 유형의 예측 모델을 만듭니다.  
  
-   **회귀 모델** - 엔진에서 오류가 발생하기 전에 지속되는 기간을 예측합니다. 샘플 모델은 TTF(Time to Failure)라고도 하는 메트릭 RUL(잔여 내용년수)을 예측합니다.  
  
-   **분류 모델** - 엔진에서 오류가 발생할 가능성이 있는지 여부를 예측합니다.  
  
    **이진 분류 모델**은 특정 기간(일수) 내에 엔진에서 오류가 발생할지 여부를 예측합니다.  
  
    **다중 클래스 분류 모델**은 특정 엔진에서 오류가 발생할지 여부를 예측하고 오류가 발생할 경우 가능한 오류 시간 창을 제공합니다. 예를 들어 주어진 날짜에 대해 해당 날짜나 주어진 날짜 이후의 일정 기간 동안 장치에서 오류가 발생할지 여부를 예측할 수 있습니다.  
      
      
## 에너지 수요 예측  
[SQL Server R Services를 사용한 에너지 수요 예측 템플릿](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast_Template_with_SQL-Server-R-Services-1)  
  
이 템플릿에서는 SQL Server R Services를 사용하여 전기 수요를 예측하는 방법을 보여 줍니다. 솔루션에는 수요 시뮬레이터, 모델 학습에 필요한 모든 R 및 T-SQL 코드, 예측 생성 및 보고에 사용할 수 있는 저장 프로시저가 포함되어 있습니다.   
  
## <a name="bkmk_HowTo"></a>템플릿 사용 방법  
각 템플릿에 포함된 파일을 다운로드하려면 GitHub 명령을 사용하거나, 링크를 열고 **Zip 다운로드**를 클릭하여 모든 파일을 컴퓨터에 저장합니다.  다운로드한 경우 일반적으로 솔루션에 다음 폴더가 포함되어 있습니다.  
  
-   **Data**: 각 응용 프로그램에 대한 샘플 데이터가 들어 있습니다.  
  
-   **R**: 솔루션에 필요한 모든 R 개발 코드가 들어 있습니다. 솔루션에는 Microsoft R Server에서 제공하는 라이브러리가 필요하지만 모든 R IDE를 통해 열고 편집할 수 있습니다. R 코드는 계산 컨텍스트를 SQL Server 인스턴스로 설정하여 "데이터베이스 내"에서 계산이 수행되도록 최적화되었습니다.  
  
-   **SQLR**: 데이터 처리, 기능 엔지니어링, 모델 배포 등의 관련 작업을 수행하는 저장 프로시저를 만들기 위해 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 등의 SQL 환경에서 실행할 수 있는 .sql 파일이 여러 개 들어 있습니다.  
  
    폴더에는 모든 스크립트를 호출하고 종단 간 환경을 만들기 위해 실행할 수 있는 PowerShell 스크립트도 들어 있습니다.  
  
    환경에 맞게 스크립트를 편집해야 합니다.  
  
  
## 관련 항목:  
[SQL Server R Services 자습서](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
[Azure ML에서 템플릿 발표](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)  
[새 예측 유지 관리 템플릿](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)  
  
  
  
