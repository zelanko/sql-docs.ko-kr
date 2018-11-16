---
title: 데이터베이스 내 Python 분석 SQL 개발자를 위한 | Microsoft Docs
description: SQL Server 저장 프로시저 및 T-SQL 함수에서 Python 코드를 포함 하는 방법에 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 728ab56a844a6c7a14f5de7e39abc5d38146c85a
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51560385"
---
# <a name="tutorial-in-database-python-analytics-for-sql-developers"></a>SQL 개발자를 위한 자습서: 데이터베이스 내 Python 분석
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL 프로그래머를 위한이 자습서에서는 알아봅니다 Python 통합에 대 한 빌드 및 사용 하 여 솔루션을 학습 하는 Python 기반 컴퓨터를 배포 하 여는 [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) SQL Server 데이터베이스에 있습니다. 

이 자습서에서는 데이터 워크플로 모델링에 사용 되는 Python 함수 소개 합니다. 데이터 탐색, 작성 및 학습 이진 분류 모델 및 모델 배포를 포함 하는 단계입니다. 뉴욕 시 택시 및 Limosine 위원회에서 샘플 데이터를 사용 하 고 여정 팁의 시간, 보이고, 거리, 승차 위치에 따라 발생할 가능성이 있는지 여부를 예측 하는 모델을 빌드합니다. 이 자습서에 사용 되는 Python 코드를 모두 만들고 Management Studio에서 실행 하는 저장된 프로시저에 래핑됩니다.

> [!NOTE]
> 이 자습서는 R 및 Python 모두에 사용할 수 있습니다. R 버전을 참조 하세요 [데이터베이스 내 분석 R 개발자를 위한](sqldev-in-database-r-for-sql-developers.md)합니다.

## <a name="overview"></a>개요

Machine learning 솔루션을 구축 하는 과정이 포함 될 수 있는 여러 도구 및 전문가 조정 하는 여러 단계에서 복잡 한:

+ 가져오기 및 데이터 정리
+ 데이터 탐색 및 모델링에 유용한 기능을 구축
+ 학습 및 모델 튜닝
+ 프로덕션에 배포

실제 코드의 개발 및 테스트는 전용 개발 환경을 사용하여 수행하는 것이 가장 좋습니다. 그러나 스크립트를 완전히 테스트 한 후 쉽게 배포할 수 있습니다 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하 여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저의 익숙한 환경에서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]합니다. 저장된 프로시저의 외부 코드를 배치 하는 것은 SQL Server의 운영과 코드에 대 한 기본 메커니즘입니다.

Python 또는 SQL로 새 Python 개발자를 새 SQL 프로그래머 라면 여부를이 다중 파트 자습서에서는 Python과 SQL Server를 사용 하 여 데이터베이스 내 분석을 수행 하기 위한 일반적인 과정을 소개 합니다. 

+ [1 단원: 데이터 탐색 및 시각화를 Python을 사용 하 여](sqldev-py3-explore-and-visualize-the-data.md)

+ [2 단원: 사용자 지정 SQL 함수를 사용 하 여 데이터 기능 만들기](sqldev-py4-create-data-features-using-t-sql.md)

+ [3 단원: 학습 및 T-SQL을 사용 하 여 Python 모델 저장](sqldev-py5-train-and-save-a-model-using-t-sql.md)

+ [저장된 프로시저에서 Python 모델을 사용 하 여 잠재적인 결과 예측 하는 4 단원:](sqldev-py6-operationalize-the-model.md)

모델 데이터베이스에 저장 된 후의 예측에 대 한 모델을 호출할 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장된 프로시저를 사용 하 여 합니다.

## <a name="prerequisites"></a>필수 구성 요소

+ [Python 사용 하 여 SQL Server 2017 Machine Learning 서비스](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [사용 권한](../security/user-permission.md)

+ [NYC Taxi 데모 데이터베이스](demo-data-nyctaxi-in-sql.md)

모든 작업을 수행할 수 있습니다 사용 하 여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]입니다.

이 자습서에는 데이터베이스 및 테이블 만들기, 데이터를 가져오는 SQL 쿼리를 작성 등 기본적인 데이터베이스 작업 지식이 있다고 가정 합니다. Python을 알 수는 가정 하지 않습니다. 따라서 모든 Python 코드가 제공 됩니다. 

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [Python을 사용 하 여 데이터 탐색 및 시각화](sqldev-py3-explore-and-visualize-the-data.md)
