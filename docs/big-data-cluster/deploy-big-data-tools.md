---
title: 빅 데이터 도구 설치
titleSuffix: SQL Server big data clusters
description: (미리 보기)와 함께 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 사용 되는 도구를 설치 하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 84c7181bfd7c0ee014b382052bb6493d68251331
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153608"
---
# <a name="install-sql-server-2019-big-data-tools"></a>SQL Server 2019 빅 데이터 도구 설치

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 (미리 보기)를 만들고 관리 하 고 사용 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 하기 위해 설치 해야 하는 클라이언트 도구에 대해 설명 합니다. 다음 섹션에서는 도구 목록 및 설치 지침 링크를 제공합니다. 빅 데이터 클러스터를 배포하기 전에 Windows 또는 Linux에서 필수로 표시된 도구를 구성합니다.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>빅 데이터 클러스터 도구

다음 표에는 일반적인 빅 데이터 클러스터 도구와 도구 설치 방법이 나와 있습니다.

| 도구 | 필수 | 설명 | 설치 |
|---|---|---|---|
| **python** | 예 | python은 동적 의미 체계를 사용하는 해석된 개체 지향 고급 프로그래밍 언어입니다. SQL Server 빅 데이터 클러스터의 대부분은 python을 사용합니다. | [python 설치](#python).|
| **azdata** | 예 | 빅 데이터 클러스터를 설치하고 관리하기 위한 명령줄 도구입니다. | [설치](deploy-install-azdata.md) |
| **kubectl**<sup>1</sup> | 예 | 기본 Kuberentes 클러스터를 모니터링하기 위한 명령줄 도구입니다([자세한 정보](https://kubernetes.io/docs/tasks/tools/install-kubectl/)). | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio-SQL Server 2019 RC (릴리스 후보)** | 예 | SQL Server 쿼리를 위한 플랫폼 간 그래픽 도구입니다. | [설치](#download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc) |
| **SQL Server 2019 확장** | 예 | 빅 데이터 클러스터에 대한 연결을 지원하는 Azure Data Studio 확장입니다. 데이터 가상화 마법사도 제공합니다. | [설치](../azure-data-studio/sql-server-2019-extension.md) |
| **Azure CLI**<sup>2</sup> | AKS의 경우 | Azure 서비스를 관리하기 위한 최신 명령줄 인터페이스입니다. AKS 빅 데이터 클러스터 배포와 함께 사용됩니다([자세한 정보](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)). | [설치](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | Optional | SQL Server를 쿼리하기 위한 최신 명령줄 인터페이스입니다([자세한 정보](https://github.com/dbcli/mssql-cli/blob/master/README.rst)). | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | 일부 스크립트의 경우 | SQL Server를 쿼리하기 위한 레거시 명령줄 도구입니다([자세한 정보](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15)). | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | 일부 스크립트의 경우 | URL을 사용하여 데이터를 전송하기 위한 명령줄 도구입니다. | [Windows](https://curl.haxx.se/windows/) \| Linux: curl 패키지 설치 |

<sup>1</sup> kubectl 버전 1.10 이상을 사용해야 합니다. 또한 kubectl 버전은 Kubernetes 클러스터의 바로 이전 또는 이후 부 버전이어야 합니다. kubectl 클라이언트에서 특정 버전을 설치하려는 경우 [Install kubectl binary via curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)(curl을 통해 kubectl 이진 설치)를 참조하세요(Windows 10에서는 Windows PowerShell이 아닌 cmd.exe를 사용하여 curl 실행).

> [!TIP]
> AKS(Azure Kubernetes Service)에서 이전에 배포한 클러스터와 함께 kubectl을 사용하려면 다음 Azure CLI 명령을 사용하여 클러스터 컨텍스트를 설정해야 합니다.
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> Azure CLI 버전 2.0.4 이상을 사용해야 합니다. 필요한 경우 `az --version`을 실행하여 버전을 찾습니다.

<sup>3</sup> Windows 10에서 실행하는 경우에는 cmd 프롬프트에서 실행할 때 **curl**이 PATH에 이미 있습니다. 다른 Windows 버전에서는 링크를 사용하여 **curl**을 다운로드한 다음, PATH에 저장합니다.

## <a name="which-tools-are-required"></a>필수 도구

위의 표에서는 빅 데이터 클러스터에서 사용되는 일반적인 도구를 모두 제공합니다. 필수 도구는 시나리오에 따라 다릅니다. 그러나 일반적으로 클러스터를 관리, 연결 및 쿼리하는 데 가장 중요한 도구는 다음과 같습니다.

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 확장**

나머지 도구는 특정 시나리오에서만 필요합니다. **Azure CLI**는 AKS 배포와 관련된 Azure 서비스를 관리하는 데 사용할 수 있습니다. **mssql-cli**는 선택 사항이지만, 클러스터의 SQL Server 마스터 인스턴스에 연결하고 명령줄에서 쿼리를 실행할 수 있도록 하는 유용한 도구입니다. 또한 GitHub 스크립트를 사용하여 샘플 데이터를 설치하려는 경우 **sqlcmd** 및 **curl**이 필요합니다.

### <a id="python"></a> python 오프라인 설치

1. 인터넷에 액세스할 수 있는 머신에서 Python을 포함하는 다음 압축 파일 중 하나를 다운로드합니다.

   | 운영 체제 | 다운로드 |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. 압축 파일을 대상 머신에 복사하고 선택한 폴더로 추출합니다.

1. 해당 폴더에서 `installLocalPythonPackages.bat`를 실행하고 동일한 폴더의 전체 경로를 매개 변수로 전달합니다(Windows에만 해당).

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

## <a name="download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc"></a>Azure Data Studio SQL Server 2019 릴리스 후보 (RC) 다운로드 및 설치

Azure Data Studio SQL Server 2019 RC는 SQL Server 2019 RC 전용 기능 및 기능을 제공 합니다.

Azure Data Studio 프로덕션 릴리스의 일반적인 경우 [Azure Data Studio 다운로드 및 설치](../azure-data-studio/download.md)의 지침을 따르세요.

|플랫폼|다운로드|릴리스 날짜| 버전 |
|:---|:---|:---|:---|
|Windows|[사용자 설치 관리자(권장)](https://go.microsoft.com/fwlink/?linkid=2102435)<br>[시스템 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2102523)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2102524)|2019 년 8 월 27 일 |RC 1.11.0-참가자|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2102436)|2019 년 8 월 27 일 |RC 1.11.0-참가자|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2102526)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2102437)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2102525)|2019 년 8 월 27 일 |RC 1.11.0-참가자|

최신 릴리스에 대한 자세한 내용은 [릴리스 정보](../big-data-cluster/release-notes-big-data-cluster.md)를 참조하십시오.

### <a name="get-azure-data-studio-for-windows"></a>Windows용 Azure Data Studio 다운로드

이 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 릴리스에는 표준 Windows 설치 관리자 환경과 .zip이 포함되어 있습니다.

‘사용자 설치 관리자’는 관리자 권한이 필요하지 않기 때문에 설치와 업그레이드가 모두 간소화되므로 권장됩니다. 사용자 설치 관리자는 해당 위치가 사용자 Local AppData(LOCALAPPDATA) 폴더에 있기 때문에 관리자 권한이 필요하지 않습니다. 또한 사용자 설치 관리자는 더 원활한 백그라운드 업데이트 환경을 제공합니다. 자세한 내용은 [Windows용 사용자 설치 프로그램](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows)을 참조하세요.

**사용자 설치 관리자**(권장)

1. [Windows용 [!INCLUDE[name-sos](../includes/name-sos-short.md)] ‘사용자’ 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2102435)를 다운로드하여 실행합니다.
2. [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 앱을 시작합니다.

**시스템 설치 관리자**

1. [Windows용 [!INCLUDE[name-sos](../includes/name-sos-short.md)] ‘시스템’ 설치 관리자](https://go.microsoft.com/fwlink/?linkid=2102523)를 다운로드하여 실행합니다.
2. [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 앱을 시작합니다.

**zip 파일**

1. [Windows용 [!INCLUDE[name-sos](../includes/name-sos-short.md)] .zip](https://go.microsoft.com/fwlink/?linkid=2102524)을 다운로드합니다.
2. 다운로드한 파일을 찾은 다음 압축을 풉니다.
3. `\azuredatastudio-windows\azuredatastudio.exe`를 실행합니다.

### <a name="get-azure-data-studio-for-macos"></a>MacOS에 대한 Azure Data Studio 가져오기

1. [macOS용 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](https://go.microsoft.com/fwlink/?linkid=2102436)를 다운로드합니다.
2. zip 내용을 확장하기 위해 두 번 클릭합니다.
3. *실행 패드*에서 [!INCLUDE[name-sos](../includes/name-sos-short.md)]를 사용할 수 있게 하려면 *Azure Data Studio.app*을 *응용 프로그램* 폴더로 끌어옵니다.

### <a name="get-azure-data-studio-for-linux"></a>Linux용 Azure Data Studio 다운로드

1. 아래에서 설치 관리자 또는 tar.gz 보관 파일 중 하나를 사용하여 Linux용 [!INCLUDE[name-sos](../includes/name-sos-short.md)]를 다운로드합니다.
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2102526)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2102437)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2102525)
1. 파일을 추출하고 [!INCLUDE[name-sos](../includes/name-sos-short.md)]를 실행하기 위해 새 터미널 창을 열고 다음 명령을 입력합니다.

   **Debian 설치:**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/azuredatastudio-linux-<version string>.deb

   azuredatastudio
   ```

   **rpm 설치:**
   ```bash
   cd ~
   yum install ./Downloads/azuredatastudio-linux-<version string>.rpm

   azuredatastudio
   ```

   **tar.gz 설치:**
   ```bash 
   cd ~ 
   cp ~/Downloads/azuredatastudio-linux-<version string>.tar.gz ~ 
   tar -xvf ~/azuredatastudio-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/azuredatastudio-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   azuredatastudio 
   ``` 

   > [!NOTE]
   > Debian, Redhat 및 Ubuntu에서는 누락된 종속성이 있을 수 있습니다. 다음 명령을 사용하여 Linux 버전에 따라 해당 종속성을 설치합니다.
   

   **Debian:** 
   ```bash
   sudo apt-get install libunwind8
   ```

   **Redhat:** 
   ```bash
   yum install libXScrnSaver
   ```

   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```

### <a name="supported-operating-systems"></a>지원되는 운영 체제

[!INCLUDE[name-sos](../includes/name-sos-short.md)]는 Windows, macOS 및 Linux에서 실행되며 다음 플랫폼에서 지원됩니다.

#### <a name="windows"></a>Windows

- Windows 10(64비트)
- Windows 8.1(64비트)
- Windows 8(64비트)
- Windows 7 (SP1) (64 비트) - [KB2533623](https://www.microsoft.com/download/details.aspx?id=26767) 필요
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2(64비트)
- Windows Server 2012(64비트)
- Windows Server 2008 R2(64비트)

#### <a name="macos"></a>macOS

- macOS 10.13 High Sierra
- macOS 10.12 Sierra

#### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>다음 단계

도구를 구성한 후에는 클라우드 또는 온-프레미스의 Kubernetes에 SQL Server 2019 빅 데이터 클러스터를 배포합니다. 자세한 내용은 다음 배포 문서를 참조하세요.

- [빠른 시작: AKS(Azure Kubernetes Service)에 SQL Server 빅 데이터 클러스터 배포](quickstart-big-data-cluster-deploy.md)
- [Kubernetes에 배포 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 하는 방법](deployment-guidance.md)

빅 데이터 클러스터에 대 한 자세한 내용은 [ [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)을 참조 하세요.
