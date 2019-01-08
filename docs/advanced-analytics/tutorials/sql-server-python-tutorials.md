---
title: SQL Server 2017 Python 자습서 개요-SQL Server Machine Learning
description: SQL Server 2017 데이터베이스 내 분석에 대 한 Python 자습서를 소개 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9101471c53ea1e253f7a6eb13e0c2cb2bc137ed3
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046463"
---
# <a name="sql-server-2017-python-tutorials"></a>SQL Server 2017 Python 자습서
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 데이터베이스 내 분석에 대 한 Python 자습서에 설명 합니다 [SQL Server 2017의 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)합니다. 

+ 줄 바꿈 및 저장된 프로시저에서 Python 코드를 실행 하는 방법에 알아봅니다.
+ Serialize 하 고 SQL Server 데이터베이스에 Python 기반 모델을 저장 합니다.
+ 원격 및 로컬 계산 컨텍스트 및 사용 시기에 대해 알아봅니다.
+ 데이터 과학 및 machine learning 작업에 대 한 Microsoft Python 모듈을 탐색 합니다.

<a name="bkmk_pythontutorials"></a>

## <a name="python-quickstarts-and-tutorials"></a>Python 빠른 시작 및 자습서

| 링크 | Description |
|------|-------------|
| [빠른 시작: SQL Server에서 "hello world" Python 스크립트](quickstart-r-run-using-tsql.md) | T-sql로 Python을 호출 하는 방법의 기본 사항을 알아봅니다. |
| [빠른 시작: 만들기, 학습 및 Python 모델을 사용 하 여 SQL Server에서 저장된 프로시저를 사용 하 여](quickstart-python-train-score-in-tsql.md) | 입력 및 저장된 프로시저 실행을 제공 하는 저장된 프로시저에서 Python 코드를 포함 하는 방법을 설명 합니다. |
| [자습서: Revoscalepy를 사용 하 여 모델 만들기](use-python-revoscalepy-to-create-model.md) | SQL Server 계산 컨텍스트를 사용 하 여 원격 Python 터미널에서 코드를 실행 하는 방법에 설명 합니다. Python 도구 및 환경을 사용 하 여 어느 정도 알고 있어야 합니다. 사용 하 여 모델을 만드는 제공 되는 샘플 코드 **rxLinMod**에서 새 **revoscalepy** 라이브러리입니다. |
| [자습서: SQL 개발자를 위한 데이터베이스 내 Python 분석에 알아봅니다](sqldev-in-database-python-for-sql-developers.md) | 이 종단 간 연습 T-SQL 저장 프로시저를 사용 하 여 완전 한 Python 솔루션 구축 과정을 보여 줍니다. 모든 Python 코드가 포함 됩니다.|

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>코드 샘플

이러한 샘플 및 SQL Server 개발 팀에서 제공 하는 데모에는 실제 응용 프로그램에 포함 된 분석을 사용할 수 있는 방법을 강조 표시 합니다.

| 링크 | Description |
|------|-------------|
| [Python 및 SQL Server를 사용 하 여 예측 모델 빌드](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/) | Ski 차량 대 여 사업에서 기계 학습 향후 대 여 예측을 비즈니스 계획 및 직원 미래 수요를 충족 하기 위해 도움이 되는 사용 하는 방법을 알아봅니다. |
| [고객 수행 Python 및 SQL Server를 사용 하 여 클러스터링](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/) | Kmeans 알고리즘을 사용 하 여 고객의 감독 되지 않은 클러스터링을 수행 하는 방법에 알아봅니다. |

## <a name="see-also"></a>참고자료

+ [SQL Server에 대 한 Python 확장](../concepts/extension-python.md)
+ [SQL Server Machine Learning Services 자습서](machine-learning-services-tutorials.md)
