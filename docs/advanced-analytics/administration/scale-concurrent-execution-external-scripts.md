---
title: 동시 스크립트 크기 조정
description: 사용자 계정 풀에서 병렬 또는 동시 R 및 Python 스크립트 실행을 구성하여 SQL Server Machine Learning Services 크기를 조정합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: c10f92bcb0f8b64441ad4b088c4b8b3e2f62236b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73727697"
---
# <a name="scale-concurrent-execution-of-external-scripts-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services에서 외부 스크립트의 동시 실행 확장
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server Machine Learning Services의 작업자 계정 및 기본 구성을 변경하여 외부 스크립트의 동시 실행 수를 조정하는 방법을 알아봅니다.

Machine Learning Services에 대한 설치 프로세스의 일부로, *서비스별 작업 실행을 지원하기 위해 새로운 Windows*사용자 계정 풀[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]이 생성됩니다. 이러한 작업자 계정의 목적은 여러 SQL Server 사용자에 의한 외부 스크립트의 동시 실행을 격리하는 것입니다.

> [!Note]
> SQL Server 2019에서 **SQLRUserGroup**의 구성원은 여러 작업자 계정이 아닌 단일 SQL Server 실행 패드 서비스 계정 하나뿐입니다. 이 문서에서는 SQL Server 2016 및 2017에 대한 작업자 계정을 설명합니다.

## <a name="worker-account-group"></a>작업자 계정 그룹

Windows 계정 그룹은 Machine Learning이 설치되었고 사용하도록 설정된 각 인스턴스에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 통해 생성됩니다.

- 기본 인스턴스에서 그룹 이름은 **SQLRUserGroup**입니다. 이 이름은 Python이나 R 또는 둘 다를 사용하는지에 관계없이 동일합니다.
- 명명된 인스턴스에서 기본 그룹 이름에는 인스턴스 이름이 접미사로 추가됩니다(예: **SQLRUserGroupMyInstanceName**).

기본적으로 사용자 계정 풀에는 20개의 사용자 계정이 포함됩니다. 대부분의 경우 Machine Learning 작업을 지원하기 위해서는 20이 적절하지만 계정 수를 변경할 수 있습니다. 최대 계정 수는 100입니다.

- 기본 인스턴스에서 개별 계정은 **MSSQLSERVER01**~**MSSQLSERVER20**으로 이름이 지정됩니다.
- 명명된 인스턴스의 경우 인스턴스 이름 뒤에 개별 계정 이름이 지정됩니다(예: **MyInstanceName01**~**MyInstanceName20**).

둘 이상의 인스턴스가 Machine Learning을 사용할 경우 컴퓨터에 여러 사용자 그룹이 포함됩니다. 그룹은 인스턴스 간에 공유될 수 없습니다.

<a name = "HowToChangeGroup"> </a>

## <a name="number-of-worker-accounts"></a>작업자 계정 수

계정 풀에서 사용자 수를 수정하려면 아래 설명된 대로 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스의 속성을 편집해야 합니다.

각 사용자 계정과 연결된 암호는 임의로 생성되지만 계정이 생성된 후 나중에 암호를 변경할 수 있습니다.

1. SQL Server 구성 관리자를 열고 **SQL Server Services**를 선택합니다.
2. SQL Server 실행 패드 서비스를 두 번 클릭하고 실행 중인 경우 서비스를 중지합니다.
3.  **서비스** 탭에서 시작 모드가 자동으로 설정되어 있는지 확인합니다. 실행 패드가 실행되지 않을 때는 외부 스크립트가 시작될 수 없습니다.
4.  **고급** 탭을 클릭하고 필요한 경우 **외부 사용자 수**의 값을 편집합니다. 이 설정은 외부 스크립트 세션을 동시에 실행할 수 있는 SQL 사용자 수를 제어합니다. 기본값은 20개 계정입니다. 최대 사용자 수는 100입니다.
5. 암호를 주기적으로 변경해야 하는 정책이 조직에 있는 경우 선택적으로 **외부 사용자 암호 다시 설정** 옵션을 _예_로 설정할 수 있습니다. 이렇게 하면 실행 패드가 사용자 계정용으로 유지 관리하는 암호화된 암호가 다시 생성됩니다. 자세한 내용은 [암호 정책 강제 적용](../security/sql-server-launchpad-service-account.md#bkmk_EnforcePolicy)을 참조하세요.
6.  실행 패드 서비스를 다시 시작합니다.

## <a name="managing-workloads"></a>워크로드 관리

이 풀의 계정 수에 따라 동시에 활성화될 수 있는 외부 스크립트 세션 수가 결정됩니다.  기본적으로 20개의 계정이 생성되고 이는 한 번에 20명의 사용자가 Python 또는 R 세션을 활성화할 수 있음을 의미합니다. 동시 스크립트를 20개 이상 실행해야 할 경우에는 작업자 계정 수를 늘릴 수 있습니다.

같은 사용자가 여러 외부 스크립트를 동시에 실행할 경우 해당 사용자가 실행하는 모든 세션에는 같은 작업자 계정이 사용됩니다. 예를 들어 단일 사용자는 리소스가 허용되는 한 100개의 Python 또는 R 스크립트를 동시에 실행할 수 있지만, 모든 스크립트가 단일 작업자 계정을 사용하여 실행됩니다.

지원할 수 있는 작업자 계정 수 및 단일 사용자가 실행할 수 있는 동시 세션 수는 서버 리소스에 따라 제한됩니다. 일반적으로 메모리는 Python 또는 R 런타임을 사용할 때 발생하는 첫 번째 병목 현상입니다.

Python 또는 R 스크립트에 사용될 수 있는 리소스는 SQL Server를 통해 관리됩니다. SQL Server DMV를 사용하여 리소스 사용을 모니터링하거나, 연결된 Windows 작업 개체에서 성능 카운터를 확인하고 이에 따라 서버 메모리 사용을 조정하는 것이 좋습니다. SQL Server Enterprise Edition이 있는 경우 [외부 리소스 풀](how-to-create-a-resource-pool.md)을 구성하여 외부 스크립트 실행에 사용되는 리소스를 할당할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [SQL Server Management Studio에서 사용자 지정 보고서를 사용하여 Python 및 R 스크립트 실행 모니터링](../../advanced-analytics/administration/monitor-sql-server-machine-learning-services-using-custom-reports-management-studio.md)
- [DMV(동적 관리 뷰)를 사용하여 SQL Server Machine Learning Services 모니터링](../../advanced-analytics/administration/monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)