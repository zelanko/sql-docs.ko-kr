---
title: Machine learning 워크 로드 관리 및 통합
description: DBA SQL Server 데이터베이스 엔진 인스턴스에 machine learning R 및 Python 하위 시스템을 배포 하기 위한 관리 작업을 검토 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2677b48daf253a85f2b74078bdad7de65e37d572
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715056"
---
# <a name="manage-and-integrate-machine-learning-workloads-on-sql-server"></a>SQL Server에서 기계 학습 워크 로드 관리 및 통합
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서는 여러 작업을 지 원하는 서버 자산에 효율적인 데이터 과학 인프라를 배포 해야 하는 SQL Server 데이터베이스 관리자를 위한 것입니다. SQL Server에서 R 및 Python 코드 실행의 관리와 관련 된 관리 문제 공간을 프레임 합니다. 

## <a name="what-is-feature-integration"></a>기능 통합 이란?

R 및 Python machine learning은 [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) 에서 데이터베이스 엔진 인스턴스에 대 한 확장으로 제공 됩니다. 통합은 기본적으로 다음과 같이 요약 된 보안 계층 및 데이터 정의 언어를 통해 수행 됩니다.

+ 저장 프로시저에는 R 및 Python 코드를 입력 매개 변수로 사용할 수 있는 기능이 있습니다. 개발자 및 데이터 과학자는 [시스템 저장 프로시저](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql?view=sql-server-2017) 를 사용 하거나 해당 코드를 래핑하는 사용자 지정 프로시저를 만들 수 있습니다.
+ 이전에 학습 된 데이터 모델을 사용할 수 있는 t-sql 함수 (즉, [예측](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)). 이 기능은 T-sql을 통해 사용할 수 있습니다. 따라서 machine learning 확장이 설치 되지 않은 시스템에서이를 호출할 수 있습니다.
+ 기존 데이터베이스 로그인 및 역할 기반 권한은 동일한 데이터를 활용 하는 사용자 호출 스크립트를 포함 합니다. 일반적으로 사용자가 쿼리를 통해 데이터에 액세스할 수 없는 경우 스크립트를 통해 데이터에 액세스할 수 없습니다.

## <a name="feature-availability"></a>기능 가용성

R 및 Python 통합은 연속 된 단계를 통해 사용할 수 있습니다. 첫 번째는 데이터베이스 엔진 인스턴스에 Machine Learning Services 기능을 [포함 하거나 추가 ](../install/sql-machine-learning-services-windows-install.md) 하는 경우 설정입니다. 이후 단계로 데이터베이스 엔진 인스턴스에서 외부 스크립팅을 사용 하도록 설정 해야 합니다 (기본적으로 해제 됨).

이 시점에서 데이터베이스 관리자만 외부 스크립트를 만들고 실행 하 고, 패키지를 추가 또는 삭제 하 고, 저장 프로시저 및 기타 개체를 만들 수 있는 모든 권한을 갖습니다.

다른 모든 사용자에 게 모든 외부 스크립트 실행 권한이 부여 되어야 합니다. 추가 [표준 데이터베이스 권한은](../security/user-permission.md) 사용자가 개체를 만들고, 스크립트를 실행 하 고, serialize 된 모델 및 학습 된 모델을 사용할 수 있는지 여부를 결정 합니다. 

## <a name="resource-allocation"></a>리소스 할당

외부 처리를 호출 하는 저장 프로시저 및 T-sql 쿼리는 기본 리소스 풀에 사용할 수 있는 리소스를 사용 합니다. 기본 구성의 일부로 R 및 Python 세션과 같은 외부 프로세스는 호스트 시스템에서 총 메모리의 최대 20%까지 허용 됩니다. 

다시 조정 높아지면를 사용 하려면 해당 시스템에서 실행 되는 machine learning 작업에 해당 하는 영향으로 기본 풀을 수정할 수 있습니다.

또 다른 옵션은 특정 시간 간격 동안 발생 하는 특정 프로그램, 호스트 또는 작업에서 시작 된 세션을 캡처하기 위해 사용자 지정 외부 리소스 풀을 만드는 것입니다. 자세한 내용은 [리소스 관리를 참조 하 여 R 및 Python 실행에 대 한 리소스 수준을 수정](../administration/resource-governance.md) 하는 방법 및 단계별 지침은 [리소스 풀을 만드는 방법](../administration/how-to-create-a-resource-pool.md) 을 참조 하세요.

