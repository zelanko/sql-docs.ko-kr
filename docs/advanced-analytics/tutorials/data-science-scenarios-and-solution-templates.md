---
title: 데이터 과학 시나리오 및 솔루션 템플릿-SQL Server Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 936bc010838b3869c567117a9e87cdc2c4ce6d52
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596128"
---
# <a name="data-science-scenarios-and-solution-templates"></a>데이터 과학 시나리오 및 솔루션 템플릿
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

템플릿은 모범 사례를 보여 주고 솔루션을 더 빠르게 구현할 수 있도록 구성 요소를 제공하는 샘플 솔루션입니다. 각 템플릿은 특정 세로 또는 업계 특정 문제를 해결 하도록 설계 되었습니다. 각 템플릿의 작업은 데이터 준비 및 기능 엔지니어링에서 모델 학습 및 점수 매기기까지 확장됩니다. 이러한 템플릿을 사용 하 여 알아봅니다 어떻게 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 작동 합니다. 그런 다음 자유롭게 사용자 지정 솔루션을 빌드하고 사용자 고유의 시나리오에 맞게 템플릿을 사용자 지정할 수 있습니다. 

해당 하는 경우 SQL 저장 프로시저 및 각 솔루션에 샘플 데이터, R 코드 또는 Python 코드에 포함 됩니다. SQL Server에서 수행 하는 계산을 사용 하 여 기본 R 또는 Python 개발 환경에서 코드를 실행할 수 있습니다. 경우에 따라 T-SQL 및 SQL Server Management Studio와 같은 모든 SQL 클라이언트 도구를 사용 하 여 직접 코드를 실행할 수 있습니다.

> [!TIP]
> 
> 템플릿 중 대부분 온-프레미스를 지 원하는 여러 버전에서 제공 하 고 클라우드 machine learning 위한 플랫폼. 예를 들어, SQL Server만 사용 하 여 솔루션을 빌드할 수 있습니다 또는 Microsoft R Server 또는 Azure Machine Learning 솔루션을 빌드할 수 있습니다.

