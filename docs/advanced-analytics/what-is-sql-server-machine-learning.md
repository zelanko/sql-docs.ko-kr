---
title: SQL Server Machine Learning Services(Python 및 R)이란?
titleSuffix: ''
description: Machine Learning Services는 관계형 데이터를 사용하여 Python 및 R 스크립트를 실행할 수 있는 기능을 제공하는 SQL Server의 기능입니다. 예측 분석 및 기계 학습에 오픈 소스 패키지와 프레임워크, Microsoft Python과 R 패키지를 사용할 수 있습니다. 스크립트는 SQL Server 외부에서 또는 네트워크를 통해 데이터를 이동하지 않고 데이터베이스 내에서 실행됩니다. 이 문서에서는 SQL Server Machine Learning Services의 기본 사항에 대해 설명합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/07/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 634f9f62a3ff1de70be84fd5a7721d8efed891bf
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2019
ms.locfileid: "71149936"
---
# <a name="what-is-sql-server-machine-learning-services-python-and-r"></a>SQL Server Machine Learning Services(Python 및 R)이란?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Machine Learning Services는 관계형 데이터를 사용하여 Python 및 R 스크립트를 실행할 수 있는 기능을 제공하는 SQL Server의 기능입니다. 예측 분석 및 기계 학습에 오픈 소스 패키지와 프레임워크, [Microsoft Python과 R 패키지](#packages)를 사용할 수 있습니다. 스크립트는 SQL Server 외부에서 또는 네트워크를 통해 데이터를 이동하지 않고 데이터베이스 내에서 실행됩니다. 이 문서에서는 SQL Server Machine Learning Services의 기본 사항에 대해 설명합니다.

Azure SQL Database에서 [Machine Learning Services](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview)는 현재 퍼블릭 미리 보기로 제공됩니다.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> SQL Server에서 Java를 실행하는 방법에 대해서는 [언어 확장 설명서](../language-extensions/language-extensions-overview.md)를 참조하세요.
::: moniker-end

## <a name="what-is-machine-learning-services"></a>Machine Learning Services란?

SQL Server Machine Learning Services를 사용하여 데이터베이스에서 Python 또는 R 스크립트를 실행할 수 있습니다. 이를 사용하여 데이터를 준비 및 정리하고, 기능 엔지니어링을 수행하고, 데이터베이스 내에서 기계 학습 모델을 학습, 평가 및 배포할 수 있습니다. 이 기능은 데이터가 상주하는 스크립트를 실행하고 네트워크를 통해 다른 서버에 데이터를 전송하는 작업을 제거합니다.

Python 및 R의 기본 배포판은 Machine Learning Services에 포함되어 있습니다. Microsoft 패키지 [revoscalepy](python/ref-py-revoscalepy.md) 및 [microsoftml](python/ref-py-microsoftml.md)(Python용), [RevoScaleR](r/ref-r-revoscaler.md), [MicrosoftML](r/ref-r-microsoftml.md), [olapR](r/ref-r-olapr.md) 및 [sqlrutils](r/ref-r-sqlrutils.md)(R용) 외에 PyTorch, TensorFlow 및 scikit-learn과 같은 오픈 소스 패키지 및 프레임워크를 설치하고 사용할 수 있습니다.

Machine Learning Services는 확장성 프레임워크를 사용하여 SQL Server에서 Python 및 R 스크립트를 실행합니다. 다음에서 이 작업을 수행하는 방법을 자세히 알아보세요.

+ [확장성 프레임워크](concepts/extensibility-framework.md)
+ [Python 확장](concepts/extension-python.md)
+ [R 확장](concepts/extension-r.md)

## <a name="what-can-i-do-with-machine-learning-services"></a>Machine Learning Services로 어떤 작업을 할 수 있나요?

Machine Learning Services를 사용하여 SQL Server 내에서 기계 학습 및 딥 러닝 모델을 작성하고 학습할 수 있습니다. 기존 모델을 Machine Learning Services에 배포하고 예측에 관계형 데이터를 사용할 수도 있습니다.

SQL Server Machine Learning Services를 사용할 수 있는 예측 유형의 예는 다음과 같습니다.

|||
|-|-|
|분류/범주화|사용자 의견을 긍정 및 부정 범주로 자동으로 구분|
|회귀/연속 값 예측|크기 및 위치를 기준으로 주택 가격 예측|
|변칙 검색|사기성 은행 거래 감지 |
|권장 사항|이전 구매에 따라 온라인 쇼핑객이 구매하려고 할 수 있는 제품 제안|

### <a name="how-to-execute-python-and-r-scripts"></a>Python 및 R 스크립트를 실행하는 방법

Machine Learning Services에서 Python 및 R 스크립트를 실행하는 두 가지 방법이 있습니다.

+ 가장 일반적인 방법은 T-SQL 저장 프로시저 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하는 것입니다.

+ 기본 설정 Python 또는 R 클라이언트를 사용하고 실행(*원격 컴퓨팅 컨텍스트*라고도 함)을 원격 SQL Server로 푸시하는 스크립트를 작성할 수도 있습니다. 자세한 내용은 [Python 개발](python/setup-python-client-tools-sql.md) 및 [R 개발](r/set-up-a-data-science-client.md)을 위해 데이터 과학 클라이언트를 설정하는 방법을 참조하세요.

<a name="packages"></a>

## <a name="python-and-r-packages"></a>Python 및 R 패키지

Microsoft의 엔터프라이즈 패키지 외에도 오픈 소스 패키지 및 프레임워크를 사용할 수 있습니다. 가장 일반적인 오픈 소스 Python 및 R 패키지는 Machine Learning Services에 미리 설치되어 있습니다. Microsoft의 다음 Python 및 R 패키지도 포함되어 있습니다.

