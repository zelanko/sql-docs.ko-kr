---
title: R 사용자 지정 런타임 설치
description: SQL Server용 R 사용자 지정 런타임을 설치하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/20/2020
ms.topic: how-to
author: cawrites
ms.author: chadam
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fb7f365fdbf4421093c11b5223bb3c1036a8d911
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956372"
---
# <a name="install-an-r-custom-runtime-for-sql-server"></a>SQL Server용 R 사용자 지정 런타임 설치

[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 SQL Server에서 R 스크립트를 실행하기 위한 사용자 지정 런타임을 설치하는 방법을 설명합니다. 사용자 지정 런타임은 확장성 프레임워크를 기반으로 하는 언어 확장 기술을 사용하여 외부 코드를 실행합니다. R에 대한 사용자 지정 런타임은 다음과 같은 시나리오에서 사용할 수 있습니다.

+ 확장성 프레임워크를 사용하는 SQL Server를 설치합니다.

+ SQL Server 2019를 사용하는 Machine Learning Services를 설치합니다. 언어 확장은 몇 가지 추가 구성 단계를 완료한 후 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)와 함께 사용할 수 있습니다.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> 이 문서에서는 Windows에 R용 사용자 지정 런타임을 설치하는 방법을 설명합니다. Linux에 설치하려면 [Linux에 SQL Server용 R 사용자 지정 런타임 설치](custom-runtime-r.md?view=sql-server-linux-ver15&preserve-view=true)를 참조하세요.

## <a name="pre-install-checklist"></a>설치 전 검사 목록

R 사용자 지정 런타임을 설치하기 전에 다음을 설치합니다.

+ [Windows용 SQL Server 2019(누적 업데이트 3 이상)](../../database-engine/install-windows/install-sql-server.md).

+ [확장성 프레임워크가 포함된 Windows의 SQL Server 언어 확장](../../language-extensions/install/install-sql-server-language-extensions-on-windows.md)

