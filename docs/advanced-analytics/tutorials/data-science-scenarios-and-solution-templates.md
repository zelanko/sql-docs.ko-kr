---
title: 데이터 과학 시나리오 및 솔루션 템플릿
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 313b00ff9c3863e8cd1c3de3b0919fc130b01d1e
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714933"
---
# <a name="data-science-scenarios-and-solution-templates"></a>데이터 과학 시나리오 및 솔루션 템플릿
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

템플릿은 모범 사례를 보여 주고 솔루션을 더 빠르게 구현할 수 있도록 구성 요소를 제공하는 샘플 솔루션입니다. 각 템플릿은 특정 수직 또는 업계에 대 한 특정 문제를 해결 하도록 설계 되었습니다. 각 템플릿의 작업은 데이터 준비 및 기능 엔지니어링에서 모델 학습 및 점수 매기기까지 확장됩니다. 이러한 템플릿을 사용 하 여가 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 작동 하는 방법을 알아보세요. 그런 다음 사용자의 시나리오에 맞게 템플릿을 자유롭게 사용자 지정 하 고 사용자 지정 솔루션을 빌드할 수 있습니다. 

각 솔루션에는 샘플 데이터, R 코드 또는 Python 코드 및 SQL 저장 프로시저 (해당 하는 경우)가 포함 됩니다. SQL Server에서 계산을 수행 하 여 선호 하는 R 또는 Python 개발 환경에서 코드를 실행할 수 있습니다. 경우에 따라 T-sql 및 SQL Server Management Studio와 같은 모든 SQL 클라이언트 도구를 사용 하 여 코드를 직접 실행할 수 있습니다.

> [!TIP]
> 
> 대부분의 템플릿은 기계 학습을 위해 온-프레미스 및 클라우드 플랫폼을 모두 지 원하는 여러 버전으로 제공 됩니다. 예를 들어 SQL Server만 사용 하 여 솔루션을 빌드하거나 Microsoft R Server 또는 Azure Machine Learning에서 솔루션을 빌드할 수 있습니다.

