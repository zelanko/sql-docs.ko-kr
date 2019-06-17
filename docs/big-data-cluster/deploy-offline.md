---
title: 오프 라인 배포
titleSuffix: SQL Server big data clusters
description: SQL Server 빅 데이터 클러스터를 오프 라인 배포를 수행 하는 방법에 알아봅니다.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fd6a1e1e6f2ad661c8a2316c434854095c7f6da5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797887"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터를 오프 라인 배포를 수행 합니다.

이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)의 오프 라인 배포를 수행 하는 방법을 설명 합니다. 빅 데이터 클러스터 권한이 있어야 합니다 Docker 리포지토리에 있는 이미지를 끌어올 컨테이너. 오프 라인 설치는 필요한 이미지를 개인 Docker 리포지토리에 배치 되는 하나입니다. 개인 리포지토리에서 다음 새 배포에 대 한 이미지 원본으로 사용 됩니다.

## <a name="prerequisites"></a>사전 요구 사항

- 지원되는 모든 Linux 배포판 또는 Mac/Windows용 Docker에서 Docker Engine 1.8+. 자세한 내용은 [사용자 Docker 설치](https://docs.docker.com/engine/installation/)를 참조하세요.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="load-images-into-a-private-repository"></a>개인 리포지토리 이미지 로드

다음 단계를 Microsoft 리포지토리에서 빅 데이터 클러스터 컨테이너 이미지를 풀 하 여 개인 리포지토리로 푸시합니다 하는 방법을 설명 합니다.

> [!TIP]
> 다음 단계는 프로세스를 설명 합니다. 그러나 작업을 간소화 하기를 사용할 수는 [자동화 스크립트](#automated) 수동으로 이러한 명령을 실행 하는 대신 합니다.

1. 먼저 사용 하 여 Microsoft Docker 레지스트리에 로그인 합니다 **docker 로그인** 명령입니다. Username 및 password Early Adoption Program의 일부로 제공 되는 Microsoft를 사용 합니다.

   ```PowerShell
   docker login private-repo.microsoft.com -u  <SOURCE_DOCKER_USERNAME> -p <SOURCE_DOCKER_PASSWORD>
   ```

   > [!TIP]
   > 이 명령은 PowerShell를 사용 하 여 예를 들어 있지만 cmd, bash 또는 docker를 실행할 수 있는 모든 명령 셸에서 실행할 수 있습니다. Linux에서 추가 `sudo` 각 명령입니다.

1. 다음 명령을 반복 하 여 빅 데이터 클러스터 컨테이너 이미지를 끌어옵니다. 바꿉니다 `<SOURCE_IMAGE_NAME>` 상호 [이미지 이름](#images)합니다. 바꿉니다 `<SOURCE_DOCKER_TAG>` 빅 데이터에 대 한 태그를 사용 하 여 릴리스에서와 같은 클러스터 **ctp3.0**합니다.  

   ```PowerShell
   docker pull private-repo.microsoft.com/mssql-private-preview/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. 대상 개인 Docker 레지스트리를 로그인 합니다.

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. 각 이미지에 대해 다음 명령 사용 하 여 로컬 이미지 태그를 지정 합니다.

   ```PowerShell
   docker tag private-repo.microsoft.com/mssql-private-preview/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. 개인 Docker 리포지토리에 로컬 이미지를 푸시하십시오.

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a> 빅 데이터 클러스터 컨테이너 이미지

다음 빅 데이터 클러스터 컨테이너 이미지를이 오프 라인 설치에 대 한 필요 합니다.

 - **mssql-appdeploy-init**
 - **mssql-monitor-fluentbit**
 - **mssql-monitor-collectd**
 - **mssql-server-data**
 - **mssql-hadoop**
 - **mssql-java**
 - **mssql-mlservices-pythonserver**
 - **mssql-mlservices-rserver**
 - **mssql-monitor-elasticsearch**
 - **mssql-monitor-influxdb**
 - **mssql-security-knox**
 - **mssql-mlserver-r-runtime**
 - **mssql-mlserver-py-runtime**
 - **mssql-controller**
 - **mssql-portal**
 - **mssql-server-controller**
 - **mssql-monitor-grafana**
 - **mssql-monitor-kibana**
 - **mssql-service-proxy**
 - **mssql-app-service-proxy**
 - **mssql-ssis-app-runtime**
 - **mssql-monitor-telegraf**

## <a id="automated"></a> 자동화 된 스크립트

자동으로 모든 필요한 컨테이너 이미지를 풀 하 고 개인 리포지토리로 푸시합니다는 자동화 된 python 스크립트를 사용할 수 있습니다.

> [!NOTE]
> Python은 스크립트를 사용 하는 것에 대 한 필수 구성 요소입니다. Python을 설치 하는 방법에 대 한 자세한 내용은 참조는 [Python 설명서](https://wiki.python.org/moin/BeginnersGuide/Download)합니다.

1. Bash 또는 PowerShell에서 사용 하 여 스크립트를 다운로드 **curl**:

   ```PowerShell
   curl -o push-bdc-images-to-custom-private-repo.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/offline/push-bdc-images-to-custom-private-repo.py"
   ```

1. 다음 명령 중 하나를 사용 하 여 스크립트를 실행 합니다.

   **Windows:**

   ```PowerShell
   python deploy-sql-big-data-aks.py
   ```

   **Linux:**

   ```bash
   sudo python deploy-sql-big-data-aks.py
   ```

1. Microsoft 리포지토리 및 개인 리포지토리 정보를 입력 하는 것에 대 한 지시를 따릅니다. 스크립트를 완료 한 후 모든 이미지를 개인 리포지토리에서 있어야 필요 합니다.

## <a name="install-tools-offline"></a>오프 라인 도구 설치

빅 데이터 클러스터 배포를 비롯 한 몇 가지 도구에 필요 **Python**하십시오 **mssqlctl**, 및 **kubectl**합니다. 오프 라인 서버에서 이러한 도구를 설치 하려면 다음 단계를 사용 합니다.

### <a id="python"></a> Python을 오프 라인 설치

1. 인터넷에 연결 된 컴퓨터에서 Python을 포함 하는 다음 압축 된 파일 중 하나를 다운로드 합니다.

   | 운영 체제 | 다운로드 |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. 대상 컴퓨터에 압축 된 파일을 복사 하 고 선택한 폴더로 추출 합니다.

1. Windows 에서만 실행 `installLocalPythonPackages.bat` 해당 폴더를 매개 변수로 동일한 폴더에 전체 경로 전달 합니다.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

### <a id="mssqlctl"></a> Mssqlctl 오프 라인 설치

1. 인터넷에 연결 된 컴퓨터에서 및 [Python](https://wiki.python.org/moin/BeginnersGuide/Download), 해제 된 모든 다운로드 하려면 다음 명령을 실행 합니다 **mssqlctl** 현재 폴더에 패키지 합니다.

   ```PowerShell
   pip download -r https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt
   ```

1. 다운로드 합니다 **requirements.txt** 파일입니다.

   ```PowerShell
   curl -o requirements.txt "https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt"
   ```

1. 다운로드 한 패키지를 복사 하며 **requirements.txt** 대상 컴퓨터에는 파일입니다.

1. 이전 파일을 복사한 폴더를 지정 하는 대상 컴퓨터에서 다음 명령을 실행 합니다.

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a> Kubectl 오프 라인 설치

설치할 **kubectl** 오프 라인 컴퓨터를 하려면 다음 단계를 사용 합니다.

1. 사용 하 여 **curl** 다운로드 하려면 **kubectl** 선택한 폴더에 있습니다. 자세한 내용은 [curl을 사용 하 여 kubectl 이진 설치](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)합니다.

1. 대상 컴퓨터에 폴더를 복사 합니다.

## <a name="deploy-from-private-repository"></a>개인 리포지토리에서 배포

개인 리포지토리에서 배포 하려면에 설명 된 단계를 사용 합니다 [배포 가이드](deployment-guidance.md), 개인 Docker 리포지토리 정보를 지정 하는 사용자 지정 배포 구성 파일을 사용 하지만 합니다. 다음 **mssqlctl** 명령은 라는 사용자 지정 배포 구성 파일에서 Docker 설정을 변경 하는 방법을 보여 줍니다 **custom.json**:

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.controlPlane.spec.docker.repository=<your-docker-repository>"
mssqlctl cluster config section set -c custom.json -j "$.spec.controlPlane.spec.docker.registry=<your-docker-registry>"
mssqlctl cluster config section set -c custom.json -j "$.spec.controlPlane.spec.docker.imageTag=<your-docker-image-tag>"
```

배포를 docker 사용자 이름과 암호를 묻는 메시지를 표시 합니다 또는 지정할 수 있습니다 합니다 **DOCKER_USERNAME** 하 고 **DOCKER_PASSWORD** 환경 변수입니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터 배포에 대 한 자세한 내용은 참조 하십시오 [빅 데이터를 SQL Server를 배포 하는 방법에서 kubernetes 클러스터](deployment-guidance.md)합니다.
