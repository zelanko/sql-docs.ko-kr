---
title: SQL Server R 자습서 개요-SQL Server Machine Learning
description: SQL Server 데이터베이스 내 분석을 위해 R 언어 자습서를 소개 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 467c9320880f1b113cecd36101345f6ee99f7b75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961930"
---
# <a name="sql-server-r-language-tutorials"></a>SQL Server R 언어 자습서
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 데이터베이스 내 분석을 위해 R 언어 자습서에 설명 합니다 [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) 하거나 [SQL Server 2017의 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)합니다.

+ 줄 바꿈 및 저장된 프로시저에서 R 코드를 실행 하는 방법에 알아봅니다.
+ Serialize 하 고 SQL Server 데이터베이스에 r 기반 모델을 저장 합니다.
+ 원격 및 로컬 계산 컨텍스트 및 사용 시기에 대해 알아봅니다.
+ 데이터 과학 및 machine learning 작업에 대 한 Microsoft R 라이브러리를 탐색 합니다.

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>R 빠른 시작 및 자습서

| 링크 | 설명 |
|------|-------------|
| [빠른 시작: T-SQL에서 R 사용](rtsql-using-r-code-in-transact-sql-quickstart.md) | SQL Server Management Studio와 같은 T-SQL 쿼리 편집기를 사용 하 여 R 함수를 호출 하기 위한 기본 구문을 보여 주는 이와 사용 하 여 몇 가지 빠른 시작의 첫 번째입니다. |
| [자습서: 데이터 과학자를 위한 데이터베이스 내 R 분석에 알아봅니다](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | 이 자습서에서는 SQL Server에 새 R 개발자를 위해 다음을 설명 합니다. SQL Server의 센터가 일반적인 데이터 과학 작업 하는 방법입니다. 로드 및 데이터 시각화, 학습 및 SQL 서버에 저장 하는 모델 및 예측 분석 모델을 사용 합니다. |
| [자습서: SQL 개발자를 위한 데이터베이스 내 R 분석에 알아봅니다](../tutorials/sqldev-in-database-r-for-sql-developers.md) | [!INCLUDE[tsql](../../includes/tsql-md.md)]를 사용해서 R 솔루션을 빌드하고 배포하세요. 솔루션을 프로덕션으로 이동에 초점을 맞춥니다. R 코드를 저장 프로시저에 래핑하고, R 모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장하고, 예측을 위해 매개 변수가 있는 R 모델 호출을 수행하는 방법을 알아봅니다. |
| [자습서: RevoScalepR 심층 분석](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | RevoScaleR 패키지에서 함수를 사용하는 방법을 알아봅니다. R 및 SQL Server 및 스위치 간 데이터 이동에 맞게 특정 작업 컨텍스트를 계산합니다. 모델 및 플롯을 만들고 개발 환경의 데이터베이스 서버 간에 이동합니다. |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>코드 샘플

| 링크 | 설명 |
|------|-------------|
| [R 및 SQL Server를 사용 하 여 예측 모델 빌드](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | Ski 차량 대 여 사업에서 기계 학습 향후 대 여 예측을 비즈니스 계획 및 직원 미래 수요를 충족 하기 위해 도움이 되는 사용 하는 방법을 알아봅니다. |
| [고객 수행 R 및 SQL Server를 사용 하 여 클러스터링](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 판매 데이터를 기반으로 하는 세그먼트 고객에 게 자율된 학습을 사용 합니다. |

## <a name="see-also"></a>참조

+ [SQL Server에 R 확장](../concepts/extension-r.md)
+ [SQL Server Machine Learning Services 자습서](machine-learning-services-tutorials.md)

