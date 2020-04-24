---
title: Python 자습서
description: 이 문서에서는 SQL Server Machine Learning Services용 Python 자습서에 대해 설명합니다. SQL Server에서 스크립트를 실행하고 기계 학습 모델을 빌드하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e3733f12ed93d7c84a86259742b6996333c3900f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487355"
---
# <a name="python-tutorials-for-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services용 Python 자습서
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)용 Python 자습서 및 빠른 시작에 대해 설명합니다.

+ Python 스크립트를 실행하는 방법을 알아봅니다.
+ Python 모델을 빌드 및 학습하고 SQL Server에 배포합니다.
+ 원격 및 로컬 컴퓨팅 컨텍스트에 대해 알아봅니다.
+ 데이터 과학 및 기계 학습을 위한 Microsoft Python 패키지를 살펴봅니다.

<a name="bkmk_pythontutorials"></a>

## <a name="python-tutorials"></a>Python 자습서

| 자습서 | Description |
|-|-|
| [선형 회귀를 사용하여 스키 대여 예측](python-ski-rental-linear-regression.md) | Python 및 선형 회귀를 사용하여 스키 대여 수를 예측합니다. 데이터를 준비하고 모델을 학습할 때는 Azure Data Studio의 Notebook을 사용하고, 모델을 배포할 때는 T-SQL을 사용합니다. |
| [k-means 클러스터링을 사용하여 고객 분류](python-clustering-model.md) | Python으로 K-Means 클러스터링 모델을 개발 및 배포하여 고객을 분류합니다. 데이터를 준비하고 모델을 학습할 때는 Azure Data Studio의 Notebook을 사용하고, 모델을 배포할 때는 T-SQL을 사용합니다. |
| [revoscalepy를 사용하여 모델 만들기](use-python-revoscalepy-to-create-model.md) | SQL Server를 컴퓨팅 컨텍스트로 사용하여 원격 Python 클라이언트에서 코드를 실행하는 방법을 보여 줍니다. 이 자습서에서는 **revoscalepy** 라이브러리의 **rxLinMod**를 사용하여 모델을 만듭니다. |
| [SQL 개발자를 위한 Python 데이터 분석](sqldev-in-database-python-for-sql-developers.md) | 이 엔드투엔드 연습은 T-SQL을 사용하여 완전한 Python 솔루션을 빌드하는 프로세스를 보여 줍니다. |

## <a name="python-quickstarts"></a>Python 빠른 시작

SQL Server Machine Learning Services를 처음 접하는 경우 Python 빠른 시작을 사용해 볼 수도 있습니다.

| 빠른 시작 | Description |
|-|-|
| [Python 및 SQL Server의 Hello World Hello World](quickstart-python-create-script.md) | [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 T-SQL에서 Python을 호출하는 방법에 대한 기본 사항을 알아봅니다. |
| [SQL Server에서 Python을 사용하여 데이터 형식 및 개체 처리](quickstart-python-data-structures.md) | SQL Server에서 Python pandas 패키지를 사용하여 데이터 구조를 처리하는 방법을 보여 줍니다. |
| [Python에서 예측 모델 만들기 및 점수 매기기](quickstart-python-train-score-model.md) | Python 모델을 만들고 학습하고 사용하여 새 데이터에서 예측을 수행하는 방법을 설명합니다. |

## <a name="next-steps"></a>다음 단계

+ [SQL Server Machine Learning Services(Python 및 R)란?](../sql-server-machine-learning-services.md)
+ [SQL Server에 대한 Python 확장](../concepts/extension-python.md)