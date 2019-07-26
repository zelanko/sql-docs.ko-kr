---
title: SQL Server R 및 Python 자습서
description: SQL Server Machine Learning Services의 R 및 Python 스크립팅에 대 한 예제 및 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: d901d11b11019a19d5e26e12956e9ba520e33e8f
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469622"
---
# <a name="sql-server-machine-learning-tutorials-in-r-and-python"></a>R 및 Python의 SQL Server Machine Learning 자습서
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) 또는 [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)의 기계 학습 기능을 보여 주는 자습서 및 코드 샘플의 포괄적인 목록을 제공 합니다. 

+ 빠른 시작은 기본 제공 데이터를 사용 하거나 최소한의 노력으로 빠른 탐색을 위해 데이터를 사용 하지 않습니다.
+ 자습서는 더 많은 작업, 더 큰 데이터 집합 및 긴 설명으로 더 자세히 살펴보겠습니다.
+ 샘플과 솔루션은 코드를 사용 하 여 시작 하는 개발자를 위한 것으로, 개념 및 교훈에 대해 뒤로 작업 하 여 지식 격차를 채웁니다.

동일한 작업 컨텍스트에서 상주 관계형 데이터를 사용 하 여 R 및 Python 라이브러리를 사용 하는 방법, 사용자 지정 코드를 실행 하 고 배포 하는 데 SQL Server 저장 프로시저를 사용 하는 방법, 고성능 데이터를 위해 Microsoft R 및 Python 라이브러리를 호출 하는 방법에 대해 알아봅니다. 과학 및 기계 학습 작업.

첫 번째 단계로 Microsoft의 R 및 Python과 SQL Server의 통합을 지 원하는 기본 개념을 검토 합니다.

## <a name="concepts"></a>개념

데이터베이스 내 분석은 SQL Server Machine Learning Services를 설치 하거나 2016 R 서비스 (R만)를 데이터베이스 엔진에 추가 기능으로 SQL Server 때 SQL Server의 R 및 Python에 대 한 기본 지원을 나타냅니다. R 및 Python 통합에는 고성능 분석을 위한 Microsoft 전용 라이브러리와 기본 오픈 소스 배포가 포함 됩니다.

아키텍처의 관점에서 코드는 데이터베이스 엔진의 무결성을 유지 하기 위해 상자에서 외부 프로세스로 실행 됩니다. 그러나 모든 데이터 액세스 및 보안은 SQL Server 데이터베이스 역할 및 사용 권한을 통해 수행 됩니다. 즉, SQL Server에 대 한 액세스 권한이 있는 모든 응용 프로그램은 해당 스크립트를 저장 프로시저로 배포 하거나 SQL에 학습 된 모델을 직렬화 하 고 저장할 때 R 및 Python 스크립트에 액세스할 수 있습니다. 서버 데이터베이스.

다른 Microsoft 제품 및 서비스의 SQL Server에 대 한 R 및 Python 지원 간의 주요 차이점은 다음과 같습니다.

+ 저장 프로시저나 이진 모델로 코드를 "패키지" 할 수 있습니다.
+ SQL Server 프로그램 파일을 사용 하 여 로컬로 설치 된 Microsoft R 및 Python 라이브러리를 호출 하는 코드를 작성 합니다.
+ R 및 Python 솔루션에 SQL Server의 데이터베이스 보안 아키텍처를 적용 합니다.
+ 사용자 지정 솔루션에 대 한 SQL Server 인프라 및 관리 지원을 활용 합니다.

## <a name="quickstarts"></a>빠른 시작

T-sql에서 R 또는 Python을 실행 하는 방법 및 SQL 프로덕션 환경에 대 한 R 및 Python 코드를 운영 하는 방법에 대해 알아보려면 여기를 시작 합니다.

