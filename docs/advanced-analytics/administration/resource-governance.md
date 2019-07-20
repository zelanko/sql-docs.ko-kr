---
title: R 및 Python 스크립트 실행에 대 한 리소스 관리
description: SQL Server 데이터베이스 엔진 인스턴스에서 R 및 Python 작업에 대 한 RAM 메모리, CPU 및 IO를 할당 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1a665fd92f630b46351ef96cc203c9bbf71f54a2
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345140"
---
# <a name="resource-governance-for-machine-learning-in-sql-server"></a>SQL Server에서 machine learning에 대 한 리소스 관리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

데이터 과학 및 기계 학습 알고리즘은 계산 집약적입니다. 워크 로드 우선 순위에 따라 데이터 과학에 사용할 수 있는 리소스를 증가 시키거나 R 및 Python 스크립트 실행이 동시에 실행 되는 다른 서비스의 성능을 약화 높아지면를 줄일 수 있습니다. 

여러 작업에서 시스템 리소스 배포의 균형을 다시 조정 해야 하는 경우 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) 를 사용 하 여 R 및 Python의 외부 런타임에 사용 되는 CPU, 물리적 IO 및 메모리 리소스를 할당할 수 있습니다. 리소스 할당을 이동 하는 경우 다른 워크 로드 및 서비스에 예약 된 메모리의 양을 줄여야 할 수도 있습니다. 

> [!NOTE] 
> Resource Governor은 Enterprise Edition 기능입니다.

## <a name="default-allocations"></a>기본 할당

기본적으로 machine learning에 대 한 외부 스크립트 런타임은 총 컴퓨터 메모리의 20%를 초과 하지 않도록 제한 됩니다. 시스템에 따라 다르지만 일반적으로 모델을 학습 하거나 많은 데이터 행을 예측 하는 것과 같은 심각한 기계 학습 작업에 대해이 제한이 적절 하지 않을 수 있습니다. 

## <a name="use-resource-governor-to-control-resourcing"></a>Resource Governor를 사용 하 여 높아지면 제어
 
기본적으로 외부 프로세스는 로컬 서버에서 전체 호스트 메모리의 최대 20%를 사용 합니다. 외부 프로세스에서 사용할 수 있는 용량을 활용 하 여 R 및 Python 프로세스에서 서버 차원의 변경을 수행 하도록 기본 리소스 풀을 수정할 수 있습니다.

또는 관련 작업 그룹 및 분류자를 사용 하 여 사용자 지정 *외부 리소스 풀*을 구성 하 여 특정 프로그램, 호스트 또는 사용자가 제공 하는 다른 기준에서 시작 되는 요청에 대 한 리소스 할당을 확인할 수 있습니다. 외부 리소스 풀은 데이터베이스 엔진 외부에서 R 및 Python 프로세스 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 를 관리할 수 있도록에 도입 된 리소스 풀의 유형입니다.

1. [리소스 관리 사용](https://docs.microsoft.com/sql/relational-databases/resource-governor/enable-resource-governor) 기본적으로 해제 되어 있습니다.

2. [CREATE EXTERNAL RESOURCE pool](https://docs.microsoft.com/sql/t-sql/statements/create-external-resource-pool-transact-sql) 를 실행 하 여 리소스 풀을 만들고 구성한 다음이를 구현 하는 [ALTER resource GOVERNOR](https://docs.microsoft.com/sql/t-sql/statements/alter-resource-governor-transact-sql) 를 실행 합니다.

3. 학습 및 점수 매기기와 같이 세부적인 할당에 대 한 작업 그룹을 만듭니다.

4. 외부 처리에 대 한 호출을 가로채는 분류자를 만듭니다.

5. 만든 개체를 사용 하 여 쿼리 및 프로시저를 실행 합니다.

연습은 단계별 지침은 [외부 R 및 Python 스크립트에 대 한 리소스 풀을 만드는 방법](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md) 을 참조 하세요.

용어 및 일반적인 개념에 대 한 소개는 [Resource Governor 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)을 참조 하세요.

## <a name="processes-under-resource-governance"></a>리소스 관리 중인 프로세스
  
 *외부 리소스 풀* 을 사용 하 여 데이터베이스 엔진 인스턴스에서 다음 실행 파일에 사용 되는 리소스를 관리할 수 있습니다.

+ SQL Server에서 로컬로 호출 되거나 원격 계산 컨텍스트로 SQL Server를 사용 하 여 원격으로 호출 되는 경우
+ Python은 SQL Server에서 로컬로 호출 되거나 원격 계산 컨텍스트로 SQL Server를 사용 하 여 원격으로 호출 됩니다.
+ BxlServer.exe 및 위성 프로세스
+ PythonLauncher와 같이 실행 패드에서 시작한 위성 프로세스
  
> [!NOTE]
> Resource Governor를 사용 하 여 실행 패드 서비스를 직접 관리 하는 것은 지원 되지 않습니다. 실행 패드는 Microsoft에서 제공 하는 실행 기가 호스트 될 수 있는 신뢰할 수 있는 서비스입니다. 신뢰할 수 있는 관리자는 과도 한 리소스를 소모 하지 않도록 명시적으로 구성 됩니다.
  
## <a name="see-also"></a>참조

+ [Machine learning 통합 관리](../r/managing-and-monitoring-r-solutions.md)
+ [기계 학습을 위한 리소스 풀 만들기](../r/how-to-create-a-resource-pool-for-r.md)
+ [리소스 풀 Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
