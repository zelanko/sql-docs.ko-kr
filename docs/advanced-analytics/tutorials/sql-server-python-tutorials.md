---
title: Python 자습서
description: 이 문서에서는 SQL Server Machine Learning Services에 대 한 Python 자습서를 설명 합니다. Python 스크립트를 실행 하는 방법을 알아봅니다. SQL Server에 Python 모델을 빌드, 학습 및 배포 합니다. 원격 및 로컬 계산 컨텍스트에 대해 알아봅니다. 데이터 과학 및 기계 학습을 위한 Microsoft Python 패키지를 살펴보세요.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cd458727fad637414d7c71865b2633f3caf80175
ms.sourcegitcommit: 949e55b32eff6610087819a93160a35af0c5f1c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/05/2019
ms.locfileid: "70383554"
---
# <a name="python-tutorials-for-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services에 대 한 Python 자습서
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)의 Python 자습서 및 빠른 시작에 대해 설명 합니다.

+ Python 스크립트를 실행 하는 방법을 알아봅니다.
+ SQL Server에 Python 모델을 빌드, 학습 및 배포 합니다.
+ 원격 및 로컬 계산 컨텍스트에 대해 알아봅니다.
+ 데이터 과학 및 기계 학습을 위한 Microsoft Python 패키지를 살펴보세요.

<a name="bkmk_pythontutorials"></a>

## <a name="python-tutorials"></a>Python 자습서

| 자습서 | 설명 |
|-|-|
| [선형 회귀를 사용 하 여 ski 임대 예측](python-ski-rental-linear-regression.md) | Python 및 선형 회귀를 사용 하 여 ski 대 여의 수를 예측 합니다. Azure Data Studio에서 노트북을 사용 하 여 데이터를 준비 하 고 모델을 학습 하 고 모델 배포를 위한 T-sql을 사용 합니다. |
| [K를 사용 하 여 고객 분류 클러스터링 이란 클러스터링](python-clustering-model.md) | Python을 사용 하 여 K를 개발 하 고 배포 합니다. 클러스터링 모델을 통해 고객을 분류 합니다. Azure Data Studio에서 노트북을 사용 하 여 데이터를 준비 하 고 모델을 학습 하 고 모델 배포를 위한 T-sql을 사용 합니다. |
| [Revoscalepy를 사용 하 여 모델 만들기](use-python-revoscalepy-to-create-model.md) | SQL Server를 계산 컨텍스트로 사용 하 여 원격 Python 클라이언트에서 코드를 실행 하는 방법을 보여 줍니다. 이 자습서에서는 **revoscalepy** 라이브러리에서 **rxLinMod** 를 사용 하 여 모델을 만듭니다. |
| [SQL 개발자를 위한 Python 데이터 분석](sqldev-in-database-python-for-sql-developers.md) | 이 종단 간 연습은 T-sql을 사용 하 여 완전 한 Python 솔루션을 구축 하는 과정을 보여 줍니다. |

## <a name="python-quickstarts"></a>Python 빠른 시작

SQL Server Machine Learning Services를 처음 접하는 경우 Python 빠른 시작을 사용해 볼 수도 있습니다.

| 빠른 시작 | 설명 |
|-|-|
| [Python 및 SQL Server에서 Hello World](quickstart-python-run-using-t-sql.md) | T-sql에서 Python을 호출 하는 방법에 대 한 기본 사항을 알아봅니다. |
| [SQL Server에서 Python을 사용 하 여 입력 및 출력 처리](quickstart-python-inputs-and-outputs.md) | [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 Python에 대 한 입력 및 출력을 처리 하는 방법을 알아봅니다. |
| [SQL Server의 Python 데이터 구조](quickstart-python-data-structures.md) | SQL Server Python pandas 패키지를 사용 하 여 데이터 구조를 처리 하는 방법을 보여 줍니다. |
| [첫 번째 모델 학습 및 사용](quickstart-python-train-score-in-tsql.md) | Python 모델을 만들고 학습 하 고 사용 하 여 새 데이터를 예측 하는 방법을 설명 합니다. |

## <a name="next-steps"></a>다음 단계

+ [SQL Server Machine Learning Services (Python 및 R)는 무엇 인가요?](../what-is-sql-server-machine-learning.md)
+ [SQL Server에 대 한 Python 확장](../concepts/extension-python.md)