---
title: 관리 하 고 SQL server에서 machine learning 워크 로드를 통합할 | Microsoft Docs
description: SQL Server DBA, 데이터베이스 엔진 인스턴스에서 R 및 Python 하위 시스템을 학습 하는 컴퓨터를 배포 하는 것에 대 한 관리 작업을 검토 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e24f9974c55d6d189f7d650902352393e3e62627
ms.sourcegitcommit: c2322c1a1dca33b47601eb06c4b2331b603829f1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50743208"
---
# <a name="manage-and-integrate-machine-learning-workloads-on-sql-server"></a>관리 하 고 SQL server machine learning 워크 로드를 통합 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 여러 워크 로드를 지 원하는 서버 자산에 대해 효율적인 데이터 과학 인프라 배포를 담당 하는 SQL Server 데이터베이스 관리자입니다. 이 프레임 R의 관리와 관련 된 관리 문제 영역 및 Python 코드에서 SQL Server를 실행 합니다. 

## <a name="what-is-feature-integration"></a>기능 통합 이란

R 및 Python 기계 학습에서 제공 하는 [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) 으로 데이터베이스 엔진 인스턴스를 확장 합니다. 통합은 주로 보안 계층과 같이 요약 데이터 정의 언어를 통해.

+ 저장된 프로시저는 R을 허용 하는 기능을 장착 하 고 Python 코드 입력된 매개 변수입니다. 개발자 및 데이터 과학자가 사용할 수는 [시스템 저장 프로시저](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql?view=sql-server-2017) 하거나 코드를 래핑하는 사용자 지정 프로시저를 만듭니다.
+ T-SQL 함수 (즉, [PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql))는 이전에 성향이 습득된 데이터 모델을 사용할 수 있습니다. 이 기능은 T-SQL을 통해 사용할 수 있습니다. 따라서 특히 machine learning 설치 된 확장 없는 시스템 호출 수입니다.
+ 기존 데이터베이스 로그인 및 역할 기반 사용 권한을 동일한 데이터를 활용 하 여 사용자가 호출한 스크립트에 설명 합니다. 일반적으로 사용자가 쿼리를 통해 데이터를 액세스할 수 없는 경우 액세스가 가능한 것은 스크립트를 통해 중 하나입니다.

## <a name="feature-availability"></a>기능 가용성

R 및 Python 통합 단계의 연속을 통해 사용할 수 있습니다. 첫 번째는 설치 때 있습니다 [포함 하거나 추가 합니다 **Machine Learning 서비스** ](../install/sql-machine-learning-services-windows-install.md) 데이터베이스 엔진 인스턴스에 대 한 기능입니다. 후속 단계에서는 (이 기본적으로 해제 되어) 데이터베이스 엔진 인스턴스에서 외부 스크립팅을 활성화 해야 합니다.

이 시점에서 데이터베이스 관리자만 만들고 외부 스크립트를 실행, 추가 하거나 패키지를 삭제 하기 위한 전체 권한을 있고 저장된 프로시저 및 기타 개체를 만듭니다.

다른 모든 사용자에 EXECUTE ANY EXTERNAL SCRIPT 권한이 부여 되어야 합니다. 추가적인 [표준 데이터베이스 사용 권한](../security/user-permission.md) 있는지 여부를 사용자 수 개체 만들기, 스크립트를 실행, serialize 및 학습 된 모델 사용 및 확인 등. 

## <a name="resource-allocation"></a>리소스 할당

저장된 프로시저 및 T-SQL 쿼리 외부 처리를 호출 하는 기본 리소스 풀에 사용할 수 있는 리소스를 사용 합니다. 기본 구성의 일환으로, R 및 Python 세션와 같은 외부 프로세스는 호스트 시스템에서 총 메모리의 20%까지 허용 됩니다. 

리소스 관리를 다시 조정 하려는 경우 해당 시스템에서 실행 되는 machine learning 워크 로드에 해당 효과 사용 하 여 기본 풀을 수정할 수 있습니다.

또 다른 옵션 특정 프로그램, 호스트 또는 특정 시간 간격 동안 발생 하는 작업에서 시작 된 세션을 캡처하는 사용자 정의 외부 리소스 풀을 만드는 것입니다. 자세한 내용은 참조 하세요. [R 및 Python 실행에 대 한 리소스 수준을 수정 하려면 리소스 거 버 넌 스](../administration/resource-governance.md) 하 고 [리소스 풀을 만드는 방법](../administration/how-to-create-a-resource-pool.md) 단계별 지침에 대 한 합니다.

