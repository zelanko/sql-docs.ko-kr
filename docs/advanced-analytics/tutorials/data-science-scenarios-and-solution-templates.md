---
title: 데이터 과학 솔루션 템플릿
description: 이 문서에서는 모범 사례를 보여 주고 솔루션을 빠르게 구현할 수 있도록 구성 요소를 제공하는 템플릿을 설명합니다. 각 템플릿은 특정 업종 또는 업계의 특정 문제를 해결하도록 설계되었습니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 01893edd0174ec7aeab262b8aeddc3babb8194f7
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727274"
---
# <a name="data-science-scenarios-and-solution-templates"></a>데이터 과학 시나리오 및 솔루션 템플릿
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

템플릿은 모범 사례를 보여 주고 솔루션을 더 빠르게 구현할 수 있도록 구성 요소를 제공하는 샘플 솔루션입니다. 각 템플릿은 특정 업종 또는 업계의 특정 문제를 해결하도록 설계되었습니다. 각 템플릿의 작업은 데이터 준비 및 기능 엔지니어링에서 모델 학습 및 점수 매기기까지 확장됩니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 작동 방법을 알아보려면 이러한 템플릿을 사용하세요. 그런 다음, 사용자의 시나리오에 맞게 템플릿을 자유롭게 사용자 지정하고 사용자 지정 솔루션을 빌드할 수 있습니다. 

각 솔루션에는 샘플 데이터, R 코드 또는 Python 코드 및 SQL 저장 프로시저(해당하는 경우)가 포함됩니다. SQL Server에서 계산을 수행하여 선호하는 R 또는 Python 개발 환경에서 코드를 실행할 수 있습니다. 경우에 따라 T-SQL 및 SQL Server Management Studio와 같은 모든 SQL 클라이언트 도구를 사용하여 코드를 직접 실행할 수 있습니다.

> [!TIP]
> 
> 대부분의 템플릿은 기계 학습에 온-프레미스 및 클라우드 플랫폼을 모두 지원하는 여러 버전으로 제공됩니다. 예를 들어 SQL Server만 사용하여 솔루션을 빌드하거나 Microsoft R Server 또는 Azure Machine Learning에서 솔루션을 빌드할 수 있습니다.

