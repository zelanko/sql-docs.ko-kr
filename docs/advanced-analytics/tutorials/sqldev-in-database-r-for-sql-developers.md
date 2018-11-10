---
title: R 및 SQL Server Machine Learning을 사용 하 여 데이터베이스 내 분석에 대 한 자습서 | Microsoft Docs
description: R 프로그래밍 언어 및 코드에서 SQL Server 저장 프로시저 T-SQL 함수를 포함 하는 방법에 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 80c4d39e87984b022340079be4d944ed6ad963e3
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51030650"
---
# <a name="tutorial-in-database-r-analytics-for-sql-developers"></a>SQL 개발자를 위한 자습서: In-database R 분석
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL 프로그래머를 위한이 자습서에서는 알아봅니다 R 통합에 대 한 빌드 및 사용 하 여 솔루션을 학습 하는 R 기반 컴퓨터를 배포 하 여는 [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) SQL Server 데이터베이스에 있습니다. 

이 자습서는 워크플로 모델링 하는 데이터에 사용 되는 R 함수를 소개 합니다. 데이터 탐색, 작성 및 학습 이진 분류 모델 및 모델 배포를 포함 하는 단계입니다. 뉴욕 시 택시 및 Limosine 위원회에서 샘플 데이터를 사용 하 고 여정 팁의 시간, 보이고, 거리, 승차 위치에 따라 발생할 가능성이 있는지 여부를 예측 하는 모델을 빌드합니다. 이 자습서에 사용 되는 R 코드를 모두 만들고 Management Studio에서 실행 하는 저장된 프로시저에 래핑됩니다.


> [!NOTE]
> 
> 이 자습서는 R 및 Python 모두에 사용할 수 있습니다. Python 버전에 대해서 [데이터베이스 내 분석 Python 개발자를 위한](../tutorials/sqldev-in-database-python-for-sql-developers.md)합니다.

## <a name="overview"></a>개요

Machine learning 솔루션을 구축 하는 과정이 포함 될 수 있는 여러 도구 및 전문가 조정 하는 여러 단계에서 복잡 한:

+ 가져오기 및 데이터 정리
+ 데이터 탐색 및 모델링에 유용한 기능을 구축
+ 학습 및 모델 튜닝
+ 프로덕션에 배포

실제 코드의 개발 및 테스트는 전용 개발 환경을 사용하여 수행하는 것이 가장 좋습니다. 그러나 스크립트를 완전히 테스트 한 후 쉽게 배포할 수 있습니다 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하 여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저의 익숙한 환경에서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]합니다.

새 r과 SQL 프로그래머 라면 여부 새 to SQL이 다중 파트 자습서는 R 개발자가 R 및 SQL Server를 사용 하 여 데이터베이스 내 분석을 수행 하기 위한 일반적인 워크플로 소개 합니다. 

- [탐색 하 고 저장된 프로시저에서 R 함수를 호출 하 여 데이터 모양 및 분포를 시각화 하는 1 단원:](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [2 단원: T-SQL 함수에서 R을 사용 하 여 데이터 기능 만들기](sqldev-create-data-features-using-t-sql.md)
  
- [3 단원: 학습 및 함수 및 저장된 프로시저를 사용 하 여 R 모델 저장](sqldev-train-and-save-a-model-using-t-sql.md)
  
- [4 단원: 저장된 프로시저에 R 모델을 사용 하는 잠재적인 결과 예측 합니다.](../tutorials/sqldev-operationalize-the-model.md)

모델 데이터베이스에 저장 된 후 모델에서 예측에 대 한 호출 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장된 프로시저를 사용 하 여 합니다.

## <a name="prerequisites"></a>필수 구성 요소

모든 작업을 수행할 수 있습니다 사용 하 여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]입니다.

이 자습서에는 데이터베이스 및 테이블 만들기, 데이터를 가져오는 SQL 쿼리를 작성 등 기본적인 데이터베이스 작업 지식이 있다고 가정 합니다. R. 알고 가정 하지 않습니다. 따라서 모든 R 코드가 제공 됩니다. 

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) 또는 [사용 하도록 설정 하는 R 사용 하 여 SQL Server 2017 Machine Learning 서비스](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [R 라이브러리](../r/determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)

+ [사용 권한](../security/user-permission.md)

+ [NYC Taxi 데모 데이터베이스](demo-data-nyctaxi-in-sql.md)


## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [NYC Taxi 데이터베이스 설정](demo-data-nyctaxi-in-sql.md)