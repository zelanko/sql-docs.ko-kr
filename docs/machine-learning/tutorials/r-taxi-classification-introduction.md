---
title: 'R 자습서: 이진 분류를 사용하여 뉴욕시 택시 요금 예측'
titleSuffix: SQL machine learning
description: 이 5부 자습서 시리즈에서는 이진 분류를 사용하여 뉴욕시 택시 요금을 예측하기 위해 SQL Machine Learning을 통해 SQL Server 저장 프로시저 및 T-SQL 함수에 R 코드를 포함하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/15/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: db8a0c073821df46e6d9d5bda43e74aae19a2501
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94585062"
---
# <a name="r-tutorial-predict-nyc-taxi-fares-with-binary-classification"></a>R 자습서: 이진 분류를 사용하여 뉴욕시 택시 요금 예측
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
SQL 프로그래머를 위한 이 5부 자습서 시리즈에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) 또는 [빅 데이터 클러스터](../../big-data-cluster/machine-learning-services.md)의 R 통합에 대해 알아봅니다.
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
SQL 프로그래머를 위한 이 5부 자습서 시리즈에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)의 R 통합에 대해 알아봅니다.
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
SQL 프로그래머를 위한 이 5부 자습서 시리즈에서는 [SQL Server 2016 R Services](../sql-server-machine-learning-services.md)의 R 통합에 대해 알아봅니다.
::: moniker-end

::: moniker range=">=azuresqldb-mi-current||=sqlallproducts-allversions"
SQL 프로그래머를 위한 이 5부 자습서 시리즈에서는 [Azure SQL Managed Instance의 Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)의 R 통합에 대해 알아봅니다.
::: moniker-end

샘플 SQL Server 데이터베이스를 사용하여 R 기반 기계 학습 솔루션을 빌드 및 배포합니다. T-SQL, Azure Data Studio 또는 SQL Server Management Studio와 SQL Machine Learning 및 R 언어를 지원하는 데이터베이스 엔진 인스턴스를 사용합니다.

이 자습서 시리즈에서는 데이터 모델링 워크플로에 사용되는 R 함수를 소개합니다. 데이터 탐색, 이진 분류 모델 빌드 및 학습, 모델 배포에 관한 부분이 포함됩니다. 뉴욕시 택시 및 리무진 위원회의 샘플 데이터를 사용합니다. 빌드할 모델은 하루 중 시간, 이동 거리 및 승차 위치를 기준으로 트립이 팁을 생성할 수 있는지 여부를 예측합니다.

이 시리즈의 1부에서는 필수 구성 요소를 설치하고 샘플 데이터베이스를 복원합니다. 2부 및 3부에서는 데이터를 준비하고 기계 학습 모델을 학습시키기 위해 R 스크립트를 개발합니다. 그런 다음 4부 및 5부에서는 데이터베이스 내부에서 T-SQL 저장 프로시저를 사용하여 R 스크립트를 실행합니다.

이 문서에서는 다음을 수행합니다.

> [!div class="checklist"]
> + 필수 구성 요소 설치
> + 샘플 데이터베이스 복원

[2부](r-taxi-classification-explore-data.md)에서는 샘플 데이터를 검토하고 몇 가지 플롯을 생성합니다.

[3부](r-taxi-classification-create-features.md)에서는 Transact-SQL 함수를 사용하여 원시 데이터에서 기능을 만드는 방법을 알아봅니다. 그런 다음 저장 프로시저에서 해당 함수를 호출하여 기능 값이 포함된 테이블을 만듭니다.

[4부](r-taxi-classification-train-model.md)에서는 SQL Server 저장 프로시저를 통해 모듈을 로드하고 필요한 함수를 호출하여 모델을 만들고 학습시킵니다.

[5부](r-taxi-classification-deploy-model.md)에서는 4부에서 학습시키고 저장한 모델을 운영하는 방법을 알아봅니다.

> [!NOTE]
> 이 자습서는 R 및 Python 모두에서 사용할 수 있습니다. Python 버전의 경우 [Python 자습서: 이진 분류를 사용하여 뉴욕시 택시 요금 예측](r-taxi-classification-introduction.md)을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation)를 설치
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
+ [SQL Server Machine Learning Services 및 R](../install/sql-machine-learning-services-windows-install.md#verify-installation)을 설치
::: moniker-end

+ [R 라이브러리](../package-management/r-package-information.md)를 설치

+ [Python 스크립트를 실행할 수 있는 권한을 부여](../security/user-permission.md)

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
+ SQL Server 2019부터 격리 메커니즘을 사용하려면 플롯 파일이 저장된 디렉터리에 대한 적절한 권한을 부여해야 합니다. 이러한 권한을 설정하는 방법에 대한 자세한 내용은 [Windows의 SQL Server 2019: Machine Learning Services에 대한 격리 변경 내용의 파일 사용 권한 섹션](../install/sql-server-machine-learning-services-2019.md#file-permissions)을 참조하세요.
::: moniker-end

+ [뉴욕시 택시 데모 데이터베이스](demo-data-nyctaxi-in-sql.md)를 복원

모든 작업은 Azure Data Studio 또는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 사용하여 수행할 수 있습니다.

이 자습서는 데이터베이스 및 테이블 만들기, 데이터 가져오기, SQL 쿼리 만들기 등의 기본 데이터베이스 작업에 익숙하다고 가정합니다. R 관련 지식은 필수가 아니며 모든 R 코드가 제공됩니다.

## <a name="background-for-sql-developers"></a>SQL 개발자를 위한 배경

기계 학습 솔루션을 빌드하는 프로세스는 여러 도구를 포함할 수 있는 복잡한 과정이며, 여러 단계에서 실무 전문가의 조율을 위한 것입니다.

+ 데이터 가져오기 및 정리
+ 모델링에 유용한 데이터 탐색 및 기능 빌드
+ 모델 학습 및 튜닝
+ 프로덕션에 배포

실제 코드의 개발 및 테스트는 전용 R 개발 환경을 사용하여 수행하는 것이 가장 좋습니다. 그러나 스크립트가 완전히 테스트된 후에는 Azure Data Studio 또는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 친숙한 환경에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 쉽게 배포할 수 있습니다. SQL Server에서 코드를 운영화하기 위한 기본 메커니즘은 저장 프로시저에 외부 코드를 래핑하는 것입니다.

모델을 데이터베이스에 저장한 후 저장 프로시저를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 예측을 위해 모델을 호출할 수 있습니다.

이 5부 자습서 시리즈는 R을 처음 사용하는 SQL 프로그래머 또는 SQL이 처음인 R 개발자 모두를 대상으로 R 및 SQL Server에서 데이터베이스 내 분석을 수행하기 위한 일반적인 워크플로를 소개합니다.

## <a name="next-steps"></a>다음 단계

이 문서에서는 다음 작업을 수행합니다.

> [!div class="checklist"]
> + 필수 구성 요소 설치
> + 샘플 데이터베이스 복원

> [!div class="nextstepaction"]
> [R 자습서: 데이터 탐색 및 시각화](r-taxi-classification-explore-data.md)