---
title: SQL Server Machine Learning Services (Python 및 R)는 무엇 인가요?
titleSuffix: ''
description: Machine Learning Services은 관계형 데이터를 사용 하 여 Python 및 R 스크립트를 실행 하는 기능을 제공 하는 SQL Server의 기능입니다. 예측 분석 및 기계 학습을 위해 오픈 소스 패키지 및 프레임 워크와 Microsoft Python 및 R 패키지를 사용할 수 있습니다. 스크립트는 SQL Server 외부에서 또는 네트워크를 통해 데이터를 이동 하지 않고 데이터베이스에서 실행 됩니다. 이 문서에서는 SQL Server Machine Learning Services의 기본 사항을 설명 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/07/2019
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 59e005e0075c9bb26210c6be9be5f52a3aa9a164
ms.sourcegitcommit: 3ec48823bee1c092ce2aba6011b95174de03fb65
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926919"
---
# <a name="what-is-sql-server-machine-learning-services-python-and-r"></a>SQL Server Machine Learning Services (Python 및 R)는 무엇 인가요?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Machine Learning Services은 관계형 데이터를 사용 하 여 Python 및 R 스크립트를 실행 하는 기능을 제공 하는 SQL Server의 기능입니다. 예측 분석 및 기계 학습을 위해 오픈 소스 패키지 및 프레임 워크와 [Microsoft Python 및 R 패키지](#packages) 를 사용할 수 있습니다. 스크립트는 SQL Server 외부에서 또는 네트워크를 통해 데이터를 이동 하지 않고 데이터베이스에서 실행 됩니다. 이 문서에서는 SQL Server Machine Learning Services의 기본 사항을 설명 합니다.

Azure SQL Database [Machine Learning Services](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview) 현재 공개 미리 보기로 제공 됩니다.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> SQL Server에서 Java를 실행 하는 방법에 대 한 자세한 내용은 [언어 확장 설명서](../language-extensions/language-extensions-overview.md)를 참조 하세요.
::: moniker-end

## <a name="what-is-machine-learning-services"></a>Machine Learning Services 이란?

SQL Server Machine Learning Services를 사용 하 여 데이터베이스 내에서 Python 및 R 스크립트를 실행할 수 있습니다. 이를 사용 하 여 데이터를 준비 하 고 정리 하며, 기능 엔지니어링을 수행 하 고, 데이터베이스 내에서 기계 학습 모델을 학습, 평가 및 배포할 수 있습니다. 이 기능은 데이터가 상주 하는 스크립트를 실행 하 고 네트워크를 통해 다른 서버에 데이터를 전송 하는 것을 제거 합니다.

Python 및 R의 기본 배포는 Machine Learning Services에 포함 되어 있습니다. PyTorch, TensorFlow 및 scikit와 같은 오픈 소스 패키지 및 프레임 워크를 사용할 수 있습니다. 예를 들어 Python 용 Microsoft 패키지 [revoscalepy](python/ref-py-revoscalepy.md) and [microsoftml](python/ref-py-microsoftml.md) 및 [RevoScaleR](r/ref-r-revoscaler.md), [microsoftml](r/ref-r-microsoftml.md), [olapr](r/ref-r-olapr.md), 및 R에 대 한 [sqlrutils](r/ref-r-sqlrutils.md) .

Machine Learning Services는 확장성 프레임 워크를 사용 하 여 SQL Server에서 Python 및 R 스크립트를 실행 합니다. 이 작업을 수행 하는 방법에 대해 자세히 알아보세요.

+ [확장성 프레임 워크](concepts/extensibility-framework.md)
+ [Python 확장](concepts/extension-python.md)
+ [R 확장](concepts/extension-r.md)

## <a name="what-can-i-do-with-machine-learning-services"></a>Machine Learning Services로 무엇을 할 수 있나요?

Machine Learning Services를 사용 하 여 SQL Server 내에서 기계 학습 및 심층 학습 모델을 작성 하 고 학습 합니다. Machine Learning Services에 기존 모델을 배포 하 고 예측에 관계형 데이터를 사용할 수도 있습니다.

Machine Learning Services SQL Server 사용할 수 있는 예측 형식의 예는 다음과 같습니다.

|||
|-|-|
|분류/분류|사용자 의견을 긍정 및 부정 범주로 자동으로 나눕니다.|
|회귀/연속 값 예측|크기 및 위치를 기준으로 주택 가격 예측|
|변칙 검색|사기성 은행 거래 검색 |
|권장 사항|이전 구매에 따라 온라인 쇼핑객에 게 구매할 수 있는 제품을 제안 합니다.|

### <a name="how-to-execute-python-and-r-scripts"></a>Python 및 R 스크립트를 실행 하는 방법

Machine Learning Services에서 Python 및 R 스크립트를 실행 하는 방법에는 두 가지가 있습니다.

+ 가장 일반적인 방법은 T-sql 저장 프로시저 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용 하는 것입니다.

+ 선호 하는 Python 또는 R 클라이언트를 사용 하 고 실행 ( *원격 계산 컨텍스트*라고도 함)을 원격 SQL Server로 푸시하는 스크립트를 작성할 수도 있습니다. 자세한 내용은 [Python 개발](python/setup-python-client-tools-sql.md) 을 위한 데이터 과학 클라이언트를 설정 하는 방법 및 [R 개발](r/set-up-a-data-science-client.md) 을 참조 하세요.

<a name="packages"></a>

