---
title: R 자습서
description: SQL Server 데이터베이스 내 분석을 위한 R 언어 자습서를 소개합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7c71ebfbda37e66050f868fa7676d0247e84840e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74119233"
---
# <a name="sql-server-r-language-tutorials"></a>SQL Server R 언어 자습서
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) 또는 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)에 대한 데이터베이스 내 분석을 위한 R 언어 자습서를 설명합니다.

+ 저장 프로시저에서 R 코드를 래핑하고 실행하는 방법에 대해 알아봅니다.
+ r 기반 모델을 직렬화하고 SQL Server 데이터베이스에 저장합니다.
+ 원격 및 로컬 컴퓨팅 컨텍스트와 이러한 컨텍스트를 사용하는 시기에 대해 알아봅니다.
+ 데이터 과학 및 기계 학습 작업을 위한 Microsoft R 라이브러리를 살펴보세요.

<a name="bkmk_sqltutorials"></a>

## <a name="r-quickstarts-and-tutorials"></a>R 빠른 시작 및 자습서

| 링크 | Description |
|------|-------------|
| [빠른 시작: 간단한 R 스크립트 만들기 및 실행](quickstart-r-create-script.md) | 몇 가지 빠른 시작에서 첫 번째는 SQL Server Management Studio와 같은 T-SQL 쿼리 편집기를 사용하여 R 함수를 호출하는 기본 구문을 보여 주는 것입니다. |
| [자습서: 데이터 과학자를 위한 데이터베이스 내 R 분석 알아보기](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) | SQL Server를 처음 사용하는 R 개발자를 위해 이 자습서에서는 SQL Server에서 일반적인 데이터 과학 작업을 수행하는 방법을 설명합니다. 데이터를 로드 및 시각화하고, 모델을 학습하여 SQL Server에 저장하고, 예측 분석을 위해 모델을 사용합니다. |
| [자습서: SQL 개발자를 위한 데이터베이스 내 R 분석 알아보기](../tutorials/sqldev-in-database-r-for-sql-developers.md) | [!INCLUDE[tsql](../../includes/tsql-md.md)] 도구만 사용하여 전체 R 솔루션을 빌드 및 배포합니다. 솔루션을 프로덕션으로 전환하는 데 중점을 둡니다. R 코드를 저장 프로시저에 래핑하고, R 모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장하고, 예측을 위해 매개 변수가 있는 R 모델 호출을 수행하는 방법을 알아봅니다. |
| [자습서: RevoScaleR 심층 분석](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) | RevoScaleR 패키지의 기능을 사용하는 방법에 대해 알아봅니다. R과 SQL Server 간에 데이터를 이동하고 특정 작업에 맞게 컴퓨팅 컨텍스트를 전환합니다. 모델 및 플롯을 만들어 개발 환경과 데이터베이스 서버 간에 이동합니다. |

<a name ="bkmk_samples"></a>

## <a name="code-samples"></a>코드 샘플

| 링크 | Description |
|------|-------------|
| [R 및 SQL Server를 사용하여 예측 모델 빌드](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction) | 스키 대여 사업에서 기계 학습을 사용하여 향후 대여 상황을 예측함으로써 향후 수요에 맞도록 효과적으로 사업 계획을 준비하고 직원이 대비할 수 있는 방법을 알아봅니다. |
| [R 및 SQL Server를 사용하여 고객 클러스터링 수행](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/) | 자율 학습을 사용하여 판매 데이터를 기준으로 고객을 분류합니다. |

## <a name="see-also"></a>참고 항목

+ [SQL Server에 대한 R 확장](../concepts/extension-r.md)
+ [SQL Server Machine Learning Services 자습서](machine-learning-services-tutorials.md)

