---
title: Linux에 SQL Server 언어 확장(Java) 설치
description: Red Hat, Ubuntu 및 SUSE에서 SQL Server 언어 확장(Java)을 설치하는 방법에 대해 알아보세요.
author: dphansen
ms.author: davidph
ms.reviewer: vanto
manager: cgronlun
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3f4f4bad8bbe72681b699af25b87eb4a533b7002
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653529"
---
# <a name="install-sql-server-2019-language-extensions-java-on-linux"></a>Linux에 SQL Server 2019 언어 확장(Java) 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

언어 확장은 데이터베이스 엔진의 추가 기능입니다. [데이터베이스 엔진과 언어 확장을 동시에 설치](#install-all)할 수 있지만, 더 많은 구성 요소를 추가하기 전에 문제를 해결할 수 있도록 먼저 SQL Server 데이터베이스 엔진을 설치하고 구성하는 것이 모범 사례입니다. 

Java 언어 확장을 설치하려면 이 문서의 단계를 따르세요.

Java 확장의 패키지 위치는 SQL Server Linux 원본 리포지토리에 있습니다. 데이터베이스 엔진 설치에 대한 원본 리포지토리를 이미 구성한 경우 동일한 리포지토리 등록을 사용하여 **mssql-server-extensibility-java** 패키지 설치 명령을 실행할 수 있습니다.

언어 확장은 Linux 컨테이너에서도 지원됩니다. 언어 확장을 사용하는 미리 빌드된 컨테이너는 제공하지 않지만 [GitHub에서 이용 가능한 예제 템플릿](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)을 사용하여 SQL Server 컨테이너에서 만들 수 있습니다.

## <a name="uninstall-previous-ctp-version"></a>이전 CTP 버전 제거

패키지 목록이 마지막 몇 개의 CTP 릴리스에 걸쳐 변경되어 패키지 개수가 줄어들게 됩니다. RC 1을 설치하기 전에 CTP 버전을 제거하여 이전 패키지를 모두 제거하는 것이 좋습니다. 여러 버전의 병렬 설치는 지원되지 않습니다.

### <a name="1-confirm-package-installation"></a>1. 패키지 설치 확인

첫 번째 단계로 이전 설치의 존재 여부를 확인하는 것이 좋습니다. 다음 파일은 기존 설치를 표시합니다. checkinstallextensibility.sh, exthost, launchpad.

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctp-packages"></a>2. 이전 CTP 패키지 제거

가장 낮은 패키지 수준에서 제거합니다. 하위 수준 패키지에 종속된 모든 업스트림 패키지는 자동으로 제거됩니다.

  + Java 통합의 경우 **mssql-server-extensibility-Java**를 제거합니다.

패키지를 제거하는 명령은 다음 표에 나와 있습니다.

| 플랫폼  | 패키지 제거 명령 | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove msssql-server-extensibility-java` |
| SLES  | `sudo zypper remove msssql-server-extensibility-java` |
| Ubuntu    | `sudo apt-get remove msssql-server-extensibility-java`|

### <a name="3-install-release-candidate-1-rc-1"></a>3. RC 1(릴리스 후보 1) 설치

운영 체제에 맞는 문서의 지침을 사용하여 가장 높은 패키지 수준에서 설치합니다.

각 OS별 설치 지침의 경우, *가장 높은 패키지 수준*은 **예 1 - 전체 설치**(전체 패키지 세트용) 또는 **예 2 - 최소 설치**(실행 가능한 설치에 필요한 최소 개수의 패키지용) 중 하나입니다.

1. Linux 배포에 대한 패키지 관리자 및 구문을 사용하여 설치 명령을 실행합니다. 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>사전 요구 사항

+ Linux 버전은 [SQL Server에서 지원](sql-server-linux-release-notes-2019.md#supported-platforms)되어야 하지만 Docker 엔진은 포함하지 않습니다. 지원되는 버전은 다음과 같습니다.

   + [Red Hat Enterprise Linux(RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux 서버](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ T-SQL 명령을 실행하기 위한 도구가 있어야 합니다. 설치 후 구성 및 유효성 검사에는 쿼리 편집기가 필요합니다. Linux에서 실행되는 체험용 다운로드인 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux)를 권장합니다.

## <a name="package-list"></a>패키지 목록

인터넷에 연결된 디바이스에서 패키지는 각 운영 체제의 패키지 설치 프로그램을 사용하여 데이터베이스 엔진과 독립적으로 다운로드 및 설치됩니다. 다음 표에서는 이용 가능한 모든 패키지에 대해 설명합니다.

| 패키지 이름 | 적용 대상 | 설명 |
|--------------|----------|-------------|
|mssql-server-extensibility  | 모든 언어 | Java 언어 확장에 사용되는 확장성 프레임워크 |
|mssql-server-extensibility-java | Java | Java 언어 확장에 사용되고 지원되는 Java 런타임을 포함하는 확장성 프레임워크 |

<a name="RHEL"></a>

## <a name="install-language-extensions"></a>언어 확장 설치

**mssql-server-extensibility-java**를 설치하여 Linux에 언어 확장 및 Java를 설치할 수 있습니다. **mssql-server-extensibility-java**를 설치할 때 JRE 11이 아직 설치되지 않은 경우 패키지가 자동으로 설치합니다. 또한 JRE_HOME이라는 환경 변수에 JVM 경로를 추가합니다.

> [!Note]
> 인터넷에 연결된 서버에서 패키지 종속성이 다운로드되고 주 패키지 설치의 일부로 설치됩니다. 서버가 인터넷에 연결되어 있지 않은 경우 [오프라인 설정](#offline-install)에서 자세한 정보를 참조하세요.

### <a name="redhat-install-command"></a>RedHat 설치 명령

다음 명령을 사용하여 RedHat에 Java용 언어 확장을 설치할 수 있습니다.

> [!Tip]
> 가능하면 `yum clean all`을 실행하여 설치 전에 시스템에서 패키지를 새로 고칩니다.

```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

### <a name="ubuntu-install-command"></a>Ubuntu 설치 명령

아래 명령을 사용하여 Ubuntu에 Java용 언어 확장을 설치할 수 있습니다.

> [!Tip]
> 가능하면 `apt-get update`를 실행하여 설치 전에 시스템에서 패키지를 새로 고칩니다. 또한 Ubuntu의 일부 docker 이미지에는 https apt 전송 옵션이 없을 수도 있습니다. 설치하려면 `apt-get install apt-transport-https`를 사용합니다.

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

### <a name="suse-install-command"></a>SUSE 설치 명령

다음 명령을 사용하여 SUSE에 Java용 언어 확장을 설치할 수 있습니다.

```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>설치 후 구성(필수)

1. Linux에 사용 권한 부여

    외부 라이브러리를 사용하는 경우 이 단계를 수행할 필요가 없습니다. 권장되는 작업 방법은 외부 라이브러리를 사용하는 것입니다. Jar 파일에서 외부 라이브러리를 만드는 방법에 대한 도움말은 [외부 라이브러리 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)를 참조하세요.

    외부 라이브러리를 사용하지 않는 경우 jar에서 Java 클래스를 실행할 수 있는 권한을 SQL Server 제공해야 합니다.

    Jar 파일에 대한 읽기 및 실행 액세스 권한을 부여하려면 jar 파일에서 다음 **chmod** 명령을 실행합니다. SQL Server로 작업할 때는 항상 jar에 클래스 파일을 배치하는 것이 좋습니다. Jar 만들기에 대한 도움말은 [jar 파일 만드는 방법](https://docs.microsoft.com/sql/language-extensions/how-to/create-a-java-jar-file-from-class-files)을 참조하세요.

    ```cmd
    chmod ug+rx <MyJarFile.jar>
    ```

    또한 mssql_satellite에 jar 파일에 대한 읽기/실행 권한을 부여해야 합니다.

    ```cmd
    chown mssql_satellite:mssql_satellite <MyJarFile.jar>
    ```

    추가 구성은 주로 [mssql-conf tool](sql-server-linux-configure-mssql-conf.md)을 통해 진행됩니다.

2. SQL Server 서비스를 실행하는 데 사용되는 mssql 사용자 계정을 추가합니다. 이는 이전에 설치를 실행하지 않은 경우에 필요합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

3. 아웃바운드 네트워크 액세스를 사용하도록 설정합니다. 아웃바운드 네트워크 액세스는 기본적으로 사용 안 함으로 설정됩니다. 아웃바운드 요청을 사용하려면 mssql-conf 도구를 사용하여 "outboundnetworkaccess" 부울 속성을 설정합니다. 자세한 내용은 [mssql-conf를 사용하여 SQL Server on Linux 구성](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)을 참조하세요.

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. SQL Server 실행 패드 서비스 및 데이터베이스 엔진 인스턴스를 다시 시작하여 INI 파일에서 업데이트된 값을 읽습니다. 다시 시작 메시지가 확장성 관련 설정이 수정될 때마다 사용자에게 알려줍니다.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

5. Transact-SQL을 실행하는 Azure Data Studio 또는 SQL Server Management Studio(Windows에만 해당)와 같은 다른 도구를 사용하여 외부 스크립트 실행을 사용하도록 설정합니다.

   ```bash
   EXEC sp_configure 'external scripts enabled', 1
   RECONFIGURE WITH OVERRIDE
   ```

6. `mssql-launchpadd` 서비스를 다시 시작합니다.

7. 언어 확장을 사용하려는 각 데이터베이스에 대해 [외부 언어 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql)를 사용하여 외부 언어를 등록해야 합니다.

## <a name="register-external-language"></a>외부 언어 등록

언어 확장을 사용하려는 각 데이터베이스에 대해 [외부 언어 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql)를 사용하여 외부 언어를 등록해야 합니다.

다음 예제는 SQL Server on Linux의 데이터베이스에 외부 언어가 호출한 Java를 추가합니다.

```SQL
CREATE EXTERNAL LANGUAGE Java
FROM (CONTENT = N'<path-to-tar.gz>', FILE_NAME = 'javaextension.so');
GO
```

자세한 내용은 [외부 언어 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql)를 참조하세요.

## <a name="verify-installation"></a>설치 확인

Java 기능 통합에는 라이브러리가 포함되지 않지만 `grep -r JRE_HOME /etc`를 실행하여 JAVA_HOME 환경 변수의 생성을 확인할 수 있습니다.

설치의 유효성을 검사하려면 Java를 호출하는 시스템 저장 프로시저를 실행하는 T-SQL 스크립트를 실행합니다. 이 작업에 대한 쿼리 도구가 필요합니다. Azure Data Studio를 선택하는 것이 좋습니다. SQL Server Management Studio 또는 PowerShell과 같이 일반적으로 사용되는 다른 도구는 Windows 전용입니다. 이러한 도구가 포함된 Windows 컴퓨터를 사용하는 경우 이를 사용하여 데이터베이스 엔진의 Linux 설치에 연결합니다.

<a name="install-all"></a>

## <a name="full-install-of-sql-server-and-language-extensions"></a>SQL Server 및 언어 확장의 전체 설치

데이터베이스 엔진을 설치하는 명령에 Java 패키지와 매개 변수를 추가하여 한 가지 프로시저에서 데이터베이스 엔진 및 언어 확장을 설치하고 구성할 수 있습니다.

1. 데이터베이스 엔진 및 언어 확장 기능을 포함하는 명령줄을 제공합니다.

  데이터베이스 엔진 설치에 Java 확장성을 추가할 수 있습니다.

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java 
  ```

3. 사용권 계약에 동의하고 설치 후 구성을 완료합니다. 이 작업을 위해 **mssql-conf** 도구를 사용합니다.

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  데이터베이스 엔진에 대한 사용권 계약에 동의하고, 버전을 선택하고, 관리자 암호를 설정하라는 메시지가 표시됩니다. 

4. 서비스를 다시 시작하라는 메시지가 표시되면 서비스를 다시 시작합니다.

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>무인 설치

데이터베이스 엔진에 대한 [무인 설치](https://docs.microsoft.com/sql/linux/sql-server-linux-setup#unattended)를 사용하여 mssql-server-extensibility-java용 패키지를 추가합니다.

<a name="offline-install"></a>


## <a name="offline-installation"></a>오프라인 설치

패키지 설치 단계의 [오프라인 설치](sql-server-linux-setup.md#offline) 지침을 따릅니다. 다운로드 사이트를 찾은 후 아래 패키지 목록을 사용하여 특정 패키지를 다운로드합니다.

> [!Tip]
> 여러 패키지 관리 도구에서 패키지 종속성을 확인하는 데 도움이 되는 명령을 제공합니다. Yum의 경우 `sudo yum deplist [package]`를 사용합니다. Ubuntu의 경우 `dpkg -I [package name].deb`와 `sudo apt-get install --reinstall --download-only [package name]`을 차례로 사용합니다.

#### <a name="download-site"></a>다운로드 사이트

[https://packages.microsoft.com/](https://packages.microsoft.com/)에서 패키지를 다운로드할 수 있습니다. Java용 모든 패키지는 데이터베이스 엔진 패키지와 함께 배치됩니다. 

#### <a name="redhat7-paths"></a>RedHat/7 경로

|||
|--|----|
| mssql/extensibility-java 패키지 | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |

#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 경로

|||
|--|----|
| mssql/extensibility-java 패키지 | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |

#### <a name="suse12-paths"></a>SUSE/12 경로

|||
|--|----|
| mssql/extensibility-java 패키지 | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |

#### <a name="package-list"></a>패키지 목록

사용하려는 확장에 따라 특정 언어에 필요한 패키지를 다운로드합니다. 정확한 파일 이름에는 접미사에 플랫폼 정보가 포함되지만, 다음의 파일 이름은 어떤 파일을 가져올지 결정할 수 있을 만큼 충분히 가까워야 합니다.

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000
```

## <a name="limitations-in-the-rc-1-release"></a>RC 1 릴리스의 제한 사항

Linux의 언어 확장 및 Java 확장성은 아직 개발 중입니다. 미리 보기 버전에서 다음 기능은 아직 사용할 수 없습니다.

+ 현재로서는 Linux에서 암시적 인증을 사용할 수 없습니다. 즉, 진행 중인 Java에서 데이터 또는 기타 리소스에 액세스하기 위해 서버에 다시 연결할 수 없습니다.


### <a name="resource-governance"></a>리소스 거버넌스

외부 리소스 풀에 대한 [리소스 거버넌스](../t-sql/statements/create-external-resource-pool-transact-sql.md)에서 Linux와 Windows 사이에 패리티가 있지만, [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)에 대한 통계는 현재 Linux에서 다른 단위를 사용합니다 
 
| 열 이름   | 설명 | Linux의 값 | 
|---------------|--------------|---------------|
|peak_memory_kb | 리소스 풀에 사용되는 최대 메모리 양입니다. | Linux에서 이 통계의 출처는 CGroups 메모리 하위 시스템이며, 여기서 값은 memory.max_usage_in_bytes입니다. |
|write_io_count | Resource Governor 통계를 다시 설정한 후 발생한 총 쓰기 IO입니다. | Linux에서 이 통계의 출처는 CGroups blkio 하위 시스템이며, 쓰기 행의 값은 blkio.throttle.io_serviced입니다. | 
|read_io_count | Resource Governor 통계를 다시 설정한 후 발생한 총 읽기 IO입니다. | Linux에서 이 통계의 출처는 CGroups blkio 하위 시스템이며, 읽기 행의 값은 blkio.throttle.io_serviced입니다. | 
|total_cpu_kernel_ms | Resource Governor 통계를 다시 설정한 후 누적된 CPU 사용자 커널 시간(밀리초)입니다. | Linux에서 이 통계의 출처는 CGroups cpuacct 하위 시스템이며, 사용자 행의 값은 cpuacct.stat입니다. |  
|total_cpu_user_ms | Resource Governor 통계를 다시 설정한 후 누적된 CPU 사용자 시간(밀리초)입니다.| Linux에서 이 통계의 출처는 CGroups cpuacct 하위 시스템이며, 시스템 행 값은 cpuacct.stat입니다. | 
|active_processes_count | 요청 순간에 실행되는 외부 프로세스의 수입니다.| Linux에서 이 통계의 출처는 GGroups pids 하위 시스템이며, 여기서 값은 pids.current입니다. | 

## <a name="next-steps"></a>다음 단계

Java 개발자는 몇 가지 간단한 예제를 시작하고 Java가 SQL Server에서 작동하는 방식의 기초를 알아볼 수 있습니다. 다음 단계로 가려면 아래 링크를 참조하세요.

+ [자습서: Java를 사용하는 정규식](../language-extensions/tutorials/search-for-string-using-regular-expressions-in-java.md)