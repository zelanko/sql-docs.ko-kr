---
title: Linux에서 SQL Server 명령줄 도구 설치
titleSuffix: SQL Server
description: 이 문서에서는 Linux에 SQL Server 도구를 설치하는 방법을 설명합니다.
author: VanMSFT
ms.author: vanto
ms.date: 06/30/2020
ms.topic: conceptual
ms.prod: sql
ms.custom: sqlfreshmay19
ms.technology: linux
ms.assetid: eff8e226-185f-46d4-a3e3-e18b7a439e63
ms.openlocfilehash: e427e429ea4fe65f1f4f0af707c1a11c16c0834b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85897333"
---
# <a name="install-sqlcmd-and-bcp-the-sql-server-command-line-tools-on-linux"></a>Linux에서 SQL Server 명령줄 도구 sqlcmd 및 bcp 설치

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

다음 단계에서는 명령줄 도구, Microsoft ODBC 드라이버 및 해당 종속성을 설치합니다. **mssql-tools** 패키지에는 다음이 포함됩니다.

- **sqlcmd**: 명령줄 쿼리 유틸리티입니다.
- **bcp**: 대량 가져오기-내보내기 유틸리티입니다.

플랫폼용 도구를 설치합니다.

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)
- [macOS](#macos)
- [Docker](#docker)

이 문서에서는 명령줄 도구를 설치하는 방법을 설명합니다. **sqlcmd** 또는 **bcp**를 사용하는 방법에 대한 예제를 검색하는 경우 이 항목의 끝부분에 있는 [링크](#next-steps)를 참조하세요.

## <a name="a-idrhelinstall-tools-on-rhel-8"></a><a id="RHEL"><a/>RHEL 8에 도구 설치

다음 단계를 사용하여 Red Hat Enterprise Linux에서 **mssql-tools**를 설치합니다. 

1. 슈퍼 사용자 모드로 전환합니다.

   ```bash
   sudo su
   ```

1. Microsoft Red Hat 리포지토리 구성 파일을 다운로드합니다.

   ```bash
   curl https://packages.microsoft.com/config/rhel/8/prod.repo > /etc/yum.repos.d/msprod.repo
   ```

1. 슈퍼 사용자 모드를 종료합니다.

   ```bash
   exit
   ```

1. 이전 버전의 **mssql-tools**가 설치되어 있는 경우 이전 unixODBC 패키지를 제거합니다.

   ```bash
   sudo yum remove mssql-tools unixODBC-utf16-devel
   ```

1. 다음 명령을 실행하여 unixODBC 개발자 패키지와 함께 **mssql-tools**를 설치합니다.

   ```bash
   sudo yum install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > 최신 버전의 **mssql-tools**로 업데이트하려면 다음 명령을 실행합니다.
   >    ```bash
   >   sudo yum check-update
   >   sudo yum update mssql-tools
   >   ```

1. **선택 사항**: Bash 셸에서 **PATH** 환경 변수에 `/opt/mssql-tools/bin/`를 추가합니다.

   로그인 세션을 위해 bash 셸에서 **sqlcmd/bcp**에 액세스할 수 있도록 설정하려면 다음 명령을 사용하여 **~/.bash_profile** 파일에서 **PATH**를 수정합니다.

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   대화형/비로그인 세션을 위해 bash 셸에서 **sqlcmd/bcp**에 액세스할 수 있도록 설정하려면 다음 명령을 사용하여 **~/.bashrc** 파일에서 **PATH**를 수정합니다.

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a name="install-tools-on-ubuntu-1604"></a><a id="ubuntu"></a>Ubuntu 16.04에 도구 설치

다음 단계에 따라 Ubuntu에 **mssql-tools**를 설치합니다.

> [!NOTE]
> SQL Server 2019 CU3부터 Ubuntu 18.04가 지원됩니다. Ubuntu 18.04를 사용하는 경우 리포지토리 경로를 `/ubuntu/16.04`에서 `/ubuntu/18.04`로 변경합니다.

1. 공용 리포지토리 GPG 키를 가져옵니다.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Microsoft Ubuntu 리포지토리를 등록합니다.

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. 원본 목록을 업데이트하고 unixODBC 개발자 패키지를 사용하여 설치 명령을 실행합니다.

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > 최신 버전의 **mssql-tools**로 업데이트하려면 다음 명령을 실행합니다.
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **선택 사항**: Bash 셸에서 **PATH** 환경 변수에 `/opt/mssql-tools/bin/`를 추가합니다.

   로그인 세션을 위해 bash 셸에서 **sqlcmd/bcp**에 액세스할 수 있도록 설정하려면 다음 명령을 사용하여 **~/.bash_profile** 파일에서 **PATH**를 수정합니다.

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   대화형/비로그인 세션을 위해 bash 셸에서 **sqlcmd/bcp**에 액세스할 수 있도록 설정하려면 다음 명령을 사용하여 **~/.bashrc** 파일에서 **PATH**를 수정합니다.

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a name="install-tools-on-sles-12"></a><a id="SLES"></a>SLES 12에 도구 설치

다음 단계를 사용하여 SUSE Linux Enterprise Server에서 **mssql-tools**를 설치합니다. 

1. Zypper에 Microsoft SQL Server 리포지토리를 추가합니다.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. unixODBC 개발자 패키지와 함께 **mssql-tools**를 설치합니다.

   ```bash
   sudo zypper install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > 최신 버전의 **mssql-tools**로 업데이트하려면 다음 명령을 실행합니다.
   >    ```bash
   >   sudo zypper refresh
   >   sudo zypper update mssql-tools
   >   ```

1. **선택 사항**: Bash 셸에서 **PATH** 환경 변수에 `/opt/mssql-tools/bin/`를 추가합니다.

   로그인 세션을 위해 bash 셸에서 **sqlcmd/bcp**에 액세스할 수 있도록 설정하려면 다음 명령을 사용하여 **~/.bash_profile** 파일에서 **PATH**를 수정합니다.

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   대화형/비로그인 세션을 위해 bash 셸에서 **sqlcmd/bcp**에 액세스할 수 있도록 설정하려면 다음 명령을 사용하여 **~/.bashrc** 파일에서 **PATH**를 수정합니다.

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a name="install-tools-on-macos"></a><a id="macos"></a>macOS에 도구 설치

이제 macOS에서 **sqlcmd** 및 **bcp** 미리 보기를 사용할 수 있습니다. 자세한 내용은 [공지](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/16/sql-server-command-line-tools-for-macos-released/)를 참조하세요.

‘아직 설치하지 않은 경우 [Homebrew](https://brew.sh)를 설치합니다.’

- `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

Mac El Capitan 및 Sierra용 도구를 설치하려면 다음 명령을 사용합니다.

```bash
# brew untap microsoft/mssql-preview if you installed the preview version 
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install mssql-tools
#for silent install: 
#HOMEBREW_NO_ENV_FILTERING=1 ACCEPT_EULA=y brew install mssql-tools
```

## <a name="docker"></a><a id="docker"></a> Docker

[Docker 컨테이너에서 SQL Server를 실행](quickstart-install-connect-docker.md)하는 경우 SQL Server 명령줄 도구가 SQL Server Linux 컨테이너 이미지에 이미 포함되어 있어야 합니다. 대화형 bash 셸을 사용하여 실행 중인 컨테이너에 연결하는 경우 도구를 로컬로 실행할 수 있습니다.

## <a name="offline-installation"></a>오프라인 설치

[!INCLUDE[SQL Server Linux offline package installation](../includes/sql-server-linux-offline-package-install-intro.md)]

1. 먼저 Linux 배포용 **mssql-tools** 패키지를 찾아서 복사합니다.

   | Linux 배포 | **mssql-tools** 패키지 위치 |
   |---|---|
   | Red Hat | [https://packages.microsoft.com/rhel/7.3/prod](https://packages.microsoft.com/rhel/7.3/prod) |
   | SLES | [https://packages.microsoft.com/sles/12/prod](https://packages.microsoft.com/sles/12/prod)|
   | Ubuntu 16.04 | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools) |

1. 또한 종속성인 **msodbcsql** 패키지를 찾아서 복사합니다. **msodbcsql** 패키지에는 **unixODBC-devel**(Red Hat 및 SLES) 또는 **unixodbc-dev**(Ubuntu)에 대한 종속성도 포함됩니다. **msodbcsql** 패키지 위치는 다음 표에 나와 있습니다.

   | Linux 배포 | ODBC 패키지 위치 |
   |---|---|
   | Red Hat | [https://packages.microsoft.com/rhel/8/prod](https://packages.microsoft.com/rhel/8/prod) |
   | SLES | [https://packages.microsoft.com/sles/12/prod](https://packages.microsoft.com/sles/12/prod)|
   | Ubuntu 16.04 | [**msodbcsql**](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql)<br/>[**unixodbc-dev**](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/u/unixodbc/) |

1. **다운로드한 패키지를 Linux 머신으로 이동합니다**. 다른 머신을 사용하여 패키지를 다운로드한 경우 패키지를 Linux 머신으로 이동하는 한 가지 방법은 **scp** 명령을 사용하는 것입니다.

1. **패키지 설치**: **mssql-tools** 및 **msodbc** 패키지를 설치합니다. 종속성 오류가 발생하면 다음 단계까지 오류를 무시합니다.

    | 플랫폼 | 패키지 설치 명령 |
    |-----|-----|
    | Red Hat | `sudo yum localinstall msodbcsql-<version>.rpm`<br/>`sudo yum localinstall mssql-tools-<version>.rpm` |
    | SLES | `sudo zypper install msodbcsql-<version>.rpm`<br/>`sudo zypper install mssql-tools-<version>.rpm` |
    | Ubuntu | `sudo dpkg -i msodbcsql_<version>.deb`<br/>`sudo dpkg -i mssql-tools_<version>.deb` |

1. **누락된 종속성을 해결합니다**. 이때 누락된 종속성이 있을 수 있습니다. 누락된 종속성이 없으면 이 단계를 건너뛰어도 됩니다. 경우에 따라 이 종속성을 수동으로 찾고 설치해야 합니다.

    RPM 패키지의 경우 다음 명령을 사용하여 필요한 종속성을 검사할 수 있습니다.

    ```bash
    rpm -qpR msodbcsql-<version>.rpm
    rpm -qpR mssql-tools-<version>.rpm
    ```

    Debian 패키지의 경우 해당 종속성을 포함하는 승인된 리포지토리에 액세스할 수 있는 경우 **apt-get** 명령을 사용하는 것이 가장 쉬운 해결 방법입니다.

    ```bash
    sudo apt-get -f install
    ```

    > [!NOTE]
    > 이 명령은 SQL Server 패키지의 설치도 완료합니다.

    Debian 패키지에 대해 이 명령이 작동하지 않으면 다음 명령을 사용하여 필요한 종속성을 검사할 수 있습니다.

    ```bash
    dpkg -I msodbcsql_<version>_amd64.deb | grep "Depends:"
    dpkg -I mssql-tools_<version>_amd64.deb | grep "Depends:"
    ```

## <a name="next-steps"></a>다음 단계

**sqlcmd**를 사용하여 SQL Server에 연결하고 데이터베이스 만드는 방법에 대한 예제는 다음 빠른 시작 중 하나를 참조하세요.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu에 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)

**bcp**를 사용하여 데이터를 대량으로 가져오고 내보내는 방법에 대한 예제는 [SQL Server on Linux로 데이터 대량 복사](sql-server-linux-migrate-bcp.md)를 참조하세요.
