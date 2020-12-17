---
title: SQL Server 2016 R Services 설치
titleSuffix: ''
description: Windows에 SQL Server 2016 R Services를 설치하는 방법을 알아봅니다. R Services를 사용하여 데이터베이스 내에서 R 스크립트를 실행할 수 있습니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/06/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: contperfq4
monikerRange: =sql-server-2016
ms.openlocfilehash: 05802b7d3a0bc9f4922cb1db68162d89a576f18c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471134"
---
# <a name="install-sql-server-2016-r-services"></a>SQL Server 2016 R Services 설치

[!INCLUDE[SQL Server 2016 only](../../includes/applies-to-version/sqlserver2016-only.md)]

Windows에 SQL Server 2016 R Services를 설치하는 방법을 알아봅니다. R Services를 사용하여 데이터베이스 내에서 R 스크립트를 실행할 수 있습니다.

> [!NOTE]
> SQL Server 2017 이상에서 R은 Python과 함께 [Machine Learning Services](../sql-server-machine-learning-services.md)에 포함되어 있습니다. R이 필요하고 SQL Server 2017 이상이 있는 경우 [SQL Server Machine Learning Services 설치](sql-machine-learning-services-windows-install.md)를 참조하여 기능을 추가하세요.

<a name="bkmk_prereqs"></a>

## <a name="pre-install-checklist"></a>설치 전 검사 목록

+ 데이터베이스 엔진 인스턴스가 필요합니다. 기존 인스턴스에 증분식으로 추가할 수 있지만 R만 설치할 수는 없습니다.

+ 비즈니스 연속성을 위해 [Always On 가용성 그룹](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)이 R Services에 대해 지원됩니다. 각 노드에서 R Services를 설치하고 패키지를 구성해야 합니다.

+ SQL Server Always On FCI(장애 조치(failover) 클러스터 인스턴스)에는 R Services를 설치하지 마세요. R 프로세스 격리에 사용되는 보안 메커니즘이 SQL Server Always On FCI(장애 조치(failover) 클러스터 인스턴스) 환경과 호환되지 않기 때문입니다.

+ 도메인 컨트롤러에는 R Services를 설치하지 마세요. 설치 시 R Services 부분이 실패하게 됩니다.

+ 데이터베이스 내 인스턴스를 실행하는 동일한 컴퓨터에 **공유 기능** > **R Server(독립 실행형)** 를 설치하지 마세요.

+ 다른 버전의 R과 함께 설치할 수 있지만 권장되지는 않습니다. 이것이 지원되는 이유는 SQL Server 인스턴스가 오픈 소스 R 배포판의 자체 복사본을 사용하기 때문입니다. 그러나 SQL Server 외부의 SQL Server 컴퓨터에서 R을 사용하는 코드를 실행하면 여러 가지 문제가 발생할 수 있습니다.

  + SQL Server에서 실행하는 경우와 다른 라이브러리 및 다른 실행 파일을 사용하여 다른 결과를 얻을 수 있습니다.
  + 외부 라이브러리에서 실행되는 R 스크립트는 SQL Server로 관리할 수 없으며 리소스 경합이 발생할 수 있습니다.
  
> [!IMPORTANT]
> 설치가 완료되면 이 문서에 설명된 구성 후 추가 단계를 완료해야 합니다. 이러한 단계에는 SQL Server에서 외부 스크립트를 사용하도록 설정하고 SQL Server가 사용자를 대신하여 R 작업을 실행하는 데 필요한 계정을 추가하는 것이 포함됩니다. 일반적으로 구성 변경 시 인스턴스를 다시 시작하거나 실행 패드 서비스를 다시 시작해야 합니다.

## <a name="get-the-installation-media"></a>설치 미디어 다운로드

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

### <a name="install-patch-requirement"></a>패치 설치 요구 사항

Microsoft는 SQL Server에서 필수 조건으로 설치되는 Microsoft VC++ 2013 런타임 이진 파일의 특정 버전과 관련된 문제를 확인했습니다. VC 런타임 이진 파일에 대한 이 업데이트가 없으면 SQL Server의 특정 시나리오에서 안정성 문제를 발생할 수 있습니다. SQL Server를 설치하기 전에 [SQL Server 릴리스 정보](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) 의 지침에 따라 해당 컴퓨터에 VC 런타임 이진 파일에 대한 패치가 필요한지 확인하세요.  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>설치 프로그램 실행

로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.

1. SQL Server 2016용 설치 마법사를 시작합니다.

