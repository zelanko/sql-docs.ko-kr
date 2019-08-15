---
title: Azure Data Studio Notebook을 사용하여 SQL Server 빅 데이터 클러스터 배포
titleSuffix: Deploy SQL Server big data cluster cluster with Azure Data Studio notebooks
description: Azure Data Studio에서 Notebook을 사용하여 빅 데이터 클러스터를 배포합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d68baa615f384dd5afb665f29decb6d72113c5a3
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028569"
---
# <a name="deploy-sql-server-big-data-cluster-with-azure-data-studio-notebooks"></a>Azure Data Studio Notebook을 사용하여 SQL Server 빅 데이터 클러스터 배포

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서는 배포 Notebook을 포함하는 Azure Data Studio 확장을 제공합니다. 배포 Notebook에는 SQL Server 빅 데이터 클러스터를 만들기 위해 Azure Data Studio에서 사용할 수 있는 코드와 설명서가 포함되어 있습니다.

원래 오픈 소스 프로젝트로 구현된 [Notebook](notebooks-guidance.md)이 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download)에 구현되었습니다. 사용 가능한 커널 중 하나와 텍스트 셀에 있는 텍스트의 Markdown을 사용하여 코드 셀에 코드를 작성할 수 있습니다.

Notebook을 사용하여 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]의 빅 데이터 클러스터를 배포할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

Notebook을 시작하려면 다음 필수 조건이 필요합니다.

* 최신 버전의 [Azure Data Studio insider build](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master) 가 설치 됨
* Azure Data Studio에 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 확장이 설치됨

위 항목 외에도 SQL Server 2019 빅 데이터 클러스터를 배포하려면 다음이 필요합니다.

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="launch-the-notebook"></a>Notebook 시작

1. Azure Data Studio 참가자를 시작 합니다.

1. **연결** 탭에서 **...** 을 클릭하고 **SQL Server 빅 데이터 클러스터 배포...** 를 선택합니다.

   ![AI 및 ML](media/deploy-notebooks/deploy-notebooks-1.png)

1. **배포 대상**의 **옵션**에서 **새 Azure Kubernetes 클러스터** 또는 **기존 Azure Kubernetes Service 클러스터**를 선택합니다.

1. **선택** 단추를 클릭 합니다.

1. 이 작업은 사용자 입력을 수집 하는 대화 상자를 시작 하 고, 필요한 정보를 제공 하 고, 기본값을 검토 합니다.

1. **노트북 열기** 단추를 클릭 합니다.
이 작업은 적절한 Notebook을 시작합니다. 배포를 완료하려면 Notebook의 지침에 따라 기존 Azure Kubernetes Service 클러스터나 새 클러스터에 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]의 빅 데이터 클러스터를 배포합니다.

## <a name="next-steps"></a>다음 단계

배포에 대한 자세한 내용은 [SQL Server 빅 데이터 클러스터 배포 지침](deployment-guidance.md)을 참조하세요.
