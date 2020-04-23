---
title: Microsoft ODBC Driver for SQL Server 설치(Linux)
description: Linux 클라이언트에 Microsoft ODBC Driver for SQL Server를 설치하여 데이터베이스 연결을 사용하도록 설정하는 방법을 알아봅니다.
ms.date: 03/05/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver, installing
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a26c8282ec5afe00c3f23987fb82e3759c77c76e
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487784"
---
# <a name="install-the-microsoft-odbc-driver-for-sql-server-linux"></a>Microsoft ODBC Driver for SQL Server 설치(Linux)

이 문서에서는 Linux에 Microsoft ODBC Driver for SQL Server를 설치하는 방법을 설명합니다. SQL Server용 선택적 명령줄 도구(`bcp` 및 `sqlcmd`)와 unixODBC 개발 헤더에 대한 지침도 포함되어 있습니다.

이 문서에서는 bash 셸에서 ODBC 드라이버를 설치하기 위한 명령을 제공합니다. 패키지를 직접 다운로드하려면 [ODBC Driver for SQL Server 다운로드](../download-odbc-driver-for-sql-server.md)를 참조하세요.

## <a name="microsoft-odbc-17"></a><a id="17"></a> Microsoft ODBC 17

다음 섹션에서는 다양한 Linux 배포용 bash 셸에서 Microsoft ODBC Driver 17을 설치하는 방법을 설명합니다.

