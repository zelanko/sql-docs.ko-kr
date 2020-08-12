---
title: Python 자습서
titleSuffix: SQL machine learning
description: 이 문서에서는 SQL 기계 학습용 Python 자습서에 대해 설명합니다. 스크립트를 실행하고 기계 학습 모델을 빌드하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/21/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: f93fc25139a69f80afa15840d254c33d2195b335
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730451"
---
# <a name="python-tutorials-for-sql-machine-learning"></a>SQL 기계 학습용 Python 자습서
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
이 문서에서는 [SQL Server의 Machine Learning Services](../sql-server-machine-learning-services.md) 및 [빅 데이터 클러스터](../../big-data-cluster/machine-learning-services.md)에 대한 Python 자습서와 빠른 시작에 대해 설명합니다.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
이 문서에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)용 Python 자습서 및 빠른 시작에 대해 설명합니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
이 문서에서는 [Azure SQL Managed Instance Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)용 Python 자습서 및 빠른 시작에 대해 설명합니다.
::: moniker-end

<a name="bkmk_pythontutorials"></a>

## <a name="python-tutorials"></a>Python 자습서

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
| 자습서 | Description |
|-|-|
| [선형 회귀를 사용하여 스키 대여 예측](python-ski-rental-linear-regression.md) | Python 및 선형 회귀를 사용하여 스키 대여 수를 예측합니다. 데이터를 준비하고 모델을 학습할 때는 Azure Data Studio의 Notebook을 사용하고, 모델을 배포할 때는 T-SQL을 사용합니다. |
| [k-means 클러스터링을 사용하여 고객 분류](python-clustering-model.md) | Python으로 K-Means 클러스터링 모델을 개발 및 배포하여 고객을 분류합니다. 데이터를 준비하고 모델을 학습할 때는 Azure Data Studio의 Notebook을 사용하고, 모델을 배포할 때는 T-SQL을 사용합니다. |
| [revoscalepy를 사용하여 모델 만들기](use-python-revoscalepy-to-create-model.md) | SQL Server를 컴퓨팅 컨텍스트로 사용하여 원격 Python 클라이언트에서 코드를 실행하는 방법을 보여 줍니다. 이 자습서에서는 **revoscalepy** 라이브러리의 **rxLinMod**를 사용하여 모델을 만듭니다. |
| [SQL 개발자를 위한 Python 데이터 분석](sqldev-in-database-python-for-sql-developers.md) | 이 엔드투엔드 연습은 T-SQL을 사용하여 완전한 Python 솔루션을 빌드하는 프로세스를 보여 줍니다. |
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
| 자습서 | Description |
|-|-|
| [선형 회귀를 사용하여 스키 대여 예측](python-ski-rental-linear-regression.md) | Python 및 선형 회귀를 사용하여 스키 대여 수를 예측합니다. 데이터를 준비하고 모델을 학습할 때는 Azure Data Studio의 Notebook을 사용하고, 모델을 배포할 때는 T-SQL을 사용합니다. |
| [k-means 클러스터링을 사용하여 고객 분류](python-clustering-model.md) | Python으로 K-Means 클러스터링 모델을 개발 및 배포하여 고객을 분류합니다. 데이터를 준비하고 모델을 학습할 때는 Azure Data Studio의 Notebook을 사용하고, 모델을 배포할 때는 T-SQL을 사용합니다. |
::: moniker-end

## <a name="python-quickstarts"></a>Python 빠른 시작

SQL 기계 학습을 처음 접하는 경우 Python 빠른 시작을 수행해도 됩니다.

| 빠른 시작 | Description |
|-|-|
| [간단한 Python 스크립트 실행](quickstart-python-create-script.md) | [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 T-SQL에서 Python을 호출하는 방법에 대한 기본 사항을 알아봅니다. |
| [Python을 사용하는 데이터 구조 및 개체](quickstart-python-data-structures.md) | SQL에서 Python pandas 패키지를 사용하여 데이터 구조를 처리하는 방법을 보여줍니다. |
| [Python에서 예측 모델 만들기 및 점수 매기기](quickstart-python-train-score-model.md) | Python 모델을 만들고 학습하고 사용하여 새 데이터에서 예측을 수행하는 방법을 설명합니다. |

## <a name="next-steps"></a>다음 단계

+ [SQL Server의 Python 확장](../concepts/extension-python.md)