## <a name="isolation-and-containment"></a>격리 및 포함

처리 아키텍처는 핵심 엔진 처리에서 외부 스크립트를 격리 하도록 설계 되었습니다. R 및 Python 스크립트를 로컬 작업자 계정으로 별도 프로세스로 실행합니다. 작업 관리자에서 모니터링할 수 있습니다 R 및 Python 프로세스를 SQL Server 서비스 계정에서 고유 권한이 낮은 로컬 사용자 계정으로 실행 합니다. 

개별 낮은 권한 계정에서 실행 중인 R 및 Python 프로세스에는 다음과 같은 이점이 있습니다.

+ 핵심 데이터베이스 작업에 영향을 주지 않고는 R 또는 Python 프로세스를 종료할 수 있습니다 하는 R 및 Python 세션에서 핵심 엔진 프로세스를 격리 합니다. 

+ 호스트 컴퓨터의 외부 스크립트 런타임 프로세스의 권한이 줄어듭니다.

최소 권한 계정을 설치 하는 동안 생성 되 고는 Windows에서 배치 *사용자 계정 풀* 호출 **SQLRUserGroup**합니다. 기본적으로이 그룹 프로그램 폴더에서 실행 파일, 라이브러리 및 기본 제공 데이터 집합을 R 및 Python에서 SQL Server에 대 한 사용 권한이 있습니다. 

DBA,으로 SQL Server 데이터 보안을 사용 하 여 스크립트를 실행할 수 있는 권한이 있는 사용자 지정 및 작업에 사용 되는 데이터를 제어 하는 보안 역할과 같은 역할에서 관리 되는 T-SQL 쿼리를 통해 액세스 합니다. 시스템 관리자를 거부할 수 있습니다 명시적 **SQLRUserGroup** Acl을 만들어 로컬 서버에서 중요 한 데이터에 액세스 합니다.

>[!NOTE]
> 기본적으로 **SQLRUserGroup** 이 없는 로그인 또는 사용 권한 자체는 SQL Server입니다. 작업자 계정 데이터 액세스에 대 한 로그인이 필요 합니다, 해당 직접 만들어야 합니다. 로그인 만들기에 대 한 명확 하 게 호출 된 경우 사용자 id가 Windows 사용자 및 연결 문자열에는 신뢰할 수 있는 사용자를 지정 하는 경우 데이터 또는 데이터베이스 엔진 인스턴스에 대 한 작업 실행에 포함 된 스크립트에서 요청을 지원 하기 위해서입니다. 자세한 내용은 [SQLRUserGroup을 데이터베이스 사용자로 추가](../../advanced-analytics/security/add-sqlrusergroup-to-database.md)합니다.

## <a name="disable-script-execution"></a>스크립트 실행을 사용 하지 않도록 설정

런어웨이 스크립트 시 모든 스크립트 실행, 애초에 외부 스크립트 실행을 사용 하도록 설정 하려면 이전에 수행할 단계를 역순으로 비활성화할 수 있습니다.

1. SQL Server Management Studio 또는 다른 쿼리 도구에서이 명령을 실행 설정 `external scripts enabled` 0 또는 FALSE로 합니다.

    ```sql
    EXEC sp_configure  'external scripts enabled', 0
    RECONFIGURE WITH OVERRIDE
    ```
2. 데이터베이스 엔진 서비스를 다시 시작 합니다.

