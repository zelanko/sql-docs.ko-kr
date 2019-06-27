---
title: Linux에서 SQL Server 언어 확장 (Java)를 설치 합니다. | Microsoft Docs
description: Red Hat, Ubuntu 및 SUSE에서 SQL Server 언어 확장 (Java)를 설치 하는 방법에 알아봅니다.
author: dphansen
ms.author: davidph
manager: cgronlun
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9231828263020c352700fda6a4a0a9953dd70760
ms.sourcegitcommit: 65ceea905030582f8d89e75e97758abf3b1f0bd6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2019
ms.locfileid: "67399932"
---
# <a name="install-sql-server-2019-language-extensions-java-on-linux"></a>Linux에서 SQL Server 2019 언어 확장 (Java)를 설치 합니다.

언어 확장은 데이터베이스 엔진에 추가 된 기능입니다. 수 있지만 [데이터베이스 엔진 및 언어 확장을 동시에 설치할](#install-all), 설치 및 구성 요소를 추가 하기 전에 모든 문제를 해결할 수 있도록 먼저 SQL Server 데이터베이스 엔진을 구성 하는 것이 좋습니다. 

Java 언어 확장을 설치 하려면이 문서의 단계를 수행 합니다.

Java 확장에 대 한 패키지 위치는 SQL Server Linux 소스 리포지토리에 있습니다. 데이터베이스 엔진 설치에 대 한 소스 리포지토리를 이미 구성한 경우 실행할 수 있습니다 합니다 **mssql server-확장성 java** 동일한 리포지토리 등록을 사용 하 여 설치 명령이 패키지 있습니다.

Linux 컨테이너에 대 한 언어 확장도 지원 됩니다. 언어 확장을 사용 하 여 미리 작성된 된 컨테이너를 제공 하지 않습니다 하지만 사용 하 여 SQL Server 컨테이너에서 만들 수 있습니다 [GitHub에서 제공 하는 예제 템플릿을](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)합니다.

## <a name="uninstall-previous-ctp"></a>이전 CTP를 제거 합니다.

패키지 목록에는 마지막 몇 가지 CTP 릴리스를 더 적은 패키지에서 결과 통해 변경 되었습니다. CTP를 제거 하는 것이 좋습니다 2.x CTP 3.1을 설치 하기 전에 모든 이전 패키지를 제거 합니다. 여러 버전의 side-by-side-설치는 지원 되지 않습니다.

### <a name="1-confirm-package-installation"></a>1. 패키지 설치를 확인 합니다.

첫 번째 단계로 이전 설치의 존재 여부를 확인 하려는 경우. 다음 파일을 기존 설치를 나타냅니다: checkinstallextensibility.sh exthost, 실행 패드입니다.

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctp-2x-packages"></a>2. 이전 CTP 2.x 패키지 제거

가장 낮은 패키지 수준에서 제거 합니다. 하위 수준 패키지에 종속 된 모든 업스트림 패키지를 자동으로 제거 됩니다.

  + Java 통합에 대 한 제거 **mssql-서버-확장성-java**

패키지 제거 명령이 표에 나타납니다.

| 플랫폼  | 패키지 제거 명령 | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove msssql-server-extensibility-java` |
| SLES  | `sudo zypper remove msssql-server-extensibility-java` |
| Ubuntu    | `sudo apt-get remove msssql-server-extensibility-java`|

### <a name="3-proceed-with-ctp-31-install"></a>3. CTP 3.1 설치를 사용 하 여 계속 합니다.

이 문서의 지침을 사용 하 여 운영 체제에 대 한 가장 높은 패키지 수준에서 설치 합니다.

설치 지침의 각 OS 특정 집합에 대 한 *최고 패키지 수준* 은 **예제 1-전체 설치** 패키지의 전체 집합 또는 **예 2-최소 설치**  가장에 대 한 실행 가능한 설치에 필요한 패키지 수입니다.

1. Linux 배포에 대 한 구문을 확인 하 고 패키지 관리자를 사용 하 여 설치 명령을 실행 합니다. 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>사전 요구 사항

+ Linux 버전 이어야 합니다 [SQL Server에서 지 원하는](sql-server-linux-release-notes-2019.md#supported-platforms), Docker 엔진을 포함 하지 않습니다. 지원 되는 버전은 다음과 같습니다.

   + [Red Hat Enterprise Linux(RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ T-SQL 명령을 실행 하기 위한 도구를 해야 합니다. 쿼리 편집기는 설치 후 구성 및 유효성 검사에 필요. 것이 좋습니다 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux), Linux에서 실행 되는 무료 다운로드 합니다.

## <a name="package-list"></a>패키지 목록

인터넷에 연결 된 장치에서 패키지는 다운로드 되 고 각 운영 체제에 대 한 패키지 설치 관리자를 사용 하 여 데이터베이스 엔진 독립적으로 설치 합니다. 다음 표에 사용 가능한 모든 패키지 있습니다.

| 패키지 이름 | 에 적용 됩니다. | Description |
|--------------|----------|-------------|
|mssql-server-extensibility  | 모든 언어 | Java 코드를 실행 하는 데 확장성 프레임 워크입니다. |
|mssql-server-extensibility-java | Java | Java 실행 환경에 로드 하기 위한 Java 확장입니다. 추가 라이브러리 없거나 Java에 대 한 패키지 있습니다. |

<a name="RHEL"></a>

## <a name="install-language-extensions"></a>언어 확장 설치

에 설치할 수 있습니다 언어 확장 및 Java Linux를 설치 하 여 **mssql server-확장성 java**합니다. 설치 하는 경우 **mssql server-확장성 java**를 이미 설치 되어 있지 않으면 패키지가 JRE 8을 자동으로 설치 합니다. 또한 JVM 경로 JRE_HOME 라는 환경 변수에 추가 됩니다.

> [!Note]
> 인터넷에 연결 된 서버에서 패키지 종속성 다운로드 되 고 주 패키지 설치의 일부로 설치 합니다. 서버가 인터넷에 연결 되어 있지 않으면에서 자세한 내용을 보려면 합니다 [오프 라인 설치](#offline-install)합니다.

### <a name="redhat-install-command"></a>RedHat 설치 명령

아래 명령을 사용 하 여 RedHat에서 Java에 대 한 언어 확장을 설치할 수 있습니다.

> [!Tip]
> 실행 가능한 경우 `yum clean all` 설치 하기 전에 시스템에서 패키지를 새로 고쳐야 합니다.

```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

### <a name="ubuntu-install-command"></a>Ubuntu 설치 명령

아래 명령을 사용 하 여 Ubuntu에서 Java에 대 한 언어 확장을 설치할 수 있습니다.

> [!Tip]
> 실행 가능한 경우 `apt-get update` 설치 하기 전에 시스템에서 패키지를 새로 고쳐야 합니다. 또한 Ubuntu의 docker 이미지 일부 https apt 전송 옵션이 없을 수 있습니다. 설치를 사용 하 여 `apt-get install apt-transport-https`입니다.

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

### <a name="suse-install-command"></a>SUSE 설치 명령

아래 명령을 사용 하 여 SUSE에서 Java에 대 한 언어 확장을 설치할 수 있습니다.

```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>설치 후 구성 (필수)

1. Linux에 대 한 권한 부여

    외부 라이브러리를 사용 하는 경우이 단계를 수행할 필요가 없습니다. 작업 하는 권장된 방법을 외부 라이브러리를 사용 합니다. Jar 파일에서 외부 라이브러리를 만드는 데 도움이 필요한 경우 참조 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)

    외부 라이브러리를 사용 하지 않는 경우에 jar에서 Java 클래스를 실행 하는 권한이 있는 SQL Server를 제공 해야 합니다.

    읽기 권한을 부여 하 고 jar 파일에 대 한 액세스를 실행 하려면 다음을 실행 **chmod** jar 파일에서 명령을 합니다. 항상 SQL Server를 사용 하 여 작업할 때 jar의 클래스 파일을 배치 하는 것이 좋습니다. Jar 만들기 도움말을 참조 하세요 [jar 파일을 만드는 방법](https://docs.microsoft.com/sql/language-extensions/how-to/create-a-java-jar-file-from-class-files)합니다.

    ```cmd
    chmod ug+rx <MyJarFile.jar>
    ```

    Jar 파일을 읽기/실행 mssql_satellite 권한을 부여 해야 합니다.

    ```cmd
    chown mssql_satellite:mssql_satellite <MyJarFile.jar>
    ```

    추가 구성은 주로 통해 합니다 [mssql-conf 도구](sql-server-linux-configure-mssql-conf.md)합니다.

2. SQL Server 서비스를 실행 하는 데 mssql 사용자 계정을 추가 합니다. 이전에 설치를 실행 하지 않은 경우 이것이 필요 합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

3. 아웃 바운드 네트워크 액세스가 사용 하도록 설정 합니다. 아웃 바운드 네트워크 액세스가 기본적으로 비활성화 됩니다. 아웃 바운드 요청을 사용 하도록 설정 하려면 "outboundnetworkaccess" mssql-conf 도구를 사용 하는 부울 속성을 설정 합니다. 자세한 내용은 [mssql conf를 사용 하 여 Linux에서 SQL Server 구성](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)합니다.

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. SQL Server 실행 패드 서비스와 INI 파일에서 업데이트 된 값을 읽는 데이터베이스 엔진 인스턴스를 다시 시작 합니다. 다시 시작 메시지를 알려는 확장성 관련 설정 수정 될 때마다 합니다.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

5. Azure Data Studio 또는 SQL Server Management Studio (Windows만 해당)와 같은 다른 도구를 사용 하 여 외부 스크립트 실행 활성화 Transact SQL을 실행 하는 합니다.

   ```bash
   EXEC sp_configure 'external scripts enabled', 1
   RECONFIGURE WITH OVERRIDE
   ```

6. 다시 시작 된 `mssql-launchpadd` 다시 서비스 합니다.

7. 언어 확장을 사용 하려면 각 데이터베이스에 대해 외부 언어를 등록 해야 [외부 언어 만들](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql)합니다.

## <a name="register-external-language"></a>외부 언어를 등록 합니다.

언어 확장을 사용 하려면 각 데이터베이스에 대해 외부 언어를 등록 해야 [외부 언어 만들](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql)합니다.

다음 예제에서는 Linux의 SQL server 데이터베이스에 Java를 호출 하는 외부 언어를 추가 합니다.

```SQL
CREATE EXTERNAL LANGUAGE Java
FROM (CONTENT = N'<path-to-tar.gz>', FILE_NAME = 'javaextension.so');
GO
```

자세한 내용은 [외부 언어 만들](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql)합니다.

## <a name="verify-installation"></a>설치 확인

Java 기능 통합은 라이브러리를 포함 하지 않지만 실행할 수 있습니다 `grep -r JRE_HOME /etc` JAVA_HOME 환경 변수 만들기를 확인 합니다.

설치 유효성 검사, 시스템을 실행 하는 T-SQL 스크립트를 실행 하려면 Java를 호출 하는 프로시저를 저장 합니다. 이 태스크에 대 한 쿼리 도구를 해야 합니다. Azure Data Studio는 것이 좋습니다. 일반적으로 사용 되는 다른 도구는 SQL Server Management Studio 또는 PowerShell 같은 Windows 전용입니다. 이러한 도구를 사용 하 여 Windows 컴퓨터에 있는 경우 데이터베이스 엔진의 Linux 설치에 연결할 때를 사용 합니다.

<a name="install-all"></a>

## <a name="full-install-of-sql-server-and-language-extensions"></a>SQL Server 및 언어 확장의 전체 설치

설치 하 고 Java 패키지 및 데이터베이스 엔진을 설치 하는 명령에 매개 변수를 추가 하 여 프로시저 하나에서 데이터베이스 엔진 및 언어 확장을 구성할 수 있습니다.

1. 데이터베이스 엔진 및 언어 확장 기능을 포함 하는 명령줄을 제공 합니다.

  확장성, 데이터베이스 엔진을 설치 하는 Java를 추가할 수 있습니다.

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java 
  ```

3. 사용권 계약에 동의 하 고 설치 후 구성을 완료 합니다. 사용 된 **mssql conf** 이 태스크에 대 한 도구입니다.

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  데이터베이스 엔진에 대 한 사용권 계약에 동의 하 고, 버전을 선택 하 고, 관리자 암호를 설정 하 라는 메시지가 표시 됩니다. 

4. 이렇게 하려면 메시지가 표시 되 면 서비스를 다시 시작 합니다.

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>무인된 설치

사용 하는 [무인된 설치](https://docs.microsoft.com/sql/linux/sql-server-linux-setup#unattended) 데이터베이스 엔진의 경우 mssql server-확장성 java에 대 한 패키지를 추가 합니다.

<a name="offline-install"></a>


## <a name="offline-installation"></a>오프라인 설치

수행 합니다 [오프 라인 설치](sql-server-linux-setup.md#offline) 에 패키지를 설치 하는 단계를 설명 합니다. 다운로드 사이트를 찾아 다음 아래 패키지 목록을 사용 하 여 특정 패키지를 다운로드 합니다.

> [!Tip]
> 패키지 종속성을 확인 하는 명령을 도움이 될 수 있는 다양 한 패키지 관리 도구를 제공 합니다. Yum을 사용 하 여 `sudo yum deplist [package]`입니다. Ubuntu를 사용 하 여 `sudo apt-get install --reinstall --download-only [package name]` 뒤에 `dpkg -I [package name].deb`입니다.

#### <a name="download-site"></a>다운로드 사이트

패키지를 다운로드할 수 있습니다 [ https://packages.microsoft.com/ ](https://packages.microsoft.com/)합니다. Java에 대 한 패키지의 모든 데이터베이스 엔진 패키지를 사용 하 여 함께 배치 됩니다. 

#### <a name="redhat7-paths"></a>RedHat/7 경로

|||
|--|----|
| mssql/확장성-java 패키지 | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |

#### <a name="ubuntu1604-paths"></a>Ubuntu 16.04/경로

|||
|--|----|
| mssql/확장성-java 패키지 | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |

#### <a name="suse12-paths"></a>SUSE/12 경로

|||
|--|----|
| mssql/확장성-java 패키지 | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |

#### <a name="package-list"></a>패키지 목록

확장 프로그램에 따라 사용 하 여, 특정 언어에 필요한 패키지를 다운로드 해야 합니다. 접미사를에 플랫폼 정보를 포함 하는 정확한 파일 이름 있지만 아래 파일 이름을 가까이 있는 파일을 결정할 수 있습니다.

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000
```

## <a name="limitations-in-ctp-releases"></a>CTP 릴리스에서 제한 사항

Linux의 언어 확장 및 Java 확장성 여전히 활성 개발입니다. 다음 기능은 아직 미리 보기 버전에서 사용 되지 않습니다.

+ 묵시적된 인증이 없는 현재 Linux에서 사용할 수 이번에 진행 중인 데이터 또는 기타 리소스에 액세스 하는 Java에서 서버에 다시 연결할 수 없습니다.


### <a name="resource-governance"></a>리소스 거 버 넌 스

Linux 및 Windows에 대 한 사이 패리티가 [리소스 거 버 넌 스](../t-sql/statements/create-external-resource-pool-transact-sql.md) 외부 리소스 풀에 대 한 통계 [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) 현재 Linux에서 서로 다른 단위입니다. 단위는 예정 된 CTP에 정렬 됩니다.
 
| 열 이름   | Description | Linux의 값 | 
|---------------|--------------|---------------|
|peak_memory_kb | 최대 리소스 풀에 사용 되는 메모리 양입니다. | Linux에서이 통계 값은 memory.max_usage_in_bytes CGroups 메모리 하위 시스템을에서 소싱 된 |
|write_io_count | 총 쓰기 Io 리소스 관리자 통계를 다시 설정한 후 실행 합니다. | Linux에서이 통계 CGroups blkio 하위 시스템 쓰기 행의 값은 blkio.throttle.io_serviced에서에서 소싱 된 | 
|read_io_count | 총 읽기 Io 리소스 관리자 통계를 다시 설정한 후 실행 합니다. | Linux에서이 통계는 읽기 행에 값 blkio.throttle.io_serviced 인 CGroups blkio 하위 시스템을에서 소싱 된 | 
|total_cpu_kernel_ms | 누적 CPU 사용자 커널 시간 리소스 관리자 통계를 다시 설정한 후 시간 (밀리초)입니다. | Linux에서이 통계 CGroups cpuacct 하위 시스템 사용자 행 값은 cpuacct.stat에서에서 소싱 된 |  
|total_cpu_user_ms | 리소스 관리자 통계를 다시 설정한 후 시간 (밀리초)의 누적 CPU 사용자 시간이 있습니다.| Linux에서이 통계 CGroups cpuacct 하위 시스템 시스템 행 값의 값은 cpuacct.stat에서에서 소싱 된 | 
|active_processes_count | 요청 시 실행 되는 외부 프로세스의 수입니다.| Linux에서이 통계 값은 pids.current GGroups pid 하위 시스템을에서 소싱 된 | 

## <a name="next-steps"></a>다음 단계

Java 개발자가 몇 가지 간단한 예제를 사용 하 여 시작할 수 있습니다 및 SQL Server를 사용 하 여 Java 작동 하는 방법의 기본 사항을 알아봅니다. 다음 단계를 다음 링크를 참조 하세요.

+ [자습서: Java 사용 하 여 정규식](../language-extensions/tutorials/search-for-string-using-regular-expressions-in-java.md)