1. **설치** 탭에서 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가** 를 선택합니다.

    ![R Services(데이터베이스 내) 설치](media/2016-setup-installation-rsvcs.png "R Services를 사용하여 데이터베이스 엔진 설치 시작")

1. **기능 선택** 페이지에서 다음 옵션을 선택합니다.

    + **데이터베이스 엔진 서비스** 를 선택합니다. 기계 학습을 사용하는 각 인스턴스에 데이터베이스 엔진이 필요합니다.
    + **R Services(데이터베이스 내)** 를 선택합니다. 데이터베이스 내의 R 사용에 대한 지원을 설치합니다.

    ![R Services 기능 선택](media/2016setup-rsvcs-features.png "데이터베이스 내 R Services에 대해 이러한 기능 선택")

    > [!IMPORTANT]
    > R Server 및 R Services를 동시에 설치하지 않도록 합니다. 

1. **Microsoft R Open 설치에 동의** 페이지에서 **동의** 를 클릭합니다.
  
    이 사용권 계약은 Microsoft R 개발 팀의 연결 공급자 및 고급 R 패키지와 함께 오픈 소스 R 기본 패키지 및 도구 배포가 포함된 Microsoft R Open을 다운로드하는 데 필요합니다.
  
1. 사용권 계약에 동의하면 설치 관리자가 준비되는 동안 잠깐 중지됩니다. **다음** 단추를 사용할 수 있게 되면 클릭합니다.

1. **설치 준비 완료** 페이지에서 다음 항목이 포함되어 있는지 확인한 다음, **설치** 를 선택합니다.

    + 데이터베이스 엔진 서비스
    + R Services(In-database)

1. 설치가 완료된 후 컴퓨터를 다시 시작하라는 메시지가 나타나면 다시 시작합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 자세한 내용은 [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)을 참조하세요.

## <a name="set-environment-variables"></a>환경 변수 설정

R 기능 통합의 경우에만 **MKL_CBWR** 환경 변수를 설정하여 Intel MKL(Math Kernel Library) 계산에서 [일관성 있는 출력을 보장](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)해야 합니다.

1. 제어판에서 **시스템 및 보안** > **시스템** > **고급 시스템 설정** > **환경 변수** 를 클릭합니다.

1. 새 사용자 또는 시스템 변수를 만듭니다.

    + 변수 이름을 `MKL_CBWR`로 설정합니다.
    + 변수 값을 `AUTO`로 설정합니다.

이 단계를 수행하려면 서버를 다시 시작해야 합니다. 모든 구성 작업이 완료될 때까지 다시 시작을 보류할 수 있습니다.

<a name="bkmk_enableFeature"></a>

##  <a name="enable-script-execution"></a>스크립트 실행 사용