이 문제를 해결 한 후 R를 다시 시작 하려는 경우 데이터베이스 엔진 인스턴스에서 스크립팅는 Python 지원 인스턴스에서 스크립트 실행을 다시 사용 하도록 설정 해야 합니다. 자세한 내용은 참조 하세요. [스크립트 실행 활성화](../install/sql-machine-learning-services-windows-install.md#enable-script-execution)

## <a name="extend-functionality"></a>기능 확장

데이터 과학에는 종종 패키지 배포 및 관리에 대 한 새로운 요구 사항을 소개합니다. 데이터 과학자, 사용자 지정 솔루션에서 오픈 소스 및 타사 패키지를 활용 하는 일반적인 방법은 것입니다. 다른 패키지에 종속성이 있는 해당 패키지의 일부,이 경우 평가 하 고 목표에 도달 하는 여러 패키지 설치 해야 할 수 있습니다.

DBA 서버 자산에 대 한 책임으로 알 수 없는 문제를 나타내는 임의 R 및 Python 패키지를 프로덕션 서버로 배포 합니다. 패키지에 추가 하기 전에 기본 제공 되는 해당 항목이 없습니다를 사용 하 여 실제로 필요한 외부 패키지에서 제공 하는 기능 인지를 평가 해야 [R 언어](r-libraries-and-data-types.md) 하 고 [Python 라이브러리](../python/python-libraries-and-data-types.md) 설치 SQL Server 설치 프로그램입니다. 

서버 패키지를 설치 하는 대신, 데이터 과학자가 할 수 있습니다 [빌드 및 외부 워크스테이션에서 솔루션 실행](../r/set-up-a-data-science-client.md), SQL Server에서 데이터를 검색 하지만 모든 분석을 사용 하 여 로컬로 수행 된 워크스테이션 대신 서버 자체에 있습니다. 

외부 라이브러리 함수는 필요 하 고 서버 작업이 나 데이터를 전체적으로 위험 이후에 판단 되는 경우 패키지를 추가 하려면 여러 방법론에서 선택할 수 있습니다. 대부분의 경우에서 SQL Server에 패키지를 추가 하려면 관리자 권한이 필요 합니다. 자세한 내용은를 참조 하세요. [SQL Server에 설치 된 Python 패키지](../python/install-additional-python-packages-on-sql-server.md) 하 고 [SQL Server에 설치할 R 패키지](install-additional-r-packages-on-sql-server.md)합니다.

> [!NOTE]
> R 패키지에 대 한 서버 관리자 권한이 필요 하지 않습니다 특히 패키지 설치에 대 한 대체 방법을 사용 하는 경우. 참조 [SQL Server에 설치할 R 패키지](install-additional-r-packages-on-sql-server.md) 세부 정보에 대 한 합니다.

## <a name="monitoring-script-execution"></a>모니터링 스크립트 실행

실행 되는 R 및 Python 스크립트 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 시작 하는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 인터페이스입니다. 하지만, 실행 패드 리소스가 관리 되거나 리소스를 적절 하 게 관리 하는 Microsoft에서 제공 하는 보안 서비스 이므로 개별적으로 모니터링 하지 않습니다.

실행 패드 서비스에서 실행 되는 외부 스크립트를 사용 하 여 관리 되는 [Windows 작업 개체](/windows/desktop/ProcThread/job-objects)합니다. 작업 개체를 사용하면 프로세스 그룹을 하나의 단위로 관리할 수 있습니다. 각 작업 개체는 계층적이며 연결된 모든 프로세스의 특성을 제어합니다. 작업 개체에서 수행된 작업은 작업 개체와 연결된 모든 프로세스에 영향을 줍니다.

즉, 개체와 연결된 하나의 작업을 종료해야 하는 경우 관련된 모든 프로세스도 종료됨에 유의하세요. Windows 작업 개체에 할당된 R 스크립트를 실행 중이며 해당 스크립트가 실행하는 관련된 ODBC 작업을 종료해야 하는 경우 부모 R 스크립트 프로세스도 종료됩니다.

병렬 처리를 사용 하는 외부 스크립트를 시작 하는 경우 단일 Windows 작업 개체는 모든 병렬 자식 프로세스를 관리 합니다.

작업에서 프로세스가 실행되고 있는지 확인하려면 `IsProcessInJob` 함수를 사용합니다.

## <a name="next-steps"></a>다음 단계

+ 개념 및 구성 요소를 검토 합니다 [확장성 아키텍처](../concepts/extensibility-framework.md) 하 고 [보안](../concepts/security.md) 자세한 배경 정보에 대 한 합니다.

+ 기능 설치의 일부로 이미 할 데이터 액세스를 제어 하지만 그렇지 않은 경우 최종 사용자를 사용 하 여 익숙한 [SQL Server machine learning에 사용자 권한 부여](../security/user-permission.md) 세부 정보에 대 한 합니다. 

+ 계산 집약적 기계 학습 워크 로드에 대 한 시스템 리소스를 조정 하는 방법에 알아봅니다. 자세한 내용은 [리소스 풀을 만드는 방법](../administration/how-to-create-a-resource-pool.md)합니다.
