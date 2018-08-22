---
title: R 및 SQL Server Machine Learning을 사용 하 여 데이터베이스 내 분석에 대 한 자습서 | Microsoft Docs
description: SQL Server에 R을 포함 하는 방법을 보여 주는 자습서 저장 프로시저 및 T-SQL 함수
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 16b3a19e8252e35fcefc817be2c8de11471b4eb3
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394521"
---
# <a name="tutorial-learn-in-database-analytics-using-r-in-sql-server"></a>자습서: SQL Server에서 R을 사용 하 여 데이터베이스 내 분석에 알아봅니다
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL 프로그래머를 위한이 자습서에서는 실습을 빌드하고 배포의 machine learning 솔루션을 저장된 프로시저에서 R 코드를 래핑하여 R 언어를 사용 하 여 얻을 수 있습니다.

이 자습서는 뉴욕 시 택시 여행을 기반으로 하는 잘 알려진 공용 데이터 집합을 사용합니다. 샘플 코드를 더 빨리 실행하기 위해 데이터의 대표적인 1 % 샘플링을 만들었습니다. 이 데이터를 사용하여 시간, 거리 및 승차 위치와 같은 열을 기반으로 특정 여행이 팁을 얻는지 여부를 예측하는 이진 분류 모델을 작성합니다.

> [!NOTE]
> 
> Python에서도 동일한 솔루션을 사용할 수 있습니다. SQL Server 2017이 필요합니다. [Python 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)을 참조하십시오.

## <a name="overview"></a>개요

일반적으로 종단 간 솔루션을 빌드하는 프로세스 구성 가져오기 및 데이터, 데이터 탐색 및 기능 엔지니어링, 모델 학습 및 튜닝, 및 마지막으로 프로덕션에 모델 배포 정리 됩니다. 실제 코드의 개발 및 테스트는 전용 개발 환경을 사용하여 수행하는 것이 가장 좋습니다. R의 경우 RStudio 또는 [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]를 의미 할 수 있습니다.

그러나 솔루션을 만든 후에는 익숙한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 사용하여 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에 쉽게 배포할 수 있습니다.

- [1 단원: NYC Taxi 데이터 설정](../tutorials/sqldev-download-the-sample-data.md)

- [2 단원: 탐색 하 고 저장된 프로시저에서 R 함수를 호출 하 여 데이터 모양 및 분포를 시각화](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [3 단원: T-SQL 함수에서 R을 사용 하 여 데이터 기능 만들기](../tutorials/sqldev-create-data-features-using-t-sql.md)
  
- [4 단원: 학습 및 함수 및 저장된 프로시저를 사용 하 여 R 모델 저장](../r/sqldev-train-and-save-a-model-using-t-sql.md)
  
- [5 단원: 래핑 R 코드 운영 화를 위한 저장된 프로시저에서](../tutorials/sqldev-operationalize-the-model.md)합니다. 
  모델을 데이터베이스에 저장한 후 저장 프로시저를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 예측을 위해 모델을 호출합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 자습서에는 데이터베이스 및 테이블 만들기, 데이터를 가져오는 SQL 쿼리를 작성 등 기본적인 데이터베이스 작업 지식이 있다고 가정 합니다. R. 알고 가정 하지 않습니다. 따라서 모든 R 코드가 제공 됩니다. 숙련 된 SQL 프로그래머는 제공 된 PowerShell 스크립트를 GitHub에서 샘플 데이터를 사용할 수 하 고 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 이 예제를 완료 합니다. 

자습서 시작 하기 전에:

- 인스턴스를 구성된 했는지 확인 [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) 하거나 [사용 하도록 설정 하는 R 사용 하 여 SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md#verify-installation)합니다. 또한 [R 라이브러리를 했는지 확인](../r/determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)합니다.
- 이 자습서에서 사용하는 로그인에는 데이터베이스 및 기타 오브젝트를 작성하고, 데이터를 업로드하고, 데이터를 선택하고, 저장 프로시저를 실행할 수 있는 권한이 있어야 합니다.

> [!NOTE]
> **를 사용하여 R 코드를 작성하거나 테스트**하지 않는 것[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]이 좋습니다. 저장된 프로시저에 포함 하는 코드에 문제가 있을 경우 저장된 프로시저에서 반환 되는 정보는 오류의 원인을 파악 하려면 일반적으로 적합 하지 않습니다.
> 
> 디버깅을 위해 [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)] 또는 RStudio와 같은 도구를 사용하는 것이 좋습니다. 이 자습서에서 제공되는 R 스크립트는 기존의 R 도구를 사용하여 이미 개발되고 디버깅되었습니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [1 단원: 샘플 데이터 다운로드](../tutorials/sqldev-download-the-sample-data.md)