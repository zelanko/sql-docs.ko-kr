---
title: "Linux에서 SQL Server 명령줄 도구를 설치 합니다. | Microsoft Docs"
description: "이 항목에서는 Linux에서 SQL Server 도구를 설치 하는 방법에 설명 합니다."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: eff8e226-185f-46d4-a3e3-e18b7a439e63
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 130da2409070f0acfda0bf78fcf2c4326bbeec92
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="install-sqlcmd-and-bcp-the-sql-server-command-line-tools-on-linux"></a>Linux에서 sqlcmd 및 bcp SQL Server 명령줄 도구를 설치

명령줄 도구, Microsoft ODBC 드라이버 및 해당 종속성을 설치 하는 다음 단계를 수행 합니다. **mssql 도구** 패키지에 포함 되어 있습니다.

- **sqlcmd**: 명령줄 쿼리 유틸리티입니다.
- **bcp**: 대량으로 가져오기 내보내기 유틸리티입니다.

플랫폼 도구를 설치 합니다.

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)
- [macOS](#macos)
- [Docker](#docker)

이 항목에서는 명령줄 도구를 설치 하는 방법에 설명 합니다. 사용 하는 방법의 예제를 보려면 원하는 경우 **sqlcmd** 또는 **bcp**, 참조는 [링크](#next-steps) 이 항목의 끝에 있습니다.

## <a name="a-idrhelainstall-tools-on-rhel-7"></a><a id="RHEL"><a/>RHEL 7에서 도구를 설치 합니다.

다음 단계를 사용 하 여 설치 하는 **mssql 도구** Red Hat Enterprise Linux에 합니다. 

1. Superuser 모드를 입력 합니다.

   ```bash
   sudo su
   ```

1. Red Hat Microsoft 저장소 구성 파일을 다운로드 합니다.

   ```bash
   curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/msprod.repo
   ```

1. Superuser 모드를 종료 합니다.

   ```bash
   exit
   ```

1. 이전 버전의 경우 **mssql 도구** 설치 이전 unixODBC 패키지를 제거 합니다.

   ```bash
   sudo yum update
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. 설치 하려면 다음 명령을 실행 **mssql 도구** unixODBC 개발자 패키지와 함께 합니다.

   ```bash
   sudo yum update
   sudo yum install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > 최신 버전으로 업데이트 하려면 **mssql 도구** 다음 명령을 실행 합니다.
   >    ```bash
   >   sudo yum check-update
   >   sudo yum update mssql-tools
   >   ```

1. **선택적**: 추가 `/opt/mssql-tools/bin/` 하 여 **경로** bash 셸의 환경 변수입니다.

   있도록 **sqlcmd/bcp** 로그인 세션에 대 한 bash 셸의에서 액세스할 수 있는 수정 프로그램 **경로** 에 **~/.bash_profile** 다음 명령 사용 하 여 파일:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   있도록 **sqlcmd/bcp** 대화형/비-로그인 세션에 대 한 bash 셸의에서 액세스할 수 있는 수정 된 **경로** 에 **~/.bashrc** 다음 명령 사용 하 여 파일:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="ubuntu"></a>Ubuntu 16.04에 도구를 설치 합니다.

다음 단계를 사용 하 여 설치 하는 **mssql 도구** ubuntu 합니다. 

1. 공용 저장소 GPG 키를 가져옵니다.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Microsoft Ubuntu 리포지토리를 등록 합니다.

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. 원본 목록 업데이트 하 고 설치 명령을 unixODBC 개발자 패키지가 함께 실행 합니다.

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > 최신 버전으로 업데이트 하려면 **mssql 도구** 다음 명령을 실행 합니다.
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **선택적**: 추가 `/opt/mssql-tools/bin/` 하 여 **경로** bash 셸의 환경 변수입니다.

   있도록 **sqlcmd/bcp** 로그인 세션에 대 한 bash 셸의에서 액세스할 수 있는 수정 프로그램 **경로** 에 **~/.bash_profile** 다음 명령 사용 하 여 파일:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   있도록 **sqlcmd/bcp** 대화형/비-로그인 세션에 대 한 bash 셸의에서 액세스할 수 있는 수정 된 **경로** 에 **~/.bashrc** 다음 명령 사용 하 여 파일:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="SLES"></a>SLES 12에 도구를 설치 합니다.

설치 하려면 다음 단계를 사용 하 여는 **mssql 도구** SUSE Linux Enterprise Server에 있습니다. 

1. Zypper에 Microsoft SQL Server 저장소를 추가 합니다.

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. 설치 **mssql 도구** unixODBC 개발자 패키지와 함께 합니다.

   ```bash
   sudo zypper install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > 최신 버전으로 업데이트 하려면 **mssql 도구** 다음 명령을 실행 합니다.
   >    ```bash
   >   sudo zypper refresh
   >   sudo zypper update mssql-tools
   >   ```

1. **선택적**: 추가 `/opt/mssql-tools/bin/` 하 여 **경로** bash 셸의 환경 변수입니다.

   있도록 **sqlcmd/bcp** 로그인 세션에 대 한 bash 셸의에서 액세스할 수 있는 수정 프로그램 **경로** 에 **~/.bash_profile** 다음 명령 사용 하 여 파일:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   있도록 **sqlcmd/bcp** 대화형/비-로그인 세션에 대 한 bash 셸의에서 액세스할 수 있는 수정 된 **경로** 에 **~/.bashrc** 다음 명령 사용 하 여 파일:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="macos"></a>MacOS에서 도구를 설치 합니다.

미리 보기 **sqlcmd** 및 **bcp** macOS에 출시 되었습니다. 자세한 내용은 참조는 [알림](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/16/sql-server-command-line-tools-for-macos-released/)합니다.

Mac El Capitan 및 시에라 도구를 설치 하려면 다음 명령을 사용 합니다.

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
#brew untap microsoft/mssql-preview if you installed the preview version 
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install --no-sandbox mssql-tools
#for silent install: 
#ACCEPT_EULA=y brew install --no-sandbox mssql-tools
```

## <a id="docker"></a>Docker

SQL Server 2017 CTP 2.0 부터는 SQL Server 명령줄 도구는 Docker 이미지에 포함 됩니다. 대화형 명령 프롬프트를 사용 하 여 이미지에 연결 하는 경우 도구를 로컬로 실행할 수 있습니다.

## <a name="offline-installation"></a>오프라인 설치

[!INCLUDE[SQL Server Linux offline package installation](../includes/sql-server-linux-offline-package-install-intro.md)]

다음 표에서 최신 도구 패키지에 대 한 위치를 제공합니다.

| 도구 패키지 | 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 도구 패키지 | 14.0.5.0-1 | [mssql 도구 RPM 패키지](https://packages.microsoft.com/rhel/7.3/prod/mssql-tools-14.0.5.0-1.x86_64.rpm) | 
| SLES RPM 도구 패키지 | 14.0.5.0-1 | [mssql 도구 RPM 패키지](https://packages.microsoft.com/sles/12/prod/mssql-tools-14.0.5.0-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 도구 패키지 | 14.0.5.0-1 | [mssql 도구 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools/mssql-tools_14.0.5.0-1_amd64.deb) |
| Ubuntu 16.10 Debian 도구 패키지 | 14.0.5.0-1 | [mssql 도구 Debian 패키지](https://packages.microsoft.com/ubuntu/16.10/prod/pool/main/m/mssql-tools/mssql-tools_14.0.5.0-1_amd64.deb) |

이러한 패키지에 종속 될 **배치한**, 먼저 설치 해야 합니다. **배치한** 패키지 때에 중 하나에 종속 되어 **unixODBC 개발자** (RPM) 또는 **unixodbc dev** (Debian). 위치는 **배치한** 패키지는 다음 표에 나열 됩니다.

| 배치한 패키지 | 버전 | 다운로드 |
|-----|-----|-----|
| Red Hat RPM 배치한 패키지 | 13.1.6.0-1 | [배치한 RPM 패키지](https://packages.microsoft.com/rhel/7.3/prod/msodbcsql-13.1.6.0-1.x86_64.rpm) | 
| SLES RPM 배치한 패키지 | 13.1.6.0-1 | [배치한 RPM 패키지](https://packages.microsoft.com/sles/12/prod/msodbcsql-13.1.6.0-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 배치한 패키지 | 13.1.6.0-1 | [배치한 Debian 패키지](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/msodbcsql_13.1.6.0-1_amd64.deb) |
| Ubuntu 16.10 Debian 배치한 패키지 | 13.1.6.0-1 | [배치한 Debian 패키지](https://packages.microsoft.com/ubuntu/16.10/prod/pool/main/m/msodbcsql/msodbcsql_13.1.6.0-1_amd64.deb) |

이러한 패키지를 수동으로 설치 하려면 다음 단계를 사용 합니다.

1. **Linux 컴퓨터에 다운로드 한 패키지를 이동**합니다. Linux 컴퓨터에 패키지를 이동 하는 한 가지 방법은와 다른 컴퓨터를 사용 하 여 패키지를 다운로드 하도록 하는 경우는 **scp** 넣습니다.

1. **설치 된 패키지 및**: 설치는 **mssql 도구** 및 **msodbc** 패키지 합니다. 종속성 오류가 발생 하는 경우 다음 단계까지 무시 됩니다.

    | 플랫폼 | 패키지 설치 명령 |
    |-----|-----|
    | Red Hat | `sudo yum localinstall msodbcsql-13.1.6.0-1.x86_64.rpm`<br/>`sudo yum localinstall mssql-tools-14.0.5.0-1.x86_64.rpm` |
    | SLES | `sudo zypper install msodbcsql-13.1.6.0-1.x86_64.rpm`<br/>`sudo zypper install mssql-tools-14.0.5.0-1.x86_64.rpm` |
    | Ubuntu | `sudo dpkg -i msodbcsql_13.1.6.0-1_amd64.deb`<br/>`sudo dpkg -i mssql-tools_14.0.5.0-1_amd64.deb` |

1. **누락 된 종속성 해결**: 누락 된 종속성이 시점에서 할 수 있습니다. 그렇지 않은 경우이 단계를 건너뛸 수 있습니다. 경우에 따라 수동으로 찾을 하며 이러한 종속성을 설치 합니다.

    RPM 패키지에 대 한 다음 명령 사용 하 여 필요한 종속성을 검사할 수 있습니다.

    ```bash
    rpm -qpR msodbcsql-13.1.6.0-1.x86_64.rpm
    rpm -qpR mssql-tools-14.0.5.0-1.x86_64.rpm
    ```

    Debian 패키지에 대 한 해당 종속성을 포함 하는 승인 된 저장소에 액세스할 수 있는 경우 가장 쉬운 방법은 사용 하 여 **apt get** 명령:

    ```bash
    sudo apt-get -f install
    ```

    > [!NOTE]
    > 이 명령은 SQL Server 패키지도의 설치를 완료합니다.

    Debian 패키지에는 작동 하지 않으면, 다음 명령 사용 하 여 필요한 종속성을 검사할 수 있습니다.

    ```bash
    dpkg -I msodbcsql_13.1.6.0-1_amd64.deb | grep "Depends:"
    dpkg -I mssql-tools_14.0.5.0-1_amd64.deb | grep "Depends:"
    ```

## <a name="next-steps"></a>다음 단계

사용 하는 방법의 예제를 보려면 **sqlcmd** 하 SQL Server에 연결 된 데이터베이스를 만들려면 다음 빠른 중 하나를 참조 시작 자습서:

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md)
- [Ubuntu 설치](quickstart-install-connect-ubuntu.md)
- [Docker에서 실행](quickstart-install-connect-ubuntu.md)

사용 하는 방법의 예제를 보려면 **bcp** 대량 가져오기 및 내보내기 데이터, 참조 [Linux에서 SQL Server로 대량 복사 데이터](sql-server-linux-migrate-bcp.md)합니다.