+ [Python: T-sql을 사용 하 여 Python 실행](run-python-using-t-sql.md)
+ [R: R 및 SQL의 Hello World](rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [R: 입력 및 출력 처리](rtsql-working-with-inputs-and-outputs.md)
+ [R: 데이터 형식 및 개체 처리](rtsql-r-and-sql-data-types-and-data-objects.md)
+ [R: R 함수 사용](rtsql-using-r-functions-with-sql-server-data.md)
+ [R: 예측 모델 만들기](rtsql-create-a-predictive-model-r.md)
+ [R: 모델에서 예측 및 그리기](rtsql-predict-and-plot-from-model.md)

## <a name="tutorials"></a>자습서

Microsoft 패키지를 자세히 살펴보고 로컬에서 원격 계산 컨텍스트로 이동 하는 것과 같은 보다 특수 한 작업을 수행 하 여 R 및 Python 및 T-sql을 사용 하 여 첫 번째 환경을 구축 하세요.

+ [Python 자습서](sql-server-python-tutorials.md)
+ [R 자습서](sql-server-r-tutorials.md)

<a name ="bkmk_samples"></a>

## <a name="samples"></a>샘플

SQL Server 및 R Server 개발 팀에서 제공 하는 이러한 샘플과 데모에서는 실제 응용 프로그램에서 포함 된 분석을 사용할 수 있는 방법을 강조 표시 합니다.

| 링크 | 설명 | 
|------|-------------|
| [R 및 SQL Server를 사용 하 여 고객 클러스터링 수행](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 자율 learning을 사용 하 여 판매 데이터를 기준으로 고객을 분할 합니다. 이 예제에서는 Microsoft R의 확장 가능한 rxKmeans 알고리즘을 사용 하 여 클러스터링 모델을 작성 합니다. |
| [Python 및 SQL Server를 사용 하 여 고객 클러스터링 수행](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Kmeans 알고리즘을 사용 하 여 고객의 자율 클러스터링을 수행 하는 방법에 대해 알아봅니다. 이 예에서는 데이터베이스 내 Python 언어를 사용 합니다.| SQL Server 2017 |
| [R 및 SQL Server를 사용 하 여 예측 모델 작성](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Ski 임대 비즈니스에서 기계 학습을 사용 하 여 미래의 대 여을 예측 하는 방법에 대해 알아봅니다 .이를 통해 비즈니스 계획 및 직원은 미래의 수요를 달성할 수 있습니다. 이 예에서는 Microsoft 알고리즘을 사용 하 여 로지스틱 회귀 및 의사 결정 트리 모델을 작성 합니다. | 
| [Python 및 SQL Server를 사용 하 여 예측 모델 작성](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Python을 사용 하 여 ski 임대 분석 응용 프로그램을 빌드하여 향후 수요를 계획할 수 있습니다. 이 예에서는 새 Python 라이브러리인 **revoscalepy**를 사용 하 여 선형 회귀 모델을 만듭니다. | 

<a name="bkmk_solutions"></a>

## <a name="solution-templates"></a>솔루션 템플릿

Microsoft 데이터 과학 팀은 일반적인 시나리오에 대 한 솔루션을 바로 시작 하는 데 사용할 수 있는 사용자 지정 가능한 솔루션 템플릿을 제공 했습니다. 각 솔루션은 특정 작업 또는 업계 문제에 맞게 조정 됩니다. 대부분의 솔루션은 SQL Server 또는 Azure Machine Learning 같은 클라우드 환경에서 실행 되도록 설계 되었습니다. 다른 솔루션은 Microsoft R Server 또는 Machine Learning Server를 사용 하 여 Linux 또는 Spark 또는 Hadoop 클러스터에서 실행할 수 있습니다.

모든 코드는 SQL Server 저장 프로시저를 사용 하 여 점수 매기기를 위한 모델을 학습 하 고 배포 하는 방법에 대 한 지침과 함께 제공 됩니다.

+ [사기 검색](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [사용자 지정 이탈 예측](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [예측 유지 관리](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [보관 기간을 예측 합니다.](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

