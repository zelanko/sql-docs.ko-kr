---
title: '배포: Azure Data Studio Notebook'
titleSuffix: SQL Server Big Data Clusters
description: Azure Data Studio에서 Notebook의 코드 및 설명서를 사용하여 SQL Server 빅 데이터 클러스터를 배포하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bcf42d76f855e6fc722caa18f3c0d3c3672f9ec7
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725846"
---
# <a name="deploy-sql-server-big-data-cluster-with-azure-data-studio-notebook"></a>Azure Data Studio Notebook을 사용하여 SQL Server 빅 데이터 클러스터 배포

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서는 배포 Notebook을 포함하는 Azure Data Studio 확장을 제공합니다. 배포 Notebook에는 SQL Server 빅 데이터 클러스터를 만들기 위해 Azure Data Studio에서 사용할 수 있는 코드와 설명서가 포함되어 있습니다.

처음에 오픈 소스 프로젝트로 구현된 [Notebook](../azure-data-studio/notebooks/notebooks-guidance.md)이 [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md?view=sql-server-ver15)에 구현되었습니다. 사용 가능한 커널 중 하나와 텍스트 셀에 있는 텍스트의 Markdown을 사용하여 코드 셀에 코드를 작성할 수 있습니다.

Notebook을 사용하여 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]의 빅 데이터 클러스터를 배포할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

Notebook을 시작하는 데 필요한 필수 조건은 다음과 같습니다.

* 최신 버전의 [Azure Data Studio 참가자 빌드](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)가 설치되어 있어야 함

위 항목 외에도 SQL Server 2019 빅 데이터 클러스터를 배포하려면 다음이 필요합니다.

* [azdata](../azdata/install/deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI(Azure에서 배포하는 경우)](/cli/azure/install-azure-cli?view=azure-cli-latest)

## <a name="launch-the-notebook"></a>Notebook 시작

1. Azure Data Studio를 시작합니다.

2. **연결** 탭에서 줄임표( **...** )를 선택한 후 **SQL Server 배포...** 를 선택합니다.

   ![SQL Server 배포](media/notebooks-deploy/deploy-notebooks.png)

3. 배포 옵션에서 **SQL Server 빅 데이터 클러스터**를 선택합니다.

4. **배포 대상**의 **옵션**에서 **새 Azure Kubernetes 클러스터** 또는 **기존 Azure Kubernetes Service 클러스터**를 선택합니다.

5. 개인정보취급방침 및 사용 조건에 동의합니다.

6. 이 대화 상자에서는 선택한 SQL 배포 유형에 필요한 도구가 호스트에 있는지도 확인합니다. 도구 확인이 성공적으로 수행되어야 **선택** 단추를 사용할 수 있습니다.

7. **선택** 단추를 누릅니다. 이 작업을 수행하면 배포 환경이 시작됩니다.

## <a name="set-deployment-configuration-template"></a>배포 구성 템플릿 설정

아래 지침에 따라 배포 프로필의 설정을 사용자 지정할 수 있습니다.

### <a name="target-configuration-template"></a>대상 구성 템플릿

사용 가능한 템플릿에서 대상 구성 템플릿을 선택합니다. 사용 가능한 프로필은 이전 대화 상자에서 선택한 배포 대상의 유형에 따라 필터링됩니다.

   ![배포 구성 템플릿 1단계](media/notebooks-deploy/deployment-configuration-template.png)

### <a name="azure-settings"></a>Azure 설정

배포 대상이 새 AKS인 경우 AKS 클러스터를 만들려면 Azure 구독 ID, 리소스 그룹, AKS 클러스터 이름, VM 수, 크기, 기타 추가 정보와 같은 정보가 필요합니다.

   ![Azure 설정](media/notebooks-deploy/azure-settings.png)

