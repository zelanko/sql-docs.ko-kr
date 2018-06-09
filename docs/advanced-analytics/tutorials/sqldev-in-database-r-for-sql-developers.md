---
title: SQL Server 기계 학습 개발자에 대 한 포함 된 R 분석 자습서 | Microsoft Docs
description: SQL Server에서 R을 포함 하는 방법을 보여 주는 자습서 저장 프로시저 및 T-SQL 함수
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3d2b77d73bb1b8f5d4c507b884d0a09f4647012b
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35250026"
---
# <a name="tutorial-embedded-r-in-stored-procedures-and-t-sql-functions"></a>자습서: T-SQL 함수와 저장된 프로시저에 R을 포함
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 자습서의 목표는 SQL 프로그래머에게 SQL Server에서 머신 러닝 솔루션을 직접 구축하는 경험을 제공하는 것입니다. 이 자습서에서는 저장 프로시저 내에 R 코드를 포함해서 응용 프로그램 또는 BI 솔루션에 R을 통합하는 방법을 학습합니다.

> [!NOTE]
> 
> Python에서도 동일한 솔루션을 사용할 수 있습니다. SQL Server 2017이 필요합니다. [Python 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)을 참조하십시오.

## <a name="overview"></a>개요

일반적으로 종단 간 솔루션을 빌드하는 프로세스는 데이터 가져오기 및 정리, 데이터 탐색 및 기능 엔지니어링, 모델 학습 및 튜닝, 마지막으로 프로덕션에 모델 배포로 구성됩니다. 실제 코드의 개발 및 테스트는 전용 개발 환경을 사용하여 수행하는 것이 가장 좋습니다. R의 경우 RStudio 또는 [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]를 의미 할 수 있습니다.

그러나 솔루션을 만든 후에는 익숙한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저를 사용하여 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에 쉽게 배포할 수 있습니다.

이 자습서에서는 솔루션에 필요한 모든 R 코드를 받았다고 가정하고, SQL Server를 사용하여 솔루션을 작성하고 배포하는 데 중점을 둡니다.

- [1 단원: 샘플 데이터와 스크립트를 다운로드 합니다.](../tutorials/sqldev-download-the-sample-data.md)

- [2 단원: 자습서 환경 설정](../r/sqldev-import-data-to-sql-server-using-powershell.md)

- [탐색 하 고 저장된 프로시저에서 R 함수를 호출 하 여 데이터 모양 및 분포를 시각화 하는 3 단원:](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [4 단원: T-SQL 함수에서 R을 사용 하 여 데이터 기능 만들기](../tutorials/sqldev-create-data-features-using-t-sql.md)
  
- [5 단원: 학습과 함수 및 저장된 프로시저를 사용 하 여 R 모델을 저장 합니다.](../r/sqldev-train-and-save-a-model-using-t-sql.md)
  
- [6 단원: 래핑 R 코드를 해결해줍니다에 대 한 저장된 프로시저에서](../tutorials/sqldev-operationalize-the-model.md)합니다. 
  모델을 데이터베이스에 저장한 후 저장 프로시저를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 예측을 위해 모델을 호출합니다.

## <a name="scenario"></a>시나리오

이 자습서는 뉴욕 시 택시 여행을 기반으로 하는 잘 알려진 공용 데이터 집합을 사용합니다. 샘플 코드를 더 빨리 실행하기 위해 데이터의 대표적인 1 % 샘플링을 만들었습니다. 이 데이터를 사용하여 시간, 거리 및 승차 위치와 같은 열을 기반으로 특정 여행이 팁을 얻는지 여부를 예측하는 이진 분류 모델을 작성합니다.

## <a name="requirements"></a>요구 사항

이 자습서에서는 데이터베이스 및 테이블 만들기, 데이터를 가져오는 경우, SQL 쿼리 작성 등 기본적인 데이터베이스 작업에 익숙하다고를 가정 합니다. 오른쪽을 알고 있는 상속 되지 않습니다. 따라서 모든 R 코드가 제공 됩니다. 숙련 된 SQL 프로그래머는 제공 된 PowerShell 스크립트, GitHub에 샘플 데이터를 사용할 수 및 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 이 예제를 완료 합니다. 

자습서 시작 하기 전에:

- 인스턴스를 구성된 해야 [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation) 또는 [사용 하도록 설정 하는 R 통한 SQL Server 2017 컴퓨터 학습 서비스](../install/sql-machine-learning-services-windows-install.md#verify-installation)합니다. 또한 [R 라이브러리 확인](../r/determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)합니다.
- 이 자습서에서 사용하는 로그인에는 데이터베이스 및 기타 오브젝트를 작성하고, 데이터를 업로드하고, 데이터를 선택하고, 저장 프로시저를 실행할 수 있는 권한이 있어야 합니다.

> [!NOTE]
> **를 사용하여 R 코드를 작성하거나 테스트**하지 않는 것[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]이 좋습니다. 저장된 프로시저에 포함 하는 코드에 문제가 있으면 저장된 프로시저에서 반환 되는 정보는 오류의 원인을 파악 하려면 일반적으로 적합 하지 않습니다.
> 
> 디버깅을 위해 [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)] 또는 RStudio와 같은 도구를 사용하는 것이 좋습니다. 이 자습서에서 제공되는 R 스크립트는 기존의 R 도구를 사용하여 이미 개발되고 디버깅되었습니다.

## <a name="next-lesson"></a>다음 단원

[1 단원: 예제 데이터 다운로드](../tutorials/sqldev-download-the-sample-data.md)
