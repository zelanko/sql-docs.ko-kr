---
title: 'Python + T-SQL: 모델 개발'
description: SQL Server 저장 프로시저 및 T-SQL 함수에 Python 코드를 포함하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b67be59da71667167594ef82e67dfef6f8118fbb
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73725215"
---
# <a name="tutorial-python-data-analytics-for-sql-developers"></a>자습서: SQL 개발자를 위한 Python 데이터 분석
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL 프로그래머를 위한 이 자습서에서는 SQL Server에서 [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) 데이터베이스를 사용하여 Python 기반 기계 학습 솔루션을 빌드 및 배포하여 Python 통합에 대해 알아봅니다. [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 및 Python 언어 지원 기능과 함께 T-SQL, SQL Server Management Studio 및 데이터베이스 엔진 인스턴스를 사용합니다.

이 자습서에서는 데이터 모델링 워크플로에 사용되는 Python 함수를 소개합니다. 단계에는 데이터 탐색, 이진 분류 모델 빌드 및 학습, 모델 배포가 포함됩니다. New York City Taxi and Limosine Commission에서 제공되는 샘플 데이터와 모델을 사용하여 하루 중 시간대와 이동 거리 및 승차 위치를 기준으로 팁을 얻을 가능성이 있는 여정을 예측합니다. 

이 자습서에 사용되는 모든 Python 코드는 Management Studio에서 만들고 실행하는 저장 프로시저로 래핑됩니다.

> [!NOTE]
> 이 자습서는 R 및 Python 모두에서 사용할 수 있습니다. R 버전의 경우 [R 개발자를 위한 데이터베이스 내 분석](sqldev-in-database-r-for-sql-developers.md)을 참조하세요.

## <a name="overview"></a>개요

기계 학습 솔루션을 빌드하는 프로세스는 여러 도구를 포함할 수 있는 복잡한 과정이며, 여러 단계에서 실무 전문가의 조율을 위한 것입니다.

+ 데이터 가져오기 및 정리
+ 모델링에 유용한 데이터 탐색 및 기능 빌드
+ 모델 학습 및 튜닝
+ 프로덕션에 배포

실제 코드의 개발 및 테스트는 전용 개발 환경을 사용하여 수행하는 것이 가장 좋습니다. 그러나 스크립트가 완전히 테스트된 후에는 익숙한 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 환경에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 쉽게 배포할 수 있습니다. SQL Server에서 코드를 운영화하기 위한 기본 메커니즘은 저장 프로시저에 외부 코드를 래핑하는 것입니다.

이 다중 파트 자습서는 Python을 처음 사용하는 SQL 프로그래머 또는 SQL이 처음인 Python 개발자 모두를 대상으로 Python 및 SQL Server에서 데이터베이스 내 분석을 수행하기 위한 일반적인 워크플로를 소개합니다. 

+ [1단원: Python을 사용하여 데이터 탐색 및 시각화](sqldev-py3-explore-and-visualize-the-data.md)

+ [2단원: 사용자 지정 SQL 함수를 사용하여 데이터 기능 만들기](sqldev-py4-create-data-features-using-t-sql.md)

+ [3단원: T-SQL을 사용하여 Python 모델 학습 및 저장](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [4단원: 저장 프로시저에서 Python 모델을 사용하여 잠재적 결과 예측](sqldev-py6-operationalize-the-model.md)

모델을 데이터베이스에 저장한 후 저장 프로시저를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 예측을 위해 모델을 호출할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

+ [SQL Server Machine Learning Services 및 Python](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [사용 권한](../security/user-permission.md)

+ [NYC Taxi 데모 데이터베이스](demo-data-nyctaxi-in-sql.md)

모든 작업은 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 사용하여 수행할 수 있습니다.

이 자습서는 데이터베이스 및 테이블 만들기, 데이터 가져오기, SQL 쿼리 만들기 등의 기본 데이터베이스 작업에 익숙하다고 가정합니다. Python 관련 지식은 필수가 아닙니다. 따라서 모든 Python 코드가 제공됩니다. 

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [Python을 사용하여 데이터 탐색 및 시각화](sqldev-py3-explore-and-visualize-the-data.md)