## <a name="isolation-and-containment"></a>격리 및 포함

처리 아키텍처는 핵심 엔진 처리에서 외부 스크립트를 격리 하도록 설계 되었습니다. R 및 Python 스크립트는 로컬 작업자 계정에서 별도의 프로세스로 실행 됩니다. 작업 관리자에서 SQL Server 서비스 계정과는 다른, 권한이 낮은 로컬 사용자 계정으로 실행 되는 R 및 Python 프로세스를 모니터링할 수 있습니다. 

낮은 권한의 개별 계정에서 R 및 Python 프로세스를 실행 하면 다음과 같은 이점이 있습니다.

+ R 및 Python 세션에서 핵심 엔진 프로세스 격리 코어 데이터베이스 작업에 영향을 주지 않고 R 또는 Python 프로세스를 종료할 수 있습니다. 

+ 호스트 컴퓨터의 외부 스크립트 런타임 프로세스에 대 한 권한을 줄입니다.

최소 권한 계정은 설치 중에 생성 되 고 **SQLRUserGroup**라는 Windows *사용자 계정 풀* 에 배치 됩니다. 기본적으로이 그룹에는 SQL Server의 R 및 Python에 대 한 program 폴더에 있는 실행 파일, 라이브러리 및 기본 제공 데이터 집합을 사용할 수 있는 권한이 있습니다. 

DBA로 SQL Server 데이터 보안을 사용 하 여 스크립트를 실행할 수 있는 권한을 가진 사용자를 지정할 수 있으며, 작업에 사용 되는 데이터는 T-sql 쿼리를 통해 액세스를 제어 하는 동일한 보안 역할을 통해 관리 됩니다. 시스템 관리자는 Acl을 만들어 로컬 서버의 중요 한 데이터에 대 한 **SQLRUserGroup** 액세스를 명시적으로 거부할 수 있습니다.

>[!NOTE]
> 기본적으로 **SQLRUserGroup** 에는 SQL Server 자체의 로그인 또는 권한이 없습니다. 작업자 계정에 데이터 액세스에 대 한 로그인이 필요한 경우 직접 만들어야 합니다. 로그인을 만들기 위해 특별히를 호출 하는 시나리오는 사용자 id가 Windows 사용자이 고 연결 문자열이 신뢰할 수 있는 사용자를 지정 하는 경우 실행 중인 스크립트의 요청, 데이터베이스 엔진 인스턴스의 데이터 또는 작업에 대 한 요청을 지 원하는 것입니다. 자세한 내용은 [데이터베이스 사용자로 SQLRUserGroup 추가](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)를 참조 하세요.

## <a name="disable-script-execution"></a>스크립트 실행 사용 안 함

런어웨이 스크립트의 경우 모든 스크립트 실행을 사용 하지 않도록 설정 하 고, 처음에 외부 스크립트 실행을 사용 하기 위해 이전에 수행 된 단계를 반대로 실행할 수 있습니다.

1. SQL Server Management Studio 또는 다른 쿼리 도구에서이 명령을 실행 하 여를 `external scripts enabled` 0 또는 FALSE로 설정 합니다.

    ```sql
    EXEC sp_configure  'external scripts enabled', 0
    RECONFIGURE WITH OVERRIDE
    ```
2. 데이터베이스 엔진 서비스를 다시 시작 합니다.