배포 대상이 기존 Kubernetes 클러스터인 경우 마법사는 *kube* 구성 파일에 대한 경로를 묻는 메시지를 표시하여 Kubernetes 클러스터 설정을 가져옵니다. SQL Server 2019 빅 데이터 클러스터를 배포할 수 있는 위치에 적절한 클러스터 컨텍스트가 선택되어 있는지 확인합니다.

   ![대상 클러스터 컨텍스트](media/notebooks-deploy/target-cluster-context.png)

### <a name="cluster-docker-and-ad-settings"></a>클러스터, Docker 및 AD 설정

1. SQL Server 2019 BDC 클러스터 이름, 관리 사용자 이름 및 암호를 입력합니다.
참고: 컨트롤러 및 SQL Server에 동일한 계정이 사용됩니다.

   ![클러스터 설정](media/notebooks-deploy/cluster-settings.png)

2. 적절한 Docker 설정을 입력합니다.

   ![Docker 설정](media/notebooks-deploy/docker-settings.png)

3. AD 인증을 사용할 수 있는 경우 AD 설정을 입력합니다.

   ![Active Directory 설정](media/notebooks-deploy/active-directory-settings.png)

### <a name="service-settings"></a>서비스 설정

이 화면에는 **크기 조정**, **엔드포인트**, **스토리지**, 기타 **고급 스토리지 설정** 등 다양한 설정에 대한 입력이 있습니다. 적절한 값을 입력하고 **다음**을 선택하세요.

#### <a name="scale-settings"></a>크기 조정 설정

빅 데이터 클러스터에 있는 각 구성 요소의 인스턴스 수를 입력합니다.

Spark 인스턴스는 HDFS에 함께 포함될 수 있습니다. 스토리지 풀 또는 Spark 풀에 자체적으로 포함됩니다.

   ![서비스 설정](media/notebooks-deploy/service-settings.png)

이러한 각 구성 요소에 대한 자세한 내용은 [마스터 인스턴스](concept-master-instance.md), [데이터 풀](concept-data-pool.md), [스토리지 풀](concept-storage-pool.md) 또는 [컴퓨팅 풀](concept-compute-pool.md)을 참조할 수 있습니다.

#### <a name="endpoint-settings"></a>엔드포인트 설정

기본 엔드포인트는 미리 채워져 있습니다. 하지만 적절히 변경할 수 있습니다.

   ![엔드포인트 설정](media/notebooks-deploy/endpoint-settings.png)

#### <a name="storage-settings"></a>스토리지 설정

스토리지 설정에는 데이터 및 로그의 스토리지 클래스와 클레임 크기가 포함되어 있습니다. 이 설정은 스토리지, 데이터 및 SQL Server 마스터 풀에서 적용될 수 있습니다.

   ![스토리지 설정](media/notebooks-deploy/storage-settings.png)

#### <a name="advanced-storage-settings"></a>고급 스토리지 설정

**고급 스토리지 설정**에서 추가 스토리지 설정을 추가할 수 있습니다.

* 스토리지 풀(HDFS)
* 데이터 풀
* SQL Server 마스터

   ![고급 스토리지 설정](media/notebooks-deploy/advanced-storage-settings.png)

### <a name="summary"></a>요약

이 화면에는 SQL Server 2019 빅 데이터 클러스터 배포를 위해 제공된 모든 입력이 요약되어 있습니다. **구성 파일 저장** 단추를 사용하여 구성 파일을 다운로드할 수 있습니다. 전체 배포 구성을 Notebook으로 스크립트하려면 **Notebook으로 스크립트**를 선택합니다. Notebook이 열리면 **셀 실행**을 선택하여 선택한 대상으로 SQL Server 2019 BDC 배포를 시작합니다.

   ![요약](media/notebooks-deploy/deploy-sql-server-big-data-cluster-on-a-new-AKS-cluster.png)

## <a name="next-steps"></a>다음 단계

배포에 대한 자세한 내용은 [SQL Server 빅 데이터 클러스터 배포 지침](deployment-guidance.md)을 참조하세요.