+ 세부 정보 및 업데이트에 대 한이 발표를 참조 하십시오. [Azure ML에서 흥미로운 새 템플릿](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

+ 다운로드 및 설치 지침을 참조 하세요 [템플릿을 사용 하는 방법을](#bkmk_HowTo)합니다.

## <a name="fraud-detection"></a>사기 검색

[온라인 사기 검색 템플릿 (SQL Server R Services)](https://github.com/Microsoft/r-server-fraud-detection)

**항목:** 사기성 트랜잭션을 검색 하는 기능은 온라인 비즈니스에 중요 합니다. 과금 청구 기능 손실을 줄이기 위해 비즈니스 도난당 한 결제 방법이 나 자격 증명을 사용 하 여 수행 된 트랜잭션을 신속 하 게 식별 해야 합니다. 사기성 거래가 발견되면 비즈니스는 일반적으로 추가 손실을 방지하기 위해 조치를 취하여 특정 계정을 최대한 빨리 차단합니다. 이 시나리오에서는 온라인 구매 거래의 데이터를에서 사용 하 여 가능한 사기 행위를 식별 하는 방법을 배웁니다.

**방법:**  사기 검색은 이진 분류 문제로 해결됩니다. 이 템플릿에서 사용되는 방법론은 다른 도메인의 사기 검색에도 쉽게 적용할 수 있습니다.


## <a name="campaign-optimization"></a>캠페인 최적화

[예측 하는 방법 및 시기에 잠재 고객에 게 문의](https://microsoft.github.io/r-server-campaign-optimization/)

**항목:** 이 솔루션에서 잠재 고객 인구 통계, 기록 응답 데이터 및 제품별 세부 정보에 따라 예측할 보험 산업 데이터를 사용 합니다.  권장 모범 채널 및 구매 동작에 영향을 줍니다 방법은 사용자에 게 시간을 나타내기 위해 생성 됩니다.

**방법:** 솔루션을 만들고 여러 모델을 비교 합니다. 또한 솔루션에는 자동화 된 데이터 통합 및 데이터 준비 저장된 프로시저를 사용 하 여 보여 줍니다. SQL Server 데이터베이스에서 Azure HDInsight Spark에 대 한 병렬 샘플이 제공 됩니다. 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>의료: 병원에서 체류 기간 예측 

[병원의 길이 예측합니다.](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**항목:** 정확 하 게는 환자 입원 장기 필요할 수를 예측 하는 것 관리와 계획의 중요 한 부분입니다. 간호인 환자의 요구를 충족할 수 있도록 보장 하려면와 관리자가 더 많은 리소스를 요청 하는 어떤 기능을 확인할 수 해야 합니다.

**방법:** 이 솔루션 데이터 과학 Virtual Machine을 사용 하 고 사용 하도록 설정 하는 machine learning을 사용한 SQL Server의 인스턴스를 포함 합니다. 또한 배포 된 모델을 사용 하 여 상호 작용 하는 데 사용할 수 있는 Power BI 보고서 집합을 포함 합니다.

## <a name="customer-churn"></a>고객 이탈

[고객 이탈 예측 템플릿 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)

**항목:** 분석 및 고객 이탈은 경쟁 업체에 고객의 손실 해야 관리 및 차단 여기서 모든 업계에서 중요 한 예측: 뱅킹, 통신 및 소매, 등입니다. 이탈 분석의 목표는 이탈 가능성이 있는 고객을 확인한 다음 적절한 조치를 취하여 해당 고객을 보존하고 비즈니스를 유지하는 것입니다.

**방법:** 이 템플릿은 이탈 문제 공식화를 **이진 분류** 문제입니다. 고객 인구 통계와 고객 거래의 두 원본에 있는 샘플 데이터를 사용하여 고객을 이탈 가능성이 있거나 없는 것으로 분류합니다.
  
## <a name="predictive-maintenance"></a>예측 유지 관리

[예측 유지 관리 템플릿 (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/Introduction.md)

**항목:** 예측 유지 관리는 이전 오류를 캡처하고 해당 정보를 사용 하 여 장치를 실패할 수 있는 시기나 위치를 예측 하 여 유지 관리 작업의 효율성을 높이기 위해 것을 목표로 합니다. 분산된 된 데이터 또는 센서를 사용 하는 응용 프로그램에 대 한 장치 노후화를 예측 하는 기능이 특히 유용 합니다. 이 메서드를 모니터링 하거나 IoT (사물 인터넷) 장치에서 오류를 예측 적용할 수도 없습니다.

자세한 내용은이 발표를 참조 하십시오. [새 예측 유지 관리 템플릿](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)

**방법:** 이 솔루션은 "경우 컴퓨터를 서비스 하지 못합니다?" 라는 질문에 답변에 집중 입력 데이터는 항공기 엔진에 대해 시뮬레이트된 센서 측정값을 나타냅니다. 엔진의 현재 작동 상태를 현재 작업 주기, 설정, 센서 측정값 등을 모니터링에서 가져온 데이터는 세 가지 유형의 예측 모델을 만드는 데 사용 됩니다.

-   **회귀 모델**- 엔진에서 오류가 발생하기 전에 지속되는 기간을 예측합니다. 샘플 모델 예측 메트릭을 "남은 가용 수명" (RUL), "시간을 하지 못했습니다." (TTF) 라고도 합니다.
  
-   **분류 모델**- 엔진에서 오류가 발생할 가능성이 있는지 여부를 예측합니다.
  
    합니다 **이진 분류 모델** 엔진 특정 시간 프레임 내에서 실패를 예측 합니다.

    합니다 **다중 클래스 분류 모델** 특정 엔진 실패할 수 있으며 오류의 가능성이 높은 기간을 제공 하는지 여부를 예측 합니다. 예를 들어 주어진 날짜에 대해 해당 날짜나 주어진 날짜 이후의 일정 기간 동안 디바이스에서 오류가 발생할지 여부를 예측할 수 있습니다.

## <a name="energy-demand-forecasting"></a>에너지 수요 예측

[에너지 수요 예측 템플릿 SQL Server R Services를 사용 하 여](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**:**: 수요 예측 하는 것은 에너지, 소매 및 서비스 등 다양 한 도메인에는 중요 한 문제입니다. 정확한 수요 예측 기업이 더 나은 프로덕션 계획, 리소스 할당을 수행 하 고 다른 중요 한 비즈니스 결정을 내릴 수 있습니다. 에너지 분야의 수요 예측은 에너지 저장소 비용을 줄이고 공급과 수요 균형 조정에 대 한 중요 합니다.

**방법:** 이 템플릿은 전기 수요를 예측 하도록 SQL Server R Services를 사용 합니다. 예측에 사용 된 모델은 기반으로 하는 임의 포리스트 회귀 모델 **rxDForest**, 고속 기계 학습 알고리즘 Microsoft R Server에 포함 합니다. 솔루션에는 수요 시뮬레이터, 모델 학습에 필요한 모든 R 및 T-SQL 코드, 예측 생성 및 보고에 사용할 수 있는 저장 프로시저가 포함되어 있습니다. 


## <a name="bkmk_HowTo"></a>템플릿을 사용 하는 방법

각 템플릿에 포함된 파일을 다운로드하려면 GitHub 명령을 사용하거나, 링크를 열고 **Zip 다운로드** 를 클릭하여 모든 파일을 컴퓨터에 저장합니다.  다운로드한 경우 일반적으로 솔루션에 다음 폴더가 포함되어 있습니다.
  
-   **데이터**: 각 응용 프로그램에 대 한 샘플 데이터를 포함합니다.
  
-   **R**: 솔루션에 필요한 모든 R 개발 코드가 들어 있습니다. 솔루션에는 Microsoft R Server에서 제공하는 라이브러리가 필요하지만 모든 R IDE를 통해 열고 편집할 수 있습니다. R 코드는 계산 컨텍스트를 SQL Server 인스턴스로 설정하여 "데이터베이스 내"에서 계산이 수행되도록 최적화되었습니다.
  
-   **SQLR**: 와 같은 SQL 환경에서 실행할 수 있는.sql 파일이 여러 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 데이터 처리와 같은 관련된 작업을 수행 하는 저장된 프로시저를 만들려면 기능 엔지니어링 및 모델 배포 합니다.
  
    폴더에는 모든 스크립트를 호출하고 종단 간 환경을 만들기 위해 실행할 수 있는 PowerShell 스크립트도 들어 있습니다. 환경에 맞게 스크립트를 편집해야 합니다.

## <a name="next-steps"></a>다음 단계

+ [SQL Server machine learning 자습서](machine-learning-services-tutorials.md)




