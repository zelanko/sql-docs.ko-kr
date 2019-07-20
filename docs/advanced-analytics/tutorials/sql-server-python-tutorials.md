---
title: SQL Server 2017 Python 자습서 개요
description: SQL Server 2017 데이터베이스 내 분석에 대 한 Python 자습서를 소개 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 86c5eaa600da0dbe9106278dd36b21eba322e2b7
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345969"
---
# <a name="sql-server-2017-python-tutorials"></a>SQL Server 2017 Python 자습서
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)의 데이터베이스 내 분석에 대 한 Python 자습서를 설명 합니다. 

+ 저장 프로시저에서 Python 코드를 래핑하고 실행 하는 방법에 대해 알아봅니다.
+ Python 기반 모델을 Serialize 하 고 SQL Server 데이터베이스에 저장 합니다.
+ 원격 및 로컬 계산 컨텍스트와 이러한 컨텍스트를 사용 하는 시기에 대해 알아봅니다.
+ 데이터 과학 및 machine learning 작업에 대 한 Microsoft Python 모듈을 탐색 합니다.

<a name="bkmk_pythontutorials"></a>

## <a name="python-quickstarts-and-tutorials"></a>Python 빠른 시작 및 자습서

| 링크 | 설명 |
|------|-------------|
| [빠른 시작: SQL Server에서 "Hello 세계" Python 스크립트](quickstart-python-run-using-t-sql.md) | T-sql에서 Python을 호출 하는 방법에 대 한 기본 사항을 알아봅니다. |
| [빠른 시작: SQL Server에서 저장 프로시저를 사용 하 여 Python 모델 만들기, 학습 및 사용](quickstart-python-train-score-in-tsql.md) | 저장 프로시저에 Python 코드를 포함 하 고 입력 및 저장 프로시저 실행을 제공 하는 메커니즘을 설명 합니다. |
| [자습서: Revoscalepy를 사용 하 여 모델 만들기](use-python-revoscalepy-to-create-model.md) | SQL Server compute 컨텍스트를 사용 하 여 원격 Python 터미널에서 코드를 실행 하는 방법을 보여 줍니다. Python 도구 및 환경에 대해 잘 알고 있어야 합니다. 새 **revoscalepy** 라이브러리에서 **rxLinMod**를 사용 하 여 모델을 만드는 샘플 코드가 제공 됩니다. |
| [자습서: SQL 개발자를 위한 데이터베이스 내 Python 분석에 대해 알아보기](sqldev-in-database-python-for-sql-developers.md) | 이 종단 간 연습은 T-sql 저장 프로시저를 사용 하 여 완전 한 Python 솔루션을 구축 하는 과정을 보여 줍니다. 모든 Python 코드가 포함 됩니다.|

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>코드 샘플

SQL Server 개발 팀에서 제공 하는 이러한 샘플과 데모는 실제 응용 프로그램에서 포함 된 분석을 사용할 수 있는 방법을 강조 표시 합니다.

| 링크 | 설명 |
|------|-------------|
| [Python 및 SQL Server를 사용 하 여 예측 모델 작성](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Ski 임대 비즈니스에서 기계 학습을 사용 하 여 미래의 대 여을 예측 하는 방법에 대해 알아봅니다 .이를 통해 비즈니스 계획 및 직원은 미래의 수요를 달성할 수 있습니다. |
| [Python 및 SQL Server를 사용 하 여 고객 클러스터링 수행](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Kmeans 알고리즘을 사용 하 여 고객의 자율 클러스터링을 수행 하는 방법에 대해 알아봅니다. |

## <a name="see-also"></a>참조

+ [SQL Server에 대 한 Python 확장](../concepts/extension-python.md)
+ [SQL Server Machine Learning Services 자습서](machine-learning-services-tutorials.md)
