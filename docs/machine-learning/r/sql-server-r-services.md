---
title: SQL Server 2016 R Services란?
titleSuffix: ''
description: R Services는 관계형 데이터를 사용하여 R 스크립트를 실행하는 기능을 제공하는 SQL Server 2016의 기능입니다. 예측 분석 및 기계 학습에 오픈 소스 패키지와 프레임워크 및 Microsoft R 패키지를 사용할 수 있습니다. 스크립트는 SQL Server 외부에서 또는 네트워크를 통해 데이터를 이동하지 않고 데이터베이스 내에서 실행됩니다. 이 문서에서는 SQL Server R Services의 기본 사항에 대해 설명합니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/06/2020
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016
ms.openlocfilehash: d1910099e1f0aa4a8f3e58f1faa01dfbe177c517
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470764"
---
# <a name="what-is-sql-server-2016-r-services"></a>SQL Server 2016 R Services란?

[!INCLUDE[SQL Server 2016 only](../../includes/applies-to-version/sqlserver2016-only.md)]

R Services는 관계형 데이터를 사용하여 R 스크립트를 실행하는 기능을 제공하는 SQL Server 2016의 기능입니다. 예측 분석 및 기계 학습에 오픈 소스 패키지와 프레임워크 및 [Microsoft R 패키지](#packages)를 사용할 수 있습니다. 스크립트는 SQL Server 외부에서 또는 네트워크를 통해 데이터를 이동하지 않고 데이터베이스 내에서 실행됩니다. 이 문서에서는 SQL Server R Services의 기본 사항에 대해 설명합니다.

> [!Note]
> R Services는 SQL Server 2017 이상에서 [Machine Learning Services](../sql-server-machine-learning-services.md)로 이름이 변경되었으며 Python과 R을 모두 지원합니다.

## <a name="what-is-r-services"></a>R Services란?

SQL Server R Services를 사용하여 데이터베이스 내에서 R 스크립트를 실행할 수 있습니다. 이를 사용하여 데이터를 준비 및 정리하고, 기능 엔지니어링을 수행하고, 데이터베이스 내에서 기계 학습 모델을 학습, 평가 및 배포할 수 있습니다. 이 기능은 데이터가 상주하는 스크립트를 실행하고 네트워크를 통해 다른 서버에 데이터를 전송하는 작업을 제거합니다.

R의 기본 배포는 R Services에 포함되어 있습니다. R을 위해 Microsoft 패키지 [RevoScaleR](../r/ref-r-revoscaler.md), [MicrosoftML](../r/ref-r-microsoftml.md), [olapR]../r/ref-r-olapr.md) 및 [sqlrutils](../r/ref-r-sqlrutils.md) 외에도 오픈 소스 패키지 및 프레임워크를 사용할 수 있습니다.

R Services는 확장성 프레임워크를 사용하여 SQL Server에서 R 스크립트를 실행합니다. 다음에서 이 작업을 수행하는 방법을 자세히 알아보세요.

+ [확장성 프레임워크](../concepts/extensibility-framework.md)
+ [R 확장](../concepts/extension-r.md)

## <a name="what-can-i-do-with-r-services"></a>R Services로 무엇을 할 수 있나요?

R Services를 사용하여 SQL Server 내에서 기계 학습 및 딥 러닝 모델을 작성하고 학습할 수 있습니다. 기존 모델을 R Services에 배포하고 예측에 관계형 데이터를 사용할 수도 있습니다.

SQL Server R Services를 사용할 수 있는 예측 유형의 예는 다음과 같습니다.

|예측 유형|예제|
|-|-|
|분류/범주화|사용자 의견을 긍정 및 부정 범주로 자동으로 구분|
|회귀/연속 값 예측|크기 및 위치를 기준으로 주택 가격 예측|
|이상 감지|사기성 은행 거래 감지 |
|권장 사항|이전 구매에 따라 온라인 쇼핑객이 구매하려고 할 수 있는 제품 제안|

### <a name="how-to-execute-r-scripts"></a>R 스크립트를 실행하는 방법

R Services에서 R 스크립트를 실행하는 방법에는 다음 두 가지가 있습니다.

+ 가장 일반적인 방법은 T-SQL 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하는 것입니다.

+ 기본 설정 R 클라이언트를 사용하고 실행(*원격 컴퓨팅 컨텍스트* 라고도 함)을 원격 SQL Server로 푸시하는 스크립트를 작성할 수도 있습니다. 자세한 내용은 [데이터 과학 클라이언트 R 개발 설정](../r/set-up-a-data-science-client.md) 방법을 참조하세요.

<a name="version"></a>

## <a name="r-versions"></a>R 버전

다음은 SQL Server 2016 R Services에 포함된 R 런타임 버전입니다.