+ [R 버전 3.3 이상](https://cran.r-project.org/).

## <a name="add-sql-server-language-extensions-for-windows"></a>Windows용 SQL Server 언어 확장 추가

> [!NOTE]
> SQL Server 2019에 Machine Learning Services가 설치되어 있는 경우 실행 패드 서비스를 사용하는 언어 확장에 대한 확장성 프레임워크가 이미 설치되어 있으므로 이 단계를 건너뛰어도 됩니다.

언어 확장은 외부 코드를 실행하는 데 확장성 프레임워크를 사용합니다. 코드 실행이 코어 엔진 프로세스에서 격리되지만 SQL Server 쿼리 실행에 완전히 통합됩니다.

1. SQL Server 2019용 설치 마법사를 시작합니다.

1. **설치** 탭에서 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**를 선택합니다.

    ![SQL Server 2019 CU3 이상 설치](../install/media/2019setup-installation-page-mlsvcs.png)

1. **기능 선택** 페이지에서 다음 옵션을 선택합니다.

    - **데이터베이스 엔진 서비스**

        SQL Server에서 언어 확장을 사용하려면 데이터베이스 엔진의 인스턴스를 설치해야 합니다. 기본 인스턴스나 명명된 인스턴스를 사용할 수 있습니다.

    - **Machine Learning Services 및 언어 확장**

       **Machine Learning Services 및 언어 확장**을 선택합니다. R을 선택할 필요가 없습니다.

    ![SQL Server 2019 CU3 이상 설치 기능](../install/media/sql-feature-selection.png)

1. **설치 준비 완료** 페이지에서 이러한 선택 사항이 포함되어 있는지 확인하고 **설치**를 선택합니다.

    + 데이터베이스 엔진 서비스
    + Machine Learning Services 및 언어 확장

1. 설치가 완료된 후 컴퓨터를 다시 시작하라는 메시지가 나타나면 다시 시작합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 자세한 내용은 [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)을 참조하세요.

## <a name="install-r"></a>R 설치

> [!NOTE]
>SQL Machine Learning Services의 경우 SQL Server 인스턴스의 **R_SERVICES** 폴더에 R이 이미 설치되어 있습니다. 예: "C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES". 이 경로를 R_HOME으로 계속 사용하려면 Rcpp 설치의 다음 단계로 건너뜁니다. 그렇지 않고 R의 다른 런타임을 사용하려면 여기에서 설치를 계속 진행합니다.

[R(3.3 이상)](https://cran.r-project.org/bin/windows/base/)을 설치하고 설치된 경로를 기록해 둡니다. 이 경로가 **R_HOME**입니다. 예를 들어 여기서는 R_HOME이 "C:\Program Files\R\R-4.0.2"입니다.

![사용자 지정 R 설치](../install/media/custom-r-installation.png)

> [!NOTE]
>다음 지침에서 %R_HOME%은 R 설치 경로이며 해당 값으로 바꾸어야 합니다.

## <a name="install-rcpp-package"></a>Rcpp 패키지 설치

+ %R_HOME%\bin에서 R 실행 파일을 찾습니다. 기본값은 `C:\Program Files\R\R-4.0.2\bin`입니다.

+ *관리자 권한* 명령 프롬프트에서 R을 시작합니다.

```CMD
%R_HOME%\bin\R.exe
```

이 *관리자 권한* R 프롬프트(%R_HOME%\bin\R.exe)에서 다음 스크립트를 실행하여 %R_HOME%\library 폴더에 Rcpp 패키지를 설치합니다.

```R
install.packages("Rcpp", lib="%R_HOME%/library");
```

## <a name="update-the-system-environment-variables"></a>시스템 환경 변수 업데이트

1. **R_HOME**을 시스템 환경 변수로 추가하거나 수정합니다.
    + Windows 검색 상자에 "환경"을 입력하고 **시스템 환경 변수 편집**을 선택합니다.
    + **고급** 탭에서 **환경 변수**를 선택합니다.

    + **시스템 변수**에서 **새로 만들기**를 선택하여 R_HOME을 만듭니다.
    환경 변수를 수정하려면 **편집**을 선택하여 환경 변수를 변경합니다. 사용자 지정 R 설치 경로를 가리키도록 값을 수정합니다.

    ![R_HOME 시스템 환경 변수를 만듭니다.](../install/media/sys-env-r-home.png)

2. **PATH** 환경 변수를 업데이트합니다.
    **R.dll** 경로를 시스템 **PATH** 환경 변수에 추가합니다. **PATH**를 선택한 다음, **편집**을 선택하고 `%R_HOME%\bin\x64`을 경로 목록에 추가합니다.

    ![PATH 시스템 환경 변수에 추가합니다.](../install/media/sys-env-path-r.png)

3. **확인**을 선택하여 나머지 창을 닫습니다.

    또는 *관리자 권한* 명령 프롬프트에서 이러한 환경 변수를 설정하려면 다음 명령을 실행합니다. 사용자 지정 R 설치 경로를 사용해야 합니다.

```CMD
setx /m R_HOME "path\to\installation\of\R"
setx /m PATH "path\to\installation\of\R\bin\x64;%PATH%"
```

## <a name="grant-access-to-the-custom-r-installation-folder"></a>사용자 지정 R 설치 폴더에 대한 액세스 권한 부여

> [!NOTE]
>기본 위치 **C:\Program Files\R\R-version**에 R을 설치한 경우 이 단계를 건너뛰어도 됩니다.

새 *관리자 권한* 명령 프롬프트에서 **icacls** 명령을 실행하여 **SQL Server 실행 패드 서비스 사용자 이름** 및 SID **S-1-15-2-1**(**ALL APPLICATION PACKAGES**)에 대한 READ 및 EXECUTE 액세스 권한을 부여합니다. 실행 패드 서비스 사용자 이름은 `NT Service\MSSQLLAUNCHPAD$INSTANCENAME` 형식이며, 여기서 `INSTANCENAME`은 SQL Server의 인스턴스 이름입니다.

이 명령은 지정된 디렉터리 경로 아래의 모든 파일 및 폴더에 대한 액세스 권한을 재귀적으로 부여합니다.

`MSSQLLAUNCHPAD`(`MSSQLLAUNCHPAD$INSTANCENAME`)에 인스턴스 이름을 추가합니다. 이 예에서 `INSTANCENAME`은 기본 인스턴스 `MSSQLSERVER`입니다.

1. **SQL Server 실행 패드 서비스 사용자 이름**에 대한 권한 부여

    ```cmd
    icacls "%R_HOME%" /grant "NT Service\MSSQLLAUNCHPAD$MSSQLSERVER":(OI)(CI)RX /T
    ```
2. **SID S-1-15-2-1**에 대한 권한 부여

    ```cmd
    icacls "%R_HOME%" /grant *S-1-15-2-1:(OI)(CI)RX /T

>[!NOTE]
>The preceding command grants permissions to the computer **SID S-1-15-2-1**, which is equivalent to ALL APPLICATION PACKAGES on an English version of Windows. Alternatively, you can use `icacls "%R_HOME%" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T` on an English version of Windows.

## Restart SQL Server Launchpad service

From an *elevated* command prompt, run the following commands. Replace "MSSQLSERVER" with the name of your SQL Server instance.


```CMD
net stop MSSQLLAUNCHPAD$MSSQLSERVER
net start MSSQLLAUNCHPAD$MSSQLSERVER
```

또는 시스템의 **서비스** 앱에서 SQL Server 실행 패드 서비스를 마우스 오른쪽 단추로 클릭하고 **다시 시작** 명령을 선택합니다. 아니면 [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)를 사용하여 서비스를 다시 시작합니다.

## <a name="download-r-language-extension"></a>R 언어 확장 다운로드

[Windows용 R 언어 확장이 들어 있는 Zip 파일](https://github.com/microsoft/sql-server-language-extensions/releases)을 다운로드합니다. 프로덕션에서 릴리스 버전을 사용하는 것이 좋습니다. 오류를 조사하기 위해 자세한 로깅 정보를 제공하는 개발 중이거나 테스트 중인 디버그 버전을 사용합니다.

## <a name="register-external-language"></a>외부 언어 등록

이 R 언어 확장을 사용하려는 각 데이터베이스의 [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md)에 등록합니다. [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio)를 사용하여 SQL Server에 연결하고 다음 T-SQL 명령을 실행합니다.
다운로드한 언어 확장 Zip 파일(R-lang-extension.zip)의 위치를 반영하도록 이 명령문의 경로를 수정합니다.

> [!NOTE]
>**R**은 예약어입니다. 외부 언어에는 다른 이름을 사용하세요(예: "myR").

```sql
CREATE EXTERNAL LANGUAGE [myR]
FROM (CONTENT = N'/path/to/R-lang-extension.zip', FILE_NAME = 'libRExtension.dll');
GO
```

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

SQL Server는 RHEL(Red Hat Enterprise Linux), SLES(SUSE Linux Enterprise Server) 및 Ubuntu에 설치할 수 있습니다. 자세한 내용은 [Installation guidance for SQL Server on Linux(SQL Server on Linux 설치 지침)의 Supported platforms(지원되는 플랫폼) 섹션](../../linux/sql-server-linux-setup.md#supportedplatforms)을 참조하세요.

> [!NOTE]
> 이 문서에서는 Linux에 R용 사용자 지정 런타임을 설치하는 방법을 설명합니다. Windows에 설치하려면 [Windows에 SQL Server용 R 사용자 지정 런타임 설치](custom-runtime-r.md?view=sql-server-ver15&preserve-view=true)를 참조하세요.

## <a name="pre-install-checklist"></a>설치 전 검사 목록

R 사용자 지정 런타임을 설치하기 전에 다음을 설치합니다.

+ [Linux용 SQL Server 2019(누적 업데이트 3 이상)](../../linux/sql-server-linux-setup.md).
Linux에 SQL Server를 설치하기 전에 Microsoft 리포지토리를 구성해야 합니다. 자세한 내용은 [리포지토리 구성](../../linux/sql-server-linux-change-repo.md)을 참조하세요.

+ [확장성 프레임워크를 사용하는 Linux의 SQL Server](../../linux/sql-server-linux-setup-language-extensions.md)

+ [R 버전 3.3 이상](https://cran.r-project.org/).

## <a name="add-sql-server-language-extensions-for-linux"></a>Linux용 SQL Server 언어 확장 추가

> [!NOTE]
> 2019 SQL Server에 Machine Learning Services가 설치된 경우 언어 확장용 **mssql-server-extensibility** 패키지가 이미 설치되어 있으므로 이 단계를 건너뛰어도 됩니다.

언어 확장은 외부 코드를 실행하는 데 확장성 프레임워크를 사용합니다. 코드 실행이 코어 엔진 프로세스에서 격리되지만 SQL Server 쿼리 실행에 완전히 통합됩니다.

다음 명령을 사용하여 Linux 버전에 맞는 언어 확장을 설치합니다.

### <a name="ubuntu"></a>Ubuntu
> [!Tip]
> 가능하다면 `sudo apt-get update`를 실행하여 설치 전에 시스템의 패키지를 새로 고칩니다. Ubuntu에는 https apt transport 옵션이 없을 수 있습니다. 설치하려면 `sudo apt-get install apt-transport-https`를 사용합니다.

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility
```

### <a name="red-hat"></a>Red Hat
```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility
```

### <a name="suse"></a>Suse
```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility
```

## <a name="install-r"></a>R 설치

>[!NOTE]
>SQL Machine Learning Services의 경우 이미 `/opt/microsoft/ropen/3.5.2/lib64/R`에 R이 설치되어 있습니다. 이 경로를 R_HOME으로 계속 사용하려면 **Rcpp 설치**의 다음 단계로 건너뜁니다. 

R의 다른 런타임을 사용하려면 먼저 새 버전을 설치하기 전에 `microsoft-r-open-mro`를 제거해야 합니다. Ubuntu 예제:

```bash
sudo apt remove microsoft-r-open-mro-3.5.2
```

[지침](https://cran.r-project.org/bin/linux/)에 따라 해당하는 linux 플랫폼용 R(3.3 이상) 설치를 완료합니다. 기본적으로 R은 **/usr/lib/R**에 설치됩니다. 이 경로가 **R_HOME**입니다. 다른 위치에 R을 설치하는 경우 해당 경로를 R_HOME으로 기록해 둡니다.

Ubuntu에 대한 지침 예제입니다. 아래의 리포지토리 URL을 사용하는 R 버전에 맞게 변경합니다.

```bash
export DEBIAN_FRONTEND=noninteractive
sudo apt-get update
sudo apt-get --no-install-recommends -y install curl zip unzip apt-transport-https libstdc++6

# Add R CRAN repository. This repository works for R 4.0.x.
#
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
sudo add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu xenial-cran40/'
sudo apt-get update

# Install R runtime.
#
sudo apt-get -y install r-base-core
```

## <a name="install-rcpp-package"></a>Rcpp 패키지 설치

다음 지침에서 ${R_HOME}은 R 설치 경로입니다. 

+ ${R_HOME}/bin에서 R 이진을 찾습니다. 기본적으로 **/usr/lib/R/bin**에 있습니다.

+ R 시작

  ```bash
  sudo ${R_HOME}/bin/R
  ```

+ 이 *관리자 권한* R 프롬프트(${R_HOME}/bin/R)에서 다음 스크립트를 실행하여 ${R_HOME}/library 폴더에 **Rcpp** 패키지를 설치합니다.

  ```R
  install.packages("Rcpp", lib = "${R_HOME}/library");
  ```

## <a name="using-a-custom-installation-of-r"></a>R의 사용자 지정 설치 사용

> [!NOTE]
>기본 위치 **/usr/lib/R**에 R을 설치한 경우 이 섹션을 건너뛰어도 됩니다.

### <a name="update-the-environment-variables"></a>환경 변수 업데이트

1. mssql-launchpadd 서비스를 편집하여 R_HOME 환경 변수를 `/etc/systemd/system/mssql-launchpadd.service.d/override.conf` 파일에 추가합니다.

    ```bash
    sudo systemctl edit mssql-launchpadd
    ```

    + 열리는 `/etc/systemd/system/mssql-launchpadd.service.d/override.conf` 파일에 다음 텍스트를 삽입합니다. R_HOME 값을 사용자 지정 R 설치 경로로 설정합니다.

    ```text
    [Service]
    Environment="R_HOME=/path/to/installation/of/R"
    ```

    + 저장하고 닫습니다.

2. **libR.so**를 로드할 수 있는지 확인합니다.

    + **/etc/ld.so.conf.d**에 custom-r.conf 파일을 만듭니다.

    ```bash
    sudo vi /etc/ld.so.conf.d/custom-r.conf
    ```

    + 열리는 파일에서 사용자 지정 R 설치의 **libR.so** 경로를 추가합니다.

    ```vi editor
    /path/to/installation/of/R/lib
    ```

    + 새 파일을 저장하고 닫습니다.

    + 다음 명령을 실행하고 모든 종속 라이브러리를 찾을 수 있는지 확인하여 `ldconfig`를 실행하고 **libR.so**를 로드할 수 있는지 확인합니다.

    ```bash
    sudo ldconfig
    ldd /path/to/installation/of/R/lib/libR.so
    ```

### <a name="grant-access-to-the-custom-r-installation-folder"></a>사용자 지정 R 설치 폴더에 대한 액세스 권한 부여

/var/opt/mssql/mssql.conf 파일의 확장성 섹션에서 `datadirectories` 옵션을 사용자 지정 R 설치로 설정합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set extensibility.datadirectories /path/to/installation/of/R
```

### <a name="restart-mssql-launchpadd-service"></a>mssql-launchpadd 서비스 다시 시작

> [!NOTE]
>기본 위치 **/usr/lib/R**에 R을 설치한 경우 이 단계를 건너뛰어도 됩니다.

```bash
sudo systemctl restart mssql-launchpadd
```

## <a name="download-r-language-extension"></a>R 언어 확장 다운로드

[Linux용 R 언어 확장이 들어 있는 Zip 파일](https://github.com/microsoft/sql-server-language-extensions/releases)을 다운로드합니다. 프로덕션에서 릴리스 버전을 사용하는 것이 좋습니다. 오류를 조사하기 위해 자세한 로깅 정보를 제공하는 개발 중이거나 테스트 중인 디버그 버전을 사용합니다.

## <a name="register-external-language"></a>외부 언어 등록

이 R 언어 확장을 사용하려는 각 데이터베이스의 [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md)에 등록합니다. [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio)를 사용하여 SQL Server에 연결하고 다음 T-SQL 명령을 실행합니다. 
다운로드한 언어 확장 Zip 파일(r-lang-extension.zip)의 위치를 반영하도록 이 명령문의 경로를 수정합니다.


> [!NOTE]
>**R**은 예약어입니다. 외부 언어에는 다른 이름을 사용하세요(예: "myR").

```sql
CREATE EXTERNAL LANGUAGE [myR]
FROM (CONTENT = N'/path/to/R-lang-extension.zip', FILE_NAME = 'libRExtension.so.1.0');
GO
```

::: moniker-end

## <a name="enable-external-script-execution-in-sql-server"></a>SQL Server에서 외부 스크립트를 실행할 수 있도록 설정

SQL Server에 대해 실행되는 저장 프로시저 [sp_execute_external script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 통해 R의 외부 스크립트를 실행할 수 있습니다. 

외부 스크립트를 사용하도록 설정하려면 SQL Server에 연결된 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio)를 사용하여 다음 SQL 명령을 실행합니다.

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;
```

## <a name="verify-language-extension-installation"></a>언어 확장 설치 확인

이 SQL 스크립트는 사용자 지정 R 언어 확장이 성공적으로 설치되었는지 확인합니다. 이 스크립트의 출력에는 R_HOME, R의 경로 및 사용자 지정 R 런타임 버전이 표시됩니다. 그리고 스크립트가 사용자 지정 런타임을 사용하고 있는지 확인합니다.

```sql
EXEC sp_execute_external_script
    @language =N'myR',
    @script=N'
print(R.home());
print(file.path(R.home("bin"), "R"));
print(R.version);
print("Hello RExtension!");'
```

## <a name="verify-parameters-and-datasets-of-different-data-types"></a>다른 데이터 형식의 매개 변수 및 데이터 세트 확인

이 스크립트는 입력/출력 매개 변수 및 데이터 세트에 대한 다양한 데이터 형식을 테스트합니다.

```sql
DECLARE @sumVal INT = 12;
DECLARE @charVal VARCHAR(30) = N'Hello';
EXEC sp_execute_external_script
    @language =N'myR',
    @script=N'
print(sumVal);
print(charVal);
sumVal <- sumVal + 300;
OutputDataSet <- InputDataSet;'
    ,@input_data_1 = N'select 1, cast(1.4 as real), ''Hi'', cast(''1'' as bit)'
    ,@params = N'@sumVal int OUTPUT, @charVal VARCHAR(30)'
    ,@sumVal = @sumVal OUTPUT
    ,@charVal =  @charVal
WITH RESULT SETS ((intCol INT, doubleCol REAL, charCol CHAR(2), logicalCol BIT));
PRINT @sumVal;
```

## <a name="see-also"></a>참고 항목

+ [SQL Server의 확장성 프레임워크](../concepts/extensibility-framework.md)
+ [언어 확장 개요](../../language-extensions/language-extensions-overview.md)