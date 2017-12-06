---
title: "데이터 과학 시나리오 및 솔루션 템플릿을 | Microsoft Docs"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 49e54fa9-9b28-44ba-b256-06dad4e8dece
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 962c3044f0cc43ded921635d12b87858affe8123
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="data-science-scenarios-and-solution-templates"></a>데이터 과학 시나리오 및 솔루션 템플릿

템플릿은 모범 사례를 보여 주고 솔루션을 더 빠르게 구현할 수 있도록 구성 요소를 제공하는 샘플 솔루션입니다. 각 템플릿에 특정 세로 축 또는 업계에 대 한 특정 문제를 해결 하도록 설계 되었습니다. 각 템플릿의 작업은 데이터 준비 및 기능 엔지니어링에서 모델 학습 및 점수 매기기까지 확장됩니다. 이러한 서식 파일을 사용 하 여 자세한 방법을 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 작동 합니다. 그런 다음 자유롭게 고유한 시나리오에 맞게 사용자 지정 솔루션을 생성 하는 템플릿을 사용자 지정할 수 있습니다. 

SQL 저장 프로시저는 해당 하는 경우 및 각 솔루션에는 예제 데이터, R 코드 또는 Python 코드가 포함 됩니다. SQL Server에서 수행 하는 계산 된 기본 Python 또는 R 개발 환경에서 코드를 실행할 수 있습니다. 경우에 따라 직접 T-SQL 및 SQL Server Management Studio와 같은 모든 SQL 클라이언트 도구를 사용 하 여 코드를 실행할 수 있습니다.

> [!TIP]
> 
> 템플릿 중 대부분 여러 버전을 지 원하는 온-프레미스 및 클라우드 플랫폼에 대 한 기계 학습 합니다. 예를 들어 SQL Server를 사용 하 여 솔루션을 빌드할 수 있습니다 또는 Microsoft R Server 또는 Azure 기계 학습에서 솔루션을 빌드할 수 있습니다.

