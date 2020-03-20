---
title: Linux에 SQL Server Machine Learning Services(Python, R) 설치
description: Linux에 SQL Server Machine Learning Services(Python 및 R) 설치하는 방법에 대해 알아보세요. Red Hat, Ubuntu 및 SUSE.
author: cawrites
ms.author: chadam
ms.reviewer: vanto
manager: cgronlun
ms.date: 03/05/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bf474ff8a7587c916591e6d7ba4dc82052b516f7
ms.sourcegitcommit: fc99fdd586eabc2d60f33056123398f263d5913d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2020
ms.locfileid: "78937655"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-linux"></a>Linux에 SQL Server Machine Learning Services(Python 및 R) 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux에 [SQL Server Machine Learning Services](../advanced-analytics/index.yml)를 설치하는 과정을 안내합니다. Machine Learning Services를 사용하여 데이터베이스 내에서 Python 및 R 스크립트를 실행할 수 있습니다.

[!NOTE]
> Machine Learning Services는 기본적으로 SQL Server 빅 데이터 클러스터에 설치됩니다. 자세한 내용은 [빅 데이터 클러스터에서 Machine Learning Services(Python 및 R) 사용](../big-data-cluster/machine-learning-services.md)을 참조하세요.

## <a name="what-are-machine-learning-services"></a>Machine Learning Services란

Machine Learning Services는 데이터베이스 엔진의 추가 기능입니다.

구성 요소를 더 추가하기 전에 문제를 해결할 수 있도록 먼저 SQL Server 데이터베이스 엔진을 설치하고 구성합니다.

## <a name="pre-install-checklist"></a>설치 전 검사 목록

