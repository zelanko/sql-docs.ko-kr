---
title: 확장 동시 실행 외부 스크립트-SQL Server Machine Learning 서비스
description: SQL Server Machine Learning Services의 크기를 조정 하는 사용자 계정 풀에서 병렬 또는 동시 R 및 Python 스크립트 실행을 구성 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 9f32e51122df8d2d13d6eada726a1a5e9bea82f0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62659514"
---
# <a name="scale-concurrent-execution-of-external-scripts-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services에 대 한 외부 스크립트의 동시 실행 크기 조정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]에 대한 설치 프로세스의 일부로 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스를 통해 태스크 실행을 지원하기 위해 새 Windows *사용자 계정 풀*이 생성됩니다. 이러한 작업자 계정의 목적은 여러 SQL 사용자가 외부 스크립트의 동시 실행을 격리 하는 것입니다.

이 문서에서는 기본 구성 및 용량 작업자 계정 및 SQL Server Machine Learning Services의 동시 실행 외부 스크립트의 수를 조정 하도록 기본 구성을 변경 하는 방법에 대 한 설명입니다.

## <a name="worker-account-group"></a>작업자 계정 그룹

Windows 계정 그룹이 만들어집니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] learning 컴퓨터에 설치 및 사용에 각 인스턴스에 대 한 설치 합니다.

- 기본 인스턴스에서 그룹 이름은 **SQLRUserGroup**입니다. 이름을 R 또는 Python을 사용 하 든 동일 합니다.
- 명명된 인스턴스에서 기본 그룹 이름에는 인스턴스 이름이 접미사로 추가됩니다(예: **SQLRUserGroupMyInstanceName**).

기본적으로 사용자 계정 풀에는 20개의 사용자 계정이 포함됩니다. 대부분의 경우에서 20 기계 학습 작업을 지원 하기 위해 필요한 것 보다 많지만 이지만 계정의 수를 변경할 수 있습니다. 계정의 최대 수는 100입니다.

- 기본 인스턴스에서 개별 계정은 **MSSQLSERVER01**~**MSSQLSERVER20**으로 이름이 지정됩니다.
- 명명된 인스턴스의 경우 인스턴스 이름 뒤에 개별 계정 이름이 지정됩니다(예: **MyInstanceName01**~**MyInstanceName20**).

둘 이상의 인스턴스가 기계를 사용 하는 경우 컴퓨터에 여러 사용자 그룹 해야 합니다. 그룹은 인스턴스 간에 공유할 수 없습니다.

> [!Note]
> SQL Server 2019 **SQLRUserGroup** 단일 SQL Server 실행 패드 서비스 계정이 여러 작업자 계정 대신 현재는 하나의 멤버가 합니다.

<a name = "HowToChangeGroup"> </a>

## <a name="number-of-worker-accounts"></a>작업자 계정 수

계정 풀에서 사용자 수를 수정하려면 아래 설명된 대로 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스의 속성을 편집해야 합니다.

각 사용자 계정과 연결된 암호는 임의로 생성되지만 계정이 생성된 후 나중에 암호를 변경할 수 있습니다.

1. SQL Server 구성 관리자를 열고 **SQL Server Services**를 선택합니다.
2. SQL Server 실행 패드 서비스를 두 번 클릭하고 실행 중인 경우 서비스를 중지합니다.
3.  **서비스** 탭에서 시작 모드가 자동으로 설정되어 있는지 확인합니다. 외부 스크립트 실행 패드를 실행 중이지 않을 때 시작할 수 없습니다.
4.  **고급** 탭을 클릭하고 필요한 경우 **외부 사용자 수**의 값을 편집합니다. 이 설정을 제어 하는 방법을 다양 한 SQL 사용자 세션을 실행할 수 외부 스크립트 동시에 합니다. 기본값은 20 개의 계정. 최대 사용자 수가 100입니다.
5. 암호를 주기적으로 변경해야 하는 정책이 조직에 있는 경우 선택적으로 **외부 사용자 암호 다시 설정** 옵션을 _예_로 설정할 수 있습니다. 이렇게 하면 실행 패드가 사용자 계정용으로 유지 관리하는 암호화된 암호가 다시 생성됩니다. 자세한 내용은 [암호 정책 강제 적용](../security/sql-server-launchpad-service-account.md#bkmk_EnforcePolicy)을 참조하세요.
6.  실행 패드 서비스를 다시 시작 합니다.

## <a name="managing-workloads"></a>워크 로드 관리

이 풀에 대 한 계정 수는 얼마나 많은 외부 스크립트 세션이 동시에 활성화할 수를 결정 합니다.  기본적으로 20 개의 계정이 만들어지면 20 명의 사용자가 활성 R 또는 Python 세션 한 번에 있을 수 있음을 의미 합니다. 20 개 이상의 동시 스크립트를 실행 하려는 경우 작업자 계정 수를 늘릴 수 있습니다.

사용자가 같은 여러 외부 스크립트를 동시에 실행 되 면 해당 사용자가 세션을 실행할 모든 동일한 작업자 계정을 사용 합니다. 예를 들어 단일 사용자 리소스가 허용 되는, 있지만 단일 작업자 계정을 사용 하 여 모든 스크립트 실행 하기만 동시에 실행 하는 100 개의 R 스크립트를 있을 수 있습니다.

모든 단일 사용자가 실행할 수 있는 동시 세션의 수와 지원할 수 있는 작업자 계정 수는 서버 리소스에 의해서만 제한 됩니다. 일반적으로 메모리는 R 런타임을 사용할 때 발생하는 첫 번째 병목 현상입니다.

Python 또는 R 스크립트에서 사용할 수 있는 리소스는 SQL Server에 의해 제어 됩니다. SQL Server DMV를 사용하여 리소스 사용을 모니터링하거나, 연결된 Windows 작업 개체에서 성능 카운터를 확인하고 이에 따라 서버 메모리 사용을 조정하는 것이 좋습니다. SQL Server Enterprise Edition을 사용 하는 경우 구성 하 여 외부 스크립트를 실행 하는 데 사용 되는 리소스를 할당할 수 있습니다는 [외부 리소스 풀](how-to-create-a-resource-pool.md)합니다.

## <a name="see-also"></a>참고자료

용량을 구성 하는 방법에 대 한 자세한 내용은 다음이 문서를 참조 하세요.

- [R Services에 대 한 SQL Server 구성](../../advanced-analytics/r/sql-server-configuration-r-services.md)
- [R Services에 대 한 성능 사례 연구](../../advanced-analytics/r/performance-case-study-r-services.md)