| 언어 | 패키지 | 설명 |
|-|-|-|
| Python | [revoscalepy](python/ref-py-revoscalepy.md) | 확장 가능한 Python의 기본 패키지입니다. 데이터 변환 및 조작, 통계 요약, 시각화 및 많은 형식의 모델링에 사용됩니다. 또한 이 패키지의 함수는 병렬 처리를 위해 사용 가능한 코어 간에 워크로드를 자동으로 분산합니다. |
| Python | [microsoftml](python/ref-py-microsoftml.md) | 텍스트 분석, 이미지 분석 및 감정 분석을 위한 사용자 지정 모델을 만들기 위한 기계 학습 알고리즘을 추가합니다. | 
| R | [RevoScaleR](r/ref-r-revoscaler.md) | 확장 가능한 R의 기본 패키지입니다. 데이터 변환 및 조작, 통계 요약, 시각화 및 많은 형식의 모델링에 사용됩니다. 또한 이 패키지의 함수는 병렬 처리를 위해 사용 가능한 코어 간에 워크로드를 자동으로 분산합니다. |
| R | [MicrosoftML(R)](r/ref-r-microsoftml.md) | 텍스트 분석, 이미지 분석 및 감정 분석을 위한 사용자 지정 모델을 만들기 위한 기계 학습 알고리즘을 추가합니다. |
| R | [olapR](r/ref-r-olapr.md) | SQL Server Analysis Services OLAP 큐브에 대한 MDX 쿼리에 사용되는 R 함수입니다. |
| R | [sqlrutils](r/ref-r-sqlrutils.md) | T-SQL 저장 프로시저에서 R 스크립트를 사용하고, 데이터베이스에 해당 저장 프로시저를 등록하고, [R 개발 환경](r/set-up-a-data-science-client.md)에서 저장 프로시저를 실행하는 메커니즘입니다. |
| R | [Microsoft R Open](https://mran.microsoft.com/rro) | MRO(Microsoft R Open)는 Microsoft에서 출시한 R의 고급 배포판입니다. 통계 분석 및 데이터 과학을 위한 완전한 오픈 소스 플랫폼입니다. R을 기준으로 하고 R과 100% 호환되며, 향상된 성능 및 재현 가능성을 위한 추가 기능을 포함합니다. |

Machine Learning Services와 함께 설치되는 패키지와 기타 패키지를 설치하는 방법에 대한 자세한 내용은 다음을 참조하세요.

+ [Python 패키지 정보 가져오기](package-management/python-package-information.md)
+ [sqlmlutils를 사용하여 Python 패키지 설치](package-management/install-additional-python-packages-on-sql-server.md)
+ [R 패키지 정보 가져오기](package-management/r-package-information.md)
+ [sqlmlutils를 사용하여 새 R 패키지 설치](package-management/install-additional-r-packages-on-sql-server.md)

## <a name="how-do-i-get-started-with-machine-learning-services"></a>Machine Learning Services를 시작하려면 어떻게 하나요?

1. [SQL Server Machine Learning Services 설치](install/sql-machine-learning-services-windows-install.md)

1. 개발 도구 구성. 다음을 사용할 수 있습니다.

    + [Azure Data Studio](../azure-data-studio/what-is.md) 또는 [SSMS(SQL Server Management Studio)](../ssms/sql-server-management-studio-ssms.md): T-SQL 및 저장 프로시저 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 Python 또는 R 스트립트를 실행합니다.
    + 사용자 고유의 개발 랩톱 또는 워크스테이션의 Python 또는 R: 스크립트를 실행합니다. 데이터를 로컬로 끌어오거나 [revoscalepy](python/ref-py-revoscalepy.md) 및 [RevoScaleR](r/ref-r-revoscaler.md)을 사용하여 SQL Server에 원격으로 실행을 푸시할 수 있습니다. 자세한 내용은 [Python 개발](python/setup-python-client-tools-sql.md) 및 [R 개발](r/set-up-a-data-science-client.md)을 위해 데이터 과학 클라이언트를 설정하는 방법을 참조하세요.

1. 첫 번째 Python 또는 R 스크립트 작성

    + 빠른 시작: [SQL에서 간단한 R 스크립트를 만들고 실행](tutorials/quickstart-r-create-script.md)
    + 빠른 시작: [R에서 예측 모델 만들기 및 학습](tutorials/quickstart-r-train-score-model.md)
    + 자습서: [T-SQL에서 Python 사용](tutorials/sqldev-in-database-python-for-sql-developers.md): 데이터 살펴보기, 기능 엔지니어링 수행, 모델 학습 및 배포, 예측 수행(5부 시리즈)
    + 자습서: [T-SQL에서 R 사용](tutorials/sqldev-in-database-r-for-sql-developers.md): 데이터 살펴보기, 기능 엔지니어링 수행, 모델 학습 및 배포, 예측 수행(5부 시리즈)
    + 자습서: [R 도구에서 Machine Learning Services 사용](tutorials/walkthrough-data-science-end-to-end-walkthrough.md): 데이터 살펴보기, 그래프와 그림 만들기, 기능 엔지니어링 수행, 모델 학습 및 배포, 예측 수행(6부 시리즈)

## <a name="next-steps"></a>다음 단계

+ [SQL Server Machine Learning Services 설치](install/sql-machine-learning-services-windows-install.md)
+ [Python 개발](python/setup-python-client-tools-sql.md) 및 [R 개발](r/set-up-a-data-science-client.md)을 위한 데이터 과학 클라이언트 설정
