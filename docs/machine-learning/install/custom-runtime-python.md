---
title: Python 사용자 지정 런타임 설치
description: SQL Server용 Python 사용자 지정 런타임을 설치하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/20/2020
ms.topic: how-to
author: cawrites
ms.author: chadam
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4a625684b3196fc246b2753fc7b7e38b3e603f6e
ms.sourcegitcommit: 43b92518c5848489d03c68505bd9905f8686cbc0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155068"
---
# <a name="install-a-python-custom-runtime-for-sql-server"></a>SQL Server용 Python 사용자 지정 런타임 설치
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 SQL Server에서 Python 스크립트를 실행하기 위한 사용자 지정 런타임을 설치하는 방법을 설명합니다. 사용자 지정 런타임은 확장성 프레임워크를 기반으로 하는 언어 확장 기술을 사용하여 외부 코드를 실행합니다. Python에 대한 사용자 지정 런타임은 다음과 같은 시나리오에서 사용할 수 있습니다.

+ 확장성 프레임워크를 사용하는 SQL Server를 설치합니다.

+ SQL Server 2019를 사용하는 Machine Learning Services를 설치합니다. 언어 확장은 몇 가지 추가 구성 단계를 완료한 후 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)와 함께 사용할 수 있습니다.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> 이 문서에서는 Windows에 Python용 사용자 지정 런타임을 설치하는 방법을 설명합니다. Linux에 설치하려면 [Linux에 SQL Server용 Python 사용자 지정 런타임 설치](custom-runtime-python.md?view=sql-server-linux-ver15&preserve-view=true)를 참조하세요.



## <a name="pre-install-checklist"></a>설치 전 검사 목록

Python 사용자 지정 런타임을 설치하기 전에 다음을 설치합니다.

+ [Windows용 SQL Server 2019 CU3 이상](../../database-engine/install-windows/install-sql-server.md).

  > [!NOTE]
  > Python 사용자 지정 런타임은 SQL Server 2019용 CU(누적 업데이트) 3 이상이 필요합니다.

+ [확장성 프레임워크가 포함된 Windows의 SQL Server 언어 확장](../../language-extensions/install/windows-java.md)