+ 다운로드 및 설정 지침은 [템플릿 사용 방법](#bkmk_HowTo)을 참조 하세요.

## <a name="fraud-detection"></a>사기 검색

[온라인 사기 검색 템플릿 (SQL Server R Services)](https://github.com/Microsoft/r-server-fraud-detection)

**이며** 사기성 트랜잭션을 검색 하는 기능은 온라인 비즈니스에 중요 합니다. 다시 요금 손실을 줄이기 위해 기업은 도난당 한 결제 방법 또는 자격 증명을 사용 하 여 만든 트랜잭션을 신속 하 게 식별 해야 합니다. 사기성 거래가 발견되면 비즈니스는 일반적으로 추가 손실을 방지하기 위해 조치를 취하여 특정 계정을 최대한 빨리 차단합니다. 이 시나리오에서는 온라인 구매 거래의 데이터를 사용 하 여 사기 행위를 식별 하는 방법을 알아봅니다.

**얼마나**  사기 검색은 이진 분류 문제로 해결됩니다. 이 템플릿에서 사용되는 방법론은 다른 도메인의 사기 검색에도 쉽게 적용할 수 있습니다.


## <a name="campaign-optimization"></a>캠페인 최적화

[잠재 고객에 게 연락 하는 방법 및 시기 예측](https://microsoft.github.io/r-server-campaign-optimization/)

**이며** 이 솔루션은 보험 업계 데이터를 사용 하 여 인구 통계, 기록 응답 데이터 및 제품별 세부 정보를 기반으로 잠재 고객을 예측 합니다.  사용자가 구매 동작에 영향을 줄 수 있는 최상의 채널과 시간을 나타내는 권장 사항도 생성 됩니다.

**얼마나** 솔루션은 여러 모델을 만들고 비교 합니다. 또한 솔루션에서는 저장 프로시저를 사용 하 여 자동화 된 데이터 통합 및 데이터 준비를 보여 줍니다. 병렬 샘플은 데이터베이스 내, Azure 및 HDInsight Spark에 SQL Server 제공 됩니다. 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>의료 보험: 병원에 유지 되는 기간 예측 

[병원의 유지 기간 예측](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**이며** 장기적인 입원 필요할 수 있는 환자을 정확 하 게 예측 하는 것은 주의 및 계획의 중요 한 부분입니다. 관리자는 더 많은 리소스를 필요로 하는 기능을 결정 하 고, 환자의 요구를 충족할 수 있도록 보장 하려고 수치가 합니다.

**얼마나** 이 솔루션은 Data Science Virtual Machine를 사용 하 고 Machine learning을 사용 하는 SQL Server 인스턴스를 포함 합니다. 또한 배포 된 모델과 상호 작용 하는 데 사용할 수 있는 Power BI 보고서 집합을 포함 합니다.

## <a name="customer-churn"></a>고객 이탈

[고객 이탈 예측 템플릿 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/README.md)

**이며** 고객 이탈을 분석 하 고 예측 하는 것은 경쟁 업체에 대 한 고객의 손실을 관리 하 고 방지할 수 있는 모든 업계에서 중요 합니다. 이탈 분석의 목표는 이탈 가능성이 있는 고객을 확인한 다음 적절한 조치를 취하여 해당 고객을 보존하고 비즈니스를 유지하는 것입니다.

**얼마나** 이 템플릿은 변동 문제를 **이진 분류** 문제로 공식화 합니다. 고객 인구 통계와 고객 거래의 두 원본에 있는 샘플 데이터를 사용하여 고객을 이탈 가능성이 있거나 없는 것으로 분류합니다.
  
## <a name="predictive-maintenance"></a>예측 유지 관리

[예측 유지 관리 템플릿 (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/README.md)

**이며** 예측 유지 관리는 과거의 오류를 캡처하고 해당 정보를 사용 하 여 장치가 실패할 때를 예측 함으로써 유지 관리 작업의 효율성을 높입니다. 장치 노후화을 예측 하는 기능은 분산 된 데이터 또는 센서를 사용 하는 응용 프로그램에 특히 유용 합니다. IoT (사물 인터넷) 장치에서 오류를 모니터링 하거나 예측 하는 데에도이 방법을 적용할 수 있습니다.

**얼마나** 이 솔루션은 "서비스 내 컴퓨터가 언제 실패할 것인가?" 라는 질문에 대 한 대답을 중점적으로 다룹니다. 입력 데이터는 항공기 엔진에 대해 시뮬레이트된 센서 측정값을 나타냅니다. 현재 작업 주기, 설정 및 센서 측정과 같은 엔진의 현재 작업 상태를 모니터링 하 여 얻은 데이터는 세 가지 유형의 예측 모델을 만드는 데 사용 됩니다.

-   **회귀 모델**- 엔진에서 오류가 발생하기 전에 지속되는 기간을 예측합니다. 샘플 모델은 "남은 유효 수명" (RUL)을 예측 합니다 .이를 ".TTF (Time to Failure)" 라고도 합니다.
  
-   **분류 모델**- 엔진에서 오류가 발생할 가능성이 있는지 여부를 예측합니다.
  
    **이진 분류 모델** 은 특정 시간 프레임 내에 엔진이 실패 하는 경우를 예측 합니다.

    **다중 클래스 분류 모델** 은 특정 엔진이 실패할 수 있는지 여부를 예측 하 고 오류 발생 가능한 시간 창을 제공 합니다. 예를 들어 주어진 날짜에 대해 해당 날짜나 주어진 날짜 이후의 일정 기간 동안 디바이스에서 오류가 발생할지 여부를 예측할 수 있습니다.

## <a name="energy-demand-forecasting"></a>에너지 수요 예측

[SQL Server R Services 포함 된 에너지 수요 예측 템플릿](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**대상:** 수요 예측은 에너지, 소매 및 서비스를 비롯 한 다양 한 도메인에서 중요 한 문제입니다. 정확한 수요 예측을 통해 기업은 프로덕션 계획과 리소스 할당을 보다 효율적으로 수행 하 고 다른 중요 한 비즈니스 의사 결정을 내릴 수 있습니다. 에너지 분야에서 수요 예측은 에너지 저장소 비용을 절감 하 고 공급 및 수요를 분산 하는 데 매우 중요 합니다.

**얼마나** 이 템플릿은 SQL Server R Services를 사용 하 여 전기 수요를 예측 합니다. 예측에 사용 되는 모델은 Microsoft R Server에 포함 된 고성능 기계 학습 알고리즘인 **rxDForest**을 기반으로 하는 임의 포리스트 회귀 모델입니다. 솔루션에는 수요 시뮬레이터, 모델 학습에 필요한 모든 R 및 T-SQL 코드, 예측 생성 및 보고에 사용할 수 있는 저장 프로시저가 포함되어 있습니다. 


## <a name="bkmk_HowTo"></a>템플릿을 사용 하는 방법

각 템플릿에 포함된 파일을 다운로드하려면 GitHub 명령을 사용하거나, 링크를 열고 **Zip 다운로드** 를 클릭하여 모든 파일을 컴퓨터에 저장합니다.  다운로드한 경우 일반적으로 솔루션에 다음 폴더가 포함되어 있습니다.
  
-   **데이터**: 각 응용 프로그램에 대 한 샘플 데이터를 포함 합니다.
  
-   **R**: 솔루션에 필요한 모든 R 개발 코드를 포함 합니다. 솔루션에는 Microsoft R Server에서 제공하는 라이브러리가 필요하지만 모든 R IDE를 통해 열고 편집할 수 있습니다. R 코드는 컴퓨팅 컨텍스트를 SQL Server 인스턴스로 설정하여 "데이터베이스 내"에서 컴퓨팅이 수행되도록 최적화되었습니다.
  
-   **SQLR**: 에는 데이터 처리, 기능 엔지니어링, 모델 배포와 같은 관련 태스크를 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 수행 하는 저장 프로시저를 만들기 위해와 같은 sql 환경에서 실행할 수 있는 여러 .sql 파일이 포함 되어 있습니다.
  
    폴더에는 모든 스크립트를 호출하고 종단 간 환경을 만들기 위해 실행할 수 있는 PowerShell 스크립트도 들어 있습니다. 환경에 맞게 스크립트를 편집해야 합니다.

## <a name="next-steps"></a>다음 단계

+ [SQL Server machine learning 자습서](machine-learning-services-tutorials.md)




