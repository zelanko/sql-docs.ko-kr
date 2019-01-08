---
title: SQL Server R 및 Python 자습서-SQL Server Machine Learning
description: 예제 및 R 및 SQL Server Machine Learning Services의 스크립팅는 Python에 대 한 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 69009a5a11e7f7985729656ae9df6c60bcba8037
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596934"
---
# <a name="sql-server-machine-learning-tutorials-in-r-and-python"></a>R 및 Python에서 SQL Server Machine Learning 자습서
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 machine learning의 기능을 보여 주는 코드 샘플 및 자습서의 종합적인 목록을 제공 [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) 하거나 [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)합니다. 

+ 퀵 스타트 최소한의 노력으로 빠른 탐색을 위해 기본 제공 데이터 또는 데이터를 사용합니다.
+ 자습서 자세히 자세한 작업, 더 큰 데이터 집합 및 긴 설명 합니다.
+ 샘플 및 솔루션 개념 및 기술 격차를 단원 거꾸로 작업 코드를 사용 하 여 시작 하려면 선호 하는 개발자를 위한 됩니다.

고성능 데이터에 대 한 동일한 작업 컨텍스트, 실행 및 사용자 지정 코드를 배포 하기 위한 SQL Server 저장 프로시저를 사용 하는 방법 및 Microsoft R을 호출 하는 관계형 데이터 상주를 사용 하 여 R 및 Python 라이브러리 및 Python 라이브러리를 사용 하는 방법을 알아봅니다. 과학 및 machine learning 작업 합니다.

첫 번째 단계로, Microsoft의 백업 하는 기본 개념을 검토 SQL Server와 R 및 Python 통합 합니다.

## <a name="concepts"></a>개념

데이터베이스 내 분석 데이터베이스 엔진에 추가 된 기능으로 SQL Server Machine Learning Services 또는 SQL Server 2016 R Services (R에만 해당)를 설치 하면 SQL Server의 R 및 Python에 대 한 기본 지원을 가리킵니다. R 및 Python 통합에는 기본 오픈 소스 배포와 고성능 분석에 대 한 Microsoft 전용 라이브러리 포함 됩니다.

아키텍처 독립 점에서 코드는 데이터베이스 엔진의 무결성을 유지 하려면 상자에서 외부 프로세스로 실행 됩니다. 그러나 모든 데이터 액세스 및 보안은 SQL Server 데이터베이스 역할을 통해, 즉, SQL Server에 대 한 액세스를 사용 하 여 응용 프로그램 사용 권한 저장 프로시저를 배포 하거나 serialize 하 고 학습 된 모델을 SQL 저장 R 및 Python 스크립트에 액세스할 수 있습니다. Server 데이터베이스입니다.

다른 Microsoft 제품의 해당 언어 지원 및 SQL Server에서 R 및 Python 간의 주요 차이점을 지원 하 고 서비스에 포함 됩니다.

+ 저장된 프로시저 또는 이진 모델 "package" 코드를 수 있습니다.
+ SQL 서버 프로그램 파일을 사용 하 여 로컬로 설치 하는 Microsoft R 및 Python 라이브러리를 호출 하는 코드를 작성 합니다.
+ R 및 Python 솔루션에 SQL Server의 데이터베이스 보안 아키텍처를 적용 합니다.
+ SQL Server 인프라 및 사용자 지정 솔루션에 대 한 관리 지원을 활용 하세요.

## <a name="quickstarts"></a>빠른 시작

T-SQL에서 R 또는 Python을 실행 하는 방법 및 SQL 프로덕션 환경에 대 한 R 및 Python 코드를 운영 하는 방법을 알아보려면 여기를 시작 합니다.