## <a name="python-and-r-packages"></a>Python 및 R 패키지

Microsoft의 엔터프라이즈 패키지 외에도 오픈 소스 패키지 및 프레임 워크를 사용할 수 있습니다. 가장 일반적인 오픈 소스 Python 및 R 패키지는 Machine Learning Services에 미리 설치 되어 있습니다. Microsoft의 다음 Python 및 R 패키지도 포함 되어 있습니다.

| 언어 | 패키지 | 설명 |
|-|-|-|
| Python | [revoscalepy](python/ref-py-revoscalepy.md) | 확장 가능한 Python의 기본 패키지입니다. 데이터 변환 및 조작, 통계 요약, 시각화 및 많은 형식의 모델링입니다. 또한이 패키지의 함수는 병렬 처리를 위해 사용 가능한 코어 간에 작업을 자동으로 분산 합니다. |
| Python | [microsoftml](python/ref-py-microsoftml.md) | 텍스트 분석, 이미지 분석 및 감정 분석을 위한 사용자 지정 모델을 만들기 위한 기계 학습 알고리즘을 추가 합니다. | 
| R | [RevoScaleR](r/ref-r-revoscaler.md) | 확장 가능한 R의 기본 패키지입니다. 데이터 변환 및 조작, 통계 요약, 시각화 및 많은 형식의 모델링입니다. 또한이 패키지의 함수는 병렬 처리를 위해 사용 가능한 코어 간에 작업을 자동으로 분산 합니다. |
| R | [MicrosoftML (R)](r/ref-r-microsoftml.md) | 텍스트 분석, 이미지 분석 및 감정 분석을 위한 사용자 지정 모델을 만들기 위한 기계 학습 알고리즘을 추가 합니다. |
| R | [olapR](r/ref-r-olapr.md) | R 함수는 SQL Server Analysis Services OLAP 큐브에 대 한 MDX 쿼리에 사용 됩니다. |
| R | [sqlrutils](r/ref-r-sqlrutils.md) | T-sql 저장 프로시저에서 R 스크립트를 사용 하 고, 해당 저장 프로시저를 데이터베이스에 등록 하 고, [r 개발 환경](r/set-up-a-data-science-client.md)에서 저장 프로시저를 실행 하는 메커니즘입니다. |
| R | [Microsoft R Open](https://mran.microsoft.com/rro) | MRO (microsoft R Open)은 Microsoft에서 R의 향상 된 배포입니다. 통계 분석 및 데이터 과학을 위한 완전 한 오픈 소스 플랫폼입니다. 이는 R과 100%의 호환성을 기반으로 하며 향상 된 성능 및 재현 가능성을 위한 추가 기능을 포함 합니다. |

## <a name="how-do-i-get-started-with-machine-learning-services"></a>Machine Learning Services을 시작 어떻게 할까요??

1. [SQL Server Machine Learning Services 설치](install/sql-machine-learning-services-windows-install.md)

1. 개발 도구를 구성 합니다. 다음을 사용할 수 있습니다.

    + [Azure Data Studio](../azure-data-studio/what-is.md) 또는 [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) t-sql 및 저장 프로시저 [Sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 를 사용 하 여 Python 또는 R 스크립트를 실행 합니다.
    + 스크립트를 실행 하는 사용자 고유의 개발 랩톱이 나 워크스테이션의 Python 또는 R 데이터를 로컬로 끌어오거나 [revoscalepy](python/ref-py-revoscalepy.md) 및 [RevoScaleR](r/ref-r-revoscaler.md)를 사용 하 여 SQL Server에 원격으로 실행할 수 있습니다. 자세한 내용은 [Python 개발](python/setup-python-client-tools-sql.md) 을 위한 데이터 과학 클라이언트를 설정 하는 방법 및 [R 개발](r/set-up-a-data-science-client.md) 을 참조 하세요.

1. 첫 번째 Python 또는 R 스크립트 작성

    + 빠른 시작: [Python](tutorials/quickstart-python-run-using-t-sql.md) 또는 [R](tutorials/quickstart-r-run-using-tsql.md) 에서 "Hello 세계" 스크립트를 실행 합니다.
    + 빠른 시작: [Python](tutorials/quickstart-python-train-score-in-tsql.md) 또는 [R](tutorials/quickstart-r-create-predictive-model.md) 에서 예측 모델 만들기
    + 자습서: [T-sql에서 Python 사용](tutorials/sqldev-in-database-python-for-sql-developers.md): 데이터 탐색, 기능 엔지니어링 수행, 모델 학습 및 배포, 예측 만들기 (5 부 시리즈)
    + 자습서: [T-sql에서 R 사용](tutorials/sqldev-in-database-r-for-sql-developers.md): 데이터 탐색, 기능 엔지니어링 수행, 모델 학습 및 배포, 예측 만들기 (5 부 시리즈)
    + 자습서: [R 도구에서 Machine Learning Services 사용](tutorials/walkthrough-data-science-end-to-end-walkthrough.md): 데이터 탐색, 그래프 및 플롯 만들기, 기능 엔지니어링 수행, 모델 학습 및 배포, 예측 만들기 (6 부 시리즈)

## <a name="next-steps"></a>다음 단계

+ [SQL Server Machine Learning Services 설치](install/sql-machine-learning-services-windows-install.md)
+ [Python 개발](python/setup-python-client-tools-sql.md) 및 [R 개발](r/set-up-a-data-science-client.md) 을 위한 데이터 과학 클라이언트 설정
