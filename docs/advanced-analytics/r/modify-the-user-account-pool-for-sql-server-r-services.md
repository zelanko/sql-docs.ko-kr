---
title: SQL Server 기계 학습에 대 한 사용자 계정 풀 수정 | Microsoft Docs
ms.date: 11/03/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 7c1efa87fef881a8b88b0967716ec062cf95e64f
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="modify-the-user-account-pool-for-sql-server-machine-learning"></a>SQL Server 기계 학습에 대 한 사용자 계정 풀 수정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]에 대한 설치 프로세스의 일부로 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스를 통해 태스크 실행을 지원하기 위해 새 Windows *사용자 계정 풀*이 생성됩니다. 이러한 작업자 계정의 목적은 다른 SQL 사용자가 외부 스크립트의 동시 실행을 격리 하는 것입니다.

이 문서에서는 기본 구성, 보안 및 작업자 계정과 기본 구성을 변경 하는 방법에 대 한 용량을 설명 합니다.

**적용 대상:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)], [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="worker-accounts-used-for-external-script-execution"></a>외부 스크립트 실행에 사용 되는 작업자 계정

Windows 계정 그룹이 만들어집니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 학습 되는 대상 컴퓨터에 설치 되었고 사용 각 인스턴스에 대 한 설치 합니다.

-   기본 인스턴스에서 그룹 이름은 **SQLRUserGroup**입니다. R, Python 또는 둘 다 사용 하 여 이름을 같습니다.
-   명명된 인스턴스에서 기본 그룹 이름에는 인스턴스 이름이 접미사로 추가됩니다(예: **SQLRUserGroupMyInstanceName**).

기본적으로 사용자 계정 풀에는 20개의 사용자 계정이 포함됩니다. 대부분의 경우에서 20 개 이상의 기계 학습 작업을 지원 하기 위해 적절 한 이지만 계정의 수를 변경할 수 있습니다.
-  기본 인스턴스에서 개별 계정은 **MSSQLSERVER01**~**MSSQLSERVER20**으로 이름이 지정됩니다.
-   명명된 인스턴스의 경우 인스턴스 이름 뒤에 개별 계정 이름이 지정됩니다(예: **MyInstanceName01**~**MyInstanceName20**).

둘 이상의 인스턴스가 기계 학습을 하는 경우 컴퓨터에 여러 개의 사용자 그룹 해야 합니다. 그룹은 인스턴스 간에 공유할 수 없습니다.

### <a name = "HowToChangeGroup"> </a>작업자 계정의 수를 변경 하는 방법

계정 풀에서 사용자 수를 수정하려면 아래 설명된 대로 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스의 속성을 편집해야 합니다.

각 사용자 계정과 연결된 암호는 임의로 생성되지만 계정이 생성된 후 나중에 암호를 변경할 수 있습니다.

1. SQL Server 구성 관리자를 열고 **SQL Server Services**를 선택합니다.
2. SQL Server 실행 패드 서비스를 두 번 클릭하고 실행 중인 경우 서비스를 중지합니다.
3.  **서비스** 탭에서 시작 모드가 자동으로 설정되어 있는지 확인합니다. 외부 스크립트 실행 패드를 실행 중이지 않을 때 시작할 수 없습니다.
4.  **고급** 탭을 클릭하고 필요한 경우 **외부 사용자 수**의 값을 편집합니다. 이 설정은 제어 얼마나 많은 다른 SQL 사용자 세션을 실행할 수 외부 스크립트 동시에 합니다. 기본값은 20 계정.
5. 암호를 주기적으로 변경해야 하는 정책이 조직에 있는 경우 선택적으로 **외부 사용자 암호 다시 설정** 옵션을 _예_로 설정할 수 있습니다. 이렇게 하면 실행 패드가 사용자 계정용으로 유지 관리하는 암호화된 암호가 다시 생성됩니다. 자세한 내용은 [암호 정책 강제 적용](#bkmk_EnforcePolicy)을 참조하세요.
6.  실행 패드 서비스를 다시 시작 합니다.

## <a name="managing-machine-learning-workloads"></a>컴퓨터 학습 작업 관리

이 풀에 있는 계정의 수는 얼마나 많은 외부 스크립트 세션 동시에 활성화할 수를 결정 합니다.  기본적으로 20 명의 다른 사용자에 활성 Python 또는 R 세션 한 번에 있을 수 있음을 의미 20 계정은 생성 됩니다. 20 개 이상 동시 스크립트를 실행 하는 것으로 예상한 경우 작업자 계정의 수를 늘릴 수 있습니다.

동일한 사용자 동시에 여러 외부 스크립트 실행, 해당 사용자가 세션을 실행 합니다. 모든 작업자 동일한 계정을 사용 합니다. 예를 들어 단일 사용자는 다른 R 스크립트를 100으로 리소스에서 허용 되지만 모든 스크립트 실행의 단일 작업자 계정을 사용 하 여 동시에 실행할 수 있을 수 있습니다.

지원할 수 있는 작업자 계정의 수 및 단일 사용자 실행할 수 있는 동시 세션 수는 서버 리소스에 의해서만 제한 됩니다. 일반적으로 메모리는 R 런타임을 사용할 때 발생하는 첫 번째 병목 현상입니다.

Python 또는 R 스크립트에서 사용할 수 있는 리소스는 SQL Server에 의해 제어 됩니다. SQL Server DMV를 사용하여 리소스 사용을 모니터링하거나, 연결된 Windows 작업 개체에서 성능 카운터를 확인하고 이에 따라 서버 메모리 사용을 조정하는 것이 좋습니다. SQL Server Enterprise Edition의 경우 구성 하 여 외부 스크립트를 실행 하는 데 사용 되는 리소스를 할당할 수 있습니다는 [외부 리소스 풀](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)합니다.

컴퓨터를 관리 하는 방법에 대 한 자세한 내용은 다음이 문서를 참조 작업 용량을 학습 합니다.

- [R 서비스에 대 한 SQL Server 구성](../../advanced-analytics/r/sql-server-configuration-r-services.md)
-  [R 서비스에 대 한 성능 사례 연구](../../advanced-analytics/r/performance-case-study-r-services.md)

## <a name="security"></a>보안

각 사용자 그룹은 특정 인스턴스에서 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스와 연결되며 다른 인스턴스에서 실행되는 R 작업을 지원할 수 없습니다.

각 작업자 계정의 경우 세션이 활성화된 동안 R 스크립트 실행 중에 R 및 SQL Server에서 사용되는 스크립트 개체, 중간 결과 및 기타 정보를 저장할 임시 폴더가 생성됩니다. ExtensibilityData 폴더에 있는 이러한 작업 파일에 대한 액세스는 관리자로 제한되고 이러한 작업 파일은 스크립트가 완료된 후 SQL Server에서 정리됩니다. 

자세한 내용은 [보안 개요](../../advanced-analytics/r-services/security-overview-sql-server-r.md)를 참조하세요.

### <a name="bkmk_EnforcePolicy"></a>암호 정책 강제 적용

암호를 주기적으로 변경해야 하는 정책이 조직에 있는 경우에는 실행 패드 서비스를 통해 실행 패드에서 작업자 계정용으로 유지 관리하는 암호화된 암호를 강제로 다시 생성해야 할 수 있습니다.  

이 설정을 사용하도록 설정하고 암호를 강제로 새로 고치려면 SQL Server 구성 관리자에서 실행 패드 서비스에 대한 **속성** 창을 열고, **고급**을 클릭하고, **외부 사용자 암호 다시 설정**을 **예**로 변경합니다. 이 변경을 적용하면 모든 사용자 계정의 암호가 즉시 다시 생성됩니다. 이 변경 후에 R 스크립트를 사용하려면 실행 패드 서비스를 다시 시작해야 합니다. 이때 새로 생성된 암호를 읽게 됩니다. 

암호를 주기적으로 다시 설정하려면 이 플래그를 수동으로 설정하거나 스크립트를 사용합니다.

### <a name="additional-permission-required-to-support-remote-compute-contexts"></a>원격 계산 컨텍스트를 지원하는 데 필요한 추가 사용 권한

기본적으로 R 작업자 계정 그룹에는 연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 로그인 권한이 **없습니다**. R 사용자가 R 스크립트를 실행하기 위해 원격 클라이언트에서 SQL Server에 연결하거나 스크립트에서 ODBC를 사용하여 추가 데이터를 가져올 경우 이로 인해 문제가 발생할 수 있습니다. 

이러한 시나리오가 지원되는지 확인하려면 데이터베이스 관리자는 R 스크립트가 실행될 SQL Server 인스턴스에 로그인할 권한을 R 작업자 계정 그룹에게 부여해야 합니다(**연결** 권한). 이 라고 *암시 된 인증이*, SQL Server 원격 사용자의 자격 증명을 사용 하 여 R 스크립트를 실행할 수 있도록 합니다.

> [!NOTE]
> SQL 로그인 자격 증명은 R 클라이언트에서 차례로 SQL Server 인스턴스와 ODBC에 명시적으로 전달되기 때문에 SQL 로그인을 사용하여 원격 워크스테이션에서 R 스크립트를 실행하는 경우에는 이 제한이 적용되지 않습니다.


### <a name="how-to-enable-implied-authentication"></a>암시적 인증을 사용하도록 설정하는 방법

1. Python 또는 R 코드를 실행할 인스턴스의 관리자 권한으로 SQL Server Management Studio를 엽니다.

2. 다음 스크립트를 실행합니다. 기본값, 컴퓨터 및 인스턴스 이름을 변경한 경우 사용자 그룹 이름을 편집해야 합니다.

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ````

