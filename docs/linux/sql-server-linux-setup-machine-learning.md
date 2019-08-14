---
title: Linux에 SQL Server Machine Learning Services(R, Python) 설치
description: Red Hat, Ubuntu 및 SUSE에 SQL Server Machine Learning Services(R, Python)를 설치하는 방법을 알아봅니다.
author: dphansen
ms.author: davidph
ms.reviewer: vanto
manager: cgronlun
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f578ae9dbc60b255959de406999feb8b68171389
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68476199"
---
# <a name="install-sql-server-2019-machine-learning-services-r-python-on-linux"></a>Linux에 SQL Server 2019 Machine Learning Services(R, Python) 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[SQL Server Machine Learning Services](../advanced-analytics/index.yml)는 SQL Server 2019의 이 미리 보기 릴리스부터 Linux 운영 체제에서 실행됩니다. 이 문서의 단계를 따라 R 및 Python용 기계 학습 확장을 설치합니다.

기계 학습 및 프로그래밍 확장은 데이터베이스 엔진의 추가 기능입니다. [데이터베이스 엔진과 Machine Learning Services를 동시에 설치](#install-all)할 수 있지만, 더 많은 구성 요소를 추가하기 전에 문제를 해결할 수 있도록 먼저 SQL Server 데이터베이스 엔진을 설치하고 구성하는 것이 좋습니다. 

R 및 Python 확장의 패키지 위치는 SQL Server Linux 원본 리포지토리에 있습니다. 데이터베이스 엔진 설치에 대한 원본 리포지토리를 이미 구성한 경우 동일한 리포지토리 등록을 사용하여 **mssql-mlservices** 패키지 설치 명령을 실행할 수 있습니다.

Machine Learning Services는 Linux 컨테이너에서도 지원됩니다. Machine Learning Services는 사용하는 미리 빌드된 컨테이너는 제공하지 않지만 [GitHub에서 이용 가능한 예제 템플릿](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)을 사용하여 SQL Server 컨테이너에서 만들 수 있습니다.

## <a name="uninstall-previous-ctp"></a>이전 CTP 제거

패키지 목록이 마지막 몇 개의 CTP 릴리스에 걸쳐 변경되어 패키지 개수가 줄어들게 됩니다. CTP 3.2를 설치하기 전에 CTP 2.x를 제거하여 이전 패키지를 모두 제거하는 것이 좋습니다. 여러 버전의 병렬 설치는 지원되지 않습니다.

### <a name="1-confirm-package-installation"></a>1. 패키지 설치 확인

첫 번째 단계로 이전 설치의 존재 여부를 확인하는 것이 좋습니다. 다음 파일은 기존 설치를 표시합니다. checkinstallextensibility.sh, exthost, launchpad.

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctp-2x-packages"></a>2. 이전 CTP 2.x 패키지 제거

가장 낮은 패키지 수준에서 제거합니다. 하위 수준 패키지에 종속된 모든 업스트림 패키지는 자동으로 제거됩니다.

  + R 통합의 경우 **microsoft -r-open**을 제거합니다.*
  + Python 통합의 경우 **mssql-mlservices-python**을 제거합니다.

패키지를 제거하는 명령은 다음 표에 나와 있습니다.

| 플랫폼  | 패키지 제거 명령 | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove microsoft-r-open-mro-3.4.4`<br/>`sudo yum remove msssql-mlservices-python` |
| SLES  | `sudo zypper remove microsoft-r-open-mro-3.4.4`<br/>`sudo zypper remove msssql-mlservices-python` |
| Ubuntu    | `sudo apt-get remove microsoft-r-open-mro-3.4.4`<br/>`sudo apt-get remove msssql-mlservices-python`|

> [!Note]
> Microsoft R Open 3.4.4는 이전에 설치한 CTP 릴리스에 따라 2~3개의 패키지로 구성됩니다. foreachiterators 패키지는 CTP 2.2의 main mro 패키지에 결합되었습니다. microsoft-r-open-mro-3.4.4를 제거한 후 이 패키지가 남아 있으면 개별적으로 제거해야 합니다.
> ```
> microsoft-r-open-foreachiterators-3.4.4
> microsoft-r-open-mkl-3.4.4
> microsoft-r-open-mro-3.4.4
> ```

### <a name="3-proceed-with-ctp-32-install"></a>3. CTP 3.2 설치 진행

운영 체제에 맞는 문서의 지침을 사용하여 가장 높은 패키지 수준에서 설치합니다.

각 OS별 설치 지침의 경우, *가장 높은 패키지 수준*은 **예 1 - 전체 설치**(전체 패키지 세트용) 또는 **예 2 - 최소 설치**(실행 가능한 설치에 필요한 최소 개수의 패키지용) 중 하나입니다.

1. R 통합의 경우 필수 조건이므로 [MRO](#mro)로 시작합니다. 이 항목 없으면 R 통합이 설치되지 않습니다.

2. 운영 체제에 대한 패키지 관리자 및 구문을 사용하여 설치 명령을 실행합니다. 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>사전 요구 사항

+ Linux 버전은 [SQL Server에서 지원](sql-server-linux-release-notes-2019.md#supported-platforms)되어야 하지만 Docker 엔진은 포함하지 않습니다. 지원되는 버전은 다음과 같습니다.

   + [Red Hat Enterprise Linux(RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux 서버](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ (R 전용) [Microsoft R Open](#mro)은 SQL Server의 R 기능에 대한 기본 R 배포를 제공합니다.

+ T-SQL 명령을 실행하기 위한 도구가 있어야 합니다. 설치 후 구성 및 유효성 검사에는 쿼리 편집기가 필요합니다. Linux에서 실행되는 체험용 다운로드인 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux)를 권장합니다.

<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>MRO(Microsoft R Open) 설치

R의 Microsoft 기본 배포는 Machine Learning Services와 함께 설치되는 RevoScaleR, MicrosoftML 및 기타 R 패키지를 사용하기 위한 필수 조건입니다.

필요한 버전은 MRO 3.5.2입니다.

다음 두 가지 방법 중 하나를 선택하여 MRO를 설치합니다.

+ MRAN에서 MRO tarball을 다운로드하고, 압축을 푼 다음, install.sh 스크립트를 실행합니다. 이 방법을 사용하려면 [MRAN에 대한 설치 지침](https://mran.microsoft.com/releases/3.5.2)을 따르면 됩니다.

+ 또는 아래 설명된 대로 **packages.microsoft.com** 리포지토리를 등록하여 MRO 배포를 구성하는 두 개의 패키지인 microsoft-r-open-mro 및 microsoft-r-open-mkl을 설치합니다. 

다음 명령은 MRO를 제공하는 리포지토리를 등록합니다. 등록 후에 mssql-mlservices-mml-r과 같은 다른 R 패키지를 설치하기 위한 명령에 MRO가 패키지 종속성으로 자동으로 포함됩니다.

#### <a name="mro-on-ubuntu"></a>Ubuntu의 MRO

```bash
# Install as root
sudo su

# Optionally, if your system does not have the https apt transport option
apt-get install apt-transport-https

# Set the location of the package repo the "prod" directory containing the distribution.
# This example specifies 16.04. Replace with 14.04 if you want that version
wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the repo
dpkg -i packages-microsoft-prod.deb

# Update packages on your system (required), including MRO installation
sudo apt-get update
```

#### <a name="mro-on-rhel"></a>RHEL의 MRO

```bash
# Import the Microsoft repository key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc


# Set the location of the package repo at the "prod" directory
# The following command is for version 7.x
# For 6.x, replace 7 with 6 to get that version
rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm

# Update packages on your system (optional)
yum update
```
#### <a name="mro-on-suse"></a>SUSE의 MRO

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SUSE in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

## <a name="package-list"></a>패키지 목록

인터넷에 연결된 디바이스에서 패키지는 각 운영 체제의 패키지 설치 프로그램을 사용하여 데이터베이스 엔진과 독립적으로 다운로드 및 설치됩니다. 다음 표에서는 사용할 수 있는 모든 패키지에 대해 설명하지만, R 및 Python의 경우 전체 기능 설치 또는 최소 기능 설치를 제공하는 패키지를 지정합니다.

| 패키지 이름 | 적용 대상 | 설명 |
|--------------|----------|-------------|
|mssql-server-extensibility  | All | R 및 Python 코드를 실행하는 데 사용되는 확장성 프레임워크입니다. |
| microsoft-openmpi  | Python, R | Linux에서 병렬 처리를 위해 Revo* 라이브러리에서 사용하는 메시지 전달 인터페이스입니다. |
| mssql-mlservices-python | Python | Anaconda 및 Python의 오픈 소스 배포입니다. |
|mssql-mlservices-mlm-py  | Python | ‘전체 설치’.  이미지 기능화 및 텍스트 감정 분석을 위한 revoscalepy, microsoftml, 미리 학습된 모델을 제공합니다.| 
|mssql-mlservices-packages-py  | Python | ‘최소 설치’.  revoscalepy 및 microsoftml을 제공합니다. <br/>미리 학습된 모델을 제외합니다. | 
| [microsoft-r-open*](#mro) | R | 3개 패키지로 구성된 R의 오픈 소스 배포입니다. |
|mssql-mlservices-mlm-r  | R | ‘전체 설치’.  이미지 기능화 및 텍스트 감정 분석을 위한 RevoScaleR, MicrosoftML, sqlRUtils, olapR, 미리 학습된 모델을 제공합니다.| 
|mssql-mlservices-packages-r  | R | ‘최소 설치’.  RevoScaleR, sqlRUtils, MicrosoftML, olapR을 제공합니다. <br/>미리 학습된 모델을 제외합니다. | 
|mssql-mlservices-mml-py  | CTP 2.0-2.1만 | Python 패키지가 mssql-mslservices-python에 통합되어 CTP 2.2에서 사용되지 않습니다. revoscalepy을 제공합니다. 미리 학습된 모델 및 microsoftml을 제외합니다.| 
|mssql-mlservices-mml-r  | CTP 2.0-2.1만 | R 패키지가 mssql-mslservices-python에 통합되어 CTP 2.2에서 사용되지 않습니다. RevoScaleR, sqlRUtils, olapR을 제공합니다. 미리 학습된 모델 및 MicrosoftML을 제외합니다.  |

<a name="RHEL"></a>

## <a name="redhat-commands"></a>RedHat 명령

필요한 모든 조합(단일 또는 여러 언어)으로 언어 지원을 설치할 수 있습니다. R 및 Python의 경우 두 가지 패키지를 선택할 수 있습니다. 하나는 사용 가능한 모든 기능을 ‘전체 설치’로 제공합니다.  대체 선택은 미리 학습된 기계 학습 모델을 제외하고 ‘최소 설치’로 간주됩니다. 

> [!Tip]
> 가능하면 `yum clean all`을 실행하여 설치 전에 시스템에서 패키지를 새로 고칩니다.

### <a name="example-1----full-installation"></a>예제 1 - 전체 설치 

R 및 Python을 위한 기계 학습 라이브러리 및 미리 학습된 모델과 함께 오픈 소스 R 및 Python, 확장성 프레임워크, microsoft-openmpi, 확장(R, Python)을 포함합니다. 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>예제 2 - 최소 설치 

R 및 Python을 위한 오픈 소스 R 및 Python, 확장성 프레임워크, microsoft-openmpi, core Revo* 라이브러리 및 기계 학습 라이브러리를 포함합니다. 미리 학습된 모델을 제외합니다.

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```

<a name="ubuntu"></a>

## <a name="ubuntu-commands"></a>Ubuntu 명령

필요한 모든 조합(단일 또는 여러 언어)으로 언어 지원을 설치할 수 있습니다. R 및 Python의 경우 두 가지 패키지를 선택할 수 있습니다. 하나는 사용 가능한 모든 기능을 ‘전체 설치’로 제공합니다.  대체 선택은 미리 학습된 기계 학습 모델을 제외하고 ‘최소 설치’로 간주됩니다. 

> [!Tip]
> 가능하면 `apt-get update`를 실행하여 설치 전에 시스템에서 패키지를 새로 고칩니다. 또한 Ubuntu의 일부 docker 이미지에는 https apt 전송 옵션이 없을 수도 있습니다. 설치하려면 `apt-get install apt-transport-https`를 사용합니다.

### <a name="example-1----full-installation"></a>예제 1 - 전체 설치 

R 및 Python을 위한 기계 학습 라이브러리 및 미리 학습된 모델과 함께 오픈 소스 R 및 Python, 확장성 프레임워크, microsoft-openmpi, 확장(R, Python)을 포함합니다. 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### <a name="example-2---minimum-installation"></a>예제 2 - 최소 설치 

R 및 Python을 위한 오픈 소스 R 및 Python, 확장성 프레임워크, microsoft-openmpi, core Revo* 라이브러리 및 기계 학습 라이브러리를 포함합니다. 미리 학습된 모델을 제외합니다. 

```bash
# Install as root or sudo
# Minimum install of R, Python
# No aasterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="suse"></a>

## <a name="suse-commands"></a>SUSE 명령

필요한 모든 조합(단일 또는 여러 언어)으로 언어 지원을 설치할 수 있습니다. R 및 Python의 경우 두 가지 패키지를 선택할 수 있습니다. 하나는 사용 가능한 모든 기능을 ‘전체 설치’로 제공합니다.  대체 선택은 미리 학습된 기계 학습 모델을 제외하고 ‘최소 설치’로 간주됩니다. 

### <a name="example-1----full-installation"></a>예제 1 - 전체 설치 

R 및 Python을 위한 기계 학습 라이브러리 및 미리 학습된 모델과 함께 오픈 소스 R 및 Python, 확장성 프레임워크, microsoft-openmpi, 확장(R, Python)을 포함합니다. 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.7*
sudo zypper install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>예제 2 - 최소 설치 

R 및 Python을 위한 오픈 소스 R 및 Python, 확장성 프레임워크, microsoft-openmpi, core Revo* 라이브러리 및 기계 학습 라이브러리를 포함합니다. 미리 학습된 모델을 제외합니다. 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.7*
sudo zypper install mssql-mlservices-packages-r-9.4.7*
```

## <a name="post-install-config-required"></a>설치 후 구성(필수)

추가 구성은 주로 [mssql-conf tool](sql-server-linux-configure-mssql-conf.md)을 통해 진행됩니다.


1. SQL Server 서비스를 실행하는 데 사용되는 mssql 사용자 계정을 추가합니다. 이는 이전에 설치를 실행하지 않은 경우에 필요합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. 오픈 소스 R 및 Python에 대한 사용권 계약에 동의합니다. 여러 가지 방법으로 이 작업을 수행할 수 있습니다. 이전에 SQL Server 라이선스에 동의했고 지금 R 또는 Python 확장을 추가하는 경우 다음 명령은 사용 약관에 대한 동의입니다.

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```

   대체 워크플로는 SQL Server 데이터베이스 엔진 사용권 계약에 아직 동의하지 않은 경우 설치 프로그램은 mssql-mlservices 패키지를 검색하고 `mssql-conf setup`이 실행될 때 EULA 동의 여부를 묻는 메시지를 표시합니다. EULA 매개 변수에 대한 자세한 내용은 [mssql-conf 도구를 사용하여 SQL Server 구성](sql-server-linux-configure-mssql-conf.md#mlservices-eula)을 참조하세요.

3. 아웃바운드 네트워크 액세스를 사용하도록 설정합니다. 아웃바운드 네트워크 액세스는 기본적으로 사용 안 함으로 설정됩니다. 아웃바운드 요청을 사용하려면 mssql-conf 도구를 사용하여 "outboundnetworkaccess" 부울 속성을 설정합니다. 자세한 내용은 [mssql-conf를 사용하여 SQL Server on Linux 구성](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)을 참조하세요.

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. R 기능 통합의 경우에만 **MKL_CBWR** 환경 변수를 설정하여 Intel MKL(Math Kernel Library) 계산에서 [일관성 있는 출력을 보장](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)합니다.

   + 사용자 홈 디렉터리에서 **.bash_profile** 파일을 편집하거나 만들어 파일에 `export MKL_CBWR="AUTO"` 줄을 추가합니다.

   + Bash 명령 프롬프트에서 `source .bash_profile`을 입력하여 이 파일을 실행합니다.

5. SQL Server 실행 패드 서비스 및 데이터베이스 엔진 인스턴스를 다시 시작하여 INI 파일에서 업데이트된 값을 읽습니다. 다시 시작 메시지가 확장성 관련 설정이 수정될 때마다 사용자에게 알려줍니다.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

6. Transact-SQL을 실행하는 Azure Data Studio 또는 SQL Server Management Studio(Windows에만 해당)와 같은 다른 도구를 사용하여 외부 스크립트 실행을 사용하도록 설정합니다. 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. 실행 패드 서비스를 다시 시작합니다.

## <a name="verify-installation"></a>설치 확인

R 라이브러리(MicrosoftML, RevoScaleR 등)는 `/opt/mssql/mlservices/libraries/RServer`에서 찾을 수 있습니다.

Python 라이브러리(microsoftml 및 revoscalepy)는 `/opt/mssql/mlservices/libraries/PythonServer`에서 찾을 수 있습니다.

설치의 유효성을 검사하려면 R 또는 Python을 호출하는 시스템 저장 프로시저를 실행하는 T-SQL 스크립트를 실행합니다. 이 작업에 대한 쿼리 도구가 필요합니다. Azure Data Studio를 선택하는 것이 좋습니다. SQL Server Management Studio 또는 PowerShell과 같이 일반적으로 사용되는 다른 도구는 Windows 전용입니다. 이러한 도구가 포함된 Windows 컴퓨터를 사용하는 경우 이를 사용하여 데이터베이스 엔진의 Linux 설치에 연결합니다.

다음 SQL 명령을 실행하여 SQL Server에서 R 실행을 테스트합니다. 스크립트가 실행되지 않으면 서비스 다시 시작인 `sudo systemctl restart mssql-server.service`를 사용해 봅니다.

```r
EXEC sp_execute_external_script   
@language =N'R', 
@script=N' 
OutputDataSet <- InputDataSet', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```
 
다음 SQL 명령을 실행하여 SQL Server에서 Python 실행을 테스트합니다. 
 
```python
EXEC sp_execute_external_script  
@language =N'Python', 
@script=N' 
OutputDataSet = InputDataSet; 
', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```

<a name="install-all"></a>

## <a name="chained-combo-install"></a>연결된 “콤보” 설치

데이터베이스 엔진을 설치하는 명령에 R 또는 Python 패키지와 매개 변수를 추가하여 한 가지 프로시저에서 데이터베이스 엔진 및 Machine Learning Services를 설치하고 구성할 수 있습니다. 

1. R 통합의 경우 [Microsoft R Open](#mro)을 필수 조건으로 설치합니다. R 기능을 설치하지 않는 경우에는 이 단계를 건너뜁니다.

2. 데이터베이스 엔진 및 언어 확장 기능을 포함하는 명령줄을 제공합니다.

  데이터베이스 엔진 설치에 Python 통합과 같은 단일 기능을 추가할 수 있습니다.

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* 
  ```

  또는 두 확장(R, Python)을 모두 추가합니다.

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* mssql-mlservices-packages-py-9.4.7*
  ```

3. 사용권 계약에 동의하고 설치 후 구성을 완료합니다. 이 작업을 위해 **mssql-conf** 도구를 사용합니다.

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  데이터베이스 엔진에 대한 사용권 계약에 동의하고, 버전을 선택하고, 관리자 암호를 설정하라는 메시지가 표시됩니다. Machine Learning Services의 사용권 계약에 동의하라는 메시지도 표시됩니다.

4. 서비스를 다시 시작하라는 메시지가 표시되면 서비스를 다시 시작합니다.

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>무인 설치

데이터베이스 엔진에 대한 [무인 설치](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended)를 사용하여 mssql-mlservices용 패키지와 EULA를 추가합니다.

사용권 계약 동의를 위해 설치 프로그램 또는 mssql-conf 도구 프롬프트를 기억합니다. 이미 SQL Server 데이터베이스 엔진을 구성하고 해당 EULA에 동의한 경우 오픈 소스 R 및 Python 배포를 위해 mlservices 관련 EULA 매개 변수 중 하나를 사용합니다.

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

EULA 동의의 가능한 모든 순열은 [mssql-conf 도구를 사용하여 SQL Server on Linux 구성](sql-server-linux-configure-mssql-conf.md#mlservices-eula)에서 설명합니다.

## <a name="offline-installation"></a>오프라인 설치

패키지 설치 단계의 [오프라인 설치](sql-server-linux-setup.md#offline) 지침을 따릅니다. 다운로드 사이트를 찾은 후 아래 패키지 목록을 사용하여 특정 패키지를 다운로드합니다.

> [!Tip]
> 여러 패키지 관리 도구에서 패키지 종속성을 확인하는 데 도움이 되는 명령을 제공합니다. Yum의 경우 `sudo yum deplist [package]`를 사용합니다. Ubuntu의 경우 `dpkg -I [package name].deb`와 `sudo apt-get install --reinstall --download-only [package name]`을 차례로 사용합니다.


#### <a name="download-site"></a>다운로드 사이트

[https://packages.microsoft.com/](https://packages.microsoft.com/)에서 패키지를 다운로드할 수 있습니다. R 및 Python용 모든 mlservices 패키지는 데이터베이스 엔진 패키지와 함께 배치됩니다. mlservices 패키지의 기본 버전은 9.4.5(CTP 2.0) 및 9.4.6(CTP 2.1 이상)입니다. microsoft-r-open 패키지가 [다른 리포지토리](#mro)에 있음을 기억합니다.

#### <a name="rhel7-paths"></a>RHEL/7 경로

|||
|--|----|
| mssql/mlservices 패키지 | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |
| microsoft-r-open 패키지 | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 경로

|||
|--|----|
| mssql/mlservices 패키지 | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |
| microsoft-r-open 패키지 | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>SLES/12 경로

|||
|--|----|
| mssql/mlservices 패키지 | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| microsoft-r-open 패키지 | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

#### <a name="package-list"></a>패키지 목록

사용하려는 확장에 따라 특정 언어에 필요한 패키지를 다운로드합니다. 정확한 파일 이름에는 접미사에 플랫폼 정보가 포함되지만, 다음의 파일 이름은 어떤 파일을 가져올지 결정할 수 있을 만큼 충분히 가까워야 합니다.

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# R
microsoft-openmpi-3.0.0
microsoft-r-open-mkl-3.5.2
microsoft-r-open-mro-3.5.2
mssql-mlservices-packages-r-9.4.7.64
mssql-mlservices-mlm-r-9.4.7.64


# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.7.64
mssql-mlservices-packages-py-9.4.7.64
mssql-mlservices-mlm-py-9.4.7.64
```

## <a name="add-more-rpython-packages"></a>R/Python 패키지 추가 
 
다른 R 및 Python 패키지를 설치하고 SQL Server 2019에서 실행되는 스크립트에서 사용할 수 있습니다.

### <a name="r-packages"></a>R 패키지 
 
1. R 세션을 시작합니다.

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R 
   ```

2. [glue](https://mran.microsoft.com/package/glue)라는 R 패키지를 설치하여 패키지 설치를 테스트합니다.

   ```r
   # install.packages("glue",lib="/opt/mssql/mlservices/libraries/RServer") 
   ```
   또는 명령줄에서 R 패키지를 설치할 수 있습니다. 

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R CMD INSTALL -l /opt/mssql/mlservices/libraries/RServer glue_1.1.1.tar.gz 
   ```

3. [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)로 R 패키지를 가져옵니다.

   ```r
   EXEC sp_execute_external_script  
   @language = N'R', 
   @script = N'library(glue)' 
   ```

### <a name="python-packages"></a>Python 패키지 
 
1. pip를 사용하여 [httpie](https://httpie.org/)라는 Python 패키지를 설치합니다. 

   ```python
   # sudo /opt/mssql/mlservices/bin/python/python -m pip install httpie 
   ``` 

2. [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)로 Python 패키지를 가져옵니다.
 
   ```python
   EXEC sp_execute_external_script  
   @language = N'Python',  
   @script = N'import httpie' 
   ```

## <a name="limitations-in-ctp-releases"></a>CTP 릴리스의 제한 사항

Linux의 R 및 Python 통합은 아직 개발 중입니다. 미리 보기 버전에서 다음 기능은 아직 사용할 수 없습니다.

+ 현재로서는 Linux의 Machine Learning Services에서 암시적 인증을 사용할 수 없습니다. 즉, 진행 중인 R 또는 Python 스크립트에서 데이터 또는 기타 리소스에 액세스하기 위해 서버에 다시 연결할 수 없습니다. 

### <a name="resource-governance"></a>리소스 거버넌스

외부 리소스 풀에 대한 [리소스 거버넌스](../t-sql/statements/create-external-resource-pool-transact-sql.md)에서 Linux와 Windows 사이에 패리티가 있지만, [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)에 대한 통계는 현재 Linux에서 다른 단위를 사용합니다 단위는 향후 CTP에 맞춰집니다.
 
| 열 이름   | 설명 | Linux의 값 | 
|---------------|--------------|---------------|
|peak_memory_kb | 리소스 풀에 사용되는 최대 메모리 양입니다. | Linux에서 이 통계의 출처는 CGroups 메모리 하위 시스템이며, 여기서 값은 memory.max_usage_in_bytes입니다. |
|write_io_count | Resource Governor 통계를 다시 설정한 후 발생한 총 쓰기 IO입니다. | Linux에서 이 통계의 출처는 CGroups blkio 하위 시스템이며, 쓰기 행의 값은 blkio.throttle.io_serviced입니다. | 
|read_io_count | Resource Governor 통계를 다시 설정한 후 발생한 총 읽기 IO입니다. | Linux에서 이 통계의 출처는 CGroups blkio 하위 시스템이며, 읽기 행의 값은 blkio.throttle.io_serviced입니다. | 
|total_cpu_kernel_ms | Resource Governor 통계를 다시 설정한 후 누적된 CPU 사용자 커널 시간(밀리초)입니다. | Linux에서 이 통계의 출처는 CGroups cpuacct 하위 시스템이며, 사용자 행의 값은 cpuacct.stat입니다. |  
|total_cpu_user_ms | Resource Governor 통계를 다시 설정한 후 누적된 CPU 사용자 시간(밀리초)입니다.| Linux에서 이 통계의 출처는 CGroups cpuacct 하위 시스템이며, 시스템 행 값은 cpuacct.stat입니다. | 
|active_processes_count | 요청 순간에 실행되는 외부 프로세스의 수입니다.| Linux에서 이 통계의 출처는 GGroups pids 하위 시스템이며, 여기서 값은 pids.current입니다. | 

## <a name="next-steps"></a>다음 단계

R 개발자는 몇 가지 간단한 예제를 시작하고 R이 SQL Server에서 작동하는 방식의 기초를 알아볼 수 있습니다. 다음 단계로 가려면 아래 링크를 참조하세요.

+ [자습서: T-SQL에서 R 사용](../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [자습서: R 개발자를 위한 데이터베이스 내 분석](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 개발자는 다음 자습서에 따라 SQL Server에서 Python을 사용하는 방법을 알아볼 수 있습니다.

+ [자습서: T-SQL에서 Python 실행](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [자습서: Python 개발자를 위한 데이터베이스 내 분석](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 [기계 학습 자습서](../advanced-analytics/tutorials/machine-learning-services-tutorials.md)를 참조하세요.