이 문제를 해결 한 후에는 데이터베이스 엔진 인스턴스에서 R 및 Python 스크립팅 지원을 다시 시작 하려면 인스턴스에서 스크립트 실행을 다시 사용 하도록 설정 해야 합니다. 자세한 내용은 [스크립트 실행 사용](../install/sql-machine-learning-services-windows-install.md#enable-script-execution) 을 참조 하세요.

## <a name="extend-functionality"></a>기능 확장

데이터 과학에는 패키지 배포 및 관리를 위한 새로운 요구 사항이 도입 되는 경우가 많습니다. 데이터 과학자 경우 사용자 지정 솔루션에서 오픈 소스 및 타사 패키지를 활용 하는 것이 일반적입니다. 이러한 패키지 중 일부는 다른 패키지에 대 한 종속성을 가지 며,이 경우에는 목표에 도달 하기 위해 여러 패키지를 평가 하 고 설치 해야 할 수 있습니다.

서버 자산을 담당 하는 DBA로 서 임의의 R 및 Python 패키지를 프로덕션 서버에 배포 하는 것은 익숙하지 않은 과제를 나타냅니다. 패키지를 추가 하기 전에 외부 패키지에서 제공 하는 기능이 실제로 필요한 지 여부를 평가 해야 합니다 .이는 기본 제공 [R 언어](r-libraries-and-data-types.md) 와 SQL Server 설치 프로그램에서 설치 하는 [Python 라이브러리](../python/python-libraries-and-data-types.md) 에 해당 하는 기능이 없습니다. 

서버 패키지 설치의 대 안으로, 데이터 과학자는 [외부 워크스테이션에서 솔루션을 빌드 및 실행](../r/set-up-a-data-science-client.md)하 여 SQL Server에서 데이터를 검색할 수 있지만 모든 분석이 서버 대신 워크스테이션에서 로컬로 수행 됩니다. 자체. 

이후에 외부 라이브러리 함수가 필요 하며 서버 작업 또는 데이터 전체에 대 한 위험이 발생 하지 않는 경우 여러 방법 중 하나를 선택 하 여 패키지를 추가할 수 있습니다. 대부분의 경우 SQL Server에 패키지를 추가 하려면 관리자 권한이 필요 합니다. 자세히 알아보려면 [SQL Server에 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md) 및 [SQL Server에서 R 패키지 설치](install-additional-r-packages-on-sql-server.md)를 참조 하세요.

> [!NOTE]
> R 패키지의 경우 대체 방법을 사용 하는 경우 패키지 설치에 서버 관리 권한이 특별히 필요 하지 않습니다. 자세한 내용은 [SQL Server에서 R 패키지 설치를](install-additional-r-packages-on-sql-server.md) 참조 하세요.

## <a name="monitoring-script-execution"></a>스크립트 실행 모니터링

에서 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 실행 되는 R 및 Python 스크립트는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 인터페이스에 의해 시작 됩니다. 그러나 실행 패드는 리소스를 적절 하 게 관리 하는 Microsoft에서 제공 하는 보안 서비스 이므로 별도로 리소스를 관리 하거나 모니터링 하지 않습니다.

실행 패드 서비스에서 실행 되는 외부 스크립트는 [Windows 작업 개체](/windows/desktop/ProcThread/job-objects)를 사용 하 여 관리 됩니다. 작업 개체를 사용하면 프로세스 그룹을 하나의 단위로 관리할 수 있습니다. 각 작업 개체는 계층적이며 연결된 모든 프로세스의 특성을 제어합니다. 작업 개체에서 수행된 작업은 작업 개체와 연결된 모든 프로세스에 영향을 줍니다.

즉, 개체와 연결된 하나의 작업을 종료해야 하는 경우 관련된 모든 프로세스도 종료됨에 유의하세요. Windows 작업 개체에 할당된 R 스크립트를 실행 중이며 해당 스크립트가 실행하는 관련된 ODBC 작업을 종료해야 하는 경우 부모 R 스크립트 프로세스도 종료됩니다.

병렬 처리를 사용 하는 외부 스크립트를 시작 하는 경우 단일 Windows 작업 개체가 모든 병렬 자식 프로세스를 관리 합니다.

작업에서 프로세스가 실행되고 있는지 확인하려면 `IsProcessInJob` 함수를 사용합니다.

## <a name="next-steps"></a>다음 단계

+ [확장성 아키텍처](../concepts/extensibility-framework.md) 및 [보안](../concepts/security.md) 의 개념과 구성 요소에 대 한 자세한 배경 정보를 검토 합니다.

+ 기능 설치의 일부로 이미 최종 사용자 데이터 액세스 제어에 대해 잘 알고 있을 수 있지만, 그렇지 않은 경우에는 [사용자에 게 machine learning SQL Server 권한 부여](../security/user-permission.md) 를 참조 하세요. 

+ 계산 집약적 기계 학습 워크 로드를 위해 시스템 리소스를 조정 하는 방법을 알아봅니다. 자세한 내용은 [리소스 풀을 만드는 방법](../administration/how-to-create-a-resource-pool.md)을 참조 하세요.
