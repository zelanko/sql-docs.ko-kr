---
title: 오프 라인 배포
titleSuffix: SQL Server big data clusters
description: SQL Server 빅 데이터 클러스터의 오프 라인 배포를 수행 하는 방법에 대해 알아봅니다.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cd8b3128fc11037a5ade494813611d473c995f8f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419372"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>SQL Server 빅 데이터 클러스터의 오프 라인 배포 수행

이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)의 오프 라인 배포를 수행 하는 방법을 설명 합니다. 빅 데이터 클러스터는 컨테이너 이미지를 끌어올 Docker 리포지토리에 액세스할 수 있어야 합니다. 오프 라인 설치는 필요한 이미지가 개인 Docker 리포지토리에 배치 되는 위치입니다. 그런 다음 해당 개인 리포지토리는 새 배포에 대 한 이미지 소스로 사용 됩니다.

## <a name="prerequisites"></a>사전 요구 사항

- 지원되는 모든 Linux 배포판 또는 Mac/Windows용 Docker에서 Docker Engine 1.8+. 자세한 내용은 [사용자 Docker 설치](https://docs.docker.com/engine/installation/)를 참조하세요.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="load-images-into-a-private-repository"></a>개인 리포지토리로 이미지 로드

다음 단계에서는 Microsoft 리포지토리에서 빅 데이터 클러스터 컨테이너 이미지를 가져와서 개인 리포지토리로 푸시하는 방법을 설명 합니다.

> [!TIP]
> 다음 단계에서는이 프로세스에 대해 설명 합니다. 그러나 작업을 단순화 하기 위해 이러한 명령을 수동으로 실행 하는 대신 [자동화 된 스크립트](#automated) 를 사용할 수 있습니다.

1. 다음 명령을 반복 하 여 빅 데이터 클러스터 컨테이너 이미지를 끌어옵니다. 각 `<SOURCE_IMAGE_NAME>` [이미지 이름](#images)으로 대체 합니다. 를 `<SOURCE_DOCKER_TAG>` **2019-ctp 3.2-ubuntu**와 같은 빅 데이터 클러스터 릴리스에 대 한 태그로 바꿉니다.  

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. 대상 개인 Docker 레지스트리에 로그인 합니다.

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. 각 이미지에 대 한 다음 명령을 사용 하 여 로컬 이미지에 태그를 합니다.

   ```PowerShell
   docker tag mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. 로컬 이미지를 개인 Docker 리포지토리에 푸시합니다.

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a>빅 데이터 클러스터 컨테이너 이미지

오프 라인 설치에는 다음과 같은 빅 데이터 클러스터 컨테이너 이미지가 필요 합니다.

 - **mssql-appdeploy-init**
 - **mssql-monitor-fluentbit**
 - **mssql-monitor-collectd**
 - **mssql-server-data**
 - **mssql-hadoop**
 - **mssql-monitor-elasticsearch**
 - **mssql-monitor-influxdb**
 - **mssql-security-knox**
 - **mssql-mlserver-r-runtime**
 - **mssql-mlserver-py-runtime**
 - **mssql-controller**
 - **mssql-server-controller**
 - **mssql-monitor-grafana**
 - **mssql-monitor-kibana**
 - **mssql-service-proxy**
 - **mssql-app-service-proxy**
 - **mssql-ssis-app-runtime**
 - **mssql-monitor-telegraf**
 - **mssql-mleap-serving-runtime**
 - **mssql-보안 지원**

## <a id="automated"></a>자동화 된 스크립트

모든 필수 컨테이너 이미지를 자동으로 끌어오고 개인 리포지토리로 푸시하는 자동화 된 python 스크립트를 사용할 수 있습니다.

> [!NOTE]
> Python은 스크립트를 사용 하기 위한 필수 구성 요소입니다. Python을 설치 하는 방법에 대 한 자세한 내용은 [python 설명서](https://wiki.python.org/moin/BeginnersGuide/Download)를 참조 하세요.

1. Bash 또는 PowerShell **에서 다음과 같이**스크립트를 다운로드 합니다.

   ```PowerShell
   curl -o push-bdc-images-to-custom-private-repo.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/offline/push-bdc-images-to-custom-private-repo.py"
   ```

1. 그런 후 다음 명령 중 하나를 사용 하 여 스크립트를 실행 합니다.

   **Windows:**

   ```PowerShell
   python deploy-sql-big-data-aks.py
   ```

   **용**

   ```bash
   sudo python deploy-sql-big-data-aks.py
   ```

1. 표시 되는 메시지에 따라 Microsoft 리포지토리 및 개인 리포지토리 정보를 입력 합니다. 스크립트가 완료 되 면 모든 필수 이미지를 개인 리포지토리에 배치 해야 합니다.

## <a name="install-tools-offline"></a>오프 라인으로 도구 설치

빅 데이터 클러스터 배포에는 **Python**, **azdata**및 **kubectl**를 비롯 한 여러 도구가 필요 합니다. 다음 단계를 사용 하 여 오프 라인 서버에 이러한 도구를 설치 합니다.

### <a id="python"></a>Python 오프 라인 설치

1. 인터넷에 액세스 된 컴퓨터에서 Python을 포함 하는 다음 압축 파일 중 하나를 다운로드 합니다.

   | 운영 체제 | 다운로드 |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. 압축 된 파일을 대상 컴퓨터에 복사 하 고 원하는 폴더에 압축을 풉니다.

1. Windows의 경우 해당 폴더 `installLocalPythonPackages.bat` 에서를 실행 하 고 전체 경로를 매개 변수와 동일한 폴더에 전달 합니다.

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

### <a id="azdata"></a>Azdata 오프 라인 설치

1. 인터넷에 연결 된 컴퓨터와 [Python](https://wiki.python.org/moin/BeginnersGuide/Download)에서 다음 명령을 실행 하 여 **azdata** 패키지를 모두 현재 폴더에 다운로드 합니다.

   ```PowerShell
   pip download -r https://aka.ms/azdata
   ```

1. 다운로드 한 패키지와 **요구 사항 .txt** 파일을 대상 컴퓨터에 복사 합니다.

1. 대상 컴퓨터에서 다음 명령을 실행 하 여 이전 파일을 복사한 폴더를 지정 합니다.

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a>Kubectl 오프 라인 설치

오프 라인 컴퓨터에 **kubectl** 를 설치 하려면 다음 단계를 사용 합니다.

1. Kubectl **를 사용** 하  여 선택한 폴더에 다운로드 합니다. 자세한 내용은 [kubectl binary를 사용 하 여 설치](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)를 참조 하세요.

1. 대상 컴퓨터에 폴더를 복사 합니다.

## <a name="deploy-from-private-repository"></a>개인 리포지토리에서 배포

개인 리포지토리에서 배포 하려면 [배포 가이드](deployment-guidance.md)에 설명 된 단계를 사용 하지만 개인 Docker 리포지토리 정보를 지정 하는 사용자 지정 배포 구성 파일을 사용 합니다. 다음 **azdata 명령은** **이라는 사용자**지정 배포 구성 파일에서 Docker 설정을 변경 하는 방법을 보여 줍니다.

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.repository=<your-docker-repository>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.registry=<your-docker-registry>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.imageTag=<your-docker-image-tag>"
```

배포에서 docker 사용자 이름 및 암호를 묻는 메시지를 표시 하거나 **DOCKER_USERNAME** 및 **DOCKER_PASSWORD** 환경 변수에 지정할 수 있습니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터 배포에 대 한 자세한 내용은 [Kubernetes에서 빅 데이터 클러스터 SQL Server 배포 하는 방법](deployment-guidance.md)을 참조 하세요.
