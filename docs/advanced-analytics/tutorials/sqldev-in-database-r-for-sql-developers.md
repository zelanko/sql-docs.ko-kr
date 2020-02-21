---
title: 'R + T-SQL 자습서: 모델 개발'
description: SQL Server 저장 프로시저 및 T-SQL 함수에 R 프로그래밍 언어 코드를 포함하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9669b2c38d2e8b571ef7e519100b13cf5a63a10d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74479410"
---
# <a name="tutorial-r-data-analytics-for-sql-developers"></a>자습서: SQL 개발자를 위한 R 데이터 분석
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL 프로그래머를 위한 이 자습서에서는 SQL Server에서 [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) 데이터베이스를 사용하여 R 기반 기계 학습 솔루션을 빌드 및 배포하여 R 통합에 대해 알아봅니다. [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 및 R 언어 지원 기능과 함께 T-SQL, SQL Server Management Studio 및 데이터베이스 엔진 인스턴스를 사용합니다.

이 자습서에서는 데이터 모델링 워크플로에 사용되는 R 함수를 소개합니다. 단계에는 데이터 탐색, 이진 분류 모델 빌드 및 학습, 모델 배포가 포함됩니다. 빌드할 모델은 하루의 시간, 이동 거리 및 선택 위치를 기준으로 트립이 팁을 생성할 수 있는지 여부를 예측합니다. 

이 자습서에 사용되는 모든 R 코드는 Management Studio에서 만들고 실행하는 저장 프로시저로 래핑됩니다.

## <a name="background-for-sql-developers"></a>SQL 개발자를 위한 배경

기계 학습 솔루션을 빌드하는 프로세스는 여러 도구를 포함할 수 있는 복잡한 과정이며, 여러 단계에서 실무 전문가의 조율을 위한 것입니다.

+ 데이터 가져오기 및 정리
+ 모델링에 유용한 데이터 탐색 및 기능 빌드
+ 모델 학습 및 튜닝
+ 프로덕션에 배포

실제 코드의 개발 및 테스트는 전용 R 개발 환경을 사용하여 수행하는 것이 가장 좋습니다. 그러나 스크립트가 완전히 테스트된 후에는 익숙한 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 환경에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 쉽게 배포할 수 있습니다.

이 여러 부분으로 구성된 자습서의 목적은 "완료된 R 코드"를 SQL Server로 마이그레이션하는 일반적인 워크플로를 소개하는 것입니다. 

- [1단원: 저장 프로시저에서 R 함수를 호출하여 데이터 형태 및 분포 탐색 및 시각화](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [2단원: T-SQL 함수에서 R을 사용하여 데이터 기능 만들기](sqldev-create-data-features-using-t-sql.md)
  
- [3단원: 함수 및 저장 프로시저를 사용하여 R 모델 학습 및 저장](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [4단원: 저장 프로시저에서 R 모델을 사용하여 잠재적 결과 예측](../tutorials/sqldev-operationalize-the-model.md)

모델을 데이터베이스에 저장한 후 저장 프로시저를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 예측을 위해 모델을 호출합니다.

## <a name="prerequisites"></a>사전 요구 사항

모든 작업은 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 사용하여 수행할 수 있습니다.

이 자습서는 데이터베이스 및 테이블 만들기, 데이터 가져오기, SQL 쿼리 만들기 등의 기본 데이터베이스 작업에 익숙하다고 가정합니다. R을 알고 있다고 가정하지는 않습니다. 따라서 모든 R 코드가 제공됩니다. 

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) 또는 [R이 활성화된 SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [R 라이브러리](../package-management/r-package-information.md)

+ [권한](../security/user-permission.md)

+ [NYC Taxi 데모 데이터베이스](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [저장 프로시저에서 R 함수를 사용하여 데이터 탐색 및 시각화](../tutorials/sqldev-explore-and-visualize-the-data.md)