+ [Python 3.7]( https://www.python.org/downloads/release/python-379/)

## <a name="add-sql-server-language-extensions-for-windows"></a>Windows용 SQL Server 언어 확장 추가

> [!NOTE]
> SQL Server 2019에 Machine Learning Services가 설치되어 있는 경우 확장성 프레임워크가 이미 설치되어 있으므로 이 단계를 건너뛰어도 됩니다.

언어 확장은 외부 코드를 실행하는 데 확장성 프레임워크를 사용합니다. 코드 실행이 코어 엔진 프로세스에서 격리되지만 SQL Server 쿼리 실행에 완전히 통합됩니다.

1. SQL Server 2019용 설치 마법사를 시작합니다.
  
1. **설치** 탭에서 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**를 선택합니다.
    
    ![SQL Server 2019 CU3 이상 설치](../install/media/2019setup-installation-page-mlsvcs.png) 

1. **기능 선택** 페이지에서 다음 옵션을 선택합니다.
  
    - **데이터베이스 엔진 서비스**
  
        SQL Server에서 언어 확장을 사용하려면 데이터베이스 엔진의 인스턴스를 설치해야 합니다. 기본 인스턴스나 명명된 인스턴스를 사용할 수 있습니다.
  
    - **Machine Learning Services 및 언어 확장**
   
       **Machine Learning Services 및 언어 확장**을 선택합니다. Python을 선택할 필요가 없습니다.

    ![SQL Server 2019 CU3 이상 설치 기능](../install/media/sql-feature-selection.png) 

1. **설치 준비 완료** 페이지에서 이러한 선택 사항이 포함되어 있는지 확인하고 **설치**를 선택합니다.
  
    + 데이터베이스 엔진 서비스
    + Machine Learning Services 및 언어 확장

1. 설치가 완료된 후 컴퓨터를 다시 시작하라는 메시지가 나타나면 다시 시작합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 자세한 내용은 [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)을 참조하세요.


## <a name="install-python-37"></a>Python 3.7 설치 

[Python 3.7]( https://www.python.org/downloads/release/python-379/)을 설치하고 PATH에 추가합니다.

![경로에 Python 3.7 추가](../install/media/python-379.png) 


#### <a name="install-pandas"></a>pandas 설치

*관리자 권한* 명령 프롬프트에서 Python용 [pandas](https://pandas.pydata.org/) 패키지를 설치합니다.

```bash
python.exe -m pip install pandas
```

## <a name="update-the-system-environment-variables"></a>시스템 환경 변수 업데이트

PYTHONHOME을 시스템 환경 변수로 추가하거나 수정합니다.

+ Windows 검색 상자에 "환경"을 입력하고 **시스템 환경 변수 편집**을 선택합니다.
+ **고급** 탭에서 **환경 변수**를 선택합니다.
+ **시스템 변수**에서 **새로 만들기**를 선택하고 Python 3.7 설치 위치를 가리키는 PYTHONHOME을 만듭니다.
PYTHONHOME이 이미 있는 경우 **편집**을 선택하여 Python 3.7 설치 위치를 가리키도록 편집합니다.
+ **확인**을 선택하여 나머지 창을 닫습니다.

![PYTHONHOME 시스템 변수를 만듭니다.](../install/media/sys-pythonhome.png)

## <a name="grant-access-to-the-custom-python-installation-folder"></a>사용자 지정 Python 설치 폴더에 대한 액세스 권한 부여

새 *관리자 권한* 명령 프롬프트에서 다음 **icacls** 명령을 실행하여 **SQL Server 실행 패드 서비스** 및 SID **S-1-15-2-1**(**ALL_APPLICATION_PACKAGES**)에 대한 READ 및 EXECUTE 액세스 권한을 PYTHONHOME에 부여합니다. 실행 패드 서비스 사용자 이름: `NT Service\MSSQLLAUNCHPAD$INSTANCENAME* where INSTANCENAME`은 SQL Server 인스턴스 이름입니다. 이 명령은 지정된 디렉터리 경로 아래의 모든 파일 및 폴더에 대한 액세스 권한을 재귀적으로 부여합니다.

`MSSQLLAUNCHPAD`(`MSSQLLAUNCHPAD$INSTANCENAME`)에 인스턴스 이름을 추가합니다. 이 예에서 INSTANCENAME은 기본 인스턴스 `MSSQLSERVER`입니다.

1. **SQL Server 실행 패드 서비스 사용자 이름**에 대한 권한을 부여합니다.

    ```cmd
    icacls "%PYTHONHOME%" /grant "NT Service\MSSQLLAUNCHPAD$MSSQLSERVER":(OI)(CI)RX /T

2. Give permissions to **SID S-1-15-2-1**.
    ```cmd
    icacls "%PYTHONHOME%" /grant *S-1-15-2-1:(OI)(CI)RX /T

>[!NOTE]
>The preceding command grants permissions to the computer **SID S-1-15-2-1**, which is equivalent to ALL APPLICATION PACKAGES on an English version of Windows. Alternatively, you can use `icacls "%R_HOME%" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T` on an English version of Windows.

## Restart SQL Server Launchpad service

From an *elevated* command prompt, run the following commands. Replace "MSSQLSERVER" with the name of your SQL Server instance.

```CMD
net stop MSSQLLAUNCHPAD$MSSQLSERVER
net start MSSQLLAUNCHPAD$MSSQLSERVER
```

또는 시스템의 **서비스** 앱에서 SQL Server 실행 패드 서비스를 마우스 오른쪽 단추로 클릭하고 **다시 시작** 명령을 클릭합니다. 아니면 [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)를 사용하여 서비스를 다시 시작합니다.

## <a name="download-python-language-extension"></a>Python 언어 확장 다운로드

[Windows용 Python 언어 확장 Zip 파일](https://github.com/microsoft/sql-server-language-extensions/releases)을 다운로드합니다. 프로덕션에서 릴리스 버전을 사용하는 것이 좋습니다. 오류를 조사하기 위해 자세한 로깅 정보를 제공하는 개발 중이거나 테스트 중인 디버그 버전을 사용합니다.

## <a name="register-external-language"></a>외부 언어 등록

이 Python 언어 확장을 사용하려는 각 데이터베이스의 [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md)에 등록합니다. [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md)를 사용하여 SQL Server에 연결하고 다음 T-SQL 명령을 실행합니다. 다운로드한 언어 확장 Zip 파일(python-lang-extension.zip)의 위치를 반영하도록 이 명령문의 경로를 수정합니다.

> [!NOTE]
> Python은 예약어입니다. 외부 언어에는 다른 이름을 사용하세요(예: "myPython").

```sql
CREATE EXTERNAL LANGUAGE [myPython]
FROM (CONTENT = N'/path/to/python-lang-extension.zip', FILE_NAME = 'pythonextension.dll');
GO
```

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

SQL Server는 RHEL(Red Hat Enterprise Linux), SLES(SUSE Linux Enterprise Server) 및 Ubuntu에 설치할 수 있습니다. 자세한 내용은 [Installation guidance for SQL Server on Linux(SQL Server on Linux 설치 지침)의 Supported platforms(지원되는 플랫폼) 섹션](../../linux/sql-server-linux-setup.md)을 참조하세요.

> [!NOTE]
> 이 문서에서는 Linux에 Python용 사용자 지정 런타임을 설치하는 방법을 설명합니다. Windows에 설치하려면 [Windows에 SQL Server용 Python 사용자 지정 런타임 설치](custom-runtime-python.md?view=sql-server-ver15&preserve-view=true)를 참조하세요.

## <a name="pre-install-checklist"></a>설치 전 검사 목록

Python 사용자 지정 런타임을 설치하기 전에 다음을 설치합니다.

+ [Linux용 SQL Server 2019(누적 업데이트 3 이상)](../../linux/sql-server-linux-setup.md).
SQL Server on Linux를 설치하는 경우 Microsoft 리포지토리를 구성해야 합니다. 자세한 내용은 [리포지토리 구성](../../linux/sql-server-linux-change-repo.md)을 참조하세요.

  > [!NOTE]
  > Python 사용자 지정 런타임은 SQL Server 2019용 CU(누적 업데이트) 3 이상이 필요합니다.

+ [확장성 프레임워크를 사용하는 Linux의 SQL Server](../../linux/sql-server-linux-setup-language-extensions-java.md)

+ [Python 3.7](https://www.python.org/downloads/release/python-379/)

## <a name="add-sql-server-language-extensions-for-linux"></a>Linux용 SQL Server 언어 확장 추가

> [!NOTE]
> 2019 SQL Server에 Machine Learning Services가 설치된 경우 언어 확장용 **mssql-server-extensibility** 패키지가 이미 설치되어 있으므로 이 단계를 건너뛰어도 됩니다.

언어 확장은 외부 코드를 실행하는 데 확장성 프레임워크를 사용합니다. 코드 실행이 코어 엔진 프로세스에서 격리되지만 SQL Server 쿼리 실행에 완전히 통합됩니다.

다음 명령을 사용하여 Linux 버전에 맞는 언어 확장을 설치합니다.

### <a name="ubuntu"></a>Ubuntu
> [!TIP]
> 가능하다면 `update`를 실행하여 설치 전에 시스템의 패키지를 새로 고칩니다. Ubuntu에는 https apt transport 옵션이 없을 수 있습니다. 설치하려면 `apt-get install apt-transport-https`를 사용합니다.

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

## <a name="install-python-37-and-pandas"></a>Python 3.7 및 pandas 설치

Python 3.7, libpython3.7 라이브러리 및 pandas 패키지를 설치합니다. 

다음은 Ubuntu에 대한 명령 예제입니다.

```bash
# Install python3.7 and the corresponding library:
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt-get update
sudo apt-get install python3.7 python3-pip libpython3.7

# Install pandas to /usr/lib:
sudo python3.7 -m pip install pandas -t /usr/lib/python3.7/dist-packages
```

## <a name="using-a-custom-installation-of-python-37"></a>Python 3.7의 사용자 지정 설치 사용

> [!NOTE]
> 기본 위치 `/usr/lib/python3.7`에 Python을 설치한 경우 [다음 섹션](#download-python-linux)을 건너뛰어도 됩니다.

사용자 고유의 Python 3.7 버전을 빌드한 경우 SQL Server가 사용자 지정 설치를 찾아서 로드할 수 있도록 다음 명령을 사용합니다.

### <a name="update-the-environment-variables"></a>환경 변수 업데이트

1. mssql-launchpadd 서비스를 편집하여 PYTHONHOME 환경 변수를 `/etc/systemd/system/mssql-launchpadd.service.d/override.conf` 파일에 추가합니다.

      ```bash
      sudo systemctl edit mssql-launchpadd
      ```

    + 열리는 `/etc/systemd/system/mssql-launchpadd.service.d/override.conf` 파일에 다음 텍스트를 삽입합니다. PYTHONHOME 값을 사용자 지정 Python 설치 경로로 설정합니다.

      ```vi
      [Service]
      Environment="PYTHONHOME=/path/to/installation/of/python3.7"
      ```

    + 저장하고 닫습니다.

2. `libpython3.7m.so.1.0`을 로드할 수 있는지 확인합니다.

    + `/etc/ld.so.conf.d`에 custom-python.conf 파일을 만듭니다.

      ```bash
      sudo vi /etc/ld.so.conf.d/custom-python.conf
      ```

    + 열리는 파일에서, 사용자 지정 Python 설치의 **libpython3.7m.so.1.0** 경로를 추가합니다.

      ```vi
      /path/to/installation/of/python3.7/lib
      ```

    + 새 파일을 저장하고 닫습니다.

    + 다음 명령을 실행하고 모든 종속 라이브러리를 찾을 수 있는지 확인하여 `ldconfig`를 실행하고 `libpython3.7m.so.1.0`을 로드할 수 있는지 확인합니다.

      ```bash
      sudo ldconfig
      ldd /path/to/installation/of/python3.7/lib/libpython3.7m.so.1.0
      ```

### <a name="grant-access-to-the-custom-python-folder"></a>사용자 지정 Python 폴더에 대한 액세스 권한 부여

/var/opt/mssql/mssql.conf 파일의 확장성 섹션에서 `datadirectories` 옵션을 사용자 지정 python 설치로 설정합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set extensibility.datadirectories /path/to/installation/of/python3.7
```

### <a name="restart-the-mssql-launchpadd-service"></a>mssql-launchpadd 서비스 다시 시작

```bash
sudo systemctl restart mssql-launchpadd
```
## <a name="download-python-language-extension"></a><a name="download-python-linux"></a> Python 언어 확장 다운로드

[Linux용 Python 언어 확장 Zip 파일](https://github.com/microsoft/sql-server-language-extensions/releases)을 다운로드합니다. 프로덕션에서 릴리스 버전을 사용하는 것이 좋습니다. 오류를 조사하기 위해 자세한 로깅 정보를 제공하는 개발 중이거나 테스트 중인 디버그 버전을 사용합니다.

## <a name="register-external-language"></a>외부 언어 등록

이 Python 언어 확장을 사용하려는 각 데이터베이스의 [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md)에 등록합니다. [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md)를 사용하여 SQL Server에 연결하고 다음 T-SQL 명령을 실행합니다. 
다운로드한 언어 확장 Zip 파일(python-lang-extension.zip)의 위치를 반영하도록 이 명령문의 경로를 수정합니다.

> [!NOTE]
>Python은 예약어입니다. 외부 언어에는 다른 이름을 사용하세요(예: "myPython").

```sql
CREATE EXTERNAL LANGUAGE myPython 
FROM (CONTENT = N'/PATH/TO/python-lang-extension.zip', FILE_NAME = 'libPythonExtension.so.1.0');
GO
```

::: moniker-end

## <a name="enable-external-script-execution-in-sql-server"></a>SQL Server에서 외부 스크립트를 실행할 수 있도록 설정

SQL Server에 대해 실행되는 저장 프로시저 [sp_execute_external script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 통해 Python의 외부 스크립트를 실행할 수 있습니다. 

외부 스크립트를 사용하도록 설정하려면 SQL Server에 연결된 [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md)를 사용하여 다음 SQL 명령을 실행합니다.

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

## <a name="verify-language-extension-installation"></a>언어 확장 설치 확인

이 SQL 스크립트는 설치된 언어 확장의 기능을 테스트합니다.

```sql
EXEC sp_execute_external_script
@language =N'myPython',
@script=N'
import sys
print(sys.path)
print(sys.version)
print(sys.executable)'
```

## <a name="verify-parameters-and-datasets-of-different-data-types"></a>다른 데이터 형식의 매개 변수 및 데이터 세트 확인

이 스크립트는 입력/출력 매개 변수 및 데이터 세트에 대한 다양한 데이터 형식을 테스트합니다.

```sql
DECLARE @sumVal int = 12;
DECLARE @charVal VARCHAR(30) = N'Hello'

EXEC sp_execute_external_script
@language =N'myPython',
@script=N'
print(sumVal)
print(charVal)
sumVal = sumVal + 300
OutputDataSet = InputDataSet'
,@input_data_1 = N'SELECT 1, CAST(1.4 as real), ''Hi'', CAST(''1'' as bit)'
,@params = N'@sumVal int OUTPUT, @charVal VARCHAR(30)'
,@sumVal = @sumVal OUTPUT
,@charVal = @charVal
WITH RESULT SETS ((intCol int, doubleCol real, charCol char(2), logicalCol bit));

PRINT @sumVal
```

## <a name="next-steps"></a>다음 단계

+ [SQL Server의 확장성 프레임워크](../concepts/extensibility-framework.md)
+ [언어 확장 개요](../../language-extensions/language-extensions-overview.md)