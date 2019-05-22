---
title: R 및 Python machine learning 설명서-SQL Server Machine Learning 서비스
description: 대규모 엔터프라이즈 데이터 분석을 위한 기본 제공 데이터 과학 모델링 및 Machine Learning 알고리즘이 포함된 SQL Server의 R 및 Python
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: overview
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e93d9ad5fd6415b6d8c1b6208857e81d60de2bd0
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994124"
---
# <a name="sql-server-machine-learning-services"></a>SQL Server Machine Learning 서비스

## <a name="sql-server-machine-learning-services-r-and-python-documentation"></a>SQL Server Machine Learning 서비스 (R 및 Python) 설명서

빠른 시작, 자습서 및 방법 문서를 사용하여 상주하는 관계형 데이터에 R 및 Python 외부 라이브러리와 언어를 사용하는 방법을 알아봅니다. [SQL Server Machine Learning](what-is-sql-server-machine-learning.md)의 R 및 Python 라이브러리에는 네트워크를 통해 데이터를 전송할 필요없이 대규모로 고성능 분석을 수행하기 위한 기본 배포, 데이터 과학 모델, Machine Learning 알고리즘 및 함수가 포함되어 있습니다.

::: moniker range="=sql-server-ver15||=sqlallproducts-allversions"
> [!NOTE]
> Java에 대 한 설명서를 참조 하세요. 합니다 [SQL Server 언어 확장 설명서](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview)합니다.
::: moniker-end

|   |   |
|---|:--|
| ![R 로고](media/index/logo_r.png) | [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package)의 [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) 및 Microsoft AI 알고리즘으로 확장된 오픈 소스 R입니다. 이러한 라이브러리는 대규모 예측 및 예측 모델, 통계 분석, 시각화 및 데이터 조작을 지원합니다.<br/>R 통합은 [SQL Server 2016](install/sql-r-services-windows-install.md)에서 시작되며 [SQL Server 2017](install/sql-machine-learning-services-windows-install.md)에도 제공됩니다. |
| ![Python 로고](media/index/logo_python.png) | Python 개발자는 대규모 예측 분석 및 Machine Learning에 Microsoft [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 및 [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) 라이브러리를 사용할 수 있습니다. Anaconda 및 Python 3.5 호환 라이브러리는 기준 배포입니다.<br/>Python 통합은 [SQL Server 2017](install/sql-machine-learning-services-windows-install.md)에서 시작됩니다. |
| &nbsp; | &nbsp; |

## <a name="5-minute-quickstarts"></a>5분 빠른 시작

- [R에서 예측 모델 만들기](tutorials/rtsql-create-a-predictive-model-r.md)

- [R을 사용하여 모델에서 예측 및 그리기](tutorials/rtsql-predict-and-plot-from-model.md)

## <a name="step-by-step-tutorials"></a>단계별 자습서

- [SQL Server에 Machine Learning 및 확장 프레임워크를 추가하는 방법](install/sql-machine-learning-services-windows-install.md)

- [T-SQL 및 저장 프로시저에서 R을 실행하는 방법](tutorials/sqldev-in-database-r-for-sql-developers.md)

- [Python에서 포함 분석을 사용하는 방법](tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="video-introduction"></a>비디오 소개

> [!VIDEO https://www.youtube.com/embed/ACejZ9optCQ]

## <a name="reference"></a>참조

| 패키지 | 언어 | Description |
|:--------|:---------|:------------|
| [RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) | R | R 작업에 대한 분산 및 병렬 처리: 데이터 변환, 탐색, 시각화, 통계 및 예측 분석 |
| [MicrosoftML](/machine-learning-server/r-reference/microsoftml/microsoftml-package) | R | Microsoft의 AI 알고리즘을 기준으로 하는 함수로, R용으로 조정되었습니다. |
| [olapR](/machine-learning-server/r-reference/olapr/olapr) | R | OLAP cube.s에서 데이터를 가져옵니다. |
| [sqlRUtils](/machine-learning-server/r-reference/sqlrutils/sqlrutils) | R | R 및 T-SQL을 캡슐화하기 위한 도우미 함수입니다. |
[revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | Python | Python 작업에 대한 분산 및 병렬 처리: 데이터 변환, 탐색, 시각화, 통계 및 예측 분석 |
| [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Python | Microsoft의 AI 알고리즘을 기준으로 하는 함수로, Python용으로 조정되었습니다. |
| &nbsp; | &nbsp; | &nbsp; |
