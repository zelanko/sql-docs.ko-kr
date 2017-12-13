---
title: "Microsoft ODBC Driver for Linux와 macOS에서 SQL Server 설치 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: driver, installing
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
caps.latest.revision: "69"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 50d515b5de665866d9e99a63d8b2136adcc82013
ms.sourcegitcommit: 4a462c7339dac7d3951a4e1f6f7fb02a3e01b331
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2017
---
# <a name="installing-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Microsoft ODBC Driver for Linux와 macOS에서 SQL Server 설치
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 항목에서는 설치 하는 방법에 설명는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] SQL Server에 대 한 선택적인 명령줄 도구 뿐만 아니라 Linux macOS 등 (`bcp` 및 `sqlcmd`) 및 unixODBC 개발 헤더입니다.

## <a name="microsoft-odbc-driver-131-for-sql-server"></a>Microsoft ODBC Driver 13.1 for SQL Server 

### <a name="debian-8"></a>Debian 8
```
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

### <a name="redhat-enterprise-server-6"></a>RedHat 엔터프라이즈 서버 6
```
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

### <a name="redhat-enterprise-server-7"></a>RedHat 엔터프라이즈 서버 7
```
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

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```
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
```
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
```
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
```
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

### <a name="os-x-1011-el-capitan-and-macos-1012-sierra"></a>OS X 10.11 (El Capitan)와 macOS 10.12 (시에라)

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install --no-sandbox msodbcsql mssql-tools
```

## <a name="microsoft-odbc-driver-13-for-sql-server"></a>Microsoft ODBC Driver 13 for SQL Server

### <a name="redhat-enterprise-server-6"></a>RedHat 엔터프라이즈 서버 6
```
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

### <a name="redhat-enterprise-server-7"></a>RedHat 엔터프라이즈 서버 7
```
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
```
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
```
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

```
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
원하는/필요로 하는 경우는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] 인터넷 연결 없이 컴퓨터에 설치 하려면 ODBC Driver 13을 해야 패키지 종속성을 수동으로 해결 합니다. [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 다음 직접 종속성이 있습니다.
- Ubuntu: libc6 (> = 2.21), libstdc + + 6 (> = 4.9), libkrb5-3, libcurl3, openssl, debconf (> = 0.5), unixodbc (> = 2.3.1-1)
- Red Hat: glibc, e2fsprogs, 하려면 krb5 라이브러리, openssl, unixODBC
- SuSE: glibc, libuuid1, 하려면 krb5, openssl, unixODBC

각이 패키지에서은 자신의 수도 시스템에 없을 수도 있습니다. 이 문제에 대 한 일반 솔루션을 배포의 패키지 관리자 설명서를 참조: [Redhat](https://wiki.centos.org/HowTos/CreateLocalRepos), [Ubuntu](http://unix.stackexchange.com/questions/87130/how-to-quickly-create-a-local-apt-repository-for-random-packages-using-a-debian), 및 [SUSE](https://en.opensuse.org/Portal:Zypper)

또한 것이 모든 종속 패키지를 수동으로 다운로드 하 고 설치 컴퓨터에 함께 배치 다음 차례로 각 패키지를 수동으로 설치를 마친는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 패키지 합니다.

#### <a name="redhat-linux-enterprise-server-7"></a>Redhat Linux Enterprise Server 7
  - 여기에서 최신 배치한.rpm 다운로드: http://packages.microsoft.com/rhel/7/prod/
  - 종속성 및 드라이버를 설치 합니다.
  
```
yum install glibc e2fsprogs krb5-libs openssl unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

#### <a name="ubuntu-1604"></a>Ubuntu 16.04
- 여기에서 최신 배치한. d 다운로드: http://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/ 
- 종속성 및 드라이버를 설치 합니다. 

```
sudo apt-get install libc6 libstdc++6 libkrb5-3 libcurl3 openssl debconf unixodbc unixodbc-dev #install dependencies
sudo dpkg -i msodbcsql_13.1.X.X-X_amd64.deb #install the Driver
```

#### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12
- 여기에서 최신 배치한.rpm 다운로드: http://packages.microsoft.com/sles/12/prod/
- 드라이버 및 종속성 설치

```
zypper install glibc, libuuid1, krb5, openssl, unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

패키지 설치를 완료 한 후 중인지를 확인할 수 있습니다는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 ldd를 실행 하 고 누락 된 라이브러리에 대 한 출력을 검사 하 여 모든 해당 종속성을 찾을 수 있습니다.
```
ldd /opt/microsoft/msodbcsql/lib64/libmsodbcsql-*
```
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-linux"></a>Microsoft ODBC Driver 11 for SQL Server에 Linux

드라이버를 사용 하려면 먼저 unixODBC 드라이버 관리자를 설치 합니다. 자세한 내용은 [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) 을 참조하세요.  

**설치 단계**  

> [!IMPORTANT]  
> 이러한 지침은를 참조 `msodbcsql-11.0.2270.0.tar.gz`, Red Hat Linux에 대 한 설치 파일인 합니다. SUSE Linux 용 Preview를 설치 하는 경우 파일 이름이 `msodbcsql-11.0.2260.0.tar.gz`합니다.  
  
드라이버를 설치하려면

1.  루트 권한이 있는지 확인합니다.  

2.  다운로드 파일을 배치한 디렉터리로 변경 `msodbcsql-11.0.2270.0.tar.gz`합니다. Linux 버전과 일치하는 \*.tar.gz 파일이 있는지 확인합니다. 파일을 추출하려면 다음 명령을 실행합니다. **tar xvzf msodbcsql-11.0.2270.0.tar.gz**  
  
3.  변경의 `msodbcsql-11.0.2270.0` 디렉터리 라는 파일을 있습니다 표시 되어야 **install.sh**합니다.  
  
4.  사용 가능한 설치 옵션 목록을 보려면 다음 명령을 실행합니다. **./install.sh**  
  
5.  **odbcinst.ini**의 백업을 만듭니다. 드라이버 설치에서 **odbcinst.ini**를 업데이트합니다. odbcinst.ini에는 unixODBC 드라이버 관리자에 등록된 드라이버 목록이 있습니다. 컴퓨터에서 odbcinst.ini의 위치를 검색하려면 다음 명령을 실행합니다. **odbc_config --odbcinstini**  
  
6.  드라이버를 설치하기 전에 다음 명령을 실행합니다. **./install.sh verify**. **./install.sh verify** 출력은 컴퓨터가 Linux 기반 ODBC 드라이버를 지원하는 데 필요한 소프트웨어가 있는지 보고합니다.  
  
7.  Linux 기반 ODBC 드라이버를 설치할 준비가 되면 다음 명령을 실행합니다. **./install.sh install**. 설치 명령(**bin-dir** 또는 **lib-dir**)을 지정해야 하는 경우 **install** 옵션 다음에 명령을 지정합니다.  
  
8.  사용권 계약을 검토한 후 **YES** 를 입력하여 설치를 계속합니다.  
  
설치에 드라이버가 배치 `/opt/microsoft/msodbcsql/11.0.2270.0`합니다. 드라이버와 해당 지원 파일에 있어야 `/opt/microsoft/msodbcsql/11.0.2270.0`합니다.  
  
Linux 기반 Microsoft ODBC 드라이버가 제대로 등록되었는지 확인하려면 다음 명령을 실행합니다. **odbcinst -q -d -n "ODBC Driver 11 for SQL Server"**.  
  
[Linux 기반 ODBC 드라이버에 대해 기존 MSDN C++ ODBC 샘플 사용](http://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) 에서는 Linux 기반 ODBC 드라이버를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 에 연결하는 코드 샘플을 보여 줍니다.  
  
**제거**  
  
다음 명령을 실행 하 여 Linux 기반 ODBC 드라이버 11을 제거할 수 있습니다.  
  
1.  `rm -f /usr/bin/sqlcmd`
  
2.  `rm -f /usr/bin/bcp`  
  
3.  `rm -rf /opt/microsoft/msodbcsql`  
  
4.  `odbcinst -u -d -n "ODBC Driver 11 for SQL Server"`
  
## <a name="troubleshooting-connection-problems"></a>연결 문제 해결  
에 대 한 연결을 만들 수 없는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] ODBC 드라이버를 사용 하 여 문제를 확인 하려면 다음 정보를 사용 합니다.  
  
가장 일반적인 연결 문제는 UnixODBC 드라이버 관리자의 복사본이 두 개 설치되는 것입니다. libodbc\*.so\*에 대해 /usr을 검색합니다. 둘 이상의 파일 버전이 표시되면 둘 이상의 드라이버 관리자가 설치된 것일 수 있습니다. 응용 프로그램이 잘못된 버전을 사용할 수 있습니다.
  
편집 하 여 연결 로그를 사용 하도록 설정 하면 `/etc/odbcinst.ini` 이러한 항목으로는 다음 섹션이 포함 파일:

```
[ODBC]
Trace = Yes
TraceFile = (path to log file, or /dev/stdout to output directly to the terminal)
```  
  
다른 연결 오류가 발생하고 로그 파일이 표시되지 않으면 컴퓨터에 드라이버 관리자의 복사본이 두 개 있을 수 있습니다. 그렇지 않으면 로그 출력은 다음과 같은 형태가 됩니다.  
  
```  
[ODBC][28783][1321576347.077780][SQLDriverConnectW.c][290]  
        Entry:  
            Connection = 0x17c858e0  
            Window Hdl = (nil)  
            Str In = [DRIVER={ODBC Driver 13 for SQL Server};SERVER={contoso.com};Trusted_Connection={YES};WSID={mydb.contoso.com};AP...][length = 139 (SQL_NTS)]  
            Str Out = (nil)  
            Str Out Max = 0  
            Str Out Ptr = (nil)  
            Completion = 0  
        UNICODE Using encoding ASCII 'UTF8' and UNICODE 'UTF16LE'  
