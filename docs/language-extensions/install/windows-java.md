---
title: Windows에 Java 언어 확장 설치
titleSuffix: SQL Server Language Extensions
description: Windows에 SQL Server Java 언어 확장을 설치하는 방법을 알아봅니다.
author: dphansen
ms.author: davidph
ms.date: 11/11/2020
ms.topic: how-to
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15'
ms.openlocfilehash: 94b54ce983679f790a560dc1971a36f9fb3c8551
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471794"
---
# <a name="install-sql-server-java-language-extension-on-windows"></a>Windows에 SQL Server Java 언어 확장 설치

[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

Windows에 SQL Server용 [Java 언어 확장](../java-overview.md) 구성 요소를 설치하는 방법을 알아봅니다. Java 언어 확장은 [SQL Server 언어 확장](../language-extensions-overview.md)의 일부입니다.

> [!NOTE]
> 이 문서는 Windows에서의 SQL Server용 Java 언어 확장을 설치하는 데 사용합니다. Linux의 경우, [Linux에 SQL Server Java 언어 확장 설치](../../linux/sql-server-linux-setup-language-extensions-java.md)를 참조하세요.

<a name="prerequisites"></a>

## <a name="pre-install-checklist"></a>설치 전 검사 목록

+ Java 언어 확장 지원을 설치하려면 SQL Server 2019 설치가 필요합니다.

+ 데이터베이스 엔진 인스턴스가 필요합니다. 기존 인스턴스에 증분식으로 추가할 수 있지만 Java 언어 확장 기능만 설치할 수는 없습니다.

+ 비즈니스 연속성을 위해 [Always On 가용성 그룹](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)이 언어 확장에 대해 지원됩니다. 언어 확장을 설치하고 각 노드에서 패키지를 구성해야 합니다.

+ Java 언어 확장 설치는 SQL Server 2019의 장애 조치(Failover) 클러스터에서 지원됩니다.

+ 도메인 컨트롤러에 SQL Server 언어 확장 또는 Java 언어 확장을 설치하지 마세요. 설치 프로그램의 언어 확장 부분이 실패합니다.

+ 언어 확장 및 [Machine Learning Services](../../machine-learning/index.yml)는 SQL Server 빅 데이터 클러스터에 기본적으로 설치됩니다. 빅 데이터 클러스터를 사용하는 경우에는 이 문서의 단계를 수행하지 않아도 됩니다. 자세한 내용은 [빅 데이터 클러스터에서 Machine Learning Services(Python 및 R) 사용](../../big-data-cluster/machine-learning-services.md)을 참조하세요.

> [!IMPORTANT]
> 설치가 완료되면 이 문서에 설명된 구성 후 단계를 완료해야 합니다. 이러한 단계에는 SQL Server에서 외부 코드를 사용하도록 설정하고 SQL Server가 사용자를 대신하여 Java 코드를 실행하는 데 필요한 계정을 추가하는 것이 포함됩니다. 일반적으로 구성 변경 시 인스턴스를 다시 시작하거나 실행 패드 서비스를 다시 시작해야 합니다.

<a name="java-jre-jdk"></a>

## <a name="java-jre-or-jdk"></a>Java JRE 또는 JDK

SQL Server에서 Java를 설치하고 사용하려면 다음 두 가지 방법을 사용합니다.

1. 기본 Java 런타임인 Zulu Open JRE 버전 11.0.3을 사용합니다. 이 런타임이 지원되며 SQL Server 설치에 포함되어 있습니다.

1. 기본 Java 런타임 대신 기본 Java 배포를 사용합니다.

    Java 11이 현재 Windows에서 지원되는 버전입니다. JRE(Java Runtime Environment)가 최소 요구 사항이지만, Java 컴파일러 및 개발 패키지를 필요로 하는 경우 JDK(Java Development Kit)가 유용합니다. JDK는 모두 포함하므로 JDK를 설치하는 경우 JRE가 필요하지 않습니다. Windows에서는 가능한 경우 기본 `/Program Files/` 폴더 아래에 JDK를 설치하는 것이 좋습니다. 그렇지 않으면 실행 파일에 대한 사용 권한을 부여하기 위한 추가 구성이 필요합니다. 자세한 내용은 이 문서의 [권한 부여(Windows)](#perms-nonwindows) 섹션을 참조하세요.

    > [!NOTE]
    > Java는 이전 버전과 호환되므로 이전 버전도 작동할 수 있지만 SQL Server 2019에서 지원되고 테스트된 버전은 Java 11입니다.

## <a name="get-the-installation-media"></a>설치 미디어 다운로드

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>설치 프로그램 실행

로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.

1. SQL Server 2019용 설치 마법사를 시작합니다.
  
1. **설치** 탭에서 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가** 를 선택합니다.

    ![SQL Server 2019 설치](../media/sql-install.png) 

1. **기능 선택** 페이지에서 다음 옵션을 선택합니다.
  
    - **데이터베이스 엔진 서비스**
  
        SQL Server에서 언어 확장을 사용하려면 데이터베이스 엔진의 인스턴스를 설치해야 합니다. 기본 인스턴스나 명명된 인스턴스를 사용할 수 있습니다.
  
    - **Machine Learning Services 및 언어 확장**
  
        이 옵션은 Java 코드 실행을 지원하는 언어 확장 구성 요소를 설치합니다.

        - 기본 Java 런타임 Zulu Open JRE 11.0.3을 설치하려는 경우에는 **Machine Learning Services 및 언어 확장** 과 **Java** 를 선택합니다.

        - 자체 Java 런타임을 사용하려면 **Machine Learning Services 및 언어 확장** 을 선택합니다. **Java** 는 선택하지 마세요.

        R 및 Python을 사용하려면 [Windows에 SQL Server Machine Learning Services 설치](../../machine-learning/install/sql-machine-learning-services-windows-install.md)를 참조하세요.

    ![언어 확장용 기능 옵션](../media/sql-install-feature-selection.png)

1. 이전 단계에서 **Java** 를 선택하여 기본 Java 런타임을 설치했다면 **Java 설치 위치** 페이지가 표시됩니다.

    **이 설치에 포함된 Open JRE 11.0.3 설치** 를 선택합니다.

    ![Java 설치 위치 선택](../media/sql-install-openjdk.png)

    > [!NOTE]
    > **이 컴퓨터에 설치된 다른 버전의 위치 제공** 은 언어 확장에 사용되지 않습니다.

1. **설치 준비 완료** 페이지에서 이러한 선택 사항이 포함되어 있는지 확인하고 **설치** 를 선택합니다.
  
    + 데이터베이스 엔진 서비스
    + Machine Learning Services 및 언어 확장

    구성 파일이 저장된 `..\Setup Bootstrap\Log` 경로 아래에 있는 폴더의 위치를 확인합니다. 설치가 완료되면 요약 파일에 설치된 구성 요소를 검토할 수 있습니다.

6. 설치가 완료된 후 컴퓨터를 다시 시작하라는 메시지가 나타나면 다시 시작합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 자세한 내용은 [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)을 참조하세요.

## <a name="add-the-jre_home-variable"></a>JRE_HOME 변수 추가

`JRE_HOME`은 Java 인터프리터의 위치를 지정하는 시스템 환경 변수입니다. 이 단계에서는 Windows에서 이에 대한 시스템 환경 변수를 만듭니다.

1. JRE 홈 경로를 찾아 복사합니다.

    예를 들어 기본 Java 런타임 Zulu JRE 11.0.3의 JRE 홈 경로는 `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Binn\AZUL-OpenJDK-JRE\`입니다.

    SQL Server 설치 경로에 따라 또는 다른 Java 런타임을 선택한 경우 JDK 또는 JRE의 위치는 위의 예제 경로와 다를 수 있습니다. JDK를 설치한 경우에도 해당 설치의 일부로 JRE 하위 폴더가 표시되는 경우가 많으므로 이 경우에는 JRE 폴더를 가리킵니다. Java 확장 프로그램은 경로 `%JRE_HOME%\bin\server`에서 `jvm.dll`을 로드하려고 시도합니다.

1. 제어판에서 **시스템 및 보안**, **시스템** 을 차례로 연 다음 **고급 시스템 속성** 을 선택합니다.

1. **환경 변수** 를 선택합니다.

1. JDK/JRE 경로(1단계에 찾음)의 값을 사용하여 `JRE_HOME`에 대한 새 시스템 변수를 만듭니다.

1. [실행 패드](../concepts/extensibility-framework.md#launchpad)를 다시 시작합니다.

    1. [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)를 엽니다.

    1. SQL Server 서비스에서 SQL Server 실행 패드를 마우스 오른쪽 단추로 클릭한 다음 **다시 시작** 을 선택합니다.

<a name="perms-nonwindows"></a>

## <a name="grant-access-to-non-default-jre-folder"></a>기본 JRE 폴더가 아닌 폴더에 대한 액세스 권한 부여

SQL Server에 포함된 기본 Zulu Open JRE를 설치하지 않고 Program Files 아래에 JDK 또는 JRE를 설치하지 않은 경우 다음 단계를 수행해야 합니다. *관리자 권한* 명령줄에서 **icacls** 명령을 실행하여 JRE에 액세스하기 위한 **SQLRUsergroup** 및 SQL Server 서비스 계정(**ALL_APPLICATION_PACKAGES**)에 대한 액세스 권한을 부여합니다. 이 명령은 지정된 디렉터리 경로 아래의 모든 파일 및 폴더에 대한 액세스 권한을 재귀적으로 부여합니다.

1. SQLRUserGroup 권한 부여

    명명된 인스턴스의 경우 인스턴스 이름을 SQLRUsergroup에 추가합니다(예: `SQLRUsergroupINSTANCENAME`).

    ```cmd
    icacls "<PATH to JRE>" /grant "SQLRUsergroup":(OI)(CI)RX /T
    ```
    
    Windows의 Program Files 아래에 있는 기본 폴더에 JDK/JRE를 설치한 경우 이 단계를 건너뛸 수 있습니다.

1. AppContainer 권한 부여

    ```cmd
    icacls “<PATH to JRE>” /grant *S-1-15-2-1:(OI)(CI)RX /T
    ```

    > [!NOTE]
    > 위의 명령은 컴퓨터 SID **S-1-15-2-1** 에 권한을 부여하며 이는 영어 버전 Windows에서의 **ALL APPLICATION PACKAGES** 와 같습니다. 또는 영어 버전 Windows에서 `icacls "<PATH to JRE>" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T`를 사용할 수도 있습니다.

## <a name="restart-the-service"></a>서비스를 다시 시작합니다.

설치가 완료되면 다음 단계를 계속하기 전에 데이터베이스 엔진을 다시 시작하여 스크립트 실행을 사용하도록 설정합니다.

서비스를 다시 시작하면 관련 SQL Server 실행 패드 서비스가 자동으로 다시 시작됩니다.

SSMS의 인스턴스에 대해 **Restart** 명령을 마우스 오른쪽 단추로 클릭하거나 제어판의 **서비스** 패널을 사용하거나 [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)를 사용하여 서비스를 다시 시작할 수 있습니다.

## <a name="enable-script-execution"></a>스크립트 실행 사용

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다. 

1. 언어 확장을 설치한 인스턴스에 연결하고 **새 쿼리** 를 클릭하여 쿼리 창을 열고 다음 명령을 실행합니다.

    ```sql
    sp_configure
    ```

    이때 속성 값 `external scripts enabled`는 **0** 이어야 합니다. 이 기능은 기본적으로 꺼져 있으며, Java 코드를 실행 하기 전에 관리자가 명시적으로 사용하도록 설정해야 합니다.

1. 외부 스크립팅 기능을 사용하도록 설정하려면 다음 문을 실행합니다.

    ```sql
    EXEC sp_configure 'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```

    이미 Machine Learning Services 기능을 사용하도록 설정한 경우 언어 확장에 대해 다시 구성을 실행하지 마세요. 기본 확장성 플랫폼은 둘 모두 지원합니다.

<a name="register_external_language"></a>

## <a name="register-external-language"></a>외부 언어 등록

언어 확장을 사용하려는 각 데이터베이스에 대해 [외부 언어 만들기](../../t-sql/statements/create-external-language-transact-sql.md)를 사용하여 외부 언어를 등록해야 합니다.

다음 예제는 Windows에서 SQL Server의 데이터베이스에 외부 언어가 호출한 Java를 추가합니다.

```SQL
CREATE EXTERNAL LANGUAGE Java
FROM (CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll');
GO
```

자세한 내용은 [외부 언어 만들기](../../t-sql/statements/create-external-language-transact-sql.md)를 참조하세요.

## <a name="verify-installation"></a>설치 확인

설치 로그에서 인스턴스의 설치 상태를 확인합니다.

외부 스크립트를 시작하는 데 사용되는 모든 구성 요소가 실행 중인지 확인하려면 다음 단계를 사용합니다.

1. SQL Server Management Studio 또는 Azure Data Studio에서 새 쿼리 창을 열고 다음 문을 실행합니다.

    ```sql
    EXEC sp_configure 'external scripts enabled'
    ```

    **run_value** 이 이제 1로 설정됩니다.

1. **서비스** 패널 또는 SQL Server 구성 관리자를 열고 **SQL Server 실행 패드 서비스** 가 실행 중인지 확인합니다. 언어 확장이 설치된 모든 데이터베이스 엔진 인스턴스에 대해 하나의 서비스가 있어야 합니다. 서비스에 대한 자세한 내용은 [확장성 프레임워크](../concepts/extensibility-framework.md)를 참조하세요.

## <a name="additional-configuration"></a>추가 구성

확인 단계가 성공하면 SQL Server Management Studio, Azure Data Studio 또는 Visual Studio Code에서 또는 T-SQL 문을 서버로 보낼 수 있는 기타 클라이언트에서 Java 코드를 실행할 수 있습니다.

명령을 실행할 때 오류가 발생하는 경우 이 섹션의 추가 구성 단계를 검토하세요. 서비스 또는 데이터베이스에 적절한 구성을 추가해야 할 수도 있습니다.

인스턴스 수준에서 추가 구성은 다음을 포함할 수 있습니다.

+ [SQL Server Machine Learning Services에 대한 방화벽 구성](../../machine-learning/security/firewall-configuration.md)
+ [추가 네트워크 프로토콜 사용](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
+ [원격 연결 사용](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
+ [SQLRUserGroup에 대한 로그인 만들기](../../machine-learning/security/create-a-login-for-sqlrusergroup.md)

<a name="bkmk_configureAccounts"></a>
<a name="permissions-external-script"></a>

데이터베이스에서는 다음 구성 업데이트가 필요할 수 있습니다.

+ [사용자에게 SQL Server Machine Learning Services 사용 권한 부여](../../machine-learning/security/user-permission.md)
+ [사용자에게 특정 언어를 실행할 수 있는 권한 부여](../../t-sql/statements/create-external-language-transact-sql.md#permissions)

> [!NOTE]
> 추가 구성이 필요한지 여부는 보안 스키마, SQL Server를 설치한 위치, 사용자가 데이터베이스에 연결하여 외부 스크립트를 실행하는 방법에 따라 결정됩니다.

## <a name="suggested-optimizations"></a>권장 최적화

이제 모두 제대로 작동하므로 Java 언어 확장을 지원하도록 서버를 최적화할 수도 있습니다.

### <a name="optimize-the-server-for-java-language-extension"></a>Java 언어 확장을 위한 서버 최적화

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에 대한 기본 설정은 데이터베이스 엔진에서 지원하는 다양한 서비스에 맞게 서버의 균형을 최적화하기 위한 것입니다. 이러한 서비스에는 ETL(추출, 변환 및 로드) 프로세스, 보고, 감사 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 사용하는 애플리케이션이 포함될 수 있습니다. 따라서 기본 설정을 사용할 경우, 특히 메모리를 많이 사용하는 작업에서는 언어 확장을 위한 리소스가 제한될 수도 있습니다.

언어 확장 작업에 적절한 우선 순위와 리소스가 지정되도록 SQL Server Resource Governor를 사용하여 외부 리소스 풀을 구성하는 것이 좋습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진에 할당된 메모리 크기를 변경하거나 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스에서 실행되는 계정 수를 늘릴 수도 있습니다.

+ 외부 리소스 관리를 위해 리소스 풀을 구성하려면 [외부 리소스 풀 만들기](../../t-sql/statements/create-external-resource-pool-transact-sql.md)를 참조하세요.
  
+ 데이터베이스에 예약된 메모리 양을 변경하려면 [서버 메모리 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)을 참조하세요.
  
Standard Edition을 사용 중인 경우 Resource Governor가 없으면 DMV(동적 관리 뷰) 및 확장 이벤트뿐만 아니라 Windows 이벤트 모니터링을 사용하여 서버 리소스를 쉽게 관리할 수 있습니다.

## <a name="next-steps"></a>다음 단계

Java 개발자는 몇 가지 간단한 예제를 시작하고 Java가 SQL Server에서 작동하는 방식의 기초를 알아볼 수 있습니다. 다음 단계는 아래 링크를 참조하세요.

+ [자습서: Java를 사용하는 정규식](../tutorials/search-for-string-using-regular-expressions-in-java.md)