+ 다운로드 및 설치 지침은 [템플릿 사용 방법](#bkmk_HowTo)을 참조하세요.

## <a name="fraud-detection"></a>사기 검색

[온라인 사기 검색 템플릿(SQL Server R Services)](https://github.com/Microsoft/r-server-fraud-detection)

**내용:** 사기 거래를 검색하는 기능은 온라인 비즈니스에 중요합니다. 환불 손실을 줄이려면 기업에서 도난 당한 결제 방법 또는 자격 증명을 사용하여 수행된 거래를 신속하게 식별해야 합니다. 사기성 거래가 발견되면 비즈니스는 일반적으로 추가 손실을 방지하기 위해 조치를 취하여 특정 계정을 최대한 빨리 차단합니다. 이 시나리오에서는 온라인 구매 거래의 데이터를 사용하여 가능한 사기 행위를 식별하는 방법을 알아봅니다.

**방법:**  사기 검색은 이진 분류 문제로 해결됩니다. 이 템플릿에서 사용되는 방법론은 다른 도메인의 사기 검색에도 쉽게 적용할 수 있습니다.


## <a name="campaign-optimization"></a>캠페인 최적화

[잠재 고객에게 연락하는 방법 및 시기 예측](https://microsoft.github.io/r-server-campaign-optimization/)

**내용:** 이 솔루션은 보험 업계 데이터를 사용하여 인구 통계, 이전의 응답 데이터 및 제품별 세부 정보를 기반으로 잠재 고객을 예측합니다.  구매 행동에 영향을 주기 위한 최적의 채널과 사용자에게 접근하는 시기를 나타내는 권장 사항도 생성됩니다.

**방법:** 이 솔루션은 여러 모델을 만들고 비교합니다. 또한 이 솔루션은 저장 프로시저를 사용한 자동 데이터 통합 및 데이터 준비를 보여줍니다. SQL Server 데이터베이스 내, Azure 및 HDInsight Spark에 병렬 샘플이 제공됩니다. 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>의료: 병원 입원 기간 예측 

[병원 입원 기간 예측](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**내용:** 장기적인 입원이 필요할 수 있는 환자를 정확하게 예측하는 것은 진료 및 계획에 중요한 부분입니다. 관리자는 더 많은 리소스가 필요한 시설을 파악할 수 있어야 하고, 간병인은 환자의 요구 사항을 충족할 수 있다는 확신을 원합니다.

**방법:** 이 솔루션은 Data Science Virtual Machine을 사용하고 기계 학습이 사용 설정된 SQL Server 인스턴스를 포함합니다. 또한 배포된 모델과 상호 작용하는 데 사용할 수 있는 Power BI 보고서 세트를 포함합니다.

## <a name="customer-churn"></a>고객 이탈

[고객 이탈 예측 템플릿(SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/README.md)

**내용:** 고객 이탈을 분석하고 예측하는 일은 경쟁 업체에 빼앗기는 고객을 관리하고 차단해야 하는 금융업, 이동통신업, 소매업 등의 모든 업계에서 중요합니다. 이탈 분석의 목표는 이탈 가능성이 있는 고객을 확인한 다음 적절한 조치를 취하여 해당 고객을 보존하고 비즈니스를 유지하는 것입니다.

**방법:** 이 템플릿은 이탈 문제를 **이진 분류** 문제로 공식화합니다. 고객 인구 통계와 고객 거래의 두 원본에 있는 샘플 데이터를 사용하여 고객을 이탈 가능성이 있거나 없는 것으로 분류합니다.
  
## <a name="predictive-maintenance"></a>예측 유지 관리

[예측 유지 관리 템플릿(SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/README.md)

**내용:** 예측 유지 관리의 목표는 이전 오류를 포착하고 해당 정보를 사용하여 디바이스에서 오류가 발생할 수 있는 시기나 위치를 예측함으로써 유지 관리 작업의 효율성을 높이는 것입니다. 디바이스 노후화를 예측하는 기능은 분산된 데이터 또는 센서를 사용하는 애플리케이션에 특히 유용합니다. IoT(사물 인터넷) 디바이스에서 오류를 모니터링하거나 예측할 때도 이 방법을 적용할 수 있습니다.

**방법:** 이 솔루션은 "서비스 중인 머신에서 언제 오류가 발생하나요?"란 질문에 대한 답변에 중점을 둡니다. 입력 데이터는 항공기 엔진에 대해 시뮬레이트된 센서 측정값을 나타냅니다. 현재 작업 주기, 설정, 센서 측정값 등 엔진의 현재 작동 상태를 모니터링하여 얻은 데이터를 사용하여 다음 세 가지 유형의 예측 모델을 만듭니다.

-   **회귀 모델**- 엔진에서 오류가 발생하기 전에 지속되는 기간을 예측합니다. 샘플 모델은 "TTF(Time to Failure)"라고도 하는 메트릭 "RUL(잔여 내용년수)"을 예측합니다.
  
-   **분류 모델**- 엔진에서 오류가 발생할 가능성이 있는지 여부를 예측합니다.
  
    **이진 분류 모델** 은 특정 기간 내에 엔진에서 오류가 발생할지 여부를 예측합니다.

    **다중 클래스 분류 모델**은 특정 엔진에서 오류가 발생할지 여부를 예측하고 가능한 오류 발생 시간 범위를 제공합니다. 예를 들어 주어진 날짜에 대해 해당 날짜나 주어진 날짜 이후의 일정 기간 동안 디바이스에서 오류가 발생할지 여부를 예측할 수 있습니다.

## <a name="energy-demand-forecasting"></a>에너지 수요 예측

[SQL Server R Services를 사용한 에너지 수요 예측 템플릿](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**내용:** 수요 예측은 에너지, 소매 및 서비스를 비롯한 다양한 분야에서 중요한 문제입니다. 기업은 정확한 수요 예측을 통해 프로덕션 계획과 리소스 할당을 보다 효율적으로 수행하고 다른 중요한 비즈니스 의사 결정을 내릴 수 있습니다. 에너지 분야에서 수요 예측은 에너지 저장 비용을 절감하고 공급 및 수요를 분산하는 데 매우 중요합니다.

**방법:** 이 템플릿에서는 SQL Server R Services를 사용하여 전기 수요를 예측합니다. 예측에 사용되는 모델은 Microsoft R Server에 포함된 고성능 기계 학습 알고리즘인 **rxDForest**를 기반으로 하는 임의 포리스트 회귀 모델입니다. 솔루션에는 수요 시뮬레이터, 모델 학습에 필요한 모든 R 및 T-SQL 코드, 예측 생성 및 보고에 사용할 수 있는 저장 프로시저가 포함되어 있습니다. 


## <a name="bkmk_HowTo"></a>템플릿 사용 방법

각 템플릿에 포함된 파일을 다운로드하려면 GitHub 명령을 사용하거나, 링크를 열고 **Zip 다운로드** 를 클릭하여 모든 파일을 컴퓨터에 저장합니다.  다운로드한 경우 일반적으로 솔루션에 다음 폴더가 포함되어 있습니다.
  
-   **Data**: 각 애플리케이션에 대한 샘플 데이터가 들어 있습니다.
  
-   **R**: 솔루션에 필요한 모든 R 개발 코드가 들어 있습니다. 솔루션에는 Microsoft R Server에서 제공하는 라이브러리가 필요하지만 모든 R IDE를 통해 열고 편집할 수 있습니다. R 코드는 컴퓨팅 컨텍스트를 SQL Server 인스턴스로 설정하여 "데이터베이스 내"에서 컴퓨팅이 수행되도록 최적화되었습니다.
  
-   **SQLR**: 데이터 처리, 기능 엔지니어링, 모델 배포 등의 관련 작업을 수행하는 저장 프로시저를 만들기 위해 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 등의 SQL 환경에서 실행할 수 있는 .sql 파일이 여러 개 들어 있습니다.
  
    폴더에는 모든 스크립트를 호출하고 엔드투엔드 환경을 만들기 위해 실행할 수 있는 PowerShell 스크립트도 들어 있습니다. 환경에 맞게 스크립트를 편집해야 합니다.

## <a name="next-steps"></a>다음 단계

+ [SQL Server 기계 학습 자습서](machine-learning-services-tutorials.md)