```  
  
ASCII 문자 인코딩이 없는 경우 u t F-8, 예: 
  
```  
UNICODE Using encoding ASCII 'ISO8859-1' and UNICODE 'UCS-2LE'  
```  
  
둘 이상의 드라이버 관리자를 설치 하 고 응용 프로그램에 하나 또는 드라이버 관리자 올바르게 만들어지지 않은 잘못 된 사용 중인 있습니다.  
  
연결 오류를 해결하는 방법에 대한 자세한 내용은 다음을 참조하세요.  
  
-   [SQL 연결 문제를 해결하는 단계](http://blogs.msdn.com/b/sql_protocols/archive/2008/04/30/steps-to-troubleshoot-connectivity-issues.aspx)  
  
-   [SQL Server 2005 연결 문제 해결 - 1부](http://blogs.msdn.com/b/sql_protocols/archive/2005/10/22/sql-server-2005-connectivity-issue-troubleshoot-part-i.aspx)  
  
-   [연결 링 버퍼를 사용하여 SQL Server 2008의 연결 문제 해결](http://blogs.msdn.com/b/sql_protocols/archive/2008/05/20/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer.aspx)  
  
-   [SQL Server 인증 문제 해결사](http://blogs.msdn.com/b/sqlsecurity/archive/2010/03/29/sql-server-authentication-troubleshooter.aspx)  
  
-   [오류 세부 정보(http://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=11001)](http://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=001)  
  
    URL(11001)에서 지정된 오류 번호가 표시되는 오류와 일치하도록 변경되어야 합니다.  
  
## <a name="see-also"></a>관련 항목:

[드라이버 관리자 설치](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[릴리스 정보](../../../connect/odbc/linux-mac/release-notes.md)

[시스템 요구 사항](../../../connect/odbc/linux-mac/system-requirements.md)