1. [SSMS(SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md) 또는 [Azure Data Studio](../../azure-data-studio/what-is.md)를 엽니다.

1. R Services를 설치한 인스턴스에 연결하고 **새 쿼리** 를 클릭하여 쿼리 창을 열고 다음 명령을 실행합니다.

   ```sql
   sp_configure
   ```

    이때 속성 값 `external scripts enabled`는 **0** 이어야 합니다. 기능이 기본적으로 해제되어 있기 때문입니다. R 스크립트를 실행하려면 먼저 관리자가 이 기능을 명시적으로 사용하도록 설정해야 합니다.

1. 외부 스크립팅 기능을 사용하도록 설정하려면 다음 문을 실행합니다.
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>서비스를 다시 시작합니다.

설치가 완료되면 다음 단계를 계속하기 전에 데이터베이스 엔진을 다시 시작하여 스크립트 실행을 사용하도록 설정합니다.

서비스를 다시 시작하면 관련 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스가 자동으로 다시 시작됩니다.

SSMS 인스턴스에 대한 오른쪽 클릭 **다시 시작** 명령을 사용하거나 [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)를 사용하여 서비스를 다시 시작할 수 있습니다.

## <a name="verify-installation"></a>설치 확인

외부 스크립트를 시작하는 데 사용되는 모든 구성 요소가 실행 중인지 확인하려면 다음 단계를 사용합니다.

1. SQL Server Management Studio에서 새 쿼리 창을 열고 다음 명령을 실행합니다.

    ```sql
    EXEC sp_configure 'external scripts enabled'
    ```

    이제 **run_value** 가 1로 설정되어야 합니다.

1. SQL Server 구성 관리자를 열고 **SQL Server 실행 패드 서비스** 가 실행 중인지 확인합니다. R이 설치된 모든 데이터베이스 엔진 인스턴스에 서비스가 하나씩 있어야 합니다. 서비스에 대한 자세한 내용은 [확장성 프레임워크](../concepts/extensibility-framework.md)를 참조하세요.

1. 실행 패드가 실행 중인 경우 간단한 R을 실행하여 외부 스크립팅 런타임이 SQL Server와 통신할 수 있는지 확인할 수 있어야 합니다.

    [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 Azure Data Studio에서 새 **쿼리** 창을 열고 다음과 같은 스크립트를 실행합니다.

    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    외부 스크립트 런타임이 처음 로드될 때 스크립트를 실행하는 데 약간의 시간이 걸릴 수 있습니다. 결과가 다음과 같이 표시됩니다.

    | hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>업데이트 적용

데이터베이스 엔진과 기계 학습 구성 요소 모두에 최신 서비스 팩 및 누적 업데이트를 적용하는 것이 좋습니다.

인터넷에 연결된 디바이스에서 누적 업데이트는 일반적으로 Windows 업데이트를 통해 적용되지만 제어되는 업데이트에 대해 아래 단계를 사용할 수도 있습니다. 데이터베이스 엔진에 대한 업데이트를 적용하는 경우 설치 프로그램은 동일한 인스턴스에 설치된 R 라이브러리의 누적 업데이트를 끌어옵니다. 

연결되지 않은 서버에서는 추가 단계가 필요합니다. 자세한 내용은 [인터넷에 액세스할 수 없는 컴퓨터에 구성 요소 설치 > 누적 업데이트 적용](sql-ml-component-install-without-internet-access.md#apply-cu)을 참조하세요.

1. 이미 설치된 기준 인스턴스를 사용하여 시작합니다. SQL Server 2016 초기 릴리스, SQL Server 2016 SP 1 또는 SQL Server 2016 SP 2

1. 누적 업데이트 목록으로 이동합니다. [Microsoft SQL Server에 대한 최신 업데이트](../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)

1. 최신 서비스 팩(아직 기준 인스턴스로 설치되지 않음) 및 누적 업데이트를 선택합니다. 실행 파일이 자동으로 다운로드되고 추출됩니다.

1. 설치 프로그램을 실행합니다. 사용 조건에 동의하고 기능 선택 페이지에서 누적 업데이트가 적용되는 기능을 검토합니다. R Services를 포함하여 현재 인스턴스에 설치된 모든 기능이 표시되어야 합니다. 설치 프로그램은 모든 기능을 업데이트하는 데 필요한 CAB 파일을 다운로드합니다.

1. R 배포판에 대한 사용 조건에 동의하여 마법사를 계속 진행합니다.

> [!NOTE]
> SQL Server 2016 SP2에 대한 CU(누적 업데이트) 14 이상에는 최신 버전의 R 런타임이 포함되어 있습니다. 자세한 내용은 [기본 언어 런타임 버전 변경](change-default-language-runtime-version.md)을 참조하세요.

<a name="bkmk_FollowUp"></a>

## <a name="additional-configuration"></a>추가 구성

외부 스크립트 확인 단계가 성공하면 SQL Server Management Studio, Azure Data Studio 또는 T-SQL 문을 서버로 보낼 수 있는 다른 모든 클라이언트에서 R 명령을 실행할 수 있습니다.

명령을 실행할 때 오류가 발생하는 경우 이 섹션의 추가 구성 단계를 검토하세요. 서비스 또는 데이터베이스에 적절한 구성을 추가해야 할 수도 있습니다.

인스턴스 수준에서 추가 구성은 다음을 포함할 수 있습니다.

* [SQL Server Machine Learning Services에 대한 방화벽 구성](../../machine-learning/security/firewall-configuration.md)
* [추가 네트워크 프로토콜 사용](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [원격 연결 사용](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [디스크 할당량을 관리](/windows/desktop/fileio/managing-disk-quotas)하여 디스크 공간을 소모하는 작업을 실행하는 외부 스크립트 방지

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

데이터베이스에서는 다음 구성 업데이트가 필요할 수 있습니다.

* [사용자에게 SQL Server Machine Learning Services 사용 권한 부여](../../machine-learning/security/user-permission.md)
* [SQLRUserGroup을 데이터베이스 사용자로 추가](../../machine-learning/security/create-a-login-for-sqlrusergroup.md)

> [!NOTE]
> 나열된 변경 내용 중 일부는 필요하지 않으며, 모든 변경 내용이 필요하지 않을 수도 있습니다. 요구 사항은 보안 스키마, SQL Server를 설치한 위치, 사용자가 데이터베이스에 연결하여 외부 스크립트를 실행하는 방법에 따라 결정됩니다. 추가 설치 지침은 여기에서 확인할 수 있습니다. [SQL Server Machine Learning Services 설치](../install/sql-machine-learning-services-windows-install.md)

## <a name="suggested-optimizations"></a>권장 최적화

R을 사용하여 기계 학습을 지원하도록 서버를 최적화하거나 미리 학습된 모델을 설치할 수도 있습니다.

### <a name="add-more-worker-accounts"></a>더 많은 작업자 계정 추가

R을 많이 사용하거나 여러 사용자가 동시에 스크립트를 실행할 것으로 예상되는 경우 실행 패드 서비스에 할당된 작업자 계정 수를 늘릴 수 있습니다. 자세한 내용은 [SQL Server Machine Learning Services에서 외부 스크립트의 동시 실행 확장](../administration/scale-concurrent-execution-external-scripts.md)을 참조하세요.

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>외부 스크립트 실행을 위한 서버 최적화

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에 대한 기본 설정은 데이터베이스 엔진에서 지원하는 다양한 서비스에 맞게 서버의 균형을 최적화하기 위한 것입니다. 이러한 서비스에는 ETL(추출, 변환 및 로드) 프로세스, 보고, 감사 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 사용하는 애플리케이션이 포함될 수 있습니다. 따라서 기본 설정을 사용할 경우, 특히 메모리를 많이 사용하는 작업에서는 기계 학습에 대한 리소스가 제한될 수도 있습니다.

기계 학습 작업에 적절한 우선 순위와 리소스가 지정되도록 SQL Server Resource Governor를 사용하여 외부 리소스 풀을 구성하는 것이 좋습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진에 할당된 메모리 크기를 변경하거나 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스에서 실행되는 계정 수를 늘릴 수도 있습니다.

- 외부 리소스 관리를 위해 리소스 풀을 구성하려면 [외부 리소스 풀 만들기](../../t-sql/statements/create-external-resource-pool-transact-sql.md)를 참조하세요.
  
- 데이터베이스에 예약된 메모리 양을 변경하려면 [서버 메모리 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)을 참조하세요.
  
- [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]에서 시작할 수 있는 R 계정 수를 변경하려면 [SQL Server Machine Learning Services에서 외부 스크립트의 동시 실행 확장](../administration/scale-concurrent-execution-external-scripts.md)을 참조하세요.

Standard Edition을 사용 중인 경우 Resource Governor가 없으면 DMV(동적 관리 뷰) 및 확장 이벤트뿐만 아니라 R에서 사용되는 Windows 이벤트 모니터링을 사용하여 서버 리소스를 쉽게 관리할 수 있습니다.

### <a name="install-additional-r-packages"></a>추가 R 패키지 설치

SQL Server용으로 만든 R 솔루션은 기본 R 함수, SQL Server와 함께 설치된 독점 패키지의 기능 및 SQL Server에서 설치한 오픈 소스 R 버전과 호환되는 타사 R 패키지를 호출할 수 있습니다.

SQL Server에서 사용할 패키지는 인스턴스에서 사용되는 기본 라이브러리에 설치되어야 합니다. R가 컴퓨터에 별도로 설치되어 있거나 패키지를 사용자 라이브러리에 설치한 경우에는 T-SQL에서 해당 패키지를 사용할 수 없습니다.

R 패키지를 설치 및 관리하는 프로세스는 SQL Server 2016 및 SQL Server 2017에서 다릅니다. SQL Server 2016에서 데이터베이스 관리자는 사용자에게 필요한 R 패키지를 설치해야 합니다. SQL Server 2017에서는 데이터베이스 수준으로 패키지를 공유하도록 사용자 그룹을 설정하거나 사용자가 자신의 패키지를 설치할 수 있도록 데이터베이스 역할을 구성할 수 있습니다. 자세한 내용은 [R 도구를 사용하여 패키지 설치](../package-management/install-r-packages-standard-tools.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

R 개발자는 몇 가지 간단한 예제를 시작하고 R이 SQL Server에서 작동하는 방식의 기초를 알아볼 수 있습니다. 다음 단계로 가려면 아래 링크를 참조하세요.

+ [빠른 시작: T-SQL에서 R 사용](../tutorials/quickstart-r-create-script.md)
+ [SQL 기계 학습용 R 자습서](../tutorials/r-tutorials.md)
+ [SQL Machine Learning 설명서](../index.yml)