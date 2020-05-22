---
title: R 자습서
titleSuffix: SQL machine learning
description: 이 문서에서는 SQL 기계 학습용 R 자습서에 대해 설명합니다. 스크립트를 실행하고 기계 학습 모델을 빌드하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.topic: tutorial
author: cawrites
ms.author: chadam
ms.reviewer: garye, davidph
ms.date: 05/04/2020
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 63c271c4e1d59c9446495607b42b0b5ad13ea246
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606925"
---
# <a name="r-tutorials-for-sql-machine-learning"></a>SQL 기계 학습용 R 자습서

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
이 문서에서는 [SQL Server의 Machine Learning Services](../sql-server-machine-learning-services.md) 및 [빅 데이터 클러스터](../../big-data-cluster/machine-learning-services.md)에 대한 R 자습서와 빠른 시작에 대해 설명합니다.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
이 문서에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)용 R 자습서 및 빠른 시작에 대해 설명합니다.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
이 문서에서는 [SQL Server 2016 R Services](../r/sql-server-r-services.md)용 R 자습서 및 빠른 시작에 대해 설명합니다.
::: moniker-end

<a name="bkmk_sqltutorials"></a>

## <a name="r-tutorials"></a>R 자습서

| 자습서 | Description |
|------|-------------|
| [의사 결정 트리를 사용하여 스키 임대 예측](r-predictive-model-introduction.md) | R 및 의사 결정 트리 모델을 사용하여 향후 스키 대여 수량을 예측합니다. 데이터를 준비하고 모델을 학습할 때는 Azure Data Studio의 Notebook을 사용하고, 모델을 배포할 때는 T-SQL을 사용합니다. |
| [k-means 클러스터링을 사용하여 고객 분류](r-clustering-model-introduction.md) | R로 K-평균 클러스터링 모델을 개발 및 배포하여 고객을 분류합니다. 데이터를 준비하고 모델을 학습할 때는 Azure Data Studio의 Notebook을 사용하고, 모델을 배포할 때는 T-SQL을 사용합니다. |
| [데이터 과학자를 위한 데이터베이스 내 R 분석](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | SQL Server를 처음 사용하는 R 개발자를 위해 이 자습서에서는 SQL Server에서 일반적인 데이터 과학 작업을 수행하는 방법을 설명합니다. 데이터를 로드 및 시각화하고, 모델을 학습하여 SQL Server에 저장하고, 예측 분석을 위해 모델을 사용합니다. |
| [SQL 개발자를 위한 데이터베이스 내 R 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md) | [!INCLUDE[tsql](../../includes/tsql-md.md)] 도구만 사용하여 전체 R 솔루션을 빌드 및 배포합니다. 솔루션을 프로덕션으로 전환하는 데 중점을 둡니다. R 코드를 저장 프로시저에 래핑하고, R 모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장하고, 예측을 위해 매개 변수가 있는 R 모델 호출을 수행하는 방법을 알아봅니다. |

## <a name="r-quickstarts"></a>R 빠른 시작

SQL 기계 학습을 처음 접하는 경우 R 빠른 시작을 수행해도 됩니다.

| 빠른 시작 | Description |
|-|-|
| [간단한 R 스크립트 실행](quickstart-r-create-script.md) | [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 T-SQL에서 R을 호출하는 방법에 대한 기본 사항을 알아봅니다. |
| [R을 사용하는 데이터 구조 및 개체](quickstart-r-data-types-and-objects.md) | SQL에서 R을 사용하여 데이터 구조를 처리하는 방법을 보여줍니다. |
| [R에서 예측 모델 만들기 및 점수 매기기](quickstart-r-data-types-and-objects.md) | R 모델을 만들고, 학습시키고, 새 데이터로 미래를 예측하는 데 사용하는 방법을 설명합니다. |

## <a name="next-steps"></a>다음 단계

SQL Server의 R에 대한 자세한 기술 정보는 [SQL Server의 R 언어 확장](../concepts/extension-r.md)을 참조하세요.
