---
title: SQL 개발자를 위한 데이터베이스 내 R 분석(자습서) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 21bc5d6af2ad34a23bb56a589f7bcbacb6034ff3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31201985"
---
# <a name="in-database-r-analytics-for-sql-developers-tutorial"></a>SQL 개발자를 위한 데이터베이스 내 R 분석(자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 자습서의 목표는 SQL 프로그래머에게 SQL Server에서 머신 러닝 솔루션을 직접 구축하는 경험을 제공하는 것입니다. 이 자습서에서는 저장 프로시저 내에 R 코드를 포함해서 응용 프로그램 또는 BI 솔루션에 R을 통합하는 방법을 학습합니다.

> [!NOTE]
> 
> Python에서도 동일한 솔루션을 사용할 수 있습니다. SQL Server 2017이 필요합니다. [Python 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)을 참조하십시오.

## <a name="overview"></a>개요

일반적으로 종단 간 솔루션을 빌드하는 프로세스는 데이터 가져오기 및 정리, 데이터 탐색 및 기능 엔지니어링, 모델 학습 및 튜닝, 마지막으로 프로덕션에 모델 배포로 구성됩니다. 실제 코드의 개발 및 테스트는 전용 개발 환경을 사용하여 수행하는 것이 가장 좋습니다. R의 경우 RStudio 또는 [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]를 의미 할 수 있습니다.

그러나 솔루션을 만든 후에는 익숙한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 사용하여 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에 쉽게 배포할 수 있습니다.

이 자습서에서는 솔루션에 필요한 모든 R 코드를 받았다고 가정하고, SQL Server를 사용하여 솔루션을 작성하고 배포하는 데 중점을 둡니다.

- [1 단원: 예제 데이터 다운로드](../tutorials/sqldev-download-the-sample-data.md)

    샘플 데이터 집합 및 샘플 SQL 스크립트 파일을 로컬 컴퓨터로 다운로드합니다.

- [2 단원: SQL server PowerShell을 사용 하 여 데이터 가져오기](../r/sqldev-import-data-to-sql-server-using-powershell.md)

    [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스에서 데이터베이스와 테이블을 만들고 샘플 데이터를 테이블에 로드하는 PowerShell 스크립트를 실행합니다.

- [3 단원: 탐색 하 고 데이터를 시각화 합니다.](../tutorials/sqldev-explore-and-visualize-the-data.md)

    [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저에서 R 패키지 및 함수를 호출하여 기본 데이터 탐색 및 시각화를 수행합니다.

- [4 단원: T-SQL을 사용 하 여 데이터 기능 만들기](../tutorials/sqldev-create-data-features-using-t-sql.md)

    사용자 정의 SQL 함수를 사용하여 새 데이터 특성을 만듭니다.
  
-   [5 단원: 학습 및 T-SQL을 사용 하 여 R 모델을 저장 합니다.](../r/sqldev-train-and-save-a-model-using-t-sql.md)

    저장된 프로시저에서 R을 사용하여 머신 러닝 모델을 작성합니다.  SQL Server 테이블에는 모델을 저장합니다.
  
-   [6 단원: 모델을 운용](../tutorials/sqldev-operationalize-the-model.md)

    모델을 데이터베이스에 저장한 후 저장 프로시저를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 예측을 위해 모델을 호출합니다.

### <a name="scenario"></a>시나리오

이 자습서에서는 잘 알려진 공용 기반으로 데이터 집합, 뉴욕시 택시의 왕복을 사용 합니다. 샘플 코드 훨씬 더 빠르게 실행 되도록 하려면 데이터의 대표 1% 샘플링을 만들었습니다. 특정 여행 인지 여부, 팁은 발생할 가능성이 시간, 거리 및 위치 선정 등의 열에 따라 예측 하는 이진 분류 모델을 작성 하는이 데이터를 사용 합니다.

### <a name="requirements"></a>요구 사항

이 자습서는 데이터베이스 및 테이블 만들기, 테이블로 데이터 가져오기, SQL 쿼리 작성 등 기본적인 데이터베이스 작업에 잘 알고 있는 사용자를 위한 것입니다. 모든 R 코드가 제공되므로 R 개발 환경은 필요하지 않습니다. 숙련 된 SQL 프로그래머는이 예제를 사용 하 여 완료할 수 있어야 합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 하 고 제공 된 PowerShell 스크립트를 실행 합니다.

그러나이 자습서를 시작 하기 전에 이러한 준비 작업을 완료 해야 합니다.

- R 서비스를 사용하여 SQL Server 2016의 인스턴스에 연결하거나 Machine Learning Services 및 R을 사용하여 SQL Server 2017에 연결합니다.
- 이 자습서에 사용 하는 로그인에 데이터베이스를 만들 수 있는 권한이 있어야 합니다. 및 다른 개체 데이터를 업로드 하는 데이터를 선택 하 고 저장된 프로시저를 실행 합니다.

> [!NOTE]
> **를 사용하여 R 코드를 작성하거나 테스트**하지 않는 것[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]이 좋습니다. 저장된 프로시저에 포함 하는 코드에 문제가 있으면 저장된 프로시저에서 반환 되는 정보는 오류의 원인을 파악 하려면 일반적으로 적합 하지 않습니다.
> 
> 디버깅의 경우와 같은 도구를 사용 하면 권장 [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)], 또는 RStudio 합니다. 이 자습서에서 제공하는 R 스크립트는 기존 R 도구를 사용하여 이미 개발 및 디버그되었습니다.

## <a name="next-lesson"></a>다음 단원

[1 단원: 예제 데이터 다운로드](../tutorials/sqldev-download-the-sample-data.md)