+ 세부 정보 및 업데이트에 대 한 참조이 알림은: [Azure 기계 학습에서 새 템플릿을 흥미로운](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

+ 다운로드 및 설치 지침을 참조 하세요. [서식 파일을 사용 하는 방법을](#bkmk_HowTo)합니다.

## <a name="fraud-detection"></a>사기 검색

[온라인 사기 감지 템플릿 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)

**:** 사기성이 있는 트랜잭션을 감지 하는 기능은 온라인 비즈니스에 중요 합니다. 환불 손실을 줄이기 위해 비즈니스 도난된 지불 수단 또는 자격 증명을 사용 하 여 트랜잭션을 신속 하 게 식별 해야 합니다. 사기성 거래가 발견되면 비즈니스는 일반적으로 추가 손실을 방지하기 위해 조치를 취하여 특정 계정을 최대한 빨리 차단합니다. 이 시나리오에서는 가능성이 사기 행위 확인 하기 온라인 구매 트랜잭션에서 데이터를 사용 하는 방법에 설명 합니다.

**방법:** 사기 감지를 이진 분류 문제를 해결 합니다. 이 템플릿에서 사용되는 방법론은 다른 도메인의 사기 검색에도 쉽게 적용할 수 있습니다.


## <a name="campaign-optimization"></a>캠페인 최적화

[방법 및 시기를 예측할 잠재 고객에 게 문의 하](https://microsoft.github.io/r-server-campaign-optimization/)

**:** 이 솔루션에서는 잠재 고객 인구 통계, 기록 응답 데이터 및 제품 관련 세부 정보에 따라 예측할 보험 업계 데이터를 사용 합니다.  권장 사항 최상의 채널 및 구매 동작에 영향을 줍니다 접근 방식 사용자에 게는 시간을 나타내기 위해 생성 됩니다.

**방법:** 솔루션을 만들고 여러 모델을 비교 합니다. 솔루션에는 또한 자동화 된 데이터 통합 및 데이터 준비 저장된 프로시저를 사용 하 여 보여 줍니다. 병렬 샘플 SQL Server에서 데이터베이스, Azure 및 HDInsight Spark에 제공 됩니다. 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>의료 보험: 병원의 지속 예측 

[병원에서 지속 예측](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**:** 주의 및 계획의 중요 한 부분이 어떤 환자 장기 hospitalization 필요할 수를 정확 하 게 예측 합니다. Caregivers 환자의 요구를 충족할 수 있는지를 보장 하려면와 관리자가 더 많은 리소스를 요청 하는 어떤 기능을 결정할 수 해야 합니다.

**방법:** 이 솔루션 데이터 과학 가상 컴퓨터를 사용 하 고 사용 하도록 설정 하는 기계 학습 된 SQL Server의 인스턴스를 포함 합니다. 또한 배포 된 모델와 상호 작용 하는 데 사용할 수 있는 Power BI 보고서 집합을 포함 합니다.

## <a name="customer-churn"></a>고객 데이터

[고객 변동 예측 템플릿 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)

**:** 분석 하 고 있는 고객을 경쟁 업체 손실 관리 및 해야 금지 모든 업계에서 고객 변동을 반드시 예측: 뱅킹, 통신, 및 소매, 등입니다. 이탈 분석의 목표는 이탈 가능성이 있는 고객을 확인한 다음 적절한 조치를 취하여 해당 고객을 보존하고 비즈니스를 유지하는 것입니다.

**방법:** 이 서식 파일에서와 변동을 문제는 **이진 분류** 문제입니다. 고객 인구 통계와 고객 거래의 두 원본에 있는 샘플 데이터를 사용하여 고객을 이탈 가능성이 있거나 없는 것으로 분류합니다.
  
## <a name="predictive-maintenance"></a>예측 유지 관리

[예측 유지 관리 템플릿 (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/Introduction.md)

**:** 예측 유지 관리 오류 지난 캡처하고 해당 정보를 사용 하 여 장치 실패할 수 있습니다 시점이 나 위치를 예측 하 여 유지 관리 작업의 효율성을 증가를 목표로 합니다. 장치 사용 하지 않는 예측 하는 기능 분산된 된 데이터 또는 센서를 사용 하는 응용 프로그램에 특히 유용 합니다. 이 메서드를 모니터링 하거나 IoT (사물 인터넷) 장치에 오류가 예측도 적용할 수 있었습니다.

이 발표에 대 한 자세한 내용은 참조 하십시오: [새 예측 유지 관리 템플릿](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

**방법:** "때 in service 컴퓨터 못합니다?" 질문에 대답할에 중점을 두고이 솔루션 입력 데이터는 항공기 엔진에 대해 시뮬레이트된 센서 측정값을 나타냅니다. 엔진의 현재 작업 등의 조건을 현재 작업 주기, 설정 및 센서 측정을 모니터링에서 가져온 데이터 세 가지 유형의 예측 모델을 만드는 데 사용 됩니다.

-   **회귀 모델**- 엔진에서 오류가 발생하기 전에 지속되는 기간을 예측합니다. 샘플 모델에 대 한 메트릭을 "나머지 연수" (RUL) 라고도 함 "시간에 오류" (TTF)을 예측 합니다.
  
-   **분류 모델**- 엔진에서 오류가 발생할 가능성이 있는지 여부를 예측합니다.
  
    **이진 분류 모델** 예측 하는 엔진 특정 시간 프레임 내에서 실패 합니다.

    **다중 클래스 분류 모델** 특정 엔진 실패할 수 있습니다 및 실패 한 예상 시간 창을 제공 여부를 예측 합니다. 예를 들어 주어진 날짜에 대해 해당 날짜나 주어진 날짜 이후의 일정 기간 동안 장치에서 오류가 발생할지 여부를 예측할 수 있습니다.

## <a name="energy-demand-forecasting"></a>에너지 수요 예측

[SQL Server R services 템플릿을 예측 에너지 요청](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**:**: 에너지, 정품 및 서비스를 포함 하 여 다양 한 도메인에는 중요 한 문제는 수요 예측 합니다. 수요를 정확 하 게 예측 회사 더 나은 프로덕션 계획, 리소스 할당을 수행 하 고 다른 중요 한 비즈니스 결정을 내릴 수 있습니다. 에너지 섹터 수요 예측은 중요 에너지 저장소 비용을 줄이고 공급 및 수요를 분산 합니다.

**방법:** 이 템플릿은 SQL Server R Services를 사용 하 여 전기에 대 한 수요를 예측할 수 있습니다. 예측에 사용 되는 모델에 기반 하는 임의 포리스트 회귀 모델은 **rxDForest**, 고성능 기계 학습 알고리즘 Microsoft R Server에 포함 합니다. 솔루션에는 수요 시뮬레이터, 모델 학습에 필요한 모든 R 및 T-SQL 코드, 예측 생성 및 보고에 사용할 수 있는 저장 프로시저가 포함되어 있습니다. 


## <a name="bkmk_HowTo"></a>서식 파일을 사용 하는 방법

각 템플릿에 포함된 파일을 다운로드하려면 GitHub 명령을 사용하거나, 링크를 열고 **Zip 다운로드** 를 클릭하여 모든 파일을 컴퓨터에 저장합니다.  다운로드한 경우 일반적으로 솔루션에 다음 폴더가 포함되어 있습니다.
  
-   **Data**: 각 응용 프로그램에 대한 샘플 데이터가 들어 있습니다.
  
-   **R**: 솔루션에 필요한 모든 R 개발 코드가 들어 있습니다. 솔루션에는 Microsoft R Server에서 제공하는 라이브러리가 필요하지만 모든 R IDE를 통해 열고 편집할 수 있습니다. R 코드는 계산 컨텍스트를 SQL Server 인스턴스로 설정하여 "데이터베이스 내"에서 계산이 수행되도록 최적화되었습니다.
  
-   **SQLR**: 데이터 처리, 기능 엔지니어링, 모델 배포 등의 관련 작업을 수행하는 저장 프로시저를 만들기 위해 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 등의 SQL 환경에서 실행할 수 있는 .sql 파일이 여러 개 들어 있습니다.
  
    폴더에는 모든 스크립트를 호출하고 종단 간 환경을 만들기 위해 실행할 수 있는 PowerShell 스크립트도 들어 있습니다. 환경에 맞게 스크립트를 편집해야 합니다.

## <a name="next-steps"></a>다음 단계

+ [SQL Server 컴퓨터 학습 자습서](machine-learning-services-tutorials.md)