- [Alpine Linux](#alpine17)
- [Debian](#debian17)
- [Red Hat Enterprise Linux 및 Oracle](#redhat17)
- [SUSE Linux Enterprise Server](#suse17)
- [Ubuntu](#ubuntu17)

> [!IMPORTANT]
> 일시적으로 사용할 수 있었던 v17 `msodbcsql` 패키지를 설치한 경우 `msodbcsql17` 패키지를 설치하기 전에 제거하는 것이 좋습니다. 그래야 충돌이 방지됩니다. `msodbcsql17` 패키지는 `msodbcsql` v13 패키지와 병렬로 설치할 수 있습니다.

### <a name="alpine-linux"></a><a id="alpine17"></a> Alpine Linux

```bash
#Download the desired package(s)
curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.1-1_amd64.apk
curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/mssql-tools_17.5.2.1-1_amd64.apk


#(Optional) Verify signature, if 'gpg' is missing install it using 'apk add gnupg':
curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.1-1_amd64.sig
curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/mssql-tools_17.5.2.1-1_amd64.sig

curl https://packages.microsoft.com/keys/microsoft.asc  | gpg --import -
gpg --verify msodbcsql17_17.5.2.1-1_amd64.sig msodbcsql17_17.5.2.1-1_amd64.apk
gpg --verify mssql-tools_17.5.2.1-1_amd64.sig mssql-tools_17.5.2.1-1_amd64.apk


#Install the package(s)
sudo apk add --allow-untrusted msodbcsql17_17.5.2.1-1_amd64.apk
sudo apk add --allow-untrusted mssql-tools_17.5.2.1-1_amd64.apk
```

> [!NOTE]
> Alpine을 지원하려면 드라이버 버전 17.5 이상이 필요합니다.

### <a name="debian"></a><a id="debian17"></a> Debian

```bash
sudo su
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Debian 8
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 9
curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 10
curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
# optional: kerberos library for debian-slim distributions
sudo apt-get install libgssapi-krb5-2
```

> [!NOTE]
> 환경 변수 'ACCEPT_EULA'를 debconf 변수 'msodbcsql/ACCEPT_EULA'로 대신 설정할 수 있습니다. `echo msodbcsql17 msodbcsql/ACCEPT_EULA boolean true | sudo debconf-set-selections`

### <a name="red-hat-enterprise-server-and-oracle-linux"></a><a id="redhat17"></a> Red Hat Enterprise Server 및 Oracle Linux

```bash
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#RedHat Enterprise Server 6
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 7
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 8 and Oracle Linux 8
curl https://packages.microsoft.com/config/rhel/8/prod.repo > /etc/yum.repos.d/mssql-release.repo

exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="suse-linux-enterprise-server"></a><a id="suse17"></a> SUSE Linux Enterprise Server

```bash
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#SUSE Linux Enterprise Server 11 SP4
#Ensure SUSE Linux Enterprise 11 Security Module has been installed 
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo

#SUSE Linux Enterprise Server 12
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo

#SUSE Linux Enterprise Server 15
zypper ar https://packages.microsoft.com/config/sles/15/prod.repo
#(Only for driver 17.3 and below)
SUSEConnect -p sle-module-legacy/15/x86_64

exit
sudo ACCEPT_EULA=Y zypper install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
```

### <a name="ubuntu"></a><a id="ubuntu17"></a> Ubuntu

```bash
sudo su
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Ubuntu 16.04
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 18.04
curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 19.10
curl https://packages.microsoft.com/config/ubuntu/19.10/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

> [!NOTE]
> - Ubuntu 18.04를 지원하려면 드라이버 버전 17.2 이상이 필요합니다.
> - Ubuntu 18.10을 지원하려면 드라이버 버전 17.3 이상이 필요합니다.

> [!NOTE]
> 환경 변수 'ACCEPT_EULA'를 debconf 변수 'msodbcsql/ACCEPT_EULA'로 대신 설정할 수 있습니다. `echo msodbcsql17 msodbcsql/ACCEPT_EULA boolean true | sudo debconf-set-selections`

## <a name="previous-versions"></a>이전 버전

다음 섹션에서는 Linux에 이전 버전의 Microsoft ODBC Driver를 설치하는 방법을 설명합니다. 해당하는 드라이버 버전은 다음과 같습니다.

- [Microsoft ODBC Driver 13.1 for SQL Server](#13.1)
- [Microsoft ODBC Driver 13 for SQL Server](#13)
- [Microsoft ODBC Driver 11 for SQL Server](#11)

## <a name="odbc-131"></a><a id="13.1"></a> ODBC 13.1

다음 섹션에서는 다양한 Linux 배포용 bash 셸에서 Microsoft ODBC Driver 13.1을 설치하는 방법을 설명합니다.

### <a name="debian-8"></a>Debian 8

```bash
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6

```bash
sudo su
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise Server 7

```bash
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="suse-linux-enterprise-server-11"></a>SUSE Linux Enterprise Server 11

```bash
sudo su
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo
exit
sudo ACCEPT_EULA=Y zypper install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
```

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```bash
sudo su
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo
exit
sudo ACCEPT_EULA=Y zypper install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
```

### <a name="ubuntu-1510"></a>Ubuntu 15.10

```bash
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="ubuntu-1604"></a>Ubuntu 16.04

```bash
sudo su
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="ubuntu-1610"></a>Ubuntu 16.10

```bash
sudo su
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

## <a name="odbc-13"></a><a id="13"></a> ODBC 13

다음 섹션에서는 다양한 Linux 배포용 bash 셸에서 Microsoft ODBC Driver 13을 설치하는 방법을 설명합니다.

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6

```bash
sudo su
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
sudo yum install unixODBC-utf16-devel #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise Server 7

```bash
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
sudo yum install unixODBC-utf16-devel #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="ubuntu-1510"></a>Ubuntu 15.10

```bash
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools=14.0.2.0-1
sudo apt-get install unixodbc-dev-utf16 #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="ubuntu-1604"></a>Ubuntu 16.04

```bash
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools=14.0.2.0-1
sudo apt-get install unixodbc-dev-utf16 #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```bash
sudo su 
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo 
zypper update 
sudo ACCEPT_EULA=Y zypper install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
zypper install unixODBC-utf16-devel
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="offline-installation"></a>오프라인 설치

[!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC 드라이버 13을 인터넷 연결이 없는 컴퓨터에 설치하는 것을 선호하거나/그렇게 설치해야 하는 경우 패키지 종속성을 수동으로 해결해야 합니다. [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC 드라이버 13에는 다음과 같은 직접 종속성이 있습니다.
- Ubuntu: libc6(>= 2.21), libstdc++6(>= 4.9), libkrb5-3, libcurl3, openssl, debconf(>= 0.5), unixodbc(>= 2.3.1-1)
- Red Hat: ```glibc, e2fsprogs, krb5-libs, openssl, unixODBC```
- SUSE: ```glibc, libuuid1, krb5, openssl, unixODBC```

위의 각 패키지는 차례로 자체의 종속성이 있으며, 시스템에 해당 종속성이 있을 수도 있고 없는 경우도 있습니다. 이 문제에 대한 일반적인 해결 방법은 다음 배포의 패키지 관리자 설명서를 참조하세요. [Redhat](https://wiki.centos.org/HowTos/CreateLocalRepos), [Ubuntu](https://unix.stackexchange.com/questions/87130/how-to-quickly-create-a-local-apt-repository-for-random-packages-using-a-debian), [SUSE](https://en.opensuse.org/Portal:Zypper)

또한 수동으로 모든 종속성 패키지를 다운로드하고 설치 컴퓨터에 함께 저장한 다음, 수동으로 각 패키지를 차례로 설치하여 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 패키지를 완성하는 것이 일반적인 방법입니다.

#### <a name="redhat-linux-enterprise-server-7"></a>Redhat Linux Enterprise Server 7

- [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/)에서 최신 `msodbcsql` `.rpm` 을 다운로드합니다.
- 종속성 및 드라이버를 설치합니다.
  
```bash
yum install glibc e2fsprogs krb5-libs openssl unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

#### <a name="ubuntu-1604"></a>Ubuntu 16.04

- [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/)에서 최신 `msodbcsql` `.deb` 을 다운로드합니다.
- 종속성 및 드라이버를 설치합니다.

```bash
sudo apt-get install libc6 libstdc++6 libkrb5-3 libcurl3 openssl debconf unixodbc unixodbc-dev #install dependencies
sudo dpkg -i msodbcsql_13.1.X.X-X_amd64.deb #install the Driver
```

#### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

- [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/)에서 최신 `msodbcsql` `.rpm` 을 다운로드합니다.
- 종속성 및 드라이버를 설치합니다.

```bash
zypper install glibc, libuuid1, krb5, openssl, unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

패키지 설치를 완료한 후 ldd를 실행하고 해당 출력에서 누락된 라이브러리를 검사하여 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13에서 모든 종속성을 찾을 수 있는지 확인할 수 있습니다.

```bash
ldd /opt/microsoft/msodbcsql/lib64/libmsodbcsql-*
```

## <a name="odbc-11"></a><a id="11"></a> ODBC 11

다음 섹션에서는 Linux에 Microsoft ODBC Driver 11을 설치하는 방법을 설명합니다. 드라이버를 사용하려면 먼저 unixODBC 드라이버 관리자를 설치합니다. 자세한 내용은 [드라이버 관리자 설치](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)를 참조하세요.

### <a name="installation-steps"></a>설치 단계  

> [!IMPORTANT]  
> 이러한 지침은 Red Hat Linux용 설치 파일인 `msodbcsql-11.0.2270.0.tar.gz`를 참조합니다. SUSE Linux용 미리 보기를 설치하는 경우 파일 이름은 `msodbcsql-11.0.2260.0.tar.gz`입니다.  
  
드라이버를 설치하려면

1. 루트 권한이 있는지 확인합니다.  

2. 다운로드할 때 `msodbcsql-11.0.2270.0.tar.gz` 파일을 저장한 디렉터리로 변경합니다. Linux 버전과 일치하는 \*.tar.gz 파일이 있는지 확인합니다. 파일을 추출하려면 `tar xvzf msodbcsql-11.0.2270.0.tar.gz` 명령을 실행합니다.  
  
3. `msodbcsql-11.0.2270.0` 디렉터리로 변경하면 **install.sh**라는 파일이 나타납니다.  
  
4. 사용 가능한 설치 옵션 목록을 보려면 다음 명령을 실행합니다. **./install.sh**  
  
5. **odbcinst.ini**의 백업을 만듭니다. 드라이버 설치에서 **odbcinst.ini**를 업데이트합니다. odbcinst.ini에는 unixODBC 드라이버 관리자에 등록된 드라이버 목록이 있습니다. 컴퓨터에서 odbcinst.ini의 위치를 검색하려면 ```odbc_config --odbcinstini``` 명령을 실행합니다.  
  
6. 드라이버를 설치하기 전에 `./install.sh verify` 명령을 실행합니다. `./install.sh verify` 출력은 컴퓨터가 Linux 기반 ODBC 드라이버를 지원하는 데 필요한 소프트웨어가 있는지 보고합니다.  
  
7. Linux 기반 ODBC 드라이버를 설치할 준비가 되면 `./install.sh install` 명령을 실행합니다. 설치 명령(`bin-dir` 또는 `lib-dir`)을 지정해야 하는 경우 **install** 옵션 다음에 명령을 지정합니다.  
  
8. 사용권 계약을 검토한 후 **YES** 를 입력하여 설치를 계속합니다.  
  
설치 시 드라이버는 `/opt/microsoft/msodbcsql/11.0.2270.0`에 저장됩니다. 드라이버 및 해당 지원 파일은 `/opt/microsoft/msodbcsql/11.0.2270.0`에 있어야 합니다.  
  
Linux 기반 Microsoft ODBC 드라이버가 제대로 등록되었는지 확인하려면 ```odbcinst -q -d -n "ODBC Driver 11 for SQL Server"``` 명령을 실행합니다.  
  
### <a name="uninstall"></a>제거  
  
다음 명령을 실행하여 Linux 기반 ODBC 드라이버 11을 제거할 수 있습니다.  
  
1. `rm -f /usr/bin/sqlcmd`
  
2. `rm -f /usr/bin/bcp`  
  
3. `rm -rf /opt/microsoft/msodbcsql`  
  
4. `odbcinst -u -d -n "ODBC Driver 11 for SQL Server"`
  
## <a name="driver-files"></a>드라이버 파일

Linux 기반 ODBC 드라이버는 다음 구성 요소를 포함합니다.

|구성 요소|Description|  
|---------------|-----------------|  
|libmsodbcsql-17.X.so.X.X 또는 libmsodbcsql-13.X.so.X.X|드라이버 기능이 모두 포함된 공유 개체(`so`) 동적 라이브러리 파일입니다. 이 파일은 드라이버 17의 경우 `/opt/microsoft/msodbcsql17/lib64/` 및 드라이버 13의 경우 `/opt/microsoft/msodbcsql/lib64/`에 설치됩니다.|  
|`msodbcsqlr17.rll` 또는 `msodbcsqlr13.rll`|드라이버 라이브러리에 대한 해당 리소스 파일입니다. 이 파일은 `[driver .so directory]../share/resources/en_US/`에 설치됩니다.| 
|msodbcsql.h|드라이버를 사용하는 데 필요한 새 정의를 모두 포함하는 헤더 파일입니다.<br /><br /> **참고:**  동일한 프로그램에 msodbcsql.h 및 odbcss.h를 참조할 수 없습니다.<br /><br /> msodbcsql.h는 드라이버 17의 경우 `/opt/microsoft/msodbcsql17/include/` 및 드라이버 13의 경우 `/opt/microsoft/msodbcsql/include/`에 설치됩니다. |
|LICENSE.txt|최종 사용자 사용권 계약의 사용 약관을 포함하는 텍스트 파일입니다. 이 파일은 드라이버 17의 경우 `/usr/share/doc/msodbcsql17/` 및 드라이버 13의 경우 `/usr/share/doc/msodbcsql/`에 저장됩니다.|
|RELEASE_NOTES|릴리스 정보를 포함하는 텍스트 파일입니다. 이 파일은 드라이버 17의 경우 `/usr/share/doc/msodbcsql17/` 및 드라이버 13의 경우 `/usr/share/doc/msodbcsql/`에 저장됩니다.|

## <a name="resource-file-loading"></a>리소스 파일 로드

드라이버가 작동하려면 리소스 파일을 로드해야 합니다. 이 파일의 이름은 드라이버 버전에 따라 `msodbcsqlr17.rll` 또는 `msodbcsqlr13.rll`입니다. `.rll` 파일의 위치는 위의 표에서 설명했듯이 드라이버 자체(`so` 또는 `dylib`)의 위치에 대한 상대 위치입니다. 버전 17.1 현재 `.rll`을 상대 경로에서 로드하는 데 실패한 경우 기본 디렉터리에서도 로드를 시도합니다. Linux의 기본 리소스 파일 경로는 `/opt/microsoft/msodbcsql17/share/resources/en_US/`입니다.

## <a name="troubleshooting"></a>문제 해결

ODBC 드라이버를 사용하여 SQL Server에 연결할 수 없는 경우 [연결 문제 해결](known-issues-in-this-version-of-the-driver.md#connectivity)에서 알려진 문제 문서를 참조하세요.

## <a name="next-steps"></a>다음 단계

드라이버를 설치한 후 [C++ ODBC 예제 애플리케이션](../../odbc/cpp-code-example-app-connect-access-sql-db.md)을 사용해 볼 수 있습니다. ODBC 애플리케이션을 개발하는 방법에 대한 자세한 내용은 [애플리케이션 개발](../../../odbc/reference/develop-app/developing-applications.md)을 참조하세요.

자세한 내용은 ODBC 드라이버 [릴리스 정보](release-notes-odbc-sql-server-linux-mac.md) 및 [시스템 요구 사항](system-requirements.md)을 참조하세요.
