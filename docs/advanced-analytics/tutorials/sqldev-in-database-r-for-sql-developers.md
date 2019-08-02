---
title: R을 사용 하 여 데이터베이스 내 분석에 대 한 자습서
description: SQL Server 저장 프로시저 및 T-sql 함수에 R 프로그래밍 언어 코드를 포함 하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e15e56dfb4a27f0a99262ff1f105ceb0a1fbc294
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715383"
---
# <a name="tutorial-r-data-analytics-for-sql-developers"></a>자습서: SQL 개발자를 위한 R 데이터 분석
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL 프로그래머를 위한이 자습서에서는 SQL Server에서 [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) 데이터베이스를 사용 하 여 r 기반 기계 학습 솔루션을 구축 하 고 배포 하 여 r 통합에 대해 알아봅니다. T-sql, SQL Server Management Studio 및 데이터베이스 엔진 인스턴스를 [Machine Learning Services] ([Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 및 R 언어 지원으로 사용 합니다.

이 자습서에서는 데이터 모델링 워크플로에 사용 되는 R 함수를 소개 합니다. 단계에는 데이터 탐색, 이진 분류 모델 빌드 및 학습 및 모델 배포가 포함 됩니다. 작성 하는 모델은 이동이 시간, 거리 이동 및 선택 위치를 기준으로 팁을 생성 하는지 여부를 예측 합니다. 

이 자습서에서 사용 되는 모든 R 코드는 Management Studio에서 만들고 실행 하는 저장 프로시저에 래핑됩니다.

## <a name="background-for-sql-developers"></a>SQL 개발자를 위한 배경

기계 학습 솔루션을 구축 하는 과정은 여러 도구를 포함할 수 있는 복잡 한 방법과 여러 단계에서 실무 전문가의 조정을 위한 것입니다.

+ 데이터 가져오기 및 정리
+ 데이터 탐색 및 모델링에 유용한 기능 빌드
+ 모델 학습 및 튜닝
+ 프로덕션 환경에 배포

실제 코드의 개발 및 테스트는 전용 R 개발 환경을 사용 하 여 수행 하는 것이 가장 좋습니다. 그러나 스크립트를 완전히 테스트 한 후에는의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]친숙 한 환경에서 저장 프로시저 [!INCLUDE[tsql](../../includes/tsql-md.md)] 를 사용 하 여 쉽게 배포할 수 있습니다.

이 여러 부분으로 구성 된 자습서의 목적은 "완료 된 R 코드"를 SQL Server으로 마이그레이션하는 일반적인 워크플로를 소개 하는 것입니다. 

- [1단원: 저장 프로시저에서 R 함수를 호출 하 여 데이터 모양 및 분포를 탐색 하 고 시각화 합니다.](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [2단원: T-sql 함수에서 R을 사용 하 여 데이터 기능 만들기](sqldev-create-data-features-using-t-sql.md)
  
- [3단원: 함수 및 저장 프로시저를 사용 하 여 R 모델 학습 및 저장](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [4단원: 저장 프로시저에서 R 모델을 사용 하 여 잠재적 결과 예측](../tutorials/sqldev-operationalize-the-model.md)

모델을 데이터베이스에 저장 한 후 저장 프로시저를 사용 하 여에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 예측을 위해 모델을 호출 합니다.

## <a name="prerequisites"></a>사전 요구 사항

모든 태스크는의 저장 프로시저 [!INCLUDE[tsql](../../includes/tsql-md.md)] 를 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]사용 하 여 수행할 수 있습니다.

이 자습서에서는 데이터베이스 및 테이블 만들기, 데이터 가져오기 및 SQL 쿼리 작성과 같은 기본적인 데이터베이스 작업에 대해 잘 알고 있는 것으로 가정 합니다. R을 알고 있다고 가정 하지 않습니다. 따라서 모든 R 코드가 제공 됩니다. 

+ [SQL Server 2016 r Services](../install/sql-r-services-windows-install.md#verify-installation) 또는 [r을 사용 하는 SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [R 라이브러리](../package-management/installed-package-information.md)

+ [사용 권한](../security/user-permission.md)

+ [NYC Taxi demo 데이터베이스](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [저장 프로시저에서 R 함수를 사용 하 여 데이터 탐색 및 시각화](../tutorials/sqldev-explore-and-visualize-the-data.md)
