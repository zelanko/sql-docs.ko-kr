---
title: Resource Governor를 사용하여 관리
description: Resource Governor를 사용하여 SQL Server Machine Learning Services에서 Python 및 R 워크로드를 위해 CPU, 물리적 IO 및 메모리 리소스 할당을 관리하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/02/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: bbd55f7796f61bfb2ac85cdfc061f5e754ca70b2
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727722"
---
# <a name="manage-python-and-r-workloads-with-resource-governor-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services에서 Resource Governor를 사용하여 Python 및 R 워크로드 관리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[Resource Governor](../../relational-databases/resource-governor/resource-governor.md)를 사용하여 SQL Server Machine Learning Services에서 Python 및 R 워크로드를 위해 CPU, 물리적 IO 및 메모리 리소스 할당을 관리하는 방법을 알아봅니다.

Python 및 R에서 Machine Learning은 일반적으로 컴퓨팅 집약적입니다. 워크로드 우선 순위에 따라 Machine Learning Services에 사용 가능한 리소스를 늘리거나 줄여야 할 수 있습니다.

자세한 내용은 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)를 참조하세요.

> [!NOTE] 
> Resource Governor는 Enterprise Edition 기능입니다.

## <a name="default-allocations"></a>기본 할당

기본적으로 Machine Learning을 위한 외부 스크립트 런타임은 총 컴퓨터 메모리의 20%를 초과하지 않도록 제한됩니다. 시스템에 따라 달라지지만, 일반적으로 여러 데이터 행에 대한 모델 학습 또는 예측과 같은 심각한 Machine Learning 작업에서는 이러한 제한이 충분하지 않을 수 있습니다. 

## <a name="manage-resources-with-resource-governor"></a>Resource Governor를 사용하여 리소스 관리
 
기본적으로 외부 프로세스는 로컬 서버에서 총 호스트 메모리를 최대 20%까지 사용합니다. 기본 리소스 풀을 수정하여 외부 프로세스에 대해 지정한 용량이 R 및 Python 프로세스에 사용되도록 서버 전체의 설정을 변경할 수 있습니다.

또는 특정 프로그램이나 호스트로부터 시작되는 요청 또는 사용자가 제공한 다른 기준에 따라 리소스 할당을 결정하기 위해 워크로드 그룹 및 분류자가 연결된 사용자 지정 **외부 리소스 풀**을 만들 수 있습니다. 외부 리소스 풀은 데이터베이스 엔진 외부의 R 및 Python 프로세스 관리를 돕기 위해 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]에 도입된 리소스 풀 유형입니다.

1. [리소스 관리를 사용하도록 설정합니다](https://docs.microsoft.com/sql/relational-databases/resource-governor/enable-resource-governor)(기본적으로 해제되어 있음).

2. [CREATE EXTERNAL RESOURCE POOL](https://docs.microsoft.com/sql/t-sql/statements/create-external-resource-pool-transact-sql)을 실행하여 리소스 풀을 만들고 구성한 후 [ALTER RESOURCE GOVERNOR](https://docs.microsoft.com/sql/t-sql/statements/alter-resource-governor-transact-sql)를 실행하여 구현합니다.

3. 학습과 채점 사이의 세부적인 할당을 위한 워크로드 그룹을 만듭니다.

4. 외부 처리를 위해 호출을 가로채는 분류자를 만듭니다.

5. 생성한 개체를 사용하여 쿼리 및 프로시저를 실행합니다.

단계별 지침과 연습은 [외부 R 및 Python 스크립트를 위해 리소스 풀을 만드는 방법](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)을 참조하세요.

용어 및 일반 개념에 대한 소개는 [Resource Governor 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)을 참조하세요.

## <a name="processes-under-resource-governance"></a>리소스 관리 중인 프로세스
  
 *외부 리소스 풀*을 사용하여 데이터베이스 엔진 인스턴스에서 다음과 같은 실행 파일에 사용되는 리소스를 관리합니다.

+ Rterm.exe - SQL Server에서 로컬로 호출되거나 원격 계산 컨텍스트로 SQL Server로 원격으로 호출되는 경우
+ Python.exe - SQL Server에서 로컬로 호출되거나 원격 계산 컨텍스트로 SQL Server로 원격으로 호출되는 경우
+ BxlServer.exe 및 위성 프로세스
+ 실행 패드에서 시작된 위성 프로세스(예: PythonLauncher.dll)
  
> [!NOTE]
> Resource Governor를 사용하여 실행 패드 서비스를 직접 관리자는 작업은 지원되지 않습니다. 실행 패드는 Microsoft에서 제공되는 시작 관리자만 호스트할 수 있는 신뢰할 수 있는 서비스입니다. 신뢰할 수 있는 시작 관리자는 과도한 리소스 사용을 피하기 위해 명시적으로 구성됩니다.
  
## <a name="next-steps"></a>다음 단계

+ [기계 학습을 위한 리소스 풀 만들기](create-external-resource-pool.md)
+ [Resource Governor 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
