---
title: 오프라인 배포
titleSuffix: SQL Server big data clusters
description: SQL Server 빅 데이터 클러스터의 오프라인 배포를 수행하는 방법을 알아봅니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 15af041e94ac0abfdae13635345de62262a4b086
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73531979"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터의 오프라인 배포 수행

이 문서에서는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 오프라인 배포를 수행하는 방법을 설명합니다. 빅 데이터 클러스터가 컨테이너 이미지를 끌어올 Docker 리포지토리에 액세스할 수 있어야 합니다. 오프라인 설치는 필요한 이미지가 프라이빗 Docker 리포지토리에 저장되는 설치입니다. 그런 다음, 해당 프라이빗 리포지토리가 새 배포의 이미지 원본으로 사용됩니다.

## <a name="prerequisites"></a>사전 요구 사항

- 지원되는 모든 Linux 배포판 또는 Mac/Windows용 Docker에서 Docker Engine 1.8+. 자세한 내용은 [사용자 Docker 설치](https://docs.docker.com/engine/installation/)를 참조하세요.

## <a name="load-images-into-a-private-repository"></a>프라이빗 리포지토리로 이미지 로드

다음 단계에서는 Microsoft 리포지토리에서 빅 데이터 클러스터 컨테이너 이미지를 끌어와 프라이빗 리포지토리로 밀어넣는 방법을 설명합니다.

> [!TIP]
> 다음 단계는 프로세스를 설명한 것입니다. 그러나 작업을 간소화하기 위해 이러한 명령을 수동으로 실행하는 대신 [자동화된 스크립트](#automated)를 사용할 수 있습니다.

1. 다음 명령을 반복하여 빅 데이터 클러스터 컨테이너 이미지를 끌어옵니다. `<SOURCE_IMAGE_NAME>`을 각 [이미지 이름](#images)으로 바꿉니다. `<SOURCE_DOCKER_TAG>`를 **2019-GDR1-ubuntu-16.04**와 같은 빅 데이터 클러스터 릴리스의 태그로 바꿉니다.  

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. 대상 프라이빗 Docker 레지스트리에 로그인합니다.

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. 각 이미지에 대해 다음 명령을 사용하여 로컬 이미지에 태그를 지정합니다.

   ```PowerShell
   docker tag mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. 로컬 이미지를 프라이빗 Docker 리포지토리에 밀어넣습니다.

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a> 빅 데이터 클러스터 컨테이너 이미지

오프라인 설치에는 다음과 같은 빅 데이터 클러스터 컨테이너 이미지가 필요합니다.
- **mssql-app-service-proxy**
- **mssql-control-watchdog**
- **mssql-controller**
- **mssql-dns**
- **mssql-hadoop**
- **mssql-mleap-serving-runtime**
- **mssql-mlserver-py-runtime**
- **mssql-mlserver-r-runtime**
- **mssql-monitor-collectd**
- **mssql-monitor-elasticsearch**
- **mssql-monitor-fluentbit**
- **mssql-monitor-grafana**
- **mssql-monitor-influxdb**
- **mssql-monitor-kibana**
- **mssql-monitor-telegraf**
- **mssql-security-domainctl**
- **mssql-security-knox**
- **mssql-security-support**
- **mssql-server**
- **mssql-server-controller**
- **mssql-server-data**
- **mssql-ha-operator**
- **mssql-ha-supervisor**
- **mssql-service-proxy**
- **mssql-ssis-app-runtime**


## <a id="automated"></a> 자동화된 스크립트

필요한 컨테이너 이미지를 자동으로 모두 끌어오고 프라이빗 리포지토리로 밀어넣는 자동화된 python 스크립트를 사용할 수 있습니다.

> [!NOTE]
> Python은 스크립트를 사용하기 위한 필수 조건입니다. Python을 설치하는 방법에 대한 자세한 내용은 [Python 설명서](https://wiki.python.org/moin/BeginnersGuide/Download)를 참조하세요.

1. bash 또는 PowerShell에서 **curl**을 사용하여 스크립트를 다운로드합니다.

   ```PowerShell
   curl -o push-bdc-images-to-custom-private-repo.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/offline/push-bdc-images-to-custom-private-repo.py"
   ```

1. 그런 후에 다음 명령 중 하나를 사용하여 스크립트를 실행합니다.

   **Windows:**

   ```PowerShell
   python push-bdc-images-to-custom-private-repo.py
   ```

   **Linux:**

   ```bash
   sudo python push-bdc-images-to-custom-private-repo.py
   ```

1. 프롬프트를 따라 Microsoft 리포지토리 및 프라이빗 리포지토리 정보를 입력합니다. 스크립트가 완료되면 필요한 이미지가 모두 프라이빗 리포지토리에 있습니다.

1. [여기](deployment-custom-configuration.md#docker)의 지침에 따라 컨테이너 레지스트리 및 리포지토리를 사용하도록 `control.json` 배포 구성 파일을 사용자 정의하는 방법을 학습합니다. 프라이빗 리포지토리에 액세스할 수 있도록 배포하기 전에 `DOCKER_USERNAME` 및 `DOCKER_PASSWORD` 환경 변수를 설정해야 합니다.

## <a name="install-tools-offline"></a>도구 오프라인 설치

빅 데이터 클러스터 배포를 사용하려면 **Python**, `azdata` 및 **kubectl**을 비롯한 여러 가지 도구가 필요합니다. 다음 단계를 사용하여 이러한 도구를 오프라인 서버에 설치합니다.

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

### <a id="azdata"></a> azdata 오프라인 설치

1. 인터넷에 액세스할 수 있고 [Python](https://wiki.python.org/moin/BeginnersGuide/Download)이 설치된 머신에서 다음 명령을 실행하여 `azdata` 패키지를 현재 폴더로 모두 다운로드합니다.

   ```PowerShell
   pip download -r https://aka.ms/azdata
   ```

1. 다운로드한 패키지와 `requirements.txt` 파일을 대상 머신에 복사합니다.

1. 대상 머신에서 다음 명령을 실행하고 이전 파일을 복사한 폴더를 지정합니다.

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a> kubectl 오프라인 설치

오프라인 머신에 **kubectl**을 설치하려면 다음 단계를 사용합니다.

1. **curl**을 사용하여 **kubectl**을 선택한 폴더로 다운로드합니다. 자세한 내용은 [curl을 사용하여 kubectl 이진 설치](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)를 참조하세요.

1. 대상 머신에 폴더를 복사합니다.

## <a name="deploy-from-private-repository"></a>프라이빗 리포지토리에서 배포

프라이빗 리포지토리에서 배포하려면 [배포 가이드](deployment-guidance.md)에 설명된 단계를 사용하되, 프라이빗 Docker 리포지토리 정보를 지정하는 사용자 지정 배포 구성 파일을 사용합니다. 다음 `azdata` 명령은 `control.json`이라는 사용자 지정 배포 구성 파일의 Docker 설정을 변경하는 방법을 보여 줍니다.

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.repository=<your-docker-repository>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.registry=<your-docker-registry>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.imageTag=<your-docker-image-tag>"
```

배포에서 docker 사용자 이름 및 암호를 묻는 메시지가 표시되거나, `DOCKER_USERNAME` 및 `DOCKER_PASSWORD` 환경 변수에 지정할 수 있습니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터 배포에 대한 자세한 내용은 [Kubernetes에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md)을 참조하세요.