SQL Server 버전 | 기본 R 런타임 버전 |
|-|-|
| SQL Server 2016 RTM - SP2 CU13 | 3.2.2 |
| SQL Server 2016 SP2 CU14 이상 | 3.2.2 및 3.5.2 |

SQL Server 2016 SP(서비스 팩) 2 이상에 대한 CU(누적 업데이트 ) 14에는 최신 R 런타임이 포함되어 있습니다. 자세한 내용은 [기본 언어 런타임 버전 변경](../install/change-default-language-runtime-version.md)을 참조하세요.

다른 버전의 R을 사용하거나 Python을 실행하려면 [SQL Server 2017 이상용 Machine Learning Services](../sql-server-machine-learning-services.md)를 사용합니다.

<a name="packages"></a>

## <a name="r-packages"></a>R 패키지

Microsoft의 엔터프라이즈 패키지 외에도 오픈 소스 패키지 및 프레임워크를 사용할 수 있습니다. 가장 일반적인 오픈 소스 R 패키지는 R Services에 미리 설치되어 있습니다. Microsoft의 다음 R 패키지도 포함되어 있습니다.

| 패키지 | Description |
|-|-|
| [RevoScaleR](../r/ref-r-revoscaler.md) | 확장 가능한 R의 기본 패키지입니다. 데이터 변환 및 조작, 통계 요약, 시각화 및 많은 형식의 모델링에 사용됩니다. 또한 이 패키지의 함수는 병렬 처리를 위해 사용 가능한 코어 간에 워크로드를 자동으로 분산합니다. |
| [MicrosoftML(R)](../r/ref-r-microsoftml.md) | 텍스트 분석, 이미지 분석 및 감정 분석을 위한 사용자 지정 모델을 만들기 위한 기계 학습 알고리즘을 추가합니다. |
| [olapR](../r/ref-r-olapr.md) | SQL Server Analysis Services OLAP 큐브에 대한 MDX 쿼리에 사용되는 R 함수입니다. |
| [sqlrutils](../r/ref-r-sqlrutils.md) | T-SQL 저장 프로시저에서 R 스크립트를 사용하고, 데이터베이스에 해당 저장 프로시저를 등록하고, [R 개발 환경](../r/set-up-a-data-science-client.md)에서 저장 프로시저를 실행하는 메커니즘입니다. |
| [Microsoft R Open](https://mran.microsoft.com/rro) | MRO(Microsoft R Open)는 Microsoft에서 출시한 R의 고급 배포판입니다. 통계 분석 및 데이터 과학을 위한 완전한 오픈 소스 플랫폼입니다. R을 기준으로 하고 R과 100% 호환되며, 향상된 성능 및 재현 가능성을 위한 추가 기능을 포함합니다. |

## <a name="how-do-i-get-started-with-rservices"></a>RServices를 시작하려면 어떻게 해야 하나요?

1. [SQL Server 2016 R Services 설치](../install/sql-r-services-windows-install.md)

1. 개발 도구 구성. 다음을 사용할 수 있습니다.

    + [Azure Data Studio](../../azure-data-studio/what-is.md) 또는 [SSMS(SQL Server Management Studio)](../../ssms/sql-server-management-studio-ssms.md): T-SQL 및 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 R 스트립트를 실행합니다.
    + 사용자 고유의 개발 랩톱 또는 워크스테이션의 R: 스크립트를 실행합니다. 데이터를 로컬로 끌어오거나 [RevoScaleR](../r/ref-r-revoscaler.md)을 사용하여 SQL Server에 원격으로 실행을 푸시할 수 있습니다. 자세한 내용은 [데이터 과학 클라이언트 R 개발 설정](../r/set-up-a-data-science-client.md) 방법을 참조하세요.

1. 첫 번째 R 스크립트 작성

    + 빠른 시작: [SQL Server에서 간단한 R 스크립트를 만들고 실행](../tutorials/quickstart-r-create-script.md)
    + 빠른 시작: [R에서 예측 모델 만들기 및 학습](../tutorials/quickstart-r-train-score-model.md)
    + 자습서: [T-SQL에서 R 사용](../tutorials/r-taxi-classification-introduction.md): 데이터 살펴보기, 기능 엔지니어링 수행, 모델 학습 및 배포, 예측 수행(5부 시리즈)
    + 자습서: [R 도구에서 R Services 사용](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md): 데이터 살펴보기, 그래프와 그림 만들기, 기능 엔지니어링 수행, 모델 학습 및 배포, 예측 수행(6부 시리즈)

## <a name="next-steps"></a>다음 단계

+ [SQL Server 2016 R Services 설치](../install/sql-r-services-windows-install.md)
+ [R 개발을 위한 데이터 과학 클라이언트 설정](../r/set-up-a-data-science-client.md)
