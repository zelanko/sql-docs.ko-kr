---
title: R-SQL Server Machine Learning을 사용 하 여 데이터베이스 내 분석에 대 한 자습서
description: R 프로그래밍 언어 및 코드에서 SQL Server 저장 프로시저 T-SQL 함수를 포함 하는 방법에 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2c9cce03a5a2255353702fd99b8efb6e3e598ad5
ms.sourcegitcommit: 299b63e04498eba22659970cd077f247c1657931
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898978"
---
# <a name="tutorial-r-data-analytics-for-sql-developers"></a>자습서: SQL 개발자를 위한 R 데이터 분석
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL 프로그래머를 위한이 자습서에서는 알아봅니다 R 통합에 대 한 빌드 및 사용 하 여 솔루션을 학습 하는 R 기반 컴퓨터를 배포 하 여는 [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) SQL Server 데이터베이스에 있습니다. T-SQL, SQL Server Management Studio 및 [Machine Learning 서비스]를 사용 하 여 데이터베이스 엔진 인스턴스를 사용할지 ([Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 및 R 언어 지원

이 자습서는 워크플로 모델링 하는 데이터에 사용 되는 R 함수를 소개 합니다. 데이터 탐색, 작성 및 학습 이진 분류 모델 및 모델 배포를 포함 하는 단계입니다. 여정 팁의 시간, 보이고, 거리, 승차 위치에 따라 발생할 가능성이 있는지 여부를 예측 하는 모델을 빌드합니다. 

이 자습서에 사용 되는 R 코드를 모두 만들고 Management Studio에서 실행 하는 저장된 프로시저에 래핑됩니다.

## <a name="background-for-sql-developers"></a>SQL 개발자를 위한 백그라운드

Machine learning 솔루션을 구축 하는 과정이 포함 될 수 있는 여러 도구 및 전문가 조정 하는 여러 단계에서 복잡 한:

+ 가져오기 및 데이터 정리
+ 데이터 탐색 및 모델링에 유용한 기능을 구축
+ 학습 및 모델 튜닝
+ 프로덕션에 배포

실제 코드의 개발 및 테스트 전용된 R 개발 환경을 사용 하 여 수행 가장 됩니다. 그러나 스크립트를 완전히 테스트 한 후 쉽게 배포할 수 있습니다 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하 여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저의 익숙한 환경에서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]합니다.

이 다중 파트 자습서의 목적은 마이그레이션 "완료 되도록 R 코드를" SQL Server에 대 한 일반적인 워크플로를 소개 합니다. 

- [1단원: 탐색 하 고 저장된 프로시저에서 R 함수를 호출 하 여 데이터 모양 및 분포를 시각화](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [2단원: T-SQL 함수에서 R을 사용 하 여 데이터 기능 만들기](sqldev-create-data-features-using-t-sql.md)
  
- [3단원: 학습 및 저장 함수 및 저장된 프로시저를 사용 하 여 R 모델](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [4단원: 저장된 프로시저에 R 모델을 사용 하 여 잠재적인 결과 예측](../tutorials/sqldev-operationalize-the-model.md)

모델 데이터베이스에 저장 된 후 모델에서 예측에 대 한 호출 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장된 프로시저를 사용 하 여 합니다.

## <a name="prerequisites"></a>사전 요구 사항

모든 작업을 수행할 수 있습니다 사용 하 여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]입니다.

이 자습서에는 데이터베이스 및 테이블 만들기, 데이터를 가져오는 SQL 쿼리를 작성 등 기본적인 데이터베이스 작업 지식이 있다고 가정 합니다. R. 알고 가정 하지 않습니다. 따라서 모든 R 코드가 제공 됩니다. 

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) 또는 [사용 하도록 설정 하는 R 사용 하 여 SQL Server 2017 Machine Learning 서비스](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [R 라이브러리](../r/determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)

+ [사용 권한](../security/user-permission.md)

+ [NYC Taxi 데모 데이터베이스](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [저장된 프로시저에서 R 함수를 사용 하 여 데이터 탐색 및 시각화](../tutorials/sqldev-explore-and-visualize-the-data.md)