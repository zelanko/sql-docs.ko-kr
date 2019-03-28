---
title: R 및 Python 스크립트 실행-SQL Server Machine Learning을 위한 리소스 거 버 넌 스
description: SQL Server 데이터베이스 엔진 인스턴스에서 R 및 Python 워크 로드에 대 한 RAM 메모리, CPU 및 IO를 할당 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2e8b3122f4083d419797abeef5ff96944bac3e6a
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512990"
---
# <a name="resource-governance-for-machine-learning-in-sql-server"></a>SQL server에서 machine learning 위한 리소스 거 버 넌 스
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

데이터 과학 및 기계 학습 알고리즘 계산이 없는 경우입니다. 작업 우선 순위에 따라 데이터 과학에 사용할 수 있는 리소스를 늘려야 할 수 있습니다 또는 감소 R 및 Python 스크립트 실행 하는 경우 리소스를 동시에 실행 되는 다른 서비스의 성능을 손상 됩니다. 

여러 워크 로드 배포 시스템 리소스의 균형을 다시 조정 해야 하는 경우 사용할 수 있습니다 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) CPU, 물리적 IO 및 R 및 Python에 대 한 외부 런타임을 사용 되는 메모리 리소스를 할당할 수 있습니다. 리소스 할당을 이동 하는 경우에 다른 워크 로드 및 서비스에 예약 된 메모리의 양을 줄일 수도 늘려야 함을 해야 합니다. 

> [!NOTE] 
> 리소스 관리자는 Enterprise Edition 기능입니다.

## <a name="default-allocations"></a>기본 할당

기본적으로 machine learning에 대 한 외부 스크립트 런타임을 개 이하의 총 컴퓨터 메모리의 20%로 제한 됩니다. 시스템에서 다르지만 일반적으로 볼 수 있습니다이 한도 모델을 학습 데이터 행 예측 등 심각한 기계 학습 작업에 대 한 부적절 한입니다. 

## <a name="use-resource-governor-to-control-resourcing"></a>리소스 관리 제어를 사용 하 여 리소스 관리자
 
기본적으로 외부 프로세스는 로컬 서버의 총 호스트 메모리의 최대 20%를 사용합니다. 외부 프로세스에 사용할 수 있도록 모든 용량을 활용 하 여 Python 프로세스 및 R 사용 하 여 서버 수준 변경은 기본 리소스 풀을 수정할 수 있습니다.

또는 사용자 지정을 생성할 수 있습니다 *외부 리소스 풀*특정 프로그램, 호스트 또는 다른 조건에서 시작 된 요청에 대 한 리소스 할당을 확인 하려면 관련 된 작업 그룹 및 분류자는 제공합니다. 외부 리소스 풀에 도입 된 리소스 풀의 형식인 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 데이터베이스 엔진에 외부 R 및 Python 프로세스를 관리할 수 있도록 합니다.

1. [리소스 거 버 넌 스를 사용 하도록 설정](https://docs.microsoft.com/sql/relational-databases/resource-governor/enable-resource-governor) (이 기본적으로 해제 되어).

2. 실행 [CREATE EXTERNAL RESOURCE POOL](https://docs.microsoft.com/sql/t-sql/statements/create-external-resource-pool-transact-sql) 뒤에 리소스 풀 만들기 및 구성 하려면 [ALTER RESOURCE GOVERNOR](https://docs.microsoft.com/sql/t-sql/statements/alter-resource-governor-transact-sql) 구현 합니다.

3. 예를 들어 학습 및 점수 매기기 간의 세분화 된 할당에 대 한 작업 그룹을 만듭니다.

4. 외부 처리에 대 한 호출을 가로채는 분류자를 만듭니다.

5. 쿼리 및 사용자가 만든 개체를 사용 하 여 프로시저를 실행 합니다.

연습을 참조 하세요 [R 및 Python에 대 한 외부 스크립트에 대 한 리소스 풀을 만드는 방법](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md) 단계별 지침에 대 한 합니다.

용어 및 일반적인 개념 소개를 참조 하세요 [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md)합니다.

## <a name="processes-under-resource-governance"></a>리소스 거 버 넌 스 프로세스
  
 사용할 수는 *외부 리소스 풀* 데이터베이스 엔진 인스턴스에서 다음과 같은 실행 파일에서 사용 하는 리소스를 관리 하려면:

+ SQL Server에서 로컬로 호출 하거나 원격 계산 컨텍스트에서 SQL Server를 사용 하 여 원격으로 호출 하는 경우 Rterm.exe
+ Python.exe SQL 서버에서 로컬로 호출 하거나 원격 계산 컨텍스트에서 SQL Server를 사용 하 여 원격으로 호출 하는 경우
+ BxlServer.exe 및 위성 프로세스
+ PythonLauncher.dll 등의 실행 패드에서 시작 된 위성 프로세스
  
> [!NOTE]
> 리소스 관리자를 사용 하 여 실행 패드 서비스에 대 한 직접 관리 지원 되지 않습니다. 실행 패드는 Microsoft에서 제공한 호스트 시작 관리자만 수행할 수 있는 신뢰할 수 있는 서비스. 신뢰할 수 있는 시작 관리자는 과도 한 리소스 사용을 방지 하려면 명시적으로 구성 됩니다.
  
## <a name="see-also"></a>참고자료

+ [Machine learning 통합 관리](../r/managing-and-monitoring-r-solutions.md)
+ [기계 학습을 위한 리소스 풀 만들기](../r/how-to-create-a-resource-pool-for-r.md)
+ [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
