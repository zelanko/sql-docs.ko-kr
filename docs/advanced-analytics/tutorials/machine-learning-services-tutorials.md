---
title: SQL Server Machine Learning Services 자습서 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b692b9660c3caec18c689f56ba382f8df194a9cc
ms.sourcegitcommit: b1990ec4491b5a8097c3675334009cb2876673ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2018
ms.locfileid: "49384128"
---
# <a name="tutorials-for-sql-server-machine-learning-services"></a>SQL Server Machine Learning 서비스에 대 한 자습서
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 자습서, 데모 및 SQL Server 2016 또는 SQL Server 2017의 machine learning 기능을 사용 하는 샘플 응용 프로그램의 종합적인 목록을 제공 합니다. T-SQL에서 R 또는 Python을 실행 하는 방법, 원격 및 로컬 계산 컨텍스트를 사용 하는 방법 및 SQL 프로덕션 환경에 대 한 R 및 Python 코드를 최적화 하는 방법을 알아보려면 여기를 시작 합니다.

+ [Python 자습서](../tutorials/sql-server-python-tutorials.md)

+ [R 자습서](../tutorials/sql-server-r-tutorials.md)

요구 사항 및 설정 하는 방법에 대 한 자세한 내용은 참조 하세요. [필수 구성 요소](#bkmk_prerequisites)합니다.

## <a name="samples-and-solutions"></a>샘플 및 솔루션

+ [샘플](#bkmk_samples) 

    SQL Server 개발 팀에서 이러한 실제 시나리오에는 응용 프로그램에서 기계 학습을 포함 하는 방법을 보여 줍니다. 프로덕션 환경에서 다운로드, 수정 및 사용 하는 코드를 포함 하는 모든 샘플.

+ [솔루션](#bkmk_solutions) 

    Microsoft 데이터 과학 팀에서 템플릿은 기계를 사용 하 여 빠르게 시작 하도록 사용자 지정할 수 있습니다. 각 솔루션은 특정 태스크 또는 업계 문제에 맞게 조정 됩니다. 솔루션의 대부분은 SQL Server 또는 Azure Machine Learning과 같은 클라우드 환경에서 실행 하도록 설계 되었습니다. 다른 솔루션에는 Microsoft R Server 또는 Machine Learning Server를 사용 하 여 Linux 또는 Spark 및 Hadoop 클러스터에서 실행할 수 있습니다.

### <a name ="bkmk_samples"></a>SQL Server 제품 샘플

이러한 샘플 및 SQL Server 및 R Server 개발 팀에서 제공 하는 데모에는 실제 응용 프로그램에 포함 된 분석을 사용할 수 있는 방법을 강조 표시 합니다.

| 링크 | Description | 적용 대상 |
|------|-------------|------------|
| [고객 수행 R 및 SQL Server를 사용 하 여 클러스터링](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 판매 데이터를 기반으로 하는 세그먼트 고객에 게 자율된 학습을 사용 합니다. 이 예제에서는 클러스터링 모델을 만드는 데 Microsoft R의 확장 가능한 rxKmeans 알고리즘을 사용 합니다. | SQL Server 2016 또는 SQL Server 2017 |
| [고객 수행 Python 및 SQL Server를 사용 하 여 클러스터링](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Kmeans 알고리즘을 사용 하 여 고객의 감독 되지 않은 클러스터링을 수행 하는 방법에 알아봅니다. 이 예제는 Python 언어에 데이터베이스를 사용합니다.| SQL Server 2017 |
| [R 및 SQL Server를 사용 하 여 예측 모델 빌드](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Ski 차량 대 여 사업에서 기계 학습 향후 대 여 예측을 비즈니스 계획 및 직원 미래 수요를 충족 하기 위해 도움이 되는 사용 하는 방법을 알아봅니다. 이 예제에서는 의사 결정 트리 모델과 로지스틱 회귀를 빌드하려면 Microsoft 알고리즘을 사용 합니다. | SQL Server 2016 또는 SQL Server 2017 |
| [Python 및 SQL Server를 사용 하 여 예측 모델 빌드](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | 향후 수요에 대 한 계획 하는 데 Python을 사용 하 여 ski 차량 대 여 분석 응용 프로그램을 빌드하십시오. 새 Python 라이브러리를 사용 하 여이 예제 **revoscalepy**, 선형 회귀 모델을 만듭니다. | SQL Server 2017 |
| [SQL Server Machine Learning Services를 사용 하 여 Tableau를 사용 하는 방법](https://blogs.msdn.microsoft.com/mlserver/2017/12/14/how-to-use-tableau-with-sql-server-machine-learning-services-with-r-and-python/) | SQL Server 및 R을 사용 하 여 Tableau 그래프를 만들어 소셜 미디어 분석 | SQL Server 2016 또는 SQL Server 2017 |

### <a name="bkmk_solutions"></a>솔루션 템플릿

Microsoft 데이터 과학 팀에는 일반적인 시나리오에 대 한 솔루션을 시작 하는 데 사용할 수 있는 솔루션 템플릿을 제공 합니다. 모든 코드를 학습 하 고 SQL Server 저장 프로시저를 사용 하 여 점수 매기기에 모델을 배포 하는 방법에 대 한 지침과 함께 제공 됩니다.

+ [사기 검색](https://gallery.cortanaanalytics.com/Tutorial/Online-Fraud-Detection-Template-with-SQL-Server-R-Services-1)
+ [사용자 지정 이탈 예측](https://gallery.cortanaanalytics.com/Tutorial/Customer-Churn-Prediction-Template-with-SQL-Server-R-Services-1)
+ [예측 유지 관리](https://gallery.cortanaanalytics.com/Tutorial/Predictive-Maintenance-Template-with-SQL-Server-R-Services-1)
+ [병원 체류 기간 예측](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

자세한 내용은 [SQL Server 2016 R Services를 사용하는 Machine Learning 템플릿](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/)을 참조하세요.

## <a name="more-resources-and-reading"></a>더 많은 리소스 및 읽기

+ [왜 빌드 않았습니다 것?](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/01/10/sql-server-r-services-why-did-we-build-it/)

    R Services와 관련된 실제 이야기를 알고 싶으세요? 개발 및 원본 및 SQL Server R Services의 목표를 설명 하는 PM 팀에서이 문서를 읽습니다.

+ [자습서 및 Microsoft R에 대 한 샘플 데이터](https://docs.microsoft.com/machine-learning-server/r/tutorial-introduction)

    Microsoft R 및 빠른 자습서의이 컬렉션에서 RevoScaleR 패키지를 제공 하는 기능에 대해 알아봅니다. RevoScaleR 데이터 원본 및 원격 계산 컨텍스트를 사용 하 여 R 코드를 한 번 작성 하 고 어디서 나 배포 하는 방법에 알아봅니다.

+ [MicrosoftML 시작](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)

  MicrosoftML 패키지에 고급 모델링이 및 여러 계산 컨텍스트에 대 한 액세스에 최적화 된 확장성 있는 데이터 변환에 대 한 새 알고리즘을 사용 하는 방법에 알아봅니다.