[SQL Server on Linux를 설치](https://docs.microsoft.com/sql/linux/sql-server-linux-setup)한 다음, 설치를 확인합니다.

* Python 및 R 확장의 SQL Server Linux 리포지토리를 확인합니다. 
* 데이터베이스 엔진 설치에 대한 원본 리포지토리를 이미 구성한 경우 동일한 리포지토리 등록을 사용하여 **mssql-mlservices** 패키지 설치 명령을 실행할 수 있습니다.

* [Microsoft R Open](#mro)은 SQL Server의 R 기능을 위한 기본 R 배포를 제공합니다.

* T-SQL 명령을 실행하기 위한 도구가 있어야 합니다. 
* 설치 후 구성 및 유효성 검사에는 쿼리 편집기가 필요합니다. 
* Linux에서 실행되는 체험용 다운로드인 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux)를 권장합니다.


<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>MRO(Microsoft R Open) 설치

R의 Microsoft 기본 배포는 Machine Learning Services와 함께 설치되는 RevoScaleR, MicrosoftML 및 기타 R 패키지를 사용하기 위한 필수 조건입니다.

필요한 버전은 MRO 3.5.2입니다.

다음 두 가지 방법 중 하나를 선택하여 MRO를 설치합니다.

+ MRAN에서 MRO tarball을 다운로드하고, 압축을 푼 다음, install.sh 스크립트를 실행합니다. 이 방법을 사용하려면 [MRAN에 대한 설치 지침](https://mran.microsoft.com/releases/3.5.2)을 따르면 됩니다.

+ 아래 설명된 대로 **packages.microsoft.com** 리포지토리를 등록하여 MRO 배포 microsoft-r-open-mro 및 microsoft-r-open-mkl을 설치합니다. 

<a name="RHEL"></a>

## <a name="install-on-redhat"></a>RedHat에 설치

### <a name="install-mro-on-red-hat"></a>Red Hat에 설치(MRO)

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

Python 및 R의 설치 옵션:

*  요구 사항에 따라 언어 지원을 설치합니다(단일 언어 또는 여러 언어).
*  ‘전체 설치’는 미리 학습된 기계 학습 모델을 포함하여 사용 가능한 모든 기능을 제공합니다. 
*  ‘최소 설치’는 모델을 제외하지만 모든 기능을 포함합니다. 

> [!Tip]
> 가능하면 `yum clean all`을 실행하여 설치 전에 시스템에서 패키지를 새로 고칩니다.

### <a name="example-1----full-installation"></a>예제 1 - 전체 설치

포함 항목:
*  오픈 소스 Python
*  오픈 소스 R
*  확장성 프레임워크
*  microsoft-openmpi
*  확장(Python, R)
*  기계 학습 라이브러리
*  Python 및 R용 미리 학습된 모델

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7*
```

### <a name="example-2---minimum-installation"></a>예제 2 - 최소 설치

포함 항목:
*  오픈 소스 Python
*  오픈 소스 R
*  확장성 프레임워크
*  microsoft-openmpi
*  핵심 Revo* 라이브러리
*  기계 학습 라이브러리

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```
<a name="ubuntu"></a>

## <a name="install-on-ubuntu"></a>Ubuntu에 설치

### <a name="install-mro-on-ubuntu"></a>Ubuntu에 설치(MRO)

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

Python 및 R의 설치 옵션:

*  요구 사항에 따라 언어 지원을 설치합니다(단일 언어 또는 여러 언어).
*  ‘전체 설치’는 미리 학습된 기계 학습 모델을 포함하여 사용 가능한 모든 기능을 제공합니다. 
*  ‘최소 설치’는 모델을 제외하지만 모든 기능을 포함합니다. 

> [!Tip]
> 가능하면 `apt-get update`을 실행하여 설치 전에 시스템에서 패키지를 새로 고칩니다. 

### <a name="example-1----full-installation"></a>예제 1 - 전체 설치 

포함 항목:
*  오픈 소스 Python
*  오픈 소스 R
*  확장성 프레임워크
*  microsoft-openmpi
*  Python 확장
*  R 확장
*  기계 학습 라이브러리
*  Python 및 R용 미리 학습된 모델

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### <a name="example-2---minimum-installation"></a>예제 2 - 최소 설치 

포함 항목:
*  오픈 소스 Python
*  오픈 소스 R
*  확장성 프레임워크
*  microsoft-openmpi
*  핵심 Revo* 라이브러리
*  기계 학습 라이브러리

```bash
# Install as root or sudo
# Minimum install of R, Python
# No asterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="SLES"></a>

## <a name="install-on-suse"></a>SUSE에 설치

### <a name="install-mro-on-susesles"></a>SUSE(SLES)에 설치(MRO)

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SUSE in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

Python 및 R의 설치 옵션:

*  요구 사항에 따라 언어 지원을 설치합니다(단일 언어 또는 여러 언어).
*  ‘전체 설치’는 미리 학습된 기계 학습 모델을 포함하여 사용 가능한 모든 기능을 제공합니다. 
*  ‘최소 설치’는 모델을 제외하지만 모든 기능을 포함합니다. 

### <a name="example-1----full-installation"></a>예제 1 - 전체 설치 

포함 항목:
*  오픈 소스 Python
*  오픈 소스 R
*  확장성 프레임워크
*  microsoft-openmpi
*  Python 및 R용 확장
*  기계 학습 라이브러리
*  Python 및 R용 미리 학습된 모델

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.7*
sudo zypper install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>예제 2 - 최소 설치 

포함 항목:
*  오픈 소스 Python
*  오픈 소스 R
*  확장성 프레임워크
*  microsoft-openmpi
*  핵심 Revo* 라이브러리
*  기계 학습 라이브러리 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.7*
sudo zypper install mssql-mlservices-packages-r-9.4.7*
```

## <a name="post-install-config-required"></a>설치 후 구성(필수)

추가 구성은 주로 [mssql-conf tool](sql-server-linux-configure-mssql-conf.md)을 통해 진행됩니다.


1. SQL Server 서비스를 실행하는 데 사용되는 mssql 사용자 계정을 추가합니다.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. 오픈 소스 Python 및 R 확장의 사용권 계약에 동의합니다. 다음 명령을 사용합니다.

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```
3. `mssql-conf setup`을 실행하면 설치 프로그램이 mssql-mlservices 패키지를 검색하고 EULA에 동의하라는 메시지를 표시합니다(이전에 동의하지 않은 경우). EULA 매개 변수에 대한 자세한 내용은 [mssql-conf 도구를 사용하여 SQL Server 구성](sql-server-linux-configure-mssql-conf.md#mlservices-eula)을 참조하세요.

4. 아웃바운드 네트워크 액세스를 사용하도록 설정합니다. 아웃바운드 네트워크 액세스는 기본적으로 사용 안 함으로 설정됩니다. 아웃바운드 요청을 사용하려면 mssql-conf 도구를 사용하여 "outboundnetworkaccess" 부울 속성을 설정합니다. 자세한 내용은 [mssql-conf를 사용하여 SQL Server on Linux 구성](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)을 참조하세요.

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

5. R 기능 통합의 경우에만 **MKL_CBWR** 환경 변수를 설정하여 Intel MKL(Math Kernel Library) 계산에서 [일관성 있는 출력을 보장](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)합니다.

   + 사용자 홈 디렉터리에서 `named.bash_profile` 파일을 편집하거나 만들고 파일에 `export MKL_CBWR="AUTO"` 줄을 추가합니다.

   + Bash 명령 프롬프트에서 `source.bash_profile`을 입력하여 이 파일을 실행합니다.

6. SQL Server 실행 패드 서비스 및 데이터베이스 엔진 인스턴스를 다시 시작하여 INI 파일에서 업데이트된 값을 읽습니다. 확장성 관련 설정을 수정하면 알림 메시지가 표시됩니다.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

7. Transact-SQL을 실행하는 Azure Data Studio 또는 SQL Server Management Studio(Windows에만 해당)와 같은 다른 도구를 사용하여 외부 스크립트 실행을 사용하도록 설정합니다. 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. 실행 패드 서비스를 다시 시작합니다.

## <a name="verify-installation"></a>설치 확인

R 라이브러리(MicrosoftML, RevoScaleR 등)는 `/opt/mssql/mlservices/libraries/RServer`에서 찾을 수 있습니다.

Python 라이브러리(microsoftml 및 revoscalepy)는 `/opt/mssql/mlservices/libraries/PythonServer`에서 찾을 수 있습니다.

설치의 유효성을 검사하려면 다음을 수행합니다.

- 쿼리 도구를 사용하여 Python 또는 R 호출 시스템 저장 프로시저를 실행하는 T-SQL 스크립트를 실행합니다. 

Windows에서는 다음을 사용합니다. 
*  Azure Data Studio
*  SQL Server Management Studio 또는 PowerShell

이러한 도구가 포함된 Windows 컴퓨터를 사용하는 경우 이를 사용하여 데이터베이스 엔진의 Linux 설치에 연결합니다.

다음 SQL 명령을 실행하여 SQL Server에서 R 실행을 테스트합니다. 오류가 발생하는 경우 서비스를 다시 시작해 보세요(`sudo systemctl restart mssql-server.service`).

```
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

## <a name="unattended-installation"></a>무인 설치

데이터베이스 엔진에 대한 [무인 설치](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended)를 사용하여 mssql-mlservices용 패키지와 EULA를 추가합니다.

 오픈 소스 R 및 Python 배포에 대해 mlservices 관련 EULA 매개 변수 중 하나를 사용합니다.

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

전체 EULA는 [mssql-conf 도구를 사용하여 SQL Server on Linux 구성](sql-server-linux-configure-mssql-conf.md#mlservices-eula)에 나와 있습니다.

## <a name="offline-installation"></a>오프라인 설치

패키지 설치 단계의 [오프라인 설치](sql-server-linux-setup.md#offline) 지침을 따릅니다. 아래 패키지 목록을 사용하여 특정 패키지를 다운로드합니다.

> [!Tip]
> 여러 패키지 관리 도구에서 패키지 종속성을 확인하는 데 도움이 되는 명령을 제공합니다. Yum의 경우 `sudo yum deplist [package]`를 사용합니다. Ubuntu의 경우 `dpkg -I [package name].deb`와 `sudo apt-get install --reinstall --download-only [package name]`을 차례로 사용합니다.


#### <a name="download-site"></a>다운로드 사이트

[https://packages.microsoft.com/](https://packages.microsoft.com/)에서 패키지를 다운로드합니다. Python 및 R용 mlservices 패키지는 모두 데이터베이스 엔진 패키지와 함께 배치됩니다. mlservices 패키지의 기본 버전은 9.4.6입니다. microsoft-r-open 패키지가 [다른 리포지토리](#mro)에 있음을 기억합니다.

#### <a name="rhel7-paths"></a>RHEL/7 경로

|||
|--|----|
| mssql/mlservices 패키지 | [https://packages.microsoft.com/rhel/7/mssql-server-2019/](https://packages.microsoft.com/rhel/7/mssql-server-2019/) |
| microsoft-r-open 패키지 | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 경로

|||
|--|----|
| mssql/mlservices 패키지 | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/) |
| microsoft-r-open 패키지 | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>SLES/12 경로

|||
|--|----|
| mssql/mlservices 패키지 | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| microsoft-r-open 패키지 | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) |

## <a name="package-list"></a>패키지 목록

사용 가능한 설치 패키지:

| 패키지 이름 | 적용 대상 | Description |
|--------------|----------|-------------|
|mssql-server-extensibility  | 모두 | Python 및 R을 실행하는 데 사용되는 확장성 프레임워크입니다. |
| microsoft-openmpi  | Python, R | Linux에서 병렬 처리를 위해 Rev* 라이브러리가 사용하는 메시지 전달 인터페이스입니다. |
| mssql-mlservices-python | Python | Anaconda 및 Python의 오픈 소스 배포입니다. |
|mssql-mlservices-mlm-py  | Python | ‘전체 설치’.  이미지 기능화 및 텍스트 감정 분석을 위한 revoscalepy, microsoftml, 미리 학습된 모델을 제공합니다.| 
|mssql-mlservices-packages-py  | Python | ‘최소 설치’.  revoscalepy 및 microsoftml을 제공합니다. <br/>미리 학습된 모델을 제외합니다. | 
| [microsoft-r-open*](#mro) | R | 3개 패키지로 구성된 R의 오픈 소스 배포입니다. |
|mssql-mlservices-mlm-r  | R | ‘전체 설치’.  제공 항목: 이미지 기능화 및 텍스트 감정 분석을 위한 미리 학습된 모델, RevoScaleR, MicrosoftML, sqlRUtils, olapR| 
|mssql-mlservices-packages-r  | R | ‘최소 설치’.  RevoScaleR, sqlRUtils, MicrosoftML, olapR을 제공합니다. <br/>미리 학습된 모델을 제외합니다. |

사용하려는 확장을 선택하고 특정 언어에 필요한 패키지를 다운로드합니다. 파일 이름의 접미사에 플랫폼 정보가 포함됩니다.

파일 목록:

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

## <a name="next-steps"></a>다음 단계

R 개발자는 몇 가지 간단한 예제를 시작하고 R이 SQL Server에서 작동하는 방식의 기초를 알아볼 수 있습니다. 다음 단계로 가려면 아래 링크를 참조하세요.

+ [자습서: T-SQL에서 R 사용](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [자습서: R 개발자를 위한 데이터베이스 내 분석](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 개발자는 다음 자습서에 따라 SQL Server에서 Python을 사용하는 방법을 알아볼 수 있습니다.

+ [자습서: T-SQL에서 Python 실행](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [자습서: Python 개발자를 위한 데이터베이스 내 분석](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 [기계 학습 자습서](../advanced-analytics/tutorials/machine-learning-services-tutorials.md)를 참조하세요.
