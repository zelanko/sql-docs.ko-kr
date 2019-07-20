---
title: SQL Server R 자습서 개요
description: 데이터베이스 내 분석 SQL Server에 대 한 R 언어 자습서를 소개 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: a020478cc59ceb1688f2c93f64c69685ab74972f
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345946"
---
# <a name="sql-server-r-language-tutorials"></a>SQL Server R 언어 자습서
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 [SQL Server 2016 r Services](../install/sql-r-services-windows-install.md) 또는 [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)에서 데이터베이스 내 분석에 대 한 R 언어 자습서를 설명 합니다.

+ 저장 프로시저에서 R 코드를 래핑하고 실행 하는 방법에 대해 알아봅니다.
+ R 기반 모델을 직렬화 하 고 SQL Server 데이터베이스에 저장 합니다.
+ 원격 및 로컬 계산 컨텍스트와 이러한 컨텍스트를 사용 하는 시기에 대해 알아봅니다.
+ 데이터 과학 및 machine learning 작업을 위한 Microsoft R 라이브러리를 살펴보세요.

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>R 빠른 시작 및 자습서

| 링크 | 설명 |
|------|-------------|
| [빠른 시작: T-sql에서 R 사용](rtsql-using-r-code-in-transact-sql-quickstart.md) | 몇 가지 빠른 시작에서 첫 번째는 SQL Server Management Studio와 같은 T-sql 쿼리 편집기를 사용 하 여 R 함수를 호출 하는 기본 구문을 보여 주는 것입니다. |
| [자습서: 데이터 과학자에 대 한 데이터베이스 내 R 분석 학습](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | SQL Server를 처음 접하는 R 개발자를 위한이 자습서에서는 SQL Server에서 일반적인 데이터 과학 작업을 설명 하는 방법을 설명 합니다. 데이터를 로드 및 시각화 하 고, 모델을 학습 하 고 SQL Server에 저장 하 고, 예측 분석에 모델을 사용 합니다. |
| [자습서: SQL 개발자를 위한 데이터베이스 내 R 분석에 대해 알아보기](../tutorials/sqldev-in-database-r-for-sql-developers.md) | [!INCLUDE[tsql](../../includes/tsql-md.md)]를 사용해서 R 솔루션을 빌드하고 배포하세요. 솔루션을 프로덕션 환경으로 전환 하는 데 중점을 둔 것입니다. R 코드를 저장 프로시저에 래핑하고, R 모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장하고, 예측을 위해 매개 변수가 있는 R 모델 호출을 수행하는 방법을 알아봅니다. |
| [자습서: RevoScalepR 심층 살펴보기](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | RevoScaleR 패키지에서 함수를 사용하는 방법을 알아봅니다. R 및 SQL Server 및 스위치 간 데이터 이동에 맞게 특정 작업 컨텍스트를 계산합니다. 모델 및 플롯을 만들고 개발 환경의 데이터베이스 서버 간에 이동합니다. |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>코드 샘플

| 링크 | 설명 |
|------|-------------|
| [R 및 SQL Server를 사용 하 여 예측 모델 작성](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Ski 임대 비즈니스에서 기계 학습을 사용 하 여 미래의 대 여을 예측 하는 방법에 대해 알아봅니다 .이를 통해 비즈니스 계획 및 직원은 미래의 수요를 달성할 수 있습니다. |
| [R 및 SQL Server를 사용 하 여 고객 클러스터링 수행](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 자율 learning을 사용 하 여 판매 데이터를 기준으로 고객을 분할 합니다. |

## <a name="see-also"></a>참조

+ [SQL Server에 대 한 R 확장](../concepts/extension-r.md)
+ [SQL Server Machine Learning Services 자습서](machine-learning-services-tutorials.md)