+ [Python: T-SQL을 사용 하 여 Python 실행](run-python-using-t-sql.md)
+ [R: R 및 SQL의 hello World](rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [R: 입 / 출력 처리](rtsql-working-with-inputs-and-outputs.md)
+ [R: 데이터 형식 및 개체를 처리 합니다.](rtsql-r-and-sql-data-types-and-data-objects.md)
+ [R: R 함수를 사용 하 여](rtsql-using-r-functions-with-sql-server-data.md)
+ [R: 예측 모델 만들기](rtsql-create-a-predictive-model-r.md)
+ [R: 모델에서 예측 및 그리기](rtsql-predict-and-plot-from-model.md)

## <a name="tutorials"></a>자습서

자세히 보기 Microsoft 패키지 및 원격 계산 컨텍스트와 로컬에서 이동 하는 등의 보다 특수 한 작업을 수행 하 여 R 및 Python 및 T-SQL을 사용 하 여 첫 번째 환경에 빌드하십시오.

+ [Python 자습서](sql-server-python-tutorials.md)
+ [R 자습서](sql-server-r-tutorials.md)

<a name ="bkmk_samples"></a>

## <a name="samples"></a>샘플

이러한 샘플 및 SQL Server 및 R Server 개발 팀에서 제공 하는 데모에는 실제 응용 프로그램에 포함 된 분석을 사용할 수 있는 방법을 강조 표시 합니다.

| 링크 | Description | 
|------|-------------|
| [고객 수행 R 및 SQL Server를 사용 하 여 클러스터링](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 판매 데이터를 기반으로 하는 세그먼트 고객에 게 자율된 학습을 사용 합니다. 이 예제에서는 클러스터링 모델을 만드는 데 Microsoft R의 확장 가능한 rxKmeans 알고리즘을 사용 합니다. |
| [고객 수행 Python 및 SQL Server를 사용 하 여 클러스터링](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Kmeans 알고리즘을 사용 하 여 고객의 감독 되지 않은 클러스터링을 수행 하는 방법에 알아봅니다. 이 예제는 Python 언어에 데이터베이스를 사용합니다.| SQL Server 2017 |
| [R 및 SQL Server를 사용 하 여 예측 모델 빌드](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Ski 차량 대 여 사업에서 기계 학습 향후 대 여 예측을 비즈니스 계획 및 직원 미래 수요를 충족 하기 위해 도움이 되는 사용 하는 방법을 알아봅니다. 이 예제에서는 의사 결정 트리 모델과 로지스틱 회귀를 빌드하려면 Microsoft 알고리즘을 사용 합니다. | 
| [Python 및 SQL Server를 사용 하 여 예측 모델 빌드](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | 향후 수요에 대 한 계획 하는 데 Python을 사용 하 여 ski 차량 대 여 분석 응용 프로그램을 빌드하십시오. 새 Python 라이브러리를 사용 하 여이 예제 **revoscalepy**, 선형 회귀 모델을 만듭니다. | 
| [SQL Server Machine Learning Services를 사용 하 여 Tableau를 사용 하는 방법](https://blogs.msdn.microsoft.com/mlserver/2017/12/14/how-to-use-tableau-with-sql-server-machine-learning-services-with-r-and-python/) | SQL Server 및 R을 사용 하 여 Tableau 그래프를 만들어 소셜 미디어 분석 | 

<a name="bkmk_solutions"></a>

## <a name="solution-templates"></a>솔루션 템플릿

Microsoft 데이터 과학 팀에는 일반적인 시나리오에 대 한 솔루션을 시작 하는 데 사용할 수 있는 사용자 지정 가능한 솔루션 템플릿을 제공 합니다. 각 솔루션은 특정 태스크 또는 업계 문제에 맞게 조정 됩니다. 솔루션의 대부분은 SQL Server 또는 Azure Machine Learning과 같은 클라우드 환경에서 실행 하도록 설계 되었습니다. 다른 솔루션에는 Microsoft R Server 또는 Machine Learning Server를 사용 하 여 Linux 또는 Spark 및 Hadoop 클러스터에서 실행할 수 있습니다.

모든 코드를 학습 하 고 SQL Server 저장 프로시저를 사용 하 여 점수 매기기에 모델을 배포 하는 방법에 대 한 지침과 함께 제공 됩니다.

+ [사기 검색](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [사용자 지정 이탈 예측](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [예측 유지 관리](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [병원 체류 기간 예측](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

자세한 내용은 [SQL Server 2016 R Services를 사용하는 Machine Learning 템플릿](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/)을 참조하세